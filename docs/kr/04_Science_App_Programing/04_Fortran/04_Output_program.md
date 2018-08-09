
# Output programing

## result 폴더 생성

FORTRAN의 경우 ```CALL SYSTEM(COMMAND [, STATUS])```를 이용하면 되며, ```result``` 폴더를 생성하는 예제는 아래와 같습니다.
```fortran
      program sample
      ...

      ...
!      결과 파일이 저장될 result 폴더 생성
      CALL SYSTEM("rm -rf result")
      CALL SYSTEM("mkdir result")
      ...
```

## 출력 파일 쓰기

```FORTRAN
      ...
!      result/result.txt을 오픈
      open(2,file="result/result.txt")
      ...

      ...
!      파일안에 데이터를 씀
      write(2,*)"Hello EDISON."
      ...


      ...
!      파일을 닫음
      CLOSE(2)
```
```open()``` 함수를 이용해 장치번호(UNIT)을 2로 설정하여 result 폴더 안 result.txt 파일을 오픈한다. 여러개의 파일을 동시에 쓰거나 읽는 경우 장치번호가 겹치지 않게 조심해야합니다.
> 장치번호는 1 부터 99 사이의 정수로 설정할 수 있으며, 5는 표준 입력 standard input, 6은 표준 출력 standard output으로 이미 설정되어 있습니다.

장치 번호와 ```write()```함수를 통해 파일에 데이터를 쓸 수 있으며, 파일쓰기가 완료된 이후 ```close()``` 함수를 이용해 파일을 닫습니다.
