
# SDE case study

C언어로 SDE에서 생성된 입력 파일을 읽는 방법을 설명하고자 합니다.

관련 문서 링크
- [SDE 프로그래밍 방법 개요](../02_Input_programing/01_Structured_Data_Editor.md)
- [SDE 데이터 타입 생성하기](../../06_EDITOR/01_SDE.md)

다음과 같이 숫자형 변수 2개(정수형 변수 1개, 실수형 변수 1개), 리스트형 변수 1개, 3차원 벡터 1개를 받는 SDE를 생성했습니다.

![Case1](../../asset/image/04/02/case1.png)

데이터 생성 방식은 다음과 같이 설정했습니다.

|KEY	|VALUE| KEY	| VALUE|
|--|--|--|--|
|value delimiter|	SPACE|Vector vracket|	SQUARE_SPACE|
|line delimiter|	NULL|Vector delimiter|	SPACE|

이렇게 설정되어 생성된 입력 파일은 다음과 같습니다.

```
INT1 42
REAL1 42.112
LIST1 a
VECTOR1 [ 1 0 0 ]
```

# Example

명령행 인자(Command Line Argument) 방식으로 생성된 입력 파일을 읽고 입력된 변수 값을 출력하는 예제 코드입니다.

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <getopt.h>

typedef struct _inputparam {
    int int1;       
    double real1;      
    char list1;      
    int vector1[3];    
} INPUT;

int main (int argc, char* argv[])
{
    int opt;
    FILE *fp_input ;
    char buf_char[256];
    INPUT input;


    // Detect the end of the options.
    while((opt = getopt(argc, argv, "i:")) != -1 ) {
    	switch(opt) {
    		case 'i':
    			if((fp_input = fopen(optarg,"r")) == NULL ) {
    				fprintf(stderr, "Error opening inputfile Path: %s\n", optarg);
    				return -1;
    			} else {
    				printf("Succeed to open inputfile Path: %s\n", optarg);
    			}
    			break;
    		default:
    			printf("Usage: %s -i [filepath] \n", argv[0]);
    			return -1;
    	}
    }
    while(1) {
        fscanf(fp_input, "%s", buf_char);

        if(feof(fp_input))
            break;

        if(!strcmp(buf_char, "INT1")) {
            fscanf(fp_input, "%d", &input.int1);
        } else if(!strcmp(buf_char, "REAL1")) {
            fscanf(fp_input, "%lf", &input.real1);
        } else if(!strcmp(buf_char, "LIST1")) {
            fscanf(fp_input, "%s", &input.list1);
        } else if(!strcmp(buf_char, "VECTOR1")) {
            fscanf(fp_input, "%*s %d %d %d %*s", &input.vector1[0], &input.vector1[1], &input.vector1[2]);
        } else {
            printf("Error Invalid value name :: %s\n", buf_char);
            exit(1);
        }
    }


    printf("int1: %d \n", input.int1);
    printf("real1: %f \n", input.real1);
    printf("list1: %c \n", input.list1);
    printf("vector1 =  %d %d %d \n",input.vector1[0], input.vector1[1], input.vector1[2]);

    fclose(fp_input);

    return 0;
}

```

> 위 예제코드는 [입력 파일이 1개인 경우 예제](./01_Inputfile_Open.md)의 코드에서 SDE 파일을 읽는 부분을 추가하였습니다.

## 주요 코드 설명

```c
    ...
[1] while(1) {
[2]     fscanf(fp_input, "%s", buf_char);

[3]     if(feof(fp_input))
            break;

[4]     if(!strcmp(buf_char, "INT1")) {
            fscanf(fp_input, "%d", &input.int1);
        } else if(!strcmp(buf_char, "REAL1")) {
            fscanf(fp_input, "%lf", &input.real1);
        } else if(!strcmp(buf_char, "LIST1")) {
            fscanf(fp_input, "%s", &input.list1);
        } else if(!strcmp(buf_char, "VECTOR1")) {
            fscanf(fp_input, "%*s %d %d %d %*s", &input.vector1[0], &input.vector1[1], &input.vector1[2]);
[5]     } else {
            printf("Error Invalid value name :: %s\n", buf_char);
            exit(1);
        }
    }
...
```

[1] ```while``` 문을 이용해 파일을 처음부터 끝까지 읽습니다.

[2] [fscanf()](http://www.cplusplus.com/reference/cstdio/fscanf/?kw=fscanf) 함수를 이용해 변수 이름이 저장되어 있는 하나의 문자열(첫 단어)를 ```buf_char```에 저장합니다.

[3] [feof()](http://www.cplusplus.com/reference/cstdio/feof/) 함수를 이용해 파일의 끝까지 읽으면 ```break``` 문을 이용해 ```while```문을 빠져 나오게 됩니다.

[4] 입력 파일에서 읽은 변수 이름을 확인하여 저장 합니다. 벡터 변수의 경우 변수 이름과 값 사이에 있는 ```[``` , ```]``` 문자를 ```%*s``` 를 사용해 읽기만 하고 따로 변수에 저장하지 않습니다.

[5] 원하지 않은 변수 값이 입력되는 경우 이에 대한 에러 메시지를 표시하고 프로그램을 종료합니다.


# SDE case study 2

SDE 생성시 데이터 생성 방식을 아래와 같이 설정한다면, 생성되는 입력 파일의 모양이 약간 달라질 것입니다.

|KEY	|VALUE| KEY	| VALUE|
|--|--|--|--|
|value delimiter|	EQUAL |Vector vracket|	SQUARE_SPACE|
|line delimiter|	SEMICOLON |Vector delimiter|	SPACE|



생성된 입력 파일
```
INT1 = 42 ;
REAL1 = 42.112 ;
LIST1 = a ;
VECTOR1 = [ 1 0 0 ] ;
```

추가된 value delimiter와 line delimiter를 고려해 코딩을 해야 합니다. ```%*s``` 이용해 변수 이름과 변수 값 사이에 있는 ```=```와 변수 끝에 있는 ```;```을 파일에서 읽기만 하고, 따로 저장하지 않는 부분을 추가하면 됩니다.
``` fscanf(fp_input, "%d", &input.int1); ``` -> ``` fscanf(fp_input, "%*s %d %*s", &input.int1); ```

변경전 코드
```c
...
[4]     if(!strcmp(buf_char, "INT1")) {
            fscanf(fp_input, "%d", &input.int1);
        } else if(!strcmp(buf_char, "REAL1")) {
            fscanf(fp_input, "%lf", &input.real1);
        } else if(!strcmp(buf_char, "LIST1")) {
            fscanf(fp_input, "%s", &input.list1);
        } else if(!strcmp(buf_char, "VECTOR1")) {
            fscanf(fp_input, "%*s %d %d %d %*s", &input.vector1[0], &input.vector1[1], &input.vector1[2]);
...
```

변경후 코드
```c
...
[4]     if(!strcmp(buf_char, "INT1")) {
            fscanf(fp_input, "%*s %d %*s", &input.int1);
        } else if(!strcmp(buf_char, "REAL1")) {
            fscanf(fp_input, "%*s %lf %*s", &input.real1);
        } else if(!strcmp(buf_char, "LIST1")) {
            fscanf(fp_input, "%*s %s %*s", &input.list1);
        } else if(!strcmp(buf_char, "VECTOR1")) {
            fscanf(fp_input, "%*s %*s %d %d %d %*s %*s", &input.vector1[0], &input.vector1[1], &input.vector1[2]);
...
```
