# Paraview

3D 과학 데이터 가시화 도구로써 [The ParaViewWeb Visualizer application](https://github.com/kitware/visualizer)을 제공하고 있습니다. [VTK file 포멧](https://www.vtk.org/wp-content/uploads/2015/04/file-formats.pdf) 형식의 데이터를 가시화 할 수 있으며, 그외 다른 데이터도 가시화 가능합니다.
- [가시화 가능 파일 포맷 확인하기](https://www.paraview.org/Wiki/ParaView/Users_Guide/List_of_readers)

![paraview](../asset/image/07/paraview1.jpg)
에디슨  Paraview을 실행환 화면입니다. 왼쪽 컨트롤 메뉴가 위치해 있으며, 두번째 파일 모양의 아이콘을 선택하면 가시화 할 수 있는 파일을 확인할 수 있습니다.

![paraview](../asset/image/07/paraview2.jpg)
Animation 을 활용하기 위해서는 각 프래임 별로 vtk 파일을 생성해야하며, <파일명>.<프래임>.<확장자> 형태의 파일 이름을 가져야 합니다.
- [Animation 기능을 사용하기 위한 파일이름 규칙](https://www.paraview.org/Wiki/Animating_legacy_VTK_file_series)


![paraview](../asset/image/07/paraview.gif)
상단 플래이 버튼을 통해 에니메이션 결과를 확인 할 수 있습니다.
