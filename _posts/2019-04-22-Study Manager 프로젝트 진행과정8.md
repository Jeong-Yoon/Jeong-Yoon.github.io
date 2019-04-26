# 2019.04.22 Study Manager 프로젝트 진행과정

### code 생성 시 특수문자 제외
- study를 만들 때, 자동으로 난수 발생을 시켜 study code를 만들도록 했는데, 영어 대소문자, 숫자 말고 특수문자가 들어가는 것을 발견하여 해결하였다.
    ```java
        while (cnt < 8) { // 원하는 난수의 길이
            int num1 = (int) 48 + (int) (ran.nextDouble() * 74);    //알파벳 대,소문자, 숫자범위의 아스키값발생
            if ((num1 >= 48 && num1 <= 57) || (num1 >= 65 && num1 <= 90) || (num1 >= 97 && num1 <= 122)) // 특수문자 제외
            {
                sb.append((char) num1);    //아스키코드값을 char로 형변환 후 저장
                cnt++;
            }
        }
    ```

### study content 내용 불러오기
- studyDetail 화면에서 curriculumDetail에 onclick 기능을 추가하여 누르면 curriculumDetailId를 가지고 가서 연결된 study content 내용을 불러오는 화면을 만들었다.
```javascript
    var curriculumDetailDiv = $('<li style="margin-left: 5%;">' + data[i].curriculumDetailContent + '</li>');

    ->

    var curriculumDetailDiv = $('<li style="margin-left: 5%;" onclick="gotoContent('+ data[i].curriculumDetailId +')">' + data[i].curriculumDetailContent + '</li>');

function gotoContent(curriculumDetailId) {
            location.href='/studyContent?curriculumDetailId='+curriculumDetailId;
}

```
- 아직 curriculumDetailContent와 curriculumContent를 가져가는 코드는 완성하지 못했다.

