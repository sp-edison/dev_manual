
# Output progrming
## result 폴더 생성

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

## 출력 파일 쓰기
C 언어에서 파일을 읽고 쓰기 위해서는 파일 입출력 함수를 사용한다. 출력 파일을 쓰기 위한 코드 구성은 다음과 같습니다.

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
```fprintf()``` 또는 ```fputs()``` 함수를 활용해 파일을 쓸 수 있습니다.
