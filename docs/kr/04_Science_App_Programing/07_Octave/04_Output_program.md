
# Output programing

## result 폴더 생성
Octave의 경우 별도의 선언없이 ```mkdir``` 함수를 이용하면 되며, ```result``` 폴더를 생성하는 예제는 아래와 같습니다.

```matlab
...
rmdir result
mkdir result
...
```

## 결과 파일 생성

```matlab
file_out = fopen('result/result.txt', 'w');
...

...
fdisp(file_out, 'Hello EDISON.');
...

...
fclose(file_out);
```


## Octave plot을 그림파일로 저장하기

```print -dpng <저장할 파일명>``` 명령어를 통해 figure()로 생성한 그래프를 그림으로 저장할 수 있다.

```matlab
x = -10:0.1:10;

figure();
plot (x, sin (x));

print -dpng result/Image_Power.png;
```
