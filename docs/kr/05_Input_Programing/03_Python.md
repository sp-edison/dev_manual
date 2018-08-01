
# 입력 파일이 1개인 경우
[[링크] Github에서 보기](https://github.com/sp-edison/python_example_input1)

[[링크] 소스코드 다운받기](https://github.com/sp-edison/python_example_input1/archive/master.zip)

## 예제코드 다운로드 및 실행

Github 사이트에 접속 해서 전체 소스가 압축된 파일을 다운 받거나, ```git clone``` 명령어를 이용해 소스 코드를 받을수 있습니다.

Bulb 서버에 접속 후 아래 명령어를 실행하면, 해당 소스코드를 다운 받을 수 있습니다.
> Bulb 서버가 아닌 곳에서도 git이 설치되어 있다면, ```git clone``` 명령어를 통해 소스코드를 다운로드 받을 수 있습니다.
> - [git 설치하기](https://git-scm.com/book/ko/v2/%EC%8B%9C%EC%9E%91%ED%95%98%EA%B8%B0-Git-%EC%84%A4%EC%B9%98)

```bash
$  git clone https://github.com/sp-edison/python_example_input1.git
```

다운로드가 완료되면, ```python_example_input1``` 폴더가 생성됩니다. 폴더 구성은 다음과 같습니다.
```bash
python_example_input1
│   README.md
└───main.py
```

Python의 경우 Script를 실행하는 형태로 별다른 컴파일 과정이 필요 없다. 하지만 리눅스 명령어 chmod 명령어를 이용해 그룹과 일반 사용자에게 읽기와 실행 권한을 주어야 합니다.  ```main.py```가 실행 파일인 경우 ```chmod u+x main.py``` 를 리눅스 상에서 실행하면 됩니다.

```bash
$ chmod u+x main.py
$ ./main.py -i /home/ino/test.input
input file = /home/ino/test.input
```

## Source Code
### main.py

```python
#!/usr/local/bin/python

import sys
import getopt

try:
      opts, args = getopt.getopt(sys.argv[1:],"i:")
except getopt.GetoptError as err:
      print str(err)
      sys.exit(1)

for opt,arg in opts:
      if  opt in ("-i"):
            f_inputdeck = open(arg, "r")

print "input file = " + f_inputdeck.name
inputdeck_lines = f_inputdeck.readlines()

f_inputdeck.close()
```

### 주요 코드 설명
```
 #!/usr/local/bin/python

import sys
import getopt
```
```#!``` 을 통해 이 스크립트를 실행시켜줄 파이썬 프로그램의 경로를 지정하여 필요한 모듈을 불러온다.
 > [Shebang과 env에 대한 설명](http://blog.gaerae.com/2015/10/what-is-the-preferred-bash-shebang.html)

 - sys 모듈 : 파이썬 인터프리터와 관련된 정보와 기능을 제공하는 모듈이며, 해당 스크립트로 넘어온 입력인자(argv)를 확인하기 위해 사용한다.
 - getopt 모듈 : 입력인자를 보다 편리하기 처리하게 해주는 모듈이다.

```Python
...

try:
      opts, args = getopt.getopt(sys.argv[1:],"i:")
except getopt.GetoptError as err:
      print str(err)
      sys.exit(1)
...
```

```getopt.getopt()``` 함수를 이용해 입력 인자를 옵션과 옵션에 대한 추가 값으로 분류 합니다. 추가 옵션 값을 가지는 ```“-i”``` 옵션을 받을 수 있으며, 이때 입력된 옵션 값은 ```opts```에 저장되고, 추가 옵션 값은 ```args```에 저장합니다.

- ```getopt.getopt(sys.argv[1:],“i:”)```에서 ```getopt.getopt()``` 함수의 첫 번째 인자는 프로그램 실행시 입력되는 파라미터 문자열 입력 받습니다. 기본적으로 실행 파일 이름을 제외한 문자열인 ```sys.argv[1:]``` 을 입력 받으며, 두 번째 인자는 입력 받을 단일 문자 옵션, 마지막 인자는 입력 받을 긴 문자 옵션이 입력됩니다.

- 옵션 뒤에 추가 옵션 값이 필요한 경우 단일 문자 옵션인 경우 옵션 명 뒤에 ```:```를 긴 문자 옵션인 경우 ```=```를 붙여 준줍니다.

- ```./main.py -i /home/ino/test.input``` 로 실행 시 ```opts```에 옵션 명과 옵션 값이 저장된 튜플 형태의 배열인 ```[(‘-i’, ‘input.dat’)]```가 저장됩니다.

입력된 옵션 값 이외에 다른 옵션 값이 입력되는 경우 ```getopt.GetoptError``` 에러가 발생하며, 이에 대한 에러 메시지는 ```err```에 저장됩니다.

```try ... except``` 구문을 이용해 잘못된 옵션 값이 입력된 경우 이에 대한 에러 값을 출력하고 프로그램을 종료합니다.

> [영어자료, getopt 함수 사용하기](https://docs.python.org/2/library/getopt.html)
> [한글자료, getopt 함수 사용하기](http://kaspyx.kr/69)

```python
...
for opt,arg in opts:
      if  opt in ("-i", "--inp"):
            f_inputdeck = open(arg, "r")
...
```
```opts```에 저장된 옵션 명을 ```opt```에 옵션 값을 ```arg```에 저장하고 이를 체크하는 부분입니다.

입력된 옵션 명이 ```-i```이면 이때의 옵션 값을 입력 파일의 경로라 판단하여 ```open()```함수를 통해 파일을 열고 이에 대한 정보를 ```f_inputdeck``` 이라는 파일 객체에 저장합니다.

```python
...
print "input file = " + f_inputdeck.name
inputdeck_lines = f_inputdeck.readlines()

f_inputdeck.close()
```
