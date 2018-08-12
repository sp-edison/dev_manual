# R 언어
R은 인터프리터 방식의 프로그래밍 언어입니다. 파이썬 언어와 마찬가지로 별도의 빌드 과정이 없이 실행 할 수 있으며, 코드의 가독성이 좋은 장점을 가지고 있습니다. R언어의 장점은 다음과 같습니다.

 - 오픈소스, 무료 소프트웨어
 - 포괄적인 통계플랫폼 : 다양한 라이브러리, 다양한 분석기법, 정형/비정형
 - 시각화 기능으로 수학 기호를 포함할 수 있는 출판물 수준의 그래프를 제공
   - 출처: http://sjh836.tistory.com/110 [빨간색코딩]

> EDISON에서 R을 사용하기 위해서는 ```module load R/<버전>``` 명렁어를 통해 사용할 수 있습니다.

파이썬 스크립트와 마찬가지로 R 스크립트를 리눅스 Command Line에서 실행하는 방법은 2가지 입니다.
- 실행 파일 앞에 Rscript을 명시하고 실행하는 방법입니다. 예를들어 main.py 파일을 실행하기 위해서는 ```Rscript run.r``` 명령어로 실행하면 됩니다.
- R 스크립트 파일 첫줄에 ```#!```(Shebang)을 통해 스크립트를 실행시켜줄 프로그램의 경로 지정해주면 됩니다.
  - 일반적으로 ```#!/usr/bin/env Rscript```로 선언하면 됩니다. 여기서 ```env```명령어가 환경 변수에서 지정한 언어의 위치를 찾아서 실행하게 됩니다.
    - 이 경우로 작성된 R 스크립트를 사이언스 앱으로 등록하는 경우, ```simrc``` 파일에 사용하는 R 경로 환경변수로 추가하거나, ```module load``` 명령어를 통해 R 모듈을 추가해주어야 합니다.
  - ```env```명령어를 쓰지 않고 직접 R 경로를 지정해 주어도 됩니다.
    - ex) ```#!/SYSTEM/R/3.3.3/bin/Rscript```
  - 이 경우 ```chmod +x run.r``` 명령어를 통해 해당 파일에 실행 권한을 줘야 합니다.

## local path에 패키지 설치하기

설치하고자 하는 위치에 폴더(ex: libs)를 생성합니다.

```bash
> mkdir libs
```

```module load R/<버전>``` 통해 R 모듈을 불러옵니다. 이후 ```R``` 명령어로 R을 실행합니다.

```bash
$ R

R version 3.4.4 (2018-03-15) -- "Someone to Lean On"
Copyright (C) 2018 The R Foundation for Statistical Computing
Platform: x86_64-apple-darwin15.6.0 (64-bit)

R is free software and comes with ABSOLUTELY NO WARRANTY.
You are welcome to redistribute it under certain conditions.
Type 'license()' or 'licence()' for distribution details.

  Natural language support but running in an English locale

R is a collaborative project with many contributors.
Type 'contributors()' for more information and
'citation()' on how to cite R or R packages in publications.

Type 'demo()' for some demos, 'help()' for on-line help, or
'help.start()' for an HTML browser interface to help.
Type 'q()' to quit R.
>
```
```install.packages("패키지이름", repos="저장소 위치", lib="설치위치")``` 명령어를 통해 패키지를 설치합니다. lib="libs"로 지정해 ```libs```경로에 설치합니다.

```lattice``` 패키지를 ```libs```폴더에 설치하는 경우
```R
> install.packages("lattice", repos="http://cran.r-project.org", lib="libs")
```

R 스크립트에서 로컬 경로에 설치된 패키지 경로를 추가해야 합니다. 패키지 경로를 추가는 ```.libPaths("<패키지 설치 경로>")``` 명령어를 실행하면 됩니다.

```libs``` 폴더의 설치된 패키지를 추가하는 경우
```
.libPaths("./libs")
```

### local path의 패키지를 사용하는 R 스크립트를 사이언스 앱으로 등록하기

사이언스 앱으로 등록하고자 하는 R 스크립트가 local path의 패키지를 사용하는 경우, 실행 R 스크립트가 있는 위치에 ```libs``` 폴더에 패키지를 설치하고, 앱 등록시 ```libs``` 폴더와 ```simrc``` 파일을 실행 스크립트와 같이 압축하여 업로드 해주시면 됩니다.
