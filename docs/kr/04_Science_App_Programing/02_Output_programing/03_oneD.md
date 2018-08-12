# oneD file format

1차원 그래프를 EDISON 시스템에서 보여주기 원한다면, 아래와 같은 파일 형태로 데이터를 생성해야 합니다.

![oneD file](../../asset/image/04/02/image1.png)

oneD 파일은 [OSPPlotViewer 분석기]()를 통해 가시화 할 수 있습니다.

# 데이터 구조 설명
 - #NumField: **nDatafield** : 한 화면에 출력할 그래프의 갯수를 입력해주는 부분으로  **nDatafield** 대신 생성하고자 하는 필드 값을 숫자로 입력해 주면 된다. 필드 값은 10가 넘지 않도록 합니다.
   - ex) #NumField: 2   // 2개의 필드 생성
 - #LavelX: **xlabelname**, LavelY: **ylabelname** : x축 y축 이름값을 넣어주는 부분으로 20자가 넘지 않도록 합니다.
   -  ex) #LabelX: position(um), LabelY: energy(eV) // x축 이름을 position(um), y축 이름을 energy(eV)로 설정
 - #Field1: **FieldLegnd**, NumPoint: **nPoint** : 첫번째 필드의 이름값과 데이터 갯수를 적는 부분
   - ex) #Field1: EF_n at V=0.15(V), NumPoint: 300 // Field1의 이름은 EF_n at V=0.15(V) 이며, 300개의 데이터를 가지고 있음
 - x축의 데이터 값과 y축의 데이터 값을 space 또는 tab 간격을 두고 위에서 정의한 갯수 만큼 데이터를 써주면 됩니다.
 - #Field2도 Field1과 마찬가지로 작성해 주면 되며, 필수 갯수에 맞게 필드를 작성하면 됩니다.

### 샘플 데이터와 가시화 결과 화면
![oned result](../../asset/image/04/02/image2.png)


언어별 예제 보기

 - [C](../03_C/05_oneD.md)
 - [Fortran](../04_Fortran/05_oneD.md)
 - [Python](../05_Python/05_oneD.md)
