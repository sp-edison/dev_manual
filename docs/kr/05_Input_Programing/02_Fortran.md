

# 입력 파일이 1개인 경우
[[링크] Github에서 보기](https://github.com/sp-edison/fortran_example_input1)

[[링크] 소스코드 다운받기](https://github.com/sp-edison/fortran_example_input1/archive/master.zip)

## 예제코드 다운로드 및 실행

Github 사이트에 접속 해서 전체 소스가 압축된 파일을 다운 받거나, ```git clone``` 명령어를 이용해 소스 코드를 받을수 있습니다.

Bulb 서버에 접속 후 아래 명령어를 실행하면, 해당 소스코드를 다운 받을 수 있습니다.
> Bulb 서버가 아닌 곳에서도 git이 설치되어 있다면, ```git clone``` 명령어를 통해 소스코드를 다운로드 받을 수 있습니다.
> - [git 설치하기](https://git-scm.com/book/ko/v2/%EC%8B%9C%EC%9E%91%ED%95%98%EA%B8%B0-Git-%EC%84%A4%EC%B9%98)

```bash
$  git clone https://github.com/sp-edison/fortran_example_input1.git
```

다운로드가 완료되면, ```fortran_example_input1``` 폴더가 생성됩니다. 폴더 구성은 다음과 같습니다.
```bash
fortran_example_input1
│   README.md
└───src
    │   Makefile
    └─  main.f
```

```bash
$ cd fortran_example_input1/src
$ make all
gfortran  -c main.f -o main.o
Compiled main.f successfully!
gfortran  -o ../bin/Hello.x main.o
Linking complete!
```

컴파일이 완료되면 ```fortran_example_input1``` 폴더 안에 ```bin``` 폴더가 생성되며, ```src/Mamkefile``` 에서 지정한 ```TARGET``` 명으로 실행 파일이 생성됩니다.
> 예제의 경우 ```TARGET```이 ```Hello.x```로 설정되어 있습니다.

생성된 ```bin``` 폴더로 이동하여, 임의의 파일을 입력 파일로 넣고 실행시 에러 없이 실행 종료됨을 확인할 수 있습니다.

```bash
$ cd ../bin
$ ./Hello.x -i /home/ino/test.input
```

이 예제에는 옵션 값이 맞는지 체크하고 옵션 뒤에 붙은 추가 파라미터 값이 파일 경로인지 확인하고 종료하는 프로그램입니다. 옵션 명이 잘못되었거나 입력 파일 경로가 잘못된 경우에는 에러가 발생합니다.

컴파일 된 파일을 삭제하고 싶은 경우에는 다시 ```src``` 폴더로 이동하여 ```make clean``` 명령어를 사용하면, 오브젝트 파일과 실행 파일을 삭제하게 됩니다.
```bash
$ cd ../src
$ make clean
rm -rf main.o ../bin/Hello.x
```

## Source Code
### main.f

```fortran
      program sample1

      CHARACTER(len=16) :: cmd_option_name , value_name , temp
      CHARACTER(len=512) :: inputdeck
      INTEGER :: num_of_args, i, io_status
      LOGICAL :: args_error_flag = .false.

      num_of_args = iargc()

      do i=1, num_of_args, 2
            call getarg(i,cmd_option_name)

            if( cmd_option_name .eq. "-i") then
                  call getarg(i+1,inputdeck)
                  write (*,*)  inputdeck
            else
                  args_error_flag = .true.
                  write (*,*) "ERROR: INVALID COMAND OPTION: " ,
     +            cmd_option_name
            endif
      enddo

      if ( args_error_flag .eqv. .true. ) then
            write (*,*) "CHECK YOUR COMAND OPTION"
            stop
      endif

      write (*,*) "Input file path : ", inputdeck



      end program
```

### 주요 변수 설명
- ```cmd_option_name``` : 커맨드 옵션(포트 명)을 저장하는 크기가 16인 character형 배열로 선언
- ```inputdeck``` : 입력 파일의 path를 저장하는 배열로 크기는 512인 characcter형 배열을 선언
- ```num_of_args``` : 실행 시 같이 입력된 argument의 개수를 저장하는 변수
- ```args_error_flag = .false.``` : 커맨드 옵션(포트 명)이 잘못 입력된 경우, 이 변수의 값을 ```.true.```로 변경

### 주요 코드 설명


```fortran
...
[1]   num_of_args = iargc()
...
```
[1] ```iargc()``` 함수를 이용하여 입력된 argument의 개수를 ```num_of_args``` 변수에 저장

```fortran
...
[2]   do i=1, num_of_args, 2
[3]         call getarg(i,cmd_option_name)

[4]         if( cmd_option_name .eq. "-i") then
                  call getarg(i+1,inputdeck)
[5]         write (*,*) inputdeck
            else
                  args_error_flag = .true.
                  write (*,*) "ERROR: INVALID COMAND OPTION: " ,
                  + cmd_option_name
            endif
      enddo
...
```
[2] ```do loop```를 이용해 ```num_of_args``` 개수 까지 ```i``` 값을 2씩 증가하면서 ```loop``` 문 수행. 예제에서 ```iargc()``` 함수로 받은 값이 2 이므로 ```loop```문이 한번만 수행 됨
[3] ```getarg()``` 함수를 이용해 ```i```번째 arument 값을 ```cmd_option_name``` 변수에 저장

[4] 저장한 ```cmd_option_name``` 값이 ```-i```와 같은지 확인하여 같으면, i+1번째 arument 값을 읽어서 ```inputdeck``` 배열에 저장.
> 커맨드 옵션을 ```-i```가 아닌 다른 옵션 명으로 설정 하고 싶다면, 이 부분을 수정하면 된다.

[5] ```cmd_option_name``` 값이 ```-i```와 다르면, ```args_error_flag``` 를 ```.false.```로 변경하고 잘못 입력한 커맨드 옵션을 출력

```fortran
      ...
[6]   if ( args_error_flag .eqv. .true. ) then
            write (*,*) "CHECK YOUR COMAND OPTION"
            stop
      endif
      ...
```
[6] 커맨드 옵션이 잘못 입력 되었는지 확인하고. 잘못 입력 되었을 경우 프로그램 종료
