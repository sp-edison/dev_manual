
# SDE case study

[[링크] Github에서 보기](https://github.com/sp-edison/r_example_sde)

[[링크] 소스코드 다운받기](https://github.com/sp-edison/r_example_sde/archive/master.zip)

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

```r
#!/usr/bin/env Rscript

library(optparse)

option_list <- list (
    make_option(c("-i","--inp"), type='character', help="Input file path", default=NULL ,metavar="character")
);

opt_parser <- OptionParser(option_list=option_list);
opt <- parse_args(opt_parser);

if (is.null(opt$inp)){
	print_help(opt_parser);
	stop("At least one argument must be supplied (input file).n", call.=FALSE);
}

inputfile = opt$inp;

## input param ##
lines <- readLines(inputfile);

sde <- list()

for (line in lines) {
    data <- unlist(strsplit(line, " "))
    if (data[1] == 'INT1') {
      sde$int1 = as.integer(data[2]);
    } else if (data[1] == 'REAL1') {
      sde$real1 = as.double(data[2]);
    } else if (data[1] == 'LIST1') {
      sde$list1 = data[2];
    } else if (data[1] == 'VECTOR1') {
      sde$vector1 = c(as.integer(data[3]),
		      as.integer(data[4]),
                      as.integer(data[5]));
    }
}

cat('INT1 is ', sde$int1, '\n');
cat('REAL1 is ', sde$real1, '\n');
cat('LIST1 is ', sde$list1, '\n');
cat('VECTOR1 is ', sde$vector1, '\n');
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
INT1 = 42
REAL1 = 42.112
LIST1 = a
VECTOR1 = [ 1 0 0 ]
```
추가된 value delimiter ``` = ```를 고려해 코딩을 해야 합니다.


```
## input param ##
con <- file(inputfile, "r");
lines <- readLines(con);
close(con);

sde <- list();

for (line in lines) {

    data <- unlist(strsplit(line, " = "))
  	if (data[1] == 'INT1') {
  		sde$int1 = as.integer(data[2]);
  	} else if (data[1] == 'REAL1') {
  		sde$real1 = as.double(data[2]);
  	} else if (data[1] == 'LIST1') {
  		sde$list1 = data[2];
      } else if (data[1] == 'VECTOR1') {
  		sde$vector1 = c(as.integer(data[3]),
  				as.integer(data[4]),
  				as.integer(data[5]));
      }
  }
```
