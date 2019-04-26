# 2019.04.25 Study Manager 프로젝트 진행과정9

### study content 페이지로 curriculumContent, curriculumDetailContent 값 넘기기
- study content 페이지로 curriculumContent, curriculumDetailContent 값을 전달했다.
    * 아직 javascript로 post로 값을 넘기는 방법을 찾지 못해서 일단 ajax로 값을 넘겨 넘어오는 지 확인하였다.
    * 값은 넘어오지만 ajax가 페이지를 이동하지 않은 상태로 값을 출력해주기 때문에 페이지 이동에 대한 문제가 남았다.
    * window.location.href 등을 시도해봤지만 페이지 이동은 되지 않았다.