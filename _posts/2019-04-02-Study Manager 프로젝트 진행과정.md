# 190402 Study Manager 프로젝트 진행과정

### 회원가입 시 email 중복 확인 api 설정
- email을 입력하고 중복확인 버튼을 누르면 입력한 email값을 전송하여 중복여부를 확인한다.
    * api를 설정하여 jquery에서 값을 넘길 때, GET방식이 아닌 POST방식으로 진행하기 때문에 RequestParam이 아닌 RequestBody로 값을 받는다.
    
    * ajax에서 data 전송을 할 때 json 형식으로 전송되기 때문에
      Map 형식으로 받아 value로 값을 넘겨서 service에서 실행될 수 있도록 한다.

    * 중복된 email이 있으면 1, 없으면 0을 리턴한다.
    * 0이 리턴 되었을 때, email입력창을 disabled로 하여 더이상 입력받지 못하도록 처리한다.  

 ```javascript
$(document).ready(function () {
            $("#check-email").unbind("click").click(function (e) {
                e.preventDefault();
                fn_emailCheck();

            });
        });

        function fn_emailCheck() {
            var email =$('#email').val();
            var userData = {'email' : email}
            var jsonData = JSON.stringify( userData );

            if(email<1){
                document.getElementById('checkemail').innerHTML = 'email을 입력해주세요!';
            }else {
                $.ajax({
                    type : 'post',
                    url : '/api/emailCheck',
                    data : jsonData,
                    contentType: "application/json",
                    error : function (err) {
                        console.log(err.toString());
                        alert("서버가 응답하지 않습니다. \n 다시 시도해주시기 바랍니다.");

                    },
                    success : function (data) {
                        if(data==0){
                            $('#email').attr('disabled', true);
                            document.getElementById('checkemail').innerHTML = '사용가능한 email 입니다!';
                        }else if(data==1){
                            document.getElementById('checkemail').innerHTML = '이미 존재하는 email 입니다. 다른 email을 사용해주세요!';
                        }else{
                            alert("에러가 발생했습니다!");
                        }
                    }
                });
            }
        }
```
