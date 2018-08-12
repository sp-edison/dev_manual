# Python 언어
Python은 인터프리터 방식의 프로그래밍 언어. 별도의 빌드 과정이 없이 실행 할 수 있으며, 코드의 가독성이 좋은 장점을 가지고 있습니다. 또한 PyPI라는 패키지 저장소가 있어 원하는 패키지를 ```pip```명령어를 통해 쉽게 내려받을 수 있습니다. 이러한 장점으로 계산과학분야에서도 Python언어는 많이 활용되고 있습니다.

파이썬 스크립트를 리눅스 Command Line에서 실행하는 방법은 2가지 입니다.
- 실행 파일 앞에 python을 명시하고 실행하는 방법입니다. 예를들어 main.py 파일을 실행하기 위해서는 ```python main.py``` 명령어로 실행하면 됩니다.
- 파이썬 스크립트 파일 첫줄에 ```#!```(Shebang)을 통해 스크립트를 실행시켜줄 프로그램의 경로 지정해주면 됩니다.
  - 일반적으로 ```#!/usr/bin/env python```로 선언하면 됩니다. 여기서 ```env```명령어가 환경 변수에서 지정한 언어의 위치를 찾아서 실행하게 됩니다.
  - ```env```명령어를 쓰지 않고 직접 python 경로를 지정해 주어도 됩니다.
    - ex) ```#!/SYSTEM/python/2.7.11/bin/python```
  - 이 경우 ```chmod +x filename.py``` 명령어를 통해 해당 파일에 실행 권한을 줘야 합니다.

## local path에 패키지 설치하기
Python으로 코드 개발시 추가 패키지 설치가 필요한 경우가 있습니다. Bulb에서 pip로 파이선 패키지 설치시 Permission denied에러가 발생합니다.

```
Could not install packages due to an EnvironmentError: [Errno 13] Permission denied: '/usr/local/lib/python2.7/site-packages/ipython_genutils-0.2.0.dist-info'
Consider using the `--user` option or check the permissions.
```
pip 명령어의 ```-t```옵션을 이용하여 python이 설치된 경로가 아닌 local 경로에 설치하면 문제를 해결할 수 있습니다.
```
pip install -t <설치할 경로> <설치할 패키지>
```
numpy 패키지를 lib 경로에 설치한다면, 아래 명령어를 사용하면 됩니다.

```bash
pip install -t ./lib numpy
```
파이썬에서 lib 경로에 설치한 패키지를 읽어올수 있도록 환경변수를 추가해줍니다.

```bash
export PYTHONPATH=lib
```

### local path의 패키지를 사용하는 파이썬 코드를 사이언스 앱으로 등록하기

사이언스 앱으로 등록하고자 하는 파이썬 코드가 local path의 패키지를 사용하는 경우, 실행 파이썬 스크립트가 있는 위치에 ```lib``` 폴더에 패키지를 설치하고, ```simrc``` 파일에 ```export PYTHONPATH=lib``` 명령어를 저장합니다. 이후 앱 등록시 ```lib``` 폴더와 ```simrc``` 파일을 실행 스크립트와 같이 압축하여 업로드 해주시면 됩니다.

## python 3 버전 사용하기
EDISON 환경에서 python3가 설치되어 있는 경로는 다음과 같습니다.
```
/SYSTEM/Python/3.6.3
```
환경변수에 파이썬 3이 설치경로를 추가해주면 python3을 사용할 수 있습니다.
```
export PATH=/SYSTEM/Python/3.6.3/bin:$PATH
```
다른 방법으로는 파이썬3 스크립트 파일 첫줄에 ```#!```을 통해 python3의 경로를 지정해주면 됩니다.

 - ```$PATH```환경변수에 python3 경로가 추가된 경우라면, ```#!/usr/bin/env python3```
 - 아니라면, ```#!SYSTEM/Python/3.6.3/bin/python```을 스크립트 파일 첫줄에 적어주어야 합니다.
