# 입력 프로그래밍

 EDISON에서 정의한 입출력 형식을 준수해야 합니다.
시뮬레이션 SW의 실행 방식은 명령행 인자(Command Line Argument) 방식을 따르며, ```./[실행 파일 명] [커맨드 옵션] [인풋 파일의 절대 경로]``` 형태로 실행해야 합니다.

- 실행 파일 이름이 a.out이고 입력 옵션이 “-i”로 설정한 경우 실행되는 명령어는 다음과 같습니다.
```bash
$ ./a.out –i /home/user1/data/input.dat
```
언어별 예제 보기

 - [C](../03_C/01_Inputfile_Open.md)
 - [Fortran](../04_Fortran/01_Inputfile_Open.md)
 - [Python](../05_Python/01_Inputfile_Open.md)
 - [R](../06_R/01_Inputfile_Open.md)
 - [Octave](../07_Octave/01_Inputfile_Open.md)

입력 파일이 두개 이상인 경우 각각의 인풋 파일의 옵션은 서로 다른 값을 가져야 한다. 이 경우에서 실행 방식은 다음과 같다.

```
./[실행 파일 명] [인풋 옵션1] [인풋 파일 1의 절대 경로] [인풋 옵션2] [인풋 파일 2의 절대 경로] …
```

 - 입력 파일이 두개이며, input.dat, block.msh 파일을 각각 “-i”, “-m” 입력 옵션을 통해 파일을 받는 경우 실행되는 명령어는 다음과 같다.
 ```
  $ ./a.out –i /home/user1/data/input.dat -m /home/user1/data/block.msh
 ```

 언어별 예제 보기

  - [C](../03_C/02_Multi_Inputfile_Open.md)
  - [Fortran](../04_Fortran/02_Multi_Inputfile_Open.md)
  - [Python](../05_Python/02_Multi_Inputfile_Open.md)
  - [R](../06_R/02_Multi_Inputfile_Open.md)


3개 이상인 경우에도 서로 다른 입력 옵션을 정하고 이를 받을 수 있도록 코드를 작성하면 된다.

>소스코드에서 [인풋 파일의 절대경로] 처리를 위해 파일 경로를 버퍼에 저장하는 경우, 버퍼 공간을 512byte 잡아야 합니다.

>다음과 같이 프로그래밍 된 시뮬레이션 SW는 EDISON 플랫폼에서 서비스 될 수 있습니다.
> - 입력 파일을 입력 받지 않고 특정 위치의 특정 이름인 입력 파일만 읽는 경우
> - 사용자 키 입력을 통해 입력 파일의 이름이나 위치를 입력 받는 경우
