# gif animation 파일 만들기

imagemagick을 사용해 여러장의 그림 파일을 하나의 gif 파일로 생성할 수 있습니다. gif animation 생성하기 위해서는, 각 프래임별 그림파일이 생성되어 있어야 합니다. ```bessel[프래임넘버].png```인 그림파일들을 하나의 gif로 생성하는 경우


```bash
$ ls
bessel001.png  bessel008.png  bessel015.png  bessel022.png  bessel029.png  bessel036.png  bessel043.png  bessel050.png
bessel002.png  bessel009.png  bessel016.png  bessel023.png  bessel030.png  bessel037.png  bessel044.png
bessel003.png  bessel010.png  bessel017.png  bessel024.png  bessel031.png  bessel038.png  bessel045.png
bessel004.png  bessel011.png  bessel018.png  bessel025.png  bessel032.png  bessel039.png  bessel046.png
bessel005.png  bessel012.png  bessel019.png  bessel026.png  bessel033.png  bessel040.png  bessel047.png
bessel006.png  bessel013.png  bessel020.png  bessel027.png  bessel034.png  bessel041.png  bessel048.png
bessel007.png  bessel014.png  bessel021.png  bessel028.png  bessel035.png  bessel042.png  bessel049.png
$ convert -delay 0.0001 -loop 0 bessel*.png result.gif
$ ls -al result.gif
-rw-r--r-- 1 edison edison 518738 2018-08-19 22:45 result.gif
```


그외 convert 명령어로는 다양한 그림 편집이 가능합니다.

[convert 명령어 사용법](http://www.albumbang.com/board/board_view.jsp?board_name=free&no=57)
