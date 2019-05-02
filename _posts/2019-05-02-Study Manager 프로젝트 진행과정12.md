# 2019.05.02 Study Manager 프로젝트 진행과정 12

### main에서 category클릭하면 category에 해당하는 study만 불러오기
- category를 눌렀을 때, 해당 category에 맞는 study만 보여주도록 했다.
    * category를 눌렀을 때와 누르지 않았을 때를 나누어 링크를 설정하였다.
    * category를 누르면 category id를 pathvalue로 가지고 가서 user id와 함께 service로 넘겨서 repository를 통해 study를 가져오도록 했다.

    #### view
    ```html
    <nav class="categorymenu">
        <ul>
            <li th:each="category: ${categories}">
            <a th:href="'/study/list/'+${category.categoryId}" th:text="${category.categoryName}"></a>
            </li>
        </ul>
    </nav>
    ``` 
    #### controller
    ```java
    @GetMapping("/list/{categoryId}")
    public String getStudiesByCategoryId(@PathVariable Long categoryId, Model model){
        StudyManagerSecurityUser securityUser = (StudyManagerSecurityUser) SecurityContextHolder.getContext().getAuthentication().getPrincipal();
        model.addAttribute("isLogin",(!SecurityContextHolder.getContext().getAuthentication().getPrincipal().equals("anonymousUser"))? true : false);
        model.addAttribute("studyList",studyService.getStudiesByUserIdAndCategoryId(securityUser.getId(),categoryId));
        model.addAttribute("categories",categoryService.getCategories());
        return "/study/main_";
    }
    ```

    #### service
    ```java
    @Transactional(readOnly = true)
    public List<Study> getStudiesByUserIdAndCategoryId(Long userId, Long categoryId) {
        return studyRepository.getStudiesByUserIdCategoryId(userId, categoryId);
    }
    ```

    #### repostory
    ```java
    @ Query("SELECT s FROM Study s INNER JOIN s.studyUsers su INNER JOIN su.studyUserId sui INNER JOIN sui.user u INNER JOIN s.category c " +
            "WHERE u.userId =:userId AND c.categoryId =:categoryId")
    public List<Study> getStudiesByUserIdCategoryId(@Param("userId") Long userId, @Param("categoryId") Long categoryId);
    ```

- main의 로고를 누르면 다시 전체 study list를 불러오도록 했다.
