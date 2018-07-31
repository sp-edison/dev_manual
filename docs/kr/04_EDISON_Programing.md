# EDISON 프로그래밍 개요

EDISON 플랫폼은 리눅스(CentOS 6)기반에서 동작하고 있으며, 시뮬레이션 SW의 경우 리눅스 환경에서 동작해야 합니다. 컴파일이 필요한 언어인 경우 리눅스(CentOS 6)에서 컴파일이 완료 되어야 합니다. 이를 위해 시뮬레이션 SW 개발자들을 위한 개발자(Bulb) 서버를 제공하고 있으며, Bulb 환경에서 동작하는 실행 파일(or 스크립트)로 개발 되어야 합니다. 입력 데이터를 받는 방식은 명령행 인자(Command Line Argument) 방식을 이용해 입력 데이터를 파일 형태로 읽어야 합니다.

# 사용가능한 Software list

## module
App 개발에 필요한 Software 목록은 module 명령어를 통해 조회가능 합니다.
> ```module av``` or ```module avail```

이후  ``` module load modulename``` 명령어를 통해 원하는 software를 사용할 수 있습니다.

> ```module load``` 통해 불러온 Software를 사용하는 앱 등록시 ```simrc```에 ``` module load modulename``` 를 작성하고 실행파일 업로드시 같이 업로드 해야합니다.

module load 예시 입력




## Compiler suite

### 1. Gnu compilers



||버전|실행방법|설치 경로|Website|
|--|--|--|--|--|
|Gnu|4.4.7|(기본값)|```gcc```|<http://gcc.gnu.org/>|
||4.9.3|```module load gcc/4.9.3``` 명령어를 실행 ||```/SYSTEM/gcc/4.9.3/build```||
||5.0.3|```module load gcc/5.0.3```|```/SYSTEM/gcc/4.9.3/build```|


# R Languege

```module load ``` 명령어를 통해


|버전|실행방법|설치 경로|
|--|--|--|
|3.3.2|```module load R/4.9.3``` 명령어를 실행|```gcc```|
|3.5.0|```module load R/4.9.3``` 명령어를 실행 |```/SYSTEM/gcc/4.9.3/build```|
|3.5.1|```module load R/5.0.3```|```/SYSTEM/gcc/4.9.3/build```|