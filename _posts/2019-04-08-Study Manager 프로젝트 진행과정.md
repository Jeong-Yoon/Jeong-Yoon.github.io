# 2019.04.08 StudyManager 프로젝트 진행과정

### csrf issue
- Spring Security에서는 http 요청을 할 때, post 방식을 사용하면 csrf 인증을 사용한다.
- 단순 html form 태그로 값을 넘길 때는 hidden 값으로 csrf 값을 넣어 보내주면 되지만 ajax를 사용하는 경우는 다르다.
- ajax에서 csrf 인증값 넘기는 방법
    * html 태그 head 부분에 <meta>로 csrf token과 csrf header를 넣어준다.
    * ajax 전에 var로 값을 넣어준 다음, beforeSend를 이용하여 request헤더에 csrf header와 token 값을 넣어주도록 한다.
    * html head부분
    
    ```html
    <meta name="_csrf" th:content="${_csrf.token}"/>
    <meta name="_csrf_header" th:content="${_csrf.headerName}"/>
    ```
    
    * ajax부분
    ```javascript
    var token = $("meta[name='_csrf']").attr("content");
    var header = $("meta[name='_csrf_header']").attr("content");

    $.ajax({
        type: 'post',
        url: '/api/emailCheck',
        data: jsonData,
        async: false,
        contentType: "application/json",
        error: function (err) {
            console.log(err.toString());
            alert("서버가 응답하지 않습니다. \n 다시 시도해주시기 바랍니다.");
            return false;
        },
        beforeSend: function( xhr ) {
            xhr.setRequestHeader(header, token);
        },
        success: function (data) {
            if (data == 0) {
                $('#checkemail').css('color', 'green');
                document.getElementById('checkemail').innerHTML = '사용가능한 email 입니다!';
                return true;
            } else if (data == 1) {
                 $('#checkemail').css('color', 'red');
                 document.getElementById('checkemail').innerHTML = '이미 존재하는 email 입니다. 다른 email을 사용해주세요!';
                return false;
            } else {
                alert("에러가 발생했습니다!");
                return false;
            }
        }
    }
            
    ```

- 값을 넣는 데 자꾸 csrf값이 넘어가지 않아 원인을 한참 찾아본 결과,
  thymeleaf로 view 페이지를 만들었는데 html값으로 넘기려고 해서 생긴 문제였다.
  content앞에 th:를 붙여주니 제대로 동작했다.
  
