
# Output programing

## result 폴더 생성

Python의 경우 ```import os``` 를 선언하고 ```os.system (const char * string);``` 함수를 이용하면 되며, result 폴더를 생성하는 예제는 아래와 같습니다.

```python
 import os

 ...
   os.remove("result");
   os.mkdir("result");
 ...
```

## 결과 파일 생성

```Python
  # open()함수를 통해 result/result.txt을 쓰기 모드로 오픈
  f_out = open("result/result.txt","w")
  ...

  ...
  # f_out.wirte() 함수를 이용해 파일에 내용을 씀
  f_out.write("Hello EDISON.\n")

  ...
  # f_out.close() 함수를 통해 파일을 닫음
  f_out.close()
```
