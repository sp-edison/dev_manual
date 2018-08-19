# Gnuplot
그누플롯은 2차원이나 3차원 함수나 자료를 그래프로 그려 주는 명령행 응용 소프트웨어입니다. EDISON 시스템에서 그누플롯을 사용하기 위해서는 ```module load``` 명령어를 통해 gnuplot 모듈을 불러와야 합니다. 설치되어 있는 gnuplot은 다음과 같습니다.

```
gnuplot/4.6.3
gnuplot/5.0.6
```

[C 예제 보기 - oned file을 gnuplot을 이용 그림으로 저장하기](../03_C/06_Gnuplot.md)



## Gnuplot을 활용 gif 파일 만들기

Gnuplot을 이용 3차원 3d bessel 함수가 시간에 따라 변화하는 그래프를 gif로 만드는 예제입니다.



### run.plt

```bash
set term gif animate size 350,262
set output "animate.gif"

# color definitions
set palette rgb 3,9,9

unset key; unset colorbox; unset border; unset tics
set lmargin at screen 0.03
set bmargin at screen 0
set rmargin at screen 0.97
set tmargin at screen 1

set parametric
# Bessel function, which is moving in time
bessel(x,t) = besj0(x) * cos(2*pi*t)
# calculate the zeros for the bessel function (see Watson, "A Treatise on the
# Theory of Bessel Functions", 1966, page 505)
n = 6 # number of zeros
k = (n*pi-1.0/4*pi)
u_0 = k + 1/(8*k) - 31/(384*k)**3 + 3779/(15360*k)**5
set urange [0:u_0]
set vrange[0:1.5*pi]
set cbrange [-1:1]
set zrange[-1:1]

set isosamples 200,100
set pm3d depthorder
set view 40,200

# initializing values for the loop and start the loop
t = 0
end_time = 1
load 'bessel.plt'
```
### bessel.plt

```bash
# bessel loop
t = t + 0.02
#set output outfile
splot u*sin(v),u*cos(v),bessel(u,t) w pm3d ls 1
if(t<end_time) reread;
```

gnuplot 명령어를 통해 run.plt 파일을 실행하면, animate.gif 파일이 생성됩니다.

```bash
$ module load gnuplot
$ gnuplot run.plt
Could not find/open font when opening font "arial", using internal non-scalable font
End of animation sequence
```


![gnuplot result](../../asset/image/04/02/animate.gif)





[래퍼런스](http://www.gnuplotting.org/animation-gif/)
