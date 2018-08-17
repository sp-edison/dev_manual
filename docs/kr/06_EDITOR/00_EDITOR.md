
# Editor (편집기)

![사이언스 앱 실행 시나리오](../asset/image/03/image02_execution_scenario.png)

편집기는 EDISON에서 앱 실행시 입력 데이터를 편집할 수 있는 구성 요소를 말합니다. 현재 등록되어 있는 에디터 목록은 다음과 같습니다.

## 범용 편집기
|이름|설명|
|--|--|
|[SDE (Structured Data Editor)](./01_SDE.md)| 시뮬레이션 수행에 필요한 변수 값, 문자열, 벡터등의 데이터를 웹에서 바로 입력할 수 있는 UI를 제공 하는 편집기입니다. 데이터 타입 생성시 데이터 구조를 설계할 수 있습니다. |
|[TEXT_EDITOR](./03_Text_Editor.md)| 텍스트 파일을 편집할 수 있는 편집기 입니다.|
|[FILE_SELECTOR](./02_File_Selector.md)| 데이터 편집 기능은 없지만, 입력 파일을 선택하는 기능을 제공합니다.|
|[CSVEditor](./04_CSV_Editor.md)|CSV file 형태를 편집할 수 있는 편집기 입니다.|

> 입력 데이터 설계시 간단한 변수 입력이 필요한 경우 SDE를 활용하고, SDE로 표현 불가능한 데이터 형태의 경우 TEXT_EDITOR를 활용하시기 바랍니다. 그외 파일이 크거나 TEXT형식이 아닌 입력 파일의 경우 FILE_SELECTOR를 활용하시면 됩니다.

그외 특정 앱에서 활용하는 편집기가 있습니다.
- SIESTA_editor
- EPF_EDITOR
- runWTE_editor
