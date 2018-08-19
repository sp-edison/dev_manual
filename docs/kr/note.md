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



# 요구사항 정리

- 데이터 타입 등록 과정에서 샘플 파일 등록은 편집기와 분석기 설정하는곳으로 이동
- SDE로 생성한 데이터를 Json형태로 보고 편집할 수 있는 text창 추가
- SDE 순서 변경 기능 추가


뉴스레터와 관련 요구사항

EDISON 멀티보드(공지사항, 뉴스레터, 등등)에서 모바일에서 보는데 불편함이 없도록 수정

search, Site map 메뉴만 사라지도록
nsubtopwrap  div 테그가 모바일에서는 안보이도록 수정

제목 옆 글쓴이와 날짜가 여러줄로 표시되는 문제 수정

그림이 들어간 경우 폭조절

좌우 여백 값이 너무 큼

입력포트의 분석기를 레이아웃에 떨구는경우 입력 포트 에디터에 데이터가 입력되는 경우 분석기에 입력파일 가시화가 되어야 함


앱 등록시 업로드한 실행파일의 목록이 다 표시되지 않음 4개의 파일을 압축하여 올린경우 3개만 보임
