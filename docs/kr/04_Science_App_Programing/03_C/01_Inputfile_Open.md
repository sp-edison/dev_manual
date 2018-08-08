

# 입력 파일이 1개인 경우
[[링크] Github에서 보기](https://github.com/sp-edison/c_example_input1)

[[링크] 소스코드 다운받기](https://github.com/sp-edison/c_example_input1/archive/master.zip)

## 예제코드 다운로드 및 실행

Github 사이트에 접속 해서 전체 소스가 압축된 파일을 다운 받거나, ```git clone``` 명령어를 이용해 소스 코드를 받을수 있습니다.

Bulb 서버에 접속 후 아래 명령어를 실행하면, 해당 소스코드를 다운 받을 수 있습니다.
> Bulb 서버가 아닌 곳에서도 git이 설치되어 있다면, ```git clone``` 명령어를 통해 소스코드를 다운로드 받을 수 있습니다.
> - [git 설치하기](https://git-scm.com/book/ko/v2/%EC%8B%9C%EC%9E%91%ED%95%98%EA%B8%B0-Git-%EC%84%A4%EC%B9%98)

```bash
$  git clone https://github.com/sp-edison/c_example_input1.git
```
다운로드가 완료되면, ```c_example_input1``` 폴더가 생성됩니다. 폴더 구성은 다음과 같습니다.
```bash
c_example_input1
│   README.md
├───src
│   │   Makefile
│   └─  main.c
└───inp
    └─  input.dat
```

 ```src``` 폴더로 이동하여 ```make all``` 명령어를 사용하면, 컴파일이 완료됩니다.

```bash
$ cd c_example_input1/src
$ make all
gcc  -c main.c -o main.o
Compiled main.c successfully!
gcc  -o ../bin/Hello.x main.o
Linking complete!
```

컴파일이 완료되면 ```c_example_input1``` 폴더 안에 ```bin``` 폴더가 생성되며, ```src/Mamkefile``` 에서 지정한 ```TARGET``` 명으로 실행 파일이 생성됩니다.
> 예제의 경우 ```TARGET```이 ```Hello.x```로 설정되어 있습니다.

생성된 ```bin``` 폴더로 이동하여, ```inp```폴더에 있는 ```input.dat```을 입력 파일로 넣고 실행시 에러 없이 실행 종료됨을 확인할 수 있습니다.

```bash
$ cd ../bin
$ ./Hello.x -i ../inp/input.dat
Succeed to open inputfile. Path: ../inp/input.dat
num
1000
```

이 예제에는 옵션 값이 맞는지 체크하고 옵션 뒤에 붙은 추가 파라미터 값이 파일 경로인지 확인하고 종료하는 프로그램입니다. 옵션 명이 잘못되었거나 입력 파일 경로가 잘못된 경우에는 에러가 발생합니다.

컴파일 된 파일을 삭제하고 싶은 경우에는 다시 ```src``` 폴더로 이동하여 ```make clean``` 명령어를 사용하면, 오브젝트 파일과 실행 파일을 삭제하게 됩니다.
```bash
$ cd ../src
$ make clean
rm -rf main.o ../bin/Hello.x
```

## Source code

### main.c

```c
#include <stdio.h>
#include <stdlib.h>
#include <getopt.h>

int main (int argc, char *argv[]) {
	int opt;
	FILE *fp_input;
	char buf_string[256];

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

	// Write an algorithm program in this section.

	while(1) {
	fscanf(fp_input, "%s", buf_string);
		if(feof(fp_input))
			break;
		printf("%s\n", buf_string);
	}

	// Input file close
	fclose(fp_input);
	return 0;
}

```

### 주요 함수 설명
```c
int main (int argc, char *argv[]);
```
많은 프로그램들은 명령행 인자(Command Line Argument) 방식으로 프로그램 실행을 위한 입력 데이터를 받게됩니다. 이때 필요한 변수가 ```argc```, ```argv```입니다.

- ```argc```는, 프로그램을 실행할 때 지정해 준 "명령행 인자"의 "개수"가 저장되는 곳입니다.
- ```argv```는, 프로그램을 실행할 때 지정해 준 "명령행 인자의 문자열들"이 실제로 저장되는 배열입니다.

> 리눅스에서 쓰이는 많은 명령어들도 이러한 형태로 사용되고 있습니다.
> 예를들어 ```cd result``` 라는 명령어도 ```cd```라는 디렉토리를 이동하는 프로그램과 이 프로그램을 실행하기 위한 입력 데이터 ```result```로 나누어 지고, result 폴더로 이동하라는 명령이 됩니다.

```c
int getopt(int argc, char * const argv[], const char *optstring);
```
입력 파라미터는 ```main()```함수가 받은 파라미터를 전달하는 ```argc```, ```argv``` 와 처리해야하는 옵션 값을 가지고 있는 optstring로 구성되어 있습니다. ```getopt()``` 함수로 처리하고자 하는 옵션을 optstring에 저장해야 하며, 옵션 뒤에 추가 파라미터가 필요한 경우에는 옵션명 뒤에 “:”를 추가합니다. 옵션명은 1개의 문자로 구성되며, 문자열을 옵션으로 받는 경우는 ```getoptlong()``` 함수를 사용하면 됩니다.

> 예를 들어 단일 옵션 ```-h```, ```-v```와 별도 파라미터가 필요한 옵션 ```-i filename```을 체크하고자 한다면 ```"hvi:"``` 값을 옵션 스트링에 넣어주면 됩니다.

이 함수를 사용하기 위해서는 ```#include <getopt.h>``` 또는 ```#include <unistd.h>``` 선언을 해야하며, ```getopt()``` 함수에 필요한 전역 변수도 호출이 됩니다.

- ```optarg``` : 옵션 뒤에 별도의 파라미터 값이 오는 경우, 이를 파싱한 결과 파라미터 값은 ```optarg```에 문자열로 저장됩니다.
- ```optind``` : 다음번 처리될 옵션의 인덱스이다. 만약 파싱한 옵션이후에 추가적인 파라미터를 받는다면 (예를 들어 입력 파일 이름 같이) 이 값을 활용할 수 있다. ```getopt()```함수는 한 번 호출될 때마다 이 값을 업데이트 합니다.
- ```opterr``` : 옵션에 문제가 있을 때, 이 값은 0이 아닌 값이되며, ```getopt()```함수가 메시지를 표시하게 됩니다.
- ```optopt``` : 알 수 없는 옵션을 만났을 때 해당 옵션이 여기에 들어갑니다. (이 때 ```getopt```의 리턴값은 ‘?’가 된다.)

### 주요 코드 설명
```c
    	...
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
  	...
```
```while```문 안에 있는  ```opt = getopt(argc, argv, "i:")```은 명령행 인자의 문자열들을 확인해 ```-i filepath``` 형태가 있는 경우 ```i```는 ```opt```변수에 ```filepath```는 ```optarg```변수에 저장합니다. 정의한 ```-i``` 옵션 이외의 다른 옵션값(ex ```-m```)이 들어오는 경우 default 문에서 예외 처리하였습니다.

> 만약 ```-i, -m``` 옵션 2개를 통해 입력 파일을 받기 원한다면, ```“i:” -> “i:m:”```으로 고치고, 아래 ```switch```문의 ```m``` case를 추가하면 됩니다.

```-i``` 옵션 값이 입력된 경우 바로 뒤에 입력한 ```filepath```가 재대로 입력되었는지 확인합니다. 입력된 경로에 파일이 있다면, ```fp_input = fopen(optarg,"r")```값이 ```NULL```이 아닌 값을 가지게 됩니다. ```NULL```인 경우에는 파일 경로가 잘못 입력된 경우로 이에 대한 에러 로그를 표준 에러(Standard error)를 통해 표시합니다.
```c
fprintf(stderr, "Error opening inputfile Path: %s\n", optarg);
```

또한 ```return -1;```을 통해 ```main``` 함수의 리턴 값을 0이 아닌 값을 반환하여 정상적으로 종료되지 않았다는 것을 알립니다.


```c
  ...
  while(1) {
      fscanf(fp_input, "%s", buf_string);
      if(feof(fp_input))
        break;
      printf("%s\n", buf_string);
  }

  // Input file close
  fclose(fp_input);
  return 0;
}
```
정상적으로 입력 파일을 오픈한 경우 오픈한 파일의 내용을 읽어 모니터에 출력합니다. 파일을 읽는 함수 중 ```fscanf(fp_input, "%s", buf_string);``` 함수를 통해 문자열 하나씩 읽어 ```buf_string```에 저장하고 이를 표준출력으로 출력합니다.
입력 파일을 모두 읽고난 이후 ```fclose(fp_input);```을 통해 파일을 닫고 ```return 0;```을 통해 ```main```함수가 정상적으로 종료됨을 알립니다.
