
# 입력 파일이 1개인 경우
[[링크] Github에서 보기](https://github.com/sp-edison/octave_example_input1)

[[링크] 소스코드 다운받기](https://github.com/sp-edison/octave_example_input1/archive/master.zip)

## 예제코드 다운로드 및 실행

Github 사이트에 접속 해서 전체 소스가 압축된 파일을 다운 받거나, ```git clone``` 명령어를 이용해 소스 코드를 받을수 있습니다.

Bulb 서버에 접속 후 아래 명령어를 실행하면, 해당 소스코드를 다운 받을 수 있습니다.
> Bulb 서버가 아닌 곳에서도 git이 설치되어 있다면, ```git clone``` 명령어를 통해 소스코드를 다운로드 받을 수 있습니다.
> - [git 설치하기](https://git-scm.com/book/ko/v2/%EC%8B%9C%EC%9E%91%ED%95%98%EA%B8%B0-Git-%EC%84%A4%EC%B9%98)

```bash
$  git clone https://github.com/sp-edison/octave_example_input1.git
```

다운로드가 완료되면, ```octave_example_input1``` 폴더가 생성됩니다. 폴더 구성은 다음과 같습니다.
```bash
r_example_input1
│   README.md
│   simrc
└───run.m
```
### 실행하기


source 명령어를 통해 simrc에 있는 명령어를 실행합니다.

  > simrc에는 R 모듈을 추가하는 명령어가 있습니다.

```bash
$ source simrc
```

R의 경우 Script를 실행하는 형태로 별다른 컴파일 과정이 필요 없습니다. 하지만 리눅스 명령어 chmod 명령어를 이용해 실행 권한을 주어야 합니다.  ```run.m```가 실행 파일인 경우 ```chmod +x run.m``` 를 리눅스 상에서 실행하면 됩니다.

```bash
$ chmod +x run.m
$ ./run.m -i /home/ino/test.input
/home/ino/test.input
```

## Source Code
### simrc

```bash
module load octave/4.0.3
```
```module load``` 명령어를 통해 octave 모듈을 추가합니다.

### run.m

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

```

## 주요 코드 설명
### 입력 인자 읽기

```
#!/usr/bin/env octave
```
```#!``` 을 통해 이 스크립트를 실행하는 파일이 ```octave```임을 지정합니다.

```m
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

```
```argv()``` 함수를 통해 매개변수 리스트를  args 변수에 저장합니다. 이후 while loop를 통해 -i 또는 --inp 값을 확인해 그 다음 매개변수를 inputfile 변수에 저장합니다.

이후 ```disp()``` 함수를 통해 입력 파일의 경로를 출력합니다.
