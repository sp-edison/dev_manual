# oneD 파일 생성하기


```
a = 1 ;
b = 0.4 ;
c = -0.5 ;
d = 0.3 ;
```


```c
    ...    // Make oneD file
    fp_output = fopen("result/result.oneD","w");

    fprintf(fp_output,"#NumField: 1\n");
    fprintf(fp_output,"#LabelX: time, LabelY: a*sine(bx+c)+d \n");
    fprintf(fp_output,"#Field1: a=%f b=%f c=%f d=%f,NumPoint:%d\n", input.a, input.b, input.c, input.d, SIZE);

    for(t=0; t< SIZE; t++) {
        x = (4*PI * t)/SIZE -2*PI;
        y = input.a*(sin( input.b*x +input.c)) +input.d;
        fprintf(fp_output, "%10.3f  %10.3f\n", x, y);
    }
    ...
```
