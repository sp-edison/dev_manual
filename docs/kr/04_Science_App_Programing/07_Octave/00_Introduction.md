# Octave 언어
Octave은 인터프리터 방식의 프로그래밍 언어입니다. Matlab과 호환성이 높은 GNU 소프트웨어로써 계산과학을 위한 도구로 사용됩니다.

> EDISON에서 R을 사용하기 위해서는 ```module load octave/4.0.3``` 명렁어를 통해 사용할 수 있습니다.


Octave 스크립트를 리눅스 Command Line에서 실행하는 방법은 2가지 입니다.
- 실행 파일 앞에 octave 명시하고 실행하는 방법입니다. 예를들어 main.py 파일을 실행하기 위해서는 ```octave run.m``` 명령어로 실행하면 됩니다.
- R 스크립트 파일 첫줄에 ```#!```(Shebang)을 통해 스크립트를 실행시켜줄 프로그램의 경로 지정해주면 됩니다.
  - 일반적으로 ```#!/usr/bin/env octave```로 선언하면 됩니다. 여기서 ```env```명령어가 환경 변수에서 지정한 언어의 위치를 찾아서 실행하게 됩니다.
    - 이 경우로 작성된 octave 스크립트를 사이언스 앱으로 등록하는 경우, ```simrc``` 파일에 사용하는 octave 경로 환경변수로 추가하거나, ```module load``` 명령어를 통해 octave 모듈을 추가해주어야 합니다.
  - ```env```명령어를 쓰지 않고 직접 octave 경로를 지정해 주어도 됩니다.
    - ex) ```#!/SYSTEM/octave-4.0.3/bin/octave```
  - 이 경우 ```chmod +x run.m``` 명령어를 통해 해당 파일에 실행 권한을 줘야 합니다.


> [Octave 메뉴얼 번역 프로젝트 링크 ](https://github.com/ptjoker95/Octave_Korean_Translate)


# Octave 스크립트 시작

Octave 스크립트를 EDISON에 올리고자 한다면 octave 스크립트 파일 맨 처음에 아래 3줄이 포함 되어있어야 합니다.

```Matlab
#!/usr/bin/env octave

clear, clc, close all
texi_macros_file("/dev/null");

...
```
``` clear, clc, close all```을 통해 스크립트 실행전 변수, 화면등을 초기화합니다. ```texi_macros_file("/dev/null");```을 통해 makeinfo와 관련된 에러메시지가 발생하지 않도록 설정합니다.


# 패키지 설치하기

```module load octave/4.0.3``` 명령어를 통해 octave 모듈을 추가하면, octave 명령어를 사용할 수 있습니다.

```bash
$ module load octave/4.0.3
$ octave
octave: X11 DISPLAY environment variable not set
octave: disabling GUI features
warning: docstring file '/SYSTEM/octave-4.0.3/share/octave/4.0.3/etc/built-in-docstrings' not found
GNU Octave, version 4.0.3
Copyright (C) 2016 John W. Eaton and others.
This is free software; see the source code for copying conditions.
There is ABSOLUTELY NO WARRANTY; not even for MERCHANTABILITY or
FITNESS FOR A PARTICULAR PURPOSE.  For details, type 'warranty'.

Octave was configured for "x86_64-pc-linux-gnu".

Additional information about Octave is available at http://www.octave.org.

Please contribute if you find this software useful.
For more information, visit http://www.octave.org/get-involved.html

Read http://www.octave.org/bugs.html to learn how to submit bug reports.
For information about changes from previous versions, type 'news'.

octave:1>
```

```pkg``` 명령어를 통해 사용하고자 하는 패키지를 설치 할 수 있습니다.
 - [pkg 명령어 설명](https://octave.sourceforge.io/octave/function/pkg.html)

패키지를 설치하고자 하는 경우 ```pkg install -local -forge <패키지이름>``` 명령어를 통해 설치 할 수 있습니다. ```-local``` 옵션을 통해 ```$HOME/octave``` 폴더에 패키지를 설치합니다.

 > pkg prifix 명령어를 통해 패기지 설치 위치를 변경할 수 있습니다.
 > local의 패키지를 설지하면 이와 관련한 정보는 ```$HOME/.octave_packages```위치에 저장됩니다.

```dataframe``` 패키지를 local에 설치하는 명령어는 다음과 같습니다.

```Matlab
 octave:1> pkg install -local -forge dataframe
 warning: creating installation directory /home/edison/octave
 warning: called from
     install at line 30 column 5
     pkg at line 405 column 9
 For information about changes from previous versions of the dataframe package, run 'news dataframe'.
 octave:2> pkg list
 Package Name  | Version | Installation directory
 --------------+---------+-----------------------
      control  |   3.0.0 | /SYSTEM/octave-4.0.3/share/octave/packages/control-3.0.0
    dataframe  |   1.2.0 | /home/edison/octave/dataframe-1.2.0
       signal  |   1.3.2 | /SYSTEM/octave-4.0.3/share/octave/packages/signal-1.3.2
 octave:3>
```
```pkg list``` 명령어를 통해 설치되어있는 패키지 확인이 가능합니다. 설치된 패키지를 사용하기 위해서는 ```pkg load <패키지이름>``` 명령어를 사용합니다.

## 간단한 예제

```module load octave/4.0.3```을 통해 octave 모듈을 추가하고, ```main.m``` 파일을 만들어 아래와 같이 작성합니다.

```Matlab
#!/usr/bin/env octave

clear, clc, close all
texi_macros_file("/dev/null");

pkg load dataframe;

truc={"Id", "Name", "Type";1, "onestring", "bla"; 2, "somestring", "foobar";}
tt=dataframe(truc)
```

이후 ```chmod +x main.m``` 명령어를 통해 실행권한을 부여하고, ./main.m 실행합니다.

```bash
$ module load octave/4.0.3
$ chmod +x main.m
$ ./main.m
octave: X11 DISPLAY environment variable not set
octave: disabling GUI features
warning: docstring file '/SYSTEM/octave-4.0.3/share/octave/4.0.3/etc/built-in-docstrings' not found
truc =
{
  [1,1] = Id
  [2,1] =  1
  [3,1] =  2
  [1,2] = Name
  [2,2] = onestring
  [3,2] = somestring
  [1,3] = Type
  [2,3] = bla
  [3,3] = foobar
}
tt = dataframe with 2 rows and 3 columns
_1     Id       Name   Type
Nr double       char   char
 1      1  onestring    bla
 2      2 somestring foobar
```

> local 패키지를 사용하는 octave 스크립트를 사이언스 앱으로 등록하고자 하는 경우, 사용하는 패키지를 관리자에게 설치해 달라고 요청해야 합니다.  
