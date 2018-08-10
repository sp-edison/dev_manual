# sin() 함수 결과를 oned로 출력하기


[[링크] Github에서 보기](https://github.com/sp-edison/fortran_example_oned)

[[링크] 소스코드 다운받기](https://github.com/sp-edison/fortran_example_oned/archive/master.zip)

## 예제코드 다운로드 및 실행

1개의 입력 파일 읽어, sin 그래프를 그리는 C언어 예제 파일입니다.

다음 수식의 변수들을 입력으로 받으며, 입력 변수는 a,b,c,d 총 4개 입니다.

$$ y = a * sin(bx+c)+d $$


입력 파일의 경우에는 Value delimiter를 ' '을 사용하였으며, Line delimiter를 구분하기 위해 ' \n '를 사용하였습니다. 파일로 입력을 받으며, 샘플 입력 파일은 아래와 같으며, **inp** 폴더에 **input.dat** 로 저장되어 있습니다.

```
a 1
b 0.4
c -0.5
d 0.3
```


본 예제는 ./[실행파일명] -[옵션] [입력 파일 경로]로 실행시 옵션 뒤에 입력된 경로의 파일을 열고 닫는 예제로 Makefile과 소스코드는 **src** 폴더에 저장되어 있으며, 컴파일이 완료되면 바이너리 파일은 **bin** 폴더에 저장됩니다.


## 설치하기

Github 사이트에 접속 해서 전체 소스가 압축된 파일을 다운 받거나, ```git clone``` 명령어를 이용해 소스 코드를 받을수 있습니다.

Bulb 서버에 접속 후 아래 명령어를 실행하면, 해당 소스코드를 다운 받을 수 있습니다.
> Bulb 서버가 아닌 곳에서도 git이 설치되어 있다면, ```git clone``` 명령어를 통해 소스코드를 다운로드 받을 수 있습니다.
> - [git 설치하기](https://git-scm.com/book/ko/v2/%EC%8B%9C%EC%9E%91%ED%95%98%EA%B8%B0-Git-%EC%84%A4%EC%B9%98)

```bash
$  git clone https://github.com/sp-edison/fortran_example_oned.git
```

```bash
fortran_example_oned
│   README.md
├───src
│   │   Makefile
│   └─  main.f
└───inp
    └─  input.dat
```

```src``` 폴더로 이동하여 ```make all``` 명령어를 사용하면, 컴파일이 완료됩니다.

```bash
$ cd fortran_example_oned/src
$ make all
gfortran -c main.f -o main.o
Compiled main.f successfully!
fortran -o ../bin/Hollo.x main.o
Linking complete!
```

컴파일이 완료되면 ```fortran_example_oned``` 폴더 안에 ```bin``` 폴더가 생성되며, ```src/Mamkefile``` 에서 지정한 ```TARGET``` 명으로 실행 파일이 생성됩니다.
> 예제의 경우 ```TARGET```이 ```Sin.x```로 설정되어 있습니다.

생성된 ```bin``` 폴더로 이동하여, ```inp```폴더에 있는 ```input.dat```을 입력 파일로 넣고 실행시 에러 없이 실행 종료됨을 확인할 수 있습니다.

```bash
$ cd ../bin
$ ./Sin.x -i ../inp/input.dat
User input is :
A = 1.000000
B = 0.400000
C = -0.500000
D = 0.300000
```


> 해당 예제를 이용하여 EDISON 웹포털에서 자동으로 소스 컴파일을 하실수 있습니다. 자동으로 소스 컴파일을 하기위해 선행되야하는 조건은 아래와 같습니다.
> - 본 예제와 같이 Makefile과 소스코드는 **src** 폴더에 저장되어 있어야 합니다.
> - **src** 폴더 안에서 ```make all``` 커맨드 입력시, 컴파일이 정상적으로 왼료된 경우 바이너리 파일이 **bin** 폴더에 저장이 되면 됩니다.

## Source code

### main.f
```fortran
program sample1

CHARACTER(len=16) :: cmd_option_name , value_name
CHARACTER(len=512) :: sde
INTEGER :: num_of_args, i, io_status, t
LOGICAL :: args_error_flag = .false.

DOUBLE PRECISION :: a, b, c, d

num_of_args = iargc()

do i=1, num_of_args, 2
      call getarg(i,cmd_option_name)

      if( cmd_option_name .eq. "-i") then
            call getarg(i+1,sde)
            write (*,*)  sde
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

write (*,*) "Input file path : ", sde


open(1,file=trim(sde),iostat=io_status, status='old')
if (io_status /= 0) then
      write(*,*) 'File open error'
      stop
end if


do
      READ(1,*, IOSTAT=io) value_name
      if ( io < 0) then
            WRITE(*,*) "SDE file read end"
            EXIT
      end if

      BACKSPACE (1)

      if ( value_name .eq. "a") then
            READ(1,*) value_name,  a
            WRITE(*,*) "a = ", a
      else if ( value_name .eq. "b") then
            READ(1,*) value_name,  b
            WRITE(*,*) "b = ", b
      else  if ( value_name .eq. "c") then
            read(1,*) value_name,  c
            write(*,*) "c = ", c
      else  if ( value_name .eq. "d") then
            read(1,*) value_name, d
            write(*,*) "d = ", d
      else
            WRITE(*,*) "SDE value read error"
            stop
      endif
end do
CLOSE(1)

CALL SYSTEM("rm -rf result")
CALL SYSTEM("mkdir result")


open(2,file="result/result.oneD")
write(2,*)"#NumField: 1"
write(2,*)"#LabelX: time, LabelY: a*sine(bx-c)+d"
write(2,*) "#Field1: sine() , NumPoint:128"

PI = 3.140592

do t = 1, 128, 1
      x = (4*PI * t )/128 -2*PI
      y = a*sin(b*x - c) +d
      write(2,'(F10.3, F10.3)') x, y
enddo

CLOSE(2)
end program

```


####주요 코드 설명

입력 파일을 읽고 이를 각각의 변수로 저장하는 부분은 [SDE 프로그래밍](./03_SDE.md) 예제를 참고하였습니다.

코드 앞부분에서 oneD 데이터 생성에 필요한 변수를 ``` INTEGER :: t``` ```DOUBLE PRECISION x, y``` 를 선언 하였습니다.


```fortran
      CALL SYSTEM("rm -rf result")
      CALL SYSTEM("mkdir result")

      open(2,file="result/result.oneD")
```

- 결과 데이터를 저장할 ```result```  폴더를 생성하는 부분이며, result 폴더안에 ```result.oneD``` 파일을 생성하고 쓰기모드로 오픈하였습니다.

```fortran
      write(2,*)"#NumField: 1"
      write(2,*)"#LabelX: time, LabelY: a*sine(bx-c)+d"
      write(2,*) "#Field1: sine() , NumPoint:128"
```

- oneD 파일의 헤더 부분의 내용을 생성합니다. [oneD 데이터 구조](../02_Output_programing/03_oneD.md)에 대한 자세한 설명은 해당 페이지를 참조하시기 바랍니다.
- 필드가 1개이며, x라벨이 time y라벨이 a * sin(bx+c)+d 이고 필드의 이름은 사용자가 입력한 a,b,c,d 값을 나타내고 있습니다.

```fortran
      PI = 3.140592

      do t = 1, 128, 1
            x = (4*PI * t )/128 -2*PI
            y = a*sin(b*x - c) +d
            write(2,'(F10.3, F10.3)') x, y
      enddo
```
- PI값을 정의하고, t=1 부터 128 까지 for문을 수행한다. 있대 $$-2*pi$$에서 $$2*pi$$ 까지 128등분으로 일정하게 나눈 값을 x에 저장하고, 이 x값에 대한 $$y=a*sin(bx+c)+d$$ 결과 값을 y에 저장한 뒤 각각 파일에 써주게 됩니다.
- 이때 저장하는 데이터의 규칙은 10진수 형태로 총 10자리를 가지고, 소수점 아래로는 3자리를 가지도록 저장합니다.
