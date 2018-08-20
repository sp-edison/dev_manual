# Structured Data Editor (SDE)

EDISON 플랫폼에서는 SDE(Structured Data Editor) 이라는 기능을 제공하여, 시뮬레이션 수행에 필요한 변수 값, 문자열, 벡터등의 데이터를 웹에서 바로 입력할 수 있는 기능을 제공하고 있습니다.

> EDISON 사업 초창기  Inputdeck으로 불리던 데이터 형태를 Structured Data Editor로 명칭을 변경하였습니다.

SDE 데이터 타입 생성과 관련하여 아래 링크를 참고하시기 바랍니다.
- [데이터 타입 생성하기](../../06_EDITOR/01_SDE.md)


SDE를 자신의 시뮬레이션 SW에 활용하고 싶다면, SDE에서 생성되는 입력 파일을 읽을 수 있도록 프로그램을 작성해야 합니다. SDE 작성 시 입력 파일을 생성하는 규칙을 정할 수 있으며, 이 규칙에 따라 생성된 입력 파일을 읽어 올 수 있으면 됩니다. 프로그램 작성 시 유의 사항은 다음과 같습니다.

 - SDE에서 생성된 파일은 text 파일 형태로 되어 있으며, 파일 한줄에 하나의 변수에 대한 이름(KEY)와 값(VALUE)로 구성되어 있다.
 - SDE 생성 규칙(Value delimiter, Line delimiter 등)에 맞게 변수 값을 읽어와야 함
 - SDE 데이터의 생성 순서에 상관 없이도 동작해야 함
 - 원하는 변수 값들이 정상적으로 입력되지 않았다면 에러 메시지를 발생 시켜야 함


## Example

다음과 같이 숫자형 변수 2개(정수형 변수 1개, 실수형 변수 1개), 리스트형 변수 1개, 3차원 벡터 1개를 받는 SDE를 생성하고, 데이터 생성 방식을 아래 표와 같이 설정하면,

 ![Case1](../../asset/image/04/02/case1.png)

 |KEY	|VALUE| KEY	| VALUE|
 |--|--|--|--|
 |value delimiter|SPACE|Vector vracket|SQUARE_SPACE|
 |line delimiter|NULL|Vector delimiter|SPACE|

생성된 입력 파일은 다음과 같습니다.

 ```
 INT1 42
 REAL1 42.112
 LIST1 a
 VECTOR1 [ 1 0 0 ]
 ```

생성 방식을 달리하여 아래 표와 같이 설정하게 되면,

 |KEY	|VALUE| KEY	| VALUE|
 |--|--|--|--|
 |value delimiter|EQUAL |Vector vracket|SQUARE_SPACE|
 |line delimiter|SEMICOLON |Vector delimiter|SPACE|


생성된 입력 파일은 다음과 같습니다.

```
INT1 = 42 ;
REAL1 = 42.112 ;
LIST1 = a ;
VECTOR1 = [ 1 0 0 ] ;
```

해석기(Solver)는 입력 파일에서 해석에 필요한 조건을 찾아 해석시 활용해야 합니다. 이것에 해단 언어별 예제는 아래 링크에 있습니다.

 - [C](../03_C/03_SDE.md)
 - [Fortran](../04_Fortran/03_SDE.md)
 - [Python](../05_Python/03_SDE.md)
 - [R](../06_R/03_SDE.md)
 - [Octave](../07_Octave/03_SDE.md)
