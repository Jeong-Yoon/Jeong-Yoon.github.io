# 2019.04.17 Study Manager 프로젝트 진행과정

### security user 수정
- 로그인을 할 때, email로 로그인을 해주기 때문에 UserDetailService에 id를 넣어주는 코드를 추가했다.
    * study list 페이지에서 login한 user의 user_id로 스터디를 불러와야 하는데 값이 전혀 들어오지 않았다. 확인해보니 user_id가 null로 되어 있었다.
    * 이전 프로젝트에서는 user_id가 없이 그냥 id를 따로 만들었기 때문에 set을 해주지 않아도 됐지만 지금은 email로 로그인을 하고 user_id는 따로 있기 때문에 set을 해주어야 불러올 수 있었다.
```java
studyManagerSecurityUser.setId(user.getUserId());
```

### 로그인 성공 시 페이지 지정
- 로그인을 성공하면 study list 페이지로 갈 수 있도록 하기 위해 SecurityConfig에 코드를 추가해 주었다.
```java
.defaultSuccessUrl("/study/list")
```

### code를 입력해서 study 추가
- 이 기능을 하기 위해서는 database도 수정해야 했다.
    * 처음에 단순히 alter문을 사용해서 code를 추가하고 not null과 unique 특성을 주려니까 되지 않았다.
    * alter문으로 추가하면 빈칸으로 생성되는데, 그 빈칸을 같은 값이라고 인식했기 때문이었다. 그래서 not null로 먼저 add를 해준 다음 code 값을 넣어주고 unique 제약조건을 주었다.
    
    ```sql
    ALTER TABLE study ADD code VARCHAR(8) NOT NULL;
    UPDATE studymanager.study SET code = '-' WHERE study_id = 1;
    ...
    ALTER TABLE study ADD CONSTRAINT code_UNIQUE UNIQUE(code);

    ```

### login 시 index 페이지 접근 불가 설정
- login을 하면 회원가입이나 login을 다시 할 이유가 없기 때문에 login을 한 다음에는 index 페이지로 접근 하려고 하면 study list 페이지로 넘어가도록 설정했다.
    * securityUser는 login을 하지 않았을 때 null이 아니라 anonymousUser로 값이 넘어온다.

    ```java
    if(!SecurityContextHolder.getContext().getAuthentication().getPrincipal().equals("anonymousUser")){
        
            return "redirect:/study/list";
    }

    ```
