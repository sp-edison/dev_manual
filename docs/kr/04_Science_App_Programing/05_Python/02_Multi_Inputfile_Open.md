# 입력 파일이 여러개인 경우

입력 파일이 여러개인 경우는 [1개인 경우 예제](./01_Inputfile_Open.md)에서 ```getopt()``` 함수에 입력 받고자 하는 옵션을 추가하고,  ```for opt,arg in opts:``` 문에서 추가한 옵션에 대한 ```if```문을 추가하면 됩니다.

예를들어 ```-i, -m``` 옵션 2개를 통해 입력 파일을 받기 원한다면, ```“i:” -> “i:m:”```으로 고치고, 아래 ```for opt,arg in opts:```문의 ```-m``` 에 대한 ```elif```문을 추가하면 됩니다.


```python
#!/usr/local/bin/python

import sys
import getopt

try:
      opts, args = getopt.getopt(sys.argv[1:],"i:m:")
except getopt.GetoptError as err:
      print str(err)
      sys.exit(1)

for opt,arg in opts:
      if  opt in ("-i"):
            f_input = open(arg, "r")
      elif  opt in ("-m"):
            f_mesh = open(arg, "r")

print "input file = " + f_input.name

f_input.close()

print "mesh file = " + f_mesh.name

f_mesh.close()

```
