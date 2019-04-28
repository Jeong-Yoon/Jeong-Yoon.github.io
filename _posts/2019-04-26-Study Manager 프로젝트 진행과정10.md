# 2019.04.26 Study Manager 프로젝트 진행과정 10

### javascript로 post 방식으로 form 만들어서 보내기
- 데이터를 보내야 하는데 ajax로 데이터를 가져와서 넣는 부분이 있어서 단순 form으로는 데이터를 넘길 수가 없고 제목을 눌러서 넘어가기 때문에 function으로 onclick 처리를 해줘야 했다.
- ajax로 데이터를 보내고 페이지를 이동하려고 했는데 데이터는 넘어가지만 페이지 이동은 되지 않았다.
- javascript안에 있는 값들은 input hidden으로 해서 id 설정을 해서 값을 
- 방법을 찾아보니 function에 form을 만들어서 넘길 수 있었다.

    ```javascript
    function gotoContent() {
        var curriculumDetailContent = $('#curriculumDetailContent').val();
        var curriculumDetailId = $("#curriculumDetailId").val();
        var curriculumContent = $("input[name=curriculumContent]").val();

        var form = document.createElement("form");
        form.setAttribute("charset", "UTF-8");
        form.setAttribute("method", "Post"); // Get 또는 Post 입력
        form.setAttribute("action", "/studyContent");
    
        var hiddenField = document.createElement("input");
        hiddenField.setAttribute("type", "hidden");
        hiddenField.setAttribute("name", "curriculumDetailId");
        hiddenField.setAttribute("value", curriculumDetailId);
        form.appendChild(hiddenField);
    
        hiddenField = document.createElement("input");
        hiddenField.setAttribute("type", "hidden");
        hiddenField.setAttribute("name", "curriculumDetailContent");
        hiddenField.setAttribute("value", curriculumDetailContent);
        form.appendChild(hiddenField);
    
        hiddenField = document.createElement("input");
        hiddenField.setAttribute("type", "hidden");
        hiddenField.setAttribute("name", "curriculumContent");
        hiddenField.setAttribute("value", curriculumContent);
        form.appendChild(hiddenField);
    
        document.body.appendChild(form);
        form.submit();
    }
    ```

    * 다른 값들은 또다른 script에서 값을 가져오기 때문에 그냥 name값으로 불러올 수 있었지만 curriculumContent는 script 밖 form에 있는 값이기 때문에 input으로 해서 값을 불러와야 했다.
