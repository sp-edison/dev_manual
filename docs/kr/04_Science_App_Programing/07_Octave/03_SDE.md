
# SDE case study

[[링크] Github에서 보기](https://github.com/sp-edison/octave_example_sde)

[[링크] 소스코드 다운받기](https://github.com/sp-edison/octave_example_sde/archive/master.zip)

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

```m
#!/usr/bin/env octave

clear, clc, close all
texi_macros_file("/dev/null");


args = argv() ;
i = 1 ;
while i <= length(args)
    option = args{i} ;
    switch option
    case {"-i" "--inp"}
        inputfile = args{++i} ;
    otherwise
        disp("err") ;
        exit(1) ;
        break ;
    endswitch
    i++ ;
endwhile

disp(inputfile)

fid = fopen(inputfile, 'r') ;

lines = textscan(fid, "%s", 'delimiter',';\n');

i=1;
while i <= length(lines{1})
    line = strsplit(lines{1}{i}, ' ' );
    i++;
    switch line{1}
    case {"INT1"}
        int1 = str2num(line{2}) ;
    case{"REAL1"}
        real1 = str2double(line{2}) ;
    case{"LIST1"}
         list1 = line{2} ;
    case{"VECTOR1"}
        vector_tmp = strsplit(line{2}, " ");
        vector1 = { str2num(vector_tmp{1}),
                    str2num(vector_tmp{2}),
                    str2num(vector_tmp{3}) } ;
    endswitch
endwhile

disp(int1)
disp(real1)
disp(list1)
disp(vector1)

fclose ("all");
```

> 위 예제코드는 [입력 파일이 1개인 경우 예제](./01_Inputfile_Open.md)의 코드에서 SDE 파일을 읽는 부분을 추가하였습니다.


# SDE case study 2

SDE 생성시 데이터 생성 방식을 아래와 같이 설정한다면, 생성되는 입력 파일의 모양이 약간 달라질 것입니다.

|KEY	|VALUE| KEY	| VALUE|
|--|--|--|--|
|value delimiter|	EQUAL |Vector vracket|	SQUARE_SPACE|
|line delimiter|	NULL |Vector delimiter|	SPACE|

생성된 입력 파일
```
INT1 = 42 ;
REAL1 = 42.112 ;
LIST1 = a ;
VECTOR1 = [ 1 0 0 ] ;
```
추가된 value delimiter ``` = ```를 고려해 코딩을 해야 합니다.


```
...
while i <= length(lines{1})
    line = strsplit(lines{1}{i}, ' = ' );
    i++;
    switch line{1}
    case {"INT1"}
        int1 = str2num(line{2}) ;
    case{"REAL1"}
        real1 = str2double(line{2}) ;
    case{"LIST1"}
         list1 = line{2} ;
    case{"VECTOR1"}
        vector_tmp = strsplit(line{2}, " ");
        vector1 = { str2num(vector_tmp{2}),
                    str2num(vector_tmp{3}),
                    str2num(vector_tmp{4}) } ;
    endswitch
endwhile
...
```
