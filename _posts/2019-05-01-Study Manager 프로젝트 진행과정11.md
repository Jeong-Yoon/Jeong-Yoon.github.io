# 2019.05.01 Study Manager 프로젝트 진행과정 11

### Study Detail 화면에서 curriculumDetail show(), hide() 기능
- Curriculum을 눌렀을 떄, CurriculumDetail 내용이 나오도록 해야했다.
- Curriculum을 누르면 내용이 나오도록 코드를 작성하니까 누를 때마다 내용이 추가되는 문제가 있었다.
- Curriculum을 눌렀을 때, 한번만 내용이 나오고 다시 누르면 내용이 없어지도록 코드를 작성했다.
    * 화살표 아이콘을 넣어서 누르기 전에는 아래 방향으로, 누르면 위 방향으로 향하게 했다.
    * 아이콘 방향에 따라서 작동할 수 있도록 if문을 사용했다. 
- 눌렀을 때, 밑에 내용을 눌러도 맨 위에 있는 화살표가 변하는 문제가 있었다.
    * curriculumId를 아이콘의 id에 넣어서 저장했더니 누르는 위치에 있는 아이콘이 반응했다.
- Curriculum Detail이 사라지기는 하는데, 다시 나타날 때 내용이 아이콘을 누른만큼 더해져서 나타났다.
    * 내용을 저장하는 curriculumDetailDiv가 empty 일때만 ajax를 실행할 수 있도록 했다.
- 내용을 나타낼 때는 show()를 숨길때는 hide()를 사용했다.

```javascript
function curriculumDetail(curriculumId) {

    var token = $("meta[name='_csrf']").attr("content");
    var header = $("meta[name='_csrf_header']").attr("content");

    var JSONObject = {'curriculumId': curriculumId};
    var jsonData = JSON.stringify(JSONObject);
    var curriculumDetailDiv = "";

    if (document.getElementById("myDIV2"+curriculumId).style.display == 'none') {
        document.getElementById("myDIV"+curriculumId).style.display = 'none';
        document.getElementById("myDIV2"+curriculumId).style.display = 'block';
        if ($('#curriculumDetails' + curriculumId).empty()) {
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
                    for (var i = 0; i < data.length; i++) {
                        curriculumDetailDiv = $('<li style="margin-left: 5%; margin-bottom:1%;" onclick="gotoContent('+ curriculumId +','+data[i].curriculumDetailId+')" value="' + data[i].curriculumDetailContent + '">' + data[i].curriculumDetailContent + '</li> ' +
                            '<input type="hidden" id="curriculumDetailContent'+data[i].curriculumDetailId+'" value="' + data[i].curriculumDetailContent + '"/>' +
                            '<input type="hidden" id="curriculumDetailId'+data[i].curriculumDetailId+'" value="' + data[i].curriculumDetailId + '"/>');
                        curriculumDetailDiv.appendTo($('#curriculumDetails' + curriculumId));
                    }
                },
                error: function (err) {
                    console.log(err.toString());
                }
            });
        }
        $('#curriculumDetails' + curriculumId).show();
    } else {
        document.getElementById("myDIV"+curriculumId).style.display = 'block';
        document.getElementById("myDIV2"+curriculumId).style.display = 'none'
        $('#curriculumDetails' + curriculumId).hide();
    }
}
```

### Study content 화면으로 내용 보내기, Study detail 화면으로 돌아가기
- Study content 화면으로 내용을 보낼 때, 각 Curriculum의 맨 처음 Curriculum detail만 데이터가 전송되는 문제가 있었다. 
    * 전송하는 모든 내용의 id마다 curriculumId와 curriculumDetailId를 붙였더니 문제를 해결할 수 있었다.

    ```javascript
    function gotoContent(curriculumId,curriculumDetailId) {

        var curriculumDetailContent = $('#curriculumDetailContent'+curriculumDetailId).val();
        var curriculumDetailId = $('#curriculumDetailId'+curriculumDetailId).val();
        var curriculumContent = $('input[id=curriculumContent'+curriculumId+']').val();
        ...

    }
    ```
- Study content 화면에서 Study Detail 화면으로 돌아가도록 history를 이용하였다.
```javascript
function gotolist() {
    history.go(-1);
}
```