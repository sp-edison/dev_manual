# Datatype

사이언스 앱에서 생성되는 다양한 데이터의 형태를 구분하는 요소입니다. 데이터 형태를 편집할 수 있는 편집기(Editor)와 분석할 수 있는 분석기(Analyzer)를 지정할 수 있으며, 앱을 등록하는 과정에서 입출력 포트를 생성하는 경우, 각 포트별로 데이터 타입을 지정해야 합니다.

![사이언스 앱 구성요소 (a) 해석기 (b) 데이터 타입](../asset/image/03/image01_app_component.png)


> 예를 들어 흔히 사용하는 텍스트 파일을 하나의 데이터 타입으로 등록할 수 있습니다.
> 아래 그림은 편집기는 TEXT_EDITOR를 지정하고, 분석기는 OSPTextViewer로 설정한 ```text``` 데이터 타입을 조회한 결과 입니다.
>
> ![text 데이터 타입](../asset/image/05/datatype1.png)


## Datatype 생성

My EDISON > Datatype 관리 > 추가를 통해 신규 Datatype을 생성할 수 있습니다.

![Datatype 생성](../asset/image/05/01/sde2.png)

> 데이터 타입 생성전 검색을 통해 생성하고자 하는 데이터 타입을 찾아볼 수 있습니다.

![Datatype의 Editor 지정](../asset/image/05/01/sde3.png)

데이터 타입 생성은 데이터타입의 이름과 설명 그리고 사용하려고 하는 편집기(Editor)와 분석기(Analyzer)지정하여 생성할 수 있습니다. 여러개의 편집기와 분석기를 선택할 수 있으며, 기본 값을 지정해 주어야 합니다.

![Datatype의 Editor 지정](../asset/image/05/01/sde4.png)

마지막으로 샘플파일을 등록하면 데이터타입 등록이 완료됩니다.
