# 2019.04.16 Study Manager 프로젝트 진행과정4

### join 실행 시 방식 수정
- Restlet으로 테스트를 하기 위해서 JoinFormDto를 @RequestBody로 받아 오도록 수정했는데, UserController가 RestController로 설정되어 있지 않고 데이터를 json 형식으로 넘기는 것이 아니라 form 그대로 넘기게 되어있기 때문에 가입이 되지 않는 문제가 발생하였다.
    * json으로 데이터를 넘기면 request header에 Content-Type이 application/json으로 되어 있지만, 그냥 form 그대로 넘기게 되면 application/x-www-form-urlencoded로 되어 있다.
     * @RequestBody로 파라미터를 설정해두면 json 형식으로 데이터가 넘어온다는 뜻인데, 그렇게 받으려면 email 중복 확인처럼 javascript로 넘기는 코드를 작성해 주어야 한다.
     <br><br>
- json으로 데이터를 넘기고 싶으면 api를 작성하자.
