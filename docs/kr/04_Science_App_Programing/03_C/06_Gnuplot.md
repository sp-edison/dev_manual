
# Gnuplot을 이용해 oneD plot 파일을 그림으로 저장하기

[[링크] Github에서 보기](https://github.com/sp-edison/c_example_gnuplot)

[[링크] 소스코드 다운받기](https://github.com/sp-edison/c_example_gnuplot/archive/master.zip)



코드는 [oneD 파일 출력하기](./05_oneD.md)의 코드에서 oneD 파일을 Gnuplot을 통해 line 그래프를 그리고 이를 그림파일로 저장하는 예제입니다.


## 주요 코드

```c
    ...
    fp_output = fopen("plot.gnu","w");

    fprintf(fp_output,"set term png\n");
    fprintf(fp_output,"set output \"result.png\"\n");
    fprintf(fp_output,"set xrange[-6:6]\n");
    fprintf(fp_output,"set yrange[-1.5:1.5]\n");
    fprintf(fp_output,"plot 'result.oneD' using 1:2 with lines\n");

    fclose(fp_output);

    system("gnuplot plot.gnu");

    system("rm -f plot.gnu");

    ...
```

fopen 함수를 통해 plot.gnu 파일에 Gnuplot 명령어들을 씁니다. 이를 통해 생성된 plot.gnu파일은 다음과 같습니다.

```bash
set term png        // png 형태로 저장
set output "result.png"   //저장하는 파일명은 result.png
set xrange[-6:6]        // x축의 범위는 -6~6까지
set yrange[-1.5:1.5]    // y축의 범위는 -1.5~1.5까지
plot 'result.oneD' using 1:2 with lines     // result.oneD 파일을 읽어 첫번째 column을 x 데이터로, 두번째 column을 y 데이터로 사용해 line plot
```


gnuplot에서 2-dimensional data file을 읽는 경우 아래와 같은 형태로 저장된 데이터를 읽습니다. #은 주석으로 처리되며, 공백이나 탭으로 column을 구분합니다.
```
#  X     Y
1.0   1.2
2.0   1.8
3.0   1.6
...
```

> [Gnuplot Data load 방법](http://lowrank.net/gnuplot/datafile-e.html#2dim)


생성된 plot.gnu 파일을 gnuplot 명령어로 실행합니다.
