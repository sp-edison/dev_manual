# simrc

simrc는 해석기(Solver)가 실행 되기전에 실행이 필요한 쉘스크립트를 저장하는 파일입니다. simrc에 작성된 쉘스크립트 명령어들은 해석기 실행되기 전에 실행됩니다. 앱 등록시 실행 파일과 같이 업로드해야 합니다.

> 쉘 프로그램은 유닉스에서 제공하는 명령어(인터페이스)를 그대로 사용할 수 있습니다.

## $PATH 환경변수
해석기로 등록한 실행 파일이나 스크립트의 환경변수 추가가 필요한 경우 simrc 파일에 환경 변수 등록 명령어를 활용할 수 있습니다.

gnuplot 명령어를 해석기에서 사용하려고 하는 경우 gnuplot을 실행하기 위해 실행 파일 위치를 다음과 같이 ```$PATH```변수에 지정해야 합니다.

```bash
export PATH=/SYSTEM/gnuplot-4.6.3/bin/bin:$PATH
```
해석기 실행 파일과 위 명령어를 simrc 파일로 작성하고, 같이 업로드 하면 해석기에서 gnuplot 명령어를 사용할 수 있습니다.

## $LD_LIBRARY_PATH 환경변수

사이언스 앱 실행시 아래와 같이 공유 라이브러리(shared libraries) 에 관련된 에러가 발생할 수 있습니다.

```
error while loading shared libraries: libblas.so.3: cannot open shared object file: No such file or directory
```

이경우 ```$LD_LIBRARY_PATH``` 환경변수애 에러가 발생한 라이브러리의 경로를 지정해 주면 해결할 수 있습니다.

```bash
export LD_LIBRARY_PATH=/SYSTEM/lapack/3.8.0/lib:$LD_LIBRARY_PATH
```

> ```ldd``` 명령어를 통해 지정한 프로그램이 요구하는 공유 라이브러리(shared libraries)를 출력하는 명령어입니다. 이 명령어를 통해 찾지 못한 공유 라이브러리를 확인 미리 확인 할 수 있습니다.


window에서 simrc 파일을 작성하는 경우 개행문자 방식이 unix 개열과 달라 에러가 발생할 수 있습니다.

윈도우 환경에서는 다음과 같은 방법으로 수정가능합니다.

Sublime text3 의 경우 Preferences -> Setting -> User 에 아래 명령어 추가

> "default_line_ending": "unix
