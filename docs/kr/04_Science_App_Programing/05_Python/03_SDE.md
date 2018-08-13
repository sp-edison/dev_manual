
# SDE case study

[[링크] Github에서 보기](https://github.com/sp-edison/python_example_sde)

[[링크] 소스코드 다운받기](https://github.com/sp-edison/python_example_sde/archive/master.zip)

관련 문서 링크
- [SDE 프로그래밍 방법 개요](../02_Input_programing/01_Structured_Data_Editor.md)
- [SDE 데이터 타입 생성하기](../../06_EDITOR/01_SDE.md)

다음과 같이 숫자형 변수 2개(정수형 변수 1개, 실수형 변수 1개), 리스트형 변수 1개, 3차원 벡터 1개를 받는 SDE를 생성했습니다.

![Case1](../../asset/image/04/02/case1.png)

데이터 생성 방식은 다음과 같이 설정했습니다.

|KEY	|VALUE| KEY	| VALUE|
|--|--|--|--|
|value delimiter|	SPACE|Vector vracket|	SQUARE_SPACE|
|line delimiter|	NULL|Vector delimiter|	SPACE|

이렇게 설정되어 생성된 입력 파일은 다음과 같습니다.

```
INT1 42
REAL1 42.112
LIST1 a
VECTOR1 [ 1 0 0 ]
```

# Example

명령행 인자(Command Line Argument) 방식으로 생성된 입력 파일을 읽고 입력된 변수 값을 출력하는 예제 코드입니다.

```python
#!/usr/local/bin/python
""" EDISON python sample code"""

import sys
import os
import getopt


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
	opt  = line.split()[0]
	if opt in "INT1":
		int1 = int(line.split()[1])
		print "init1 :" + str(int1)
	elif opt in "REAL1":
		real1 = float(line.split()[1])
		print "real1 :" + str(real1)
	elif opt in "LIST1":
		list1 = line.split()[1]
		print "list1 :" + list1
	elif opt in "VECTOR1":
		vector1 = map(int, line.split("[")[1].split(']')[0].split())
		print "vector1 :" + str(vector1)
	else:
		print "SDE value read error. your input key is " + str(opt)
		sys.exit(1)

f_sde.close()
```

> 위 예제코드는 [입력 파일이 1개인 경우 예제](./01_Inputfile_Open.md)의 코드에서 SDE 파일을 읽는 부분을 추가하였습니다.

## 주요 코드 설명

#####주요 코드 설명

```Python
...
sde_lines = f_sde.readlines()

for line in sde_lines:
	opt  = line.split()[0]
	if opt in "INT1":
		int1 = int(line.split()[1])
		print "init1 :" + str(int1)
	elif opt in "REAL1":
		real1 = float(line.split()[1])
		print "real1 :" + str(real1)
	elif opt in "LIST1":
		list1 = line.split()[1]
		print "list1 :" + list1
	elif opt in "VECTOR1":
		vector1 = map(int, line.split("[")[1].split(']')[0].split())
		print "vector1 :" + str(vector1)
	else:
		print "SDE value read error. your input key is " + str(opt)
		sys.exit(1)
...
```
- ```f_sde.readlines()```함수를 이용해 입력 파일을 한줄씩 ```sde_lines``` 리스트에 저장합니다.

-  ```for ... in ... :``` 문을 이용해 ```sde_lines```원소를 하나씩 ```line```에 저장하고 ```sde_lines```의 길이 만큼 ```for``` 문을 반복합니다.
- 문자열을 나누기 위해 [split()](https://wikidocs.net/13) 함수를 사용합니다. 예제에서 처럼 괄호 안에 아무런 값도 넣어 주지 않으면 공백을 기준으로 문자열을 나눕니다.
  - ```line = "INT1 42"``` 인 경우 이 문자열을 나눈 결과 ```line.split()```는 ```['INT1', '42']``` 가 되고, 각각의 요소들을 지정하기 위해 뒤에 ```[숫자]``` 추가해 요소를 지정합니다. ```line.split()[0] ='INT1'``` 이며, ```line.split()[1] = 42```이 됩니다..
- 공백으로 나눈 값의 첫 번째 요소를 ```opt```에 저장해 해석에 필요한 변수 이름과 비교에 각각 저장합니다.
- 입력 파일에 저장된 값들은 문자열 이므로 숫자를 저장해야 하는 경우 이에 맞게 형 변환을 해주어야 합니다. 정수 형으로 변환하는 경우 ```int()```, 실수로 저장하는 경우 ```float()```을 이용하면 됩니다.

- ```vector1 = map(int, line.split("[")[1].split(']')[0].split())``` 을 정리하면
  - 초기 ```line```은 ```VECTOR1 [ 1 3 0 ]```이며, 이를 ```[```로 나누면, 나눠서 저장된 배열의 2번째 값 ```line.split("[")[1]```은 ```1 3 0 ]```이 됩니다.
  - 이를 다시 ```]```나눈 값의 첫 번째 값 ```.split("]")[0]```은 ```1 3 0``` 이 됩니다.
  - 이를 다시 공백으로 나누어 배열에 저장하고 [map(int, [배열])](http://stackoverflow.com/questions/7368789/convert-all-strings-in-a-list-to-int) 함수를 통해 문자 값인 각각의 원소를 정수 형으로 변환 시킵니다.


# SDE case study 2

SDE 생성시 데이터 생성 방식을 아래와 같이 설정한다면, 생성되는 입력 파일의 모양이 약간 달라질 것입니다.

|KEY	|VALUE| KEY	| VALUE|
|--|--|--|--|
|value delimiter|	EQUAL |Vector vracket|	SQUARE_SPACE|
|line delimiter|	SEMICOLON |Vector delimiter|	SPACE|

생성된 입력 파일
```
INT1 = 42 ;
REAL1 = 42.112 ;
LIST1 = a ;
VECTOR1 = [ 1 0 0 ] ;
```
추가된 value delimiter ```=``` 와 line delimiter```;```를 고려해 코딩을 해야 합니다.

변경전 코드
```python
...
for line in sde_lines:
	opt  = line.split()[0]
	if opt in "INT1":
		int1 = int(line.split()[1])
		print "init1 :" + str(int1)
	elif opt in "REAL1":
		real1 = float(line.split()[1])
		print "real1 :" + str(real1)
	elif opt in "LIST1":
		list1 = line.split()[1]
		print "list1 :" + list1
	elif opt in "VECTOR1":
		vector1 = map(int, line.split("[")[1].split(']')[0].split())
		print "vector1 :" + str(vector1)
	else:
		print "SDE value read error. your input key is " + str(opt)
		sys.exit(1)
...
```

변경후 코드
```python
...
for line in sde_lines:
      opt  = line.split()[0]
      if opt in "INT1":
            int1 = int(line.split('=')[1].split(';')[0])
            print "init1 : " + str(int1)
      elif opt in "REAL1":
            real1 = float(line.split('=')[1].split(';')[0])
            print "real1 : " + str(real1)
      elif opt in "LIST1":
            list1 = line.split('=')[1].split(';')[0]
            print "list1 : " + list1
      elif opt in "VECTOR1":
            vector1 = map(int,line.split("[")[1].split(']')[0].split())
            print "vector1 :" + str(vector1)
      else:
            print "error"
            sys.exit(1)
...
```
### 주요코드설명

```Python
int1 = int(line.split('=')[1].split(';')[0])
```
- ```line = 'INT1 = 42 ;'``` 이며 이를 ```=```로 나눈 ```line.split('=')[1]``` 값의 두 번째 값은 ```'42 ;'``` 가 됩니다. 이를 다시 ```;```로 나눈 첫번째 값은  ```'42'```인 문자열이 되며, 이를 ```int()``` 를 통해 정수로 형 변환을 시킵니다.
