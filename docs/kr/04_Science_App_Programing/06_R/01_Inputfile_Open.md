
# 입력 파일이 1개인 경우
[[링크] Github에서 보기](https://github.com/sp-edison/r_example_input1)

[[링크] 소스코드 다운받기](https://github.com/sp-edison/r_example_input1/archive/master.zip)

## 예제코드 다운로드 및 실행

Github 사이트에 접속 해서 전체 소스가 압축된 파일을 다운 받거나, ```git clone``` 명령어를 이용해 소스 코드를 받을수 있습니다.

Bulb 서버에 접속 후 아래 명령어를 실행하면, 해당 소스코드를 다운 받을 수 있습니다.
> Bulb 서버가 아닌 곳에서도 git이 설치되어 있다면, ```git clone``` 명령어를 통해 소스코드를 다운로드 받을 수 있습니다.
> - [git 설치하기](https://git-scm.com/book/ko/v2/%EC%8B%9C%EC%9E%91%ED%95%98%EA%B8%B0-Git-%EC%84%A4%EC%B9%98)

```bash
$  git clone https://github.com/sp-edison/octave_example_input1.git
```

다운로드가 완료되면, ```r_example_input1``` 폴더가 생성됩니다. 폴더 구성은 다음과 같습니다.
```bash
r_example_input1
│   README.md
│   simrc
└───run.r
```
### 실행하기


source 명령어를 통해 simrc에 있는 명령어를 실행합니다.

  > simrc에는 R 모듈을 추가하는 명령어가 있습니다.

```bash
$ source simrc
```

R의 경우 Script를 실행하는 형태로 별다른 컴파일 과정이 필요 없습니다. 하지만 리눅스 명령어 chmod 명령어를 이용해 실행 권한을 주어야 합니다.  ```run.r```가 실행 파일인 경우 ```chmod +x run.r``` 를 리눅스 상에서 실행하면 됩니다.

```bash
$ chmod +x run.r
$ ./run.r -i /home/ino/test.input
input file = /home/ino/test.input
```

## Source Code
### simrc

```bash
module load R/3.3.2
```
```module load``` 명령어를 통해 R 모듈을 추가합니다.

### run.r

```r
#!/usr/bin/env Rscript


library(optparse)

option_list <- list (
    make_option(c("-i","--inp"), type='character', help="Input file path", default=NULL ,metavar="character")
);

opt_parser <- OptionParser(option_list=option_list);
opt <- parse_args(opt_parser);

if (is.null(opt$inp)){
      print_help(opt_parser)
  stop("At least one argument must be supplied (input file).n", call.=FALSE)
}

inputfile = opt$inp;

print(inputfile);
```

### 주요 코드 설명
#### 입력 인자 읽기

```
#!/usr/bin/env Rscript
```
```#!``` 을 통해 이 스크립트를 실행하는 파일이 ```Rscript```임을 지정합니다.

> EDISON 서버에서의 ```R``` 설치 위치는 ```/SYSTEM/R```에 버전 별로 정리되어 있습니다.
> ```module load``` 명령어를 통해 원하는 버전의 R 모듈을 추가할 수 있습니다.

```r
library(optparse)
```

```optparse``` 모듈을 이용하여 커맨드 라인에서 스크립트 실행시 입력 옵션과 입력 파일을 받을 수 있도록 구성합니다.


``` r
option_list <- list (
    make_option(c("-i","--inp"), type='character', help="Input file path", default=NULL ,metavar="character")
);
```

```“-i”, “-inp”``` 옵션을 생성해 ```option_list```에 저장합니다.
```type='character'```을 통해 옵션 뒤에 받을 추가 값을 ```character```로 지정합니다. ```default=NULL```을 통해 기본값을 따로 지정하지 않으며, ```help```와 ```metaver```을 설정해 help 커멘드 실행시 필요한 정보를 입력합니다.

> 입력 옵션이 여러개인 경우 ```make_option```부분을 추가하여 작성합니다.

``` r
opt_parser <- OptionParser(option_list=option_list);
opt <- parse_args(opt_parser);

inputfilepath = opt$inp;
print(inputfilepath);
```
스크립트 실행시 입력된 입력 인자들을 ```option_list```와 비교하여 옵션에 맞게 입력 되어 있다면, ```opt <- parse_args(opt_parser);``` 을 통해 ```opt$[옵션명]```에 해당 옵션을 통해 받은 추가 문자열(입력파일 경로)을 저장합니다.

이후 ```print()``` 함수를 통해 입력 파일의 경로를 출력합니다.
