
# SDE case study

[[링크] Github에서 보기](https://github.com/sp-edison/fortran_example_sde)

[[링크] 소스코드 다운받기](https://github.com/sp-edison/fortran_example_sde/archive/master.zip)

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

```fortran
program sample1

CHARACTER(len=16) :: cmd_option_name , value_name , temp
CHARACTER(len=512) :: sde
INTEGER :: num_of_args, i, io_status
LOGICAL :: args_error_flag = .false.

INTEGER INT1
DOUBLE PRECISION REAL1
CHARACTER LIST1, tempchar
INTEGER :: VECTOR1(3)

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

      if ( value_name .eq. "INT1") then
            READ(1,*) value_name,  INT1
            WRITE(*,*) "INT1 = ", INT1
      else if ( value_name .eq. "REAL1") then
            READ(1,*) value_name,  REAL1
            WRITE(*,*) "REAL1 = ", REAL1
      else  if ( value_name .eq. "LIST1") then
            read(1,*) value_name,  LIST1
            write(*,*) "list = ", LIST1
      else  if ( value_name .eq. "VECTOR1") then
            read(1,*) value_name, tempchar, VECTOR1(1),
+ VECTOR1(2), VECTOR1(3)
            write(*,*) "Vector = ", VECTOR1(1), VECTOR1(2),
+ VECTOR1(3)
      else
            WRITE(*,*) "SDE value read error"
            stop
      endif
end do



CLOSE(1)



end program

```

> 위 예제코드는 [입력 파일이 1개인 경우 예제](./01_Inputfile_Open.md)의 코드에서 SDE 파일을 읽는 부분을 추가하였습니다.

## 주요 코드 설명


### 주요 변수 설명
- ```INT1```, ```REAL1```, ```LIST1```, ```VECTOR1(3)``` : Inputdeck 파일에서 각각의 변수 값를 저장하는 변수
- ```io_status``` : 입력 파일 오픈 시 에러 발생 여부를 저장하는 변수

### 주요 코드 설명

```fortran
...

[1]   open(1,file=trim(inputdeck),iostat=io_status, status='old')
[2]   if (io_status /= 0) then
            write(*,*) 'File open error'
            stop
      end if

...
```
1. [open()](https://docs.oracle.com/cd/E19957-01/805-4939/6j4m0vnaf/index.html) 함수를 이용해 장치번호(UNIT)을 1로 설정하여 ```inputdeck``` 배열에 저장된 PATH의 인풋 파일 읽는다. 이때 [trim()](https://gcc.gnu.org/onlinedocs/gfortran/TRIM.html) 함수를 이용해 앞에서 받은 inputdeck 경로 뒤에 붙은 공백을 제거한다.
  - ```iostat=io_status``` 은 파일 오픈 시 에러 발생 여부를 확인하는 옵션으로, 정상적으로 파일 오픈시 0 값을 저장
  - ```status='old'``` 는 기존의 있는 파일을 오픈하는 경우 ```old``` 값을 입력한다.
  - 예를들어 ```trim("Hello　　　　 ")``` 실항하면, "Hello"를 리턴하게 된다.
2. 입력된 path에 파일이 없거나 정상적으로 파일이 오픈이 안되는 경우 ```io_status```값이 0이 아닌 값을 리턴한다. 에러 메시지를 표시하고 프로그램을 종료한다.

```fortran
...
      do
[1]         READ(1,*, IOSTAT=io) value_name
            if ( io < 0) then
                  WRITE(*,*) "SDE file read end"
                  EXIT
            end if

[2]         BACKSPACE (1)

[3]         if ( value_name .eq. "INT1") then
                  READ(1,*) value_name,  INT1
                  WRITE(*,*) "INT1 = ", INT1
            else if ( value_name .eq. "REAL1") then
                  READ(1,*) value_name,  REAL1
                  WRITE(*,*) "REAL1 = ", REAL1
            else  if ( value_name .eq. "LIST1") then
                  read(1,*) value_name,  LIST1
                  write(*,*) "list = ", LIST1
            else  if ( value_name .eq. "VECTOR1") then
                  read(1,*) value_name, tempchar, VECTOR1(1),
     + VECTOR1(2), VECTOR1(3)
                  write(*,*) "Vector = ", VECTOR1(1), VECTOR1(2),
     + VECTOR1(3)
[4]         else
                  WRITE(*,*) "Inputdeck value read error"
                  stop
            endif
      end do



      CLOSE(1)
...
```
1. 장치 번호 1번을 사용해 앞서 open한 입력 파일의 한 줄을 [read()](https://docs.oracle.com/cd/E19957-01/805-4939/6j4m0vnat/index.html)를 사용해 읽는다. 이때 입력 파일의 첫 번째 문자열인 변수 이름을 ```value_name```에 저장한다.
 - 여기서 파일을 끝까지 다 읽은 경우 파일 read를 하게 되면 ```io``` 값이 0보다 작게 된다. 이를 통해 파일을 끝까지 다 읽었는지 여부를 판단하고 파일을 끝까지 다 읽은 경우 loop문을 빠저나온다.
2. [read()](https://docs.oracle.com/cd/E19957-01/805-4939/6j4m0vnat/index.html)함수를 이용해 이미 앞에서 읽었던 파일 라인의 변수의 값을 다시 읽기 위해서, [backspace()](https://docs.oracle.com/cd/E19957-01/805-4939/6j4m0vn7j/index.html)를 이용 방금 읽었던 파일 라인을 다시 읽을 수 있도록 파일 포인터를 이동한다.
3. 입력 파일에서 읽은 변수 이름을 확인하여 저장 함. 벡터 변수의 경우 변수 이름과 값 사이에 있는 ```[``` 문자를 ```tempchar``` 변수에 저장하고, ```VECTOR1(1~3)``` 에 각각의 벡터 원소들을 저장한다.
4. 원하지 않은 변수 값이 입력되는 경우 이에 대한 에러 메시지를 표시하고 프로그램을 종료


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

추가된 value delimiter와 line delimiter를 고려해 코딩을 해야 합니다. 위의 예제 코드와 크게 다르지 않으며, ```tempchar``` 변수를 이용해 변수 이름과 변수 값 사이에 있는 ```=``` 을 처리하는 부분을 추가하였다.

``` fscanf(fp_input, "%d", &input.int1); ``` -> ``` fscanf(fp_input, "%*s %d %*s", &input.int1); ```

변경전 코드
```fortran
...

    do
          READ(1,*, IOSTAT=io) value_name
          if ( io < 0) then
                WRITE(*,*) "SDE file read end"
                EXIT
          end if

          BACKSPACE (1)

          if ( value_name .eq. "INT1") then
                READ(1,*) value_name,  INT1
                WRITE(*,*) "INT1 = ", INT1
          else if ( value_name .eq. "REAL1") then
                READ(1,*) value_name,  REAL1
                WRITE(*,*) "REAL1 = ", REAL1
          else  if ( value_name .eq. "LIST1") then
                read(1,*) value_name,  LIST1
                write(*,*) "list = ", LIST1
          else  if ( value_name .eq. "VECTOR1") then
                read(1,*) value_name, tempchar, VECTOR1(1),
    + VECTOR1(2), VECTOR1(3)
                write(*,*) "Vector = ", VECTOR1(1), VECTOR1(2),
    + VECTOR1(3)
          else
                WRITE(*,*) "SDE value read error"
                stop
          endif
    end do
...
```

변경후 코드
```fortran
...
    do
          READ(1,*, IOSTAT=io) value_name
          if ( io < 0) then
                WRITE(*,*) "SDE file read end"
                EXIT
          end if

          BACKSPACE (1)

          if ( value_name .eq. "INT1") then
                READ(1,*) value_name, tempchar, INT1
                WRITE(*,*) "INT1 = ", INT1
          else if ( value_name .eq. "REAL1") then
                READ(1,*) value_name, tempchar, REAL1
                WRITE(*,*) "REAL1 = ", REAL1
          else  if ( value_name .eq. "LIST1") then
                read(1,*) value_name, tempchar, LIST1
                write(*,*) "list = ", LIST1
          else  if ( value_name .eq. "VECTOR1") then
                read(1,*) value_name, tempchar, tempchar,
    + VECTOR1(1), VECTOR1(2), VECTOR1(3)
                write(*,*) "Vector = ", VECTOR1(1), VECTOR1(2),
    + VECTOR1(3)
          else
                WRITE(*,*) "SDE value read error"
                stop
          endif
    end do
...
```
