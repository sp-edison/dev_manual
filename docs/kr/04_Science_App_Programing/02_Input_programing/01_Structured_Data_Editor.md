# Structured Data Editor (SDE)

EDISON 플랫폼에서는 SDE(Structured Data Editor) 이라는 기능을 제공하여, 시뮬레이션 수행에 필요한 변수 값, 문자열, 벡터등의 데이터를 웹에서 바로 입력할 수 있는 기능을 제공하고 있습니다.

> EDISON 사업 초창기  SDE으로 불리던 데이터 형태를 Structured Data Editor로 명칭을 변경하였습니다.

SDE를 자신의 시뮬레이션 SW에 활용하고 싶다면, SDE에서 생성되는 입력 파일을 읽을 수 있도록 프로그램을 작성해야 합니다. SDE 작성 시 입력 파일을 생성하는 규칙을 정할 수 있으며, 이 규칙에 따라 생성된 입력 파일을 읽어 올 수 있으면 됩니다. 프로그램 작성 시 유의 사항은 다음과 같습니다.
 - SDE 생성 규칙에 맞게 변수 값을 읽어와야 함
 - SDE 데이터의 생성 순서에 상관 없이도 동작해야 함
 - 원하는 변수 값들이 정상적으로 입력되지 않았다면 에러 메시지를 발생 시켜야 함

My EDISON > Datatype 관리 > Datatype 생성에서 신규 Datatype 생성 시 Editor 목록에서 SDE을 선택하고 추가 버튼을 누르면 SDE을 Editor로 사용하는 Datatype를 생성할 수 있습니다.
