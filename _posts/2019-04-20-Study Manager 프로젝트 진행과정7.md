# 2019.04.20 Study Manager 프로젝트 진행과정

### curriculum_detail 불러오기
- curriculum을 눌렀을 때, 밑에 curriculum_detail 내용을 뜨도록 했다.
    * ajax를 이용해서 내용을 불러오고 그 내용을 정해둔 div에 뜨도록 했다.

    ```javascript
    $.ajax({
         url: '/api/curriculumDetail',
        method: 'post',
        data: jsonData,
        async: false,
        contentType: "application/json",
        beforeSend: function( xhr ) {
            xhr.setRequestHeader(header, token);
        },
        success: function (data) {
            for(var i = 0; i < data.length; i++) {
                var curriculumDetailDiv = $('<li style="margin-left: 5%;">' + data[i].curriculumDetailContent + '</li>');
                curriculumDetailDiv.appendTo($('#curriculumDetails'+curriculumId));
            }
        },
        error: function (err) {
            console.log(err.toString());
        }
    });
   
    ```

    * div에 코드를 입력하는 것이 아니라 ajax가 성공하면 띄우도록 직접 html 코드를 넣어준다.
    * for문을 이용해서 curriculum과 관련된 모든 detail을 불러와서 출력해준다. 
