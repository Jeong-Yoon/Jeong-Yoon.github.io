# 2019.04.19 Study Manager 프로젝트 진행과정

### Study Detail 페이지
- study list 페이지에서 제목을 눌러서 study detail로 이동할 수 있도록 함.

```html
<a th:href="'/study/studyDetail/'+${study.studyId}" th:text="${study.studyName}">
```

- studyId로 curriculum까지 불러오는 것은 성공했지만 그 curriculum을 눌렀을 때, curriculum_detail을 불러오는 것은 실패했다. 
    * 페이지가 이동하는 것이 아니라 api와 javascript를 사용해서 바로 밑에 내용이 나오도록 하는 방법을 찾고 있다.
    * java.lang.StackOverflowError: null 에러가 발생한 상태이다.
