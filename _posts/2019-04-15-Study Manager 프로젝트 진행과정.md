# 2019.04.15 StudyManager 프로젝트 진행과정
### login 페이지 생성, index, join 페이지 수정
- 기존에 있던 view 페이지들과 새로 만든 페이지를 모바일에 맞게 수정하였다.
- 페이지마다 비슷하지만 다르게 크기 설정 등을 해줘야 하는 부분이 있어 각각 css 파일을 만들었다.
- 사이트의 기본 폰트를 나눔 고딕으로 설정하였다.
    * 한글만 나눔 고딕을 사용하고 영어는 Noto Sans를 사용하려고 했지만 한글과 영어를 나누어서 폰트 설정을 하려면 기본 폰트를 하나 정해두고 다른 언어는 그 언어마다 font-family로 지정해야 한다고 해서 일단 나눔 고딕으로 통일했다.

- login 페이지를 만들고 직접 로그인을 테스트를 하는데 계속 로그인 실패가 뜨길래 이유를 찾아보았다. Security config 파일을 설정할 때, usernameParameter를 id에서 email로 수정해주지 않아서 발생한 문제였다.

```java
.usernameParameter("id") -> .usernameParameter("email")
```
