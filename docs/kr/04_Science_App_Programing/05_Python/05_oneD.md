# sin() 함수 결과를 oned로 출력하기


[[링크] Github에서 보기](https://github.com/sp-edison/python_example_oned)

[[링크] 소스코드 다운받기](https://github.com/sp-edison/python_example_oned/archive/master.zip)

## 예제코드 다운로드 및 실행

1개의 입력 파일 읽어, sin 그래프를 그리는 Python언어 예제 파일입니다.

다음 수식의 변수들을 입력으로 받으며, 입력 변수는 a,b,c,d 총 4개 입니다.

$$ y = a * sin(bx+c)+d $$


입력 파일의 경우에는 Value delimiter를 'SPACE'을 사용하였으며, Line delimiter를 구분하기 위해 'NULL'를 사용하였습니다. 파일로 입력을 받으며, 샘플 입력 파일은 아래와 같으며, **inp** 폴더에 **input.dat** 로 저장되어 있습니다.

```
a 1
b 0.4
c -0.5
d 0.3
```

본 예제는 ./[실행파일명] -[옵션] [입력 파일 경로]로 실행시 옵션 뒤에 입력된 경로의 파일을 열고 닫는 예제는 **bin** 폴더에 main.py 파일을 바로 실행합니다.

## 설치하기

Github 사이트에 접속 해서 전체 소스가 압축된 파일을 다운 받거나, ```git clone``` 명령어를 이용해 소스 코드를 받을수 있습니다.

Bulb 서버에 접속 후 아래 명령어를 실행하면, 해당 소스코드를 다운 받을 수 있습니다.
> Bulb 서버가 아닌 곳에서도 git이 설치되어 있다면, ```git clone``` 명령어를 통해 소스코드를 다운로드 받을 수 있습니다.
> - [git 설치하기](https://git-scm.com/book/ko/v2/%EC%8B%9C%EC%9E%91%ED%95%98%EA%B8%B0-Git-%EC%84%A4%EC%B9%98)

```bash
$  git clone https://github.com/sp-edison/python_example_oned.git
```

```bash
python_example_oned
│   README.md
├───bin
│   └─  main.py
└───inp
    └─  input.dat
```

```bin``` 폴더로 이동하여, ```inp```폴더에 있는 ```input.dat```을 입력 파일로 넣고 실행시 에러 없이 실행 종료됨을 확인할 수 있습니다.

```bash
$ cd ../bin
$ ./main.py -i ../inp/input.dat
input file = ../inp/input.dat
a : 1.0
b : 2.0
c : 0.5
d : 2.3
```


## Source code

### main.py
```python
#!/usr/local/bin/python
""" EDISON python sample code"""

import sys
import os
import getopt
import math
import numpy as np


try:
    otps, args = getopt.getopt(sys.argv[1:], "i:")
except getopt.GetoptError as err:
    print(str(err))
    sys.exit(1)

for opt, arg in otps:
    if opt in "-i":
        f_sde = open(arg, "r")

print("input file = " + f_sde.name)
sde_lines = f_sde.readlines()

for line in sde_lines:
    opt = line.split()[0]
    if opt in "a":
        a = float(line.split()[1])
        print("a : " + str(a))
    elif opt in "b":
        b = float(line.split()[1])
        print("b : " + str(b))
    elif opt in "c":
        c = float(line.split()[1])
        print("c : " + str(c))
    elif opt in "d":
        d = float(line.split()[1])
        print("d : " + str(d))
    else:
        print("SDE value read error. your input key is " + str(opt))
        sys.exit(1)

f_sde.close()

os.system("rm -rf result")
os.system("mkdir result")


f_out = open("result/result.oneD", "w")

times = np.arange(-2.0*math.pi, 2.0*math.pi, 0.1)

f_out.write("#NumField: 1\n")
f_out.write("#LabelX: time, LabelY: a*sine(x+b) \n")
f_out.write("#Field1: a=%f b=%f c=%f d=%f,NumPoint:%i\n" % (a, b, c, d, len(times)))

for time in times:
    y = a*math.sin(b*time-c)+d
    f_out.write("%10.3f     %10.3f\n" % (time, y))

f_out.close()
```


####주요 코드 설명

####주요 코드 설명

입력 파일을 읽고 이를 각각의 변수로 저장하는 부분은 [SDE 프로그래밍](./03_SDE.md) 예제에서 가져왔습니다.

```Python
import sys, os
import getopt
import math
import numpy as np
...
```
- [os.system()](https://wikidocs.net/33), [sin()](https://docs.python.org/2/library/math.html), [arange()](http://docs.scipy.org/doc/numpy/reference/generated/numpy.arange.html)을 사용하기 위해 ```math```와 ```numpy```를 import 하였습니다.

```Python
...
os.system("rm -rf result")
os.system("mkdir result")
...

```
- 결과 데이터를 저장할 ```result```  폴더를 생성합니다.


```python
f_out = open("result/result.oneD","w")

times = np.arange(-2.0*math.pi, 2.0*math.pi, 0.1)
```
- result.oneD 파일을 result 폴더에 쓰기 모드로 오픈하였으며, 이를 f_out에 저장하였습니다.
- numpy에서 제공하는 [arange()](http://docs.scipy.org/doc/numpy/reference/generated/numpy.arange.html) 함수를 이용해 -2*pi 부터 2*pi까지 0.1 간격의 배열인 ```times```을 생성하였습니다.

```python

f_out.write("#NumField: 1\n")
f_out.write("#LabelX: time, LabelY: a*sine(x+b) \n")
f_out.write("#Field1: a=%f b=%f c=%f d=%f,NumPoint:%i\n" % (a, b, c, d, len(times)))

```
- oneD 파일의 헤더 부분의 내용을 생성합니다. [oneD 데이터 구조](../02_Output_programing/03_oneD.md)에 대한 자세한 설명은 해당 페이지를 참조하시기 바랍니다.
- 필드가 1개이며, x라벨이 time y라벨이 a * sin(bx+c)+d 이고 필드의 이름은 사용자가 입력한 a,b,c,d 값을 나타내고 있습니다.

```python
for time in times:
    y = a*math.sin(b*time-c)+d
    f_out.write("%10.3f     %10.3f\n" % (time, y))

f_out.close()
```
- for문을 이용해 앞서 생성한 ```times```의 배열 값을 하나씩 읽고 이를 이용하여 $$y=a*sin(bx+c)+d$$ 에 대한 결과 y를 계산합니다. 이후 x에 저장할 값인 time과 y에 저장할 값인 y를 각각 파일에 쓰게됩니다.
- 이때 저장하는 데이터의 규칙은 10진수 형태로 총 10자리를 가지고, 소수점 아래로는 3자리를 가지도록 저장하였습니다.
