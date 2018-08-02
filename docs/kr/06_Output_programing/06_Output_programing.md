# 출력 프로그래밍 기초

해석 결과 데이터는 파일 형태로 출력해야 하며, result 폴더에 생성되어야 합니다.

> result 폴더 생성하는 예제를 보시면 예제코드에서는 result 폴더를 생성하는 명령어를 실행하기 전 result 폴더를 삭제하는 명령어를 실행합니다.
> 프로그램 테스트과정 중 이전 테스트한 결과 데이터가 남아있는 상황에서 프로그램을 실행하게 되면 여러 문제가 발생할 수 있습니다. 이를 방지하고자 result 폴더를 삭제하는 코드를 추가하였습니다.

이후 파일 입출력 함수 이용해 result 폴더안에 파일을 쓰기 모드로 생성하면 됩니다.


## C Coded
### result 폴더 생성

C 언어의 경우 ```#include <stdlib.h>``` 헤더를 선언하고 ```int system (const char * string);``` 함수를 이용하면 되며, ```result``` 폴더를 생성하는 예제는 아래와 같습니다.
```c
 #include <stdlib.h>

 int main (int argc, char* argv[])
 {
 ...
   system("rm -rf result");
   system("mkdir result");
 ...
   return 0
 }

```

### 출력 파일 쓰기
C 언어에서 파일을 읽고 쓰기 위해서는 파일 입출력 함수를 사용한다. 출력 파일을 쓰기 위한 코드 구성은 다음과 같다.

```c
#include  <stdio.h>
...

int main (int argc, char *argv[]) {  
    ...

    ...
    // 파일 포인터를 이용 result/result.txt을 쓰기 모드로 오픈
    fp_out = fopen("result/result.txt","w");
    ...

    ...
    // fprintf() 함수를 이용해 파일에 내용을 씀
    fprintf(fp_out,"Hello EDISON.\n");
    ...

    ...
    // 파일 쓰기가 끝났으면, 파일을 닫음.
    fclose(fp_out);
    ...
}
```
```fprintf()``` 또는 ```fputs()``` 함수를 활용해 파일을 쓸 수 있다.

## FORTRAN Code
### result 폴더 생성

FORTRAN의 경우 ```CALL SYSTEM(COMMAND [, STATUS])```를 이용하면 되며, ```result``` 폴더를 생성하는 예제는 아래와 같습니다.
```fortran
      program sample
      ...

      ...
!      결과 파일이 저장될 result 폴더 생성
      CALL SYSTEM("rm -rf result")
      CALL SYSTEM("mkdir result")
      ...
```

### 출력 파일 쓰기

```FORTRAN
      ...
!      result/result.txt을 오픈
      open(2,file="result/result.txt")
      ...

      ...
!      파일안에 데이터를 씀
      write(2,*)"Hello EDISON."
      ...


      ...
!      파일을 닫음
      CLOSE(2)
```
```open()``` 함수를 이용해 장치번호(UNIT)을 2로 설정하여 result 폴더 안 result.txt 파일을 오픈한다. 여러개의 파일을 동시에 쓰거나 읽는 경우 장치번호가 겹치지 않게 조심해야한다.
> 장치번호는 1 부터 99 사이의 정수로 설정할 수 있으며, 5는 표준 입력 standard input, 6은 표준 출력 standard output으로 이미 설정되어 있다.

장치 번호와 ```write()```함수를 통해 파일에 데이터를 쓸 수 있으며, 파일쓰기가 완료된 이후 ```close()``` 함수를 이용해 파일을 닫는다.

## Python Code
### result 폴더 생성

Python의 경우 ```import os``` 를 선언하고 ```os.system (const char * string);``` 함수를 이용하면 되며, result 폴더를 생성하는 예제는 아래와 같습니다.

```python
 import os

 ...
   os.remove("result");
   os.mkdir("result");
 ...
```

### 결과 파일 생성

```Python
  # open()함수를 통해 result/result.txt을 쓰기 모드로 오픈
  f_out = open("result/result.txt","w")
  ...

  ...
  # f_out.wirte() 함수를 이용해 파일에 내용을 씀
  f_out.write("Hello EDISON.\n")

  ...
  # f_out.close() 함수를 통해 파일을 닫음
  f_out.close()
```


### R
### result 폴더 생성
R의 경우 별도의 선언없이 ```dir.create()``` 함수를 이용하면 되며, ```result``` 폴더를 생성하는 예제는 아래와 같습니다.

```r
unlink("result", recursive=TRUE)
dir.create("result");
...
```

### 결과 파일 생성

```r
fileOut<-file("result/output.txt")

...
writeLines(c("Hello EDISON."), fileOut)

close(fileOut)
```

### Octave
### result 폴더 생성
Octave의 경우 별도의 선언없이 ```mkdir``` 함수를 이용하면 되며, ```result``` 폴더를 생성하는 예제는 아래와 같습니다.

```matlab
...
rmdir result
mkdir result
...
```

### 결과 파일 생성

```matlab
file_out = fopen('result/result.txt', 'w');
...

...
fdisp(file_out, 'Hello EDISON.');
...

...
fclose(file_out);
```
