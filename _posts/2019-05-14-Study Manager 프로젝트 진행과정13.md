# 2019.05.14 Study Manager 프로젝트 진행과정 13

### thymeleaf오류
- ec2에서 build를 해서 프로젝트를 실행하니 아래와 같은 에러가 나왔다. 템플릿 엔진이 찾는 파일이 없을 때 나타나는 메세지다.
    * org.thymeleaf.exceptions.TemplateInputException: Error resolving template "/study/_main", template might not exist or might not be accessible by any of the configured Template Resolvers
- 확인 해 보니 study main으로 가는 controller에서 '/'를 붙여 절대 경로를 사용하려고 했기 때문이었다.
- /study/_main 에서 study/_main으로 수정하였다.
    ```java
    return "/study/main_";
    ↓
    return "study/main_";
    ```

