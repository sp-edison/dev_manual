
# Output programing

## result 폴더 생성
R의 경우 별도의 선언없이 ```dir.create()``` 함수를 이용하면 되며, ```result``` 폴더를 생성하는 예제는 아래와 같습니다.

```r
unlink("result", recursive=TRUE)
dir.create("result");
...
```

## 결과 파일 생성

```r
fileOut<-file("result/output.txt")

...
writeLines(c("Hello EDISON."), fileOut)

close(fileOut)
```
