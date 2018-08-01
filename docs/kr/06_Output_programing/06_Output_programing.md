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



```c
#include  <stdio.h>
...

int main (int argc, char *argv[]) {
    FILE *fp_out;

    system("rm -rf result");
    system("mkdir result");
    ...

    ...
    fp_out = fopen("result/result.oneD","w");
    ...

    ...
    fprintf(fp_out,"#NumField: 1\n");
    ...

    ...
    fclose(fp_out);
    ...
}
```

### FORTRAN Code
FORTRAN의 경우 ```CALL SYSTEM(COMMAND [, STATUS])```를 이용하면 되며, ```result``` 폴더를 생성하는 예제는 아래와 같습니다.
```fortran
      program sample

      ...
      CALL SYSTEM("rm -rf result")
      CALL SYSTEM("mkdir result")
      ...

      end program
```

### Python Code
Python의 경우 ```import os``` 를 선언하고 ```os.system (const char * string);``` 함수를 이용하면 되며, result 폴더를 생성하는 예제는 아래와 같습니다.

```python
 import os

 ...
   os.remove("result");
   os.mkdir("result");
 ...
```

### R
R의 경우 별도의 선언없이 ```dir.create()``` 함수를 이용하면 되며, ```result``` 폴더를 생성하는 예제는 아래와 같습니다.

```r
...
unlink("result", recursive=TRUE)
dir.create("result");
...
```


### Octave
Octave의 경우 별도의 선언없이 ```mkdir``` 함수를 이용하면 되며, ```result``` 폴더를 생성하는 예제는 아래와 같습니다.

```matlab
...
rmdir result
mkdir result
...
```
