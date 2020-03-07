# Summary
* https://www.youtube.com/watch?v=uBOdEEzjxzE&feature=youtu.be&fbclid=IwAR340osHaLT81UfzyghBa_fzRBcCy8GxblBO5xp8X4j4Y4yonGsxhx5C0D0
* yaml파일 위치
    * .github/workflows
* yaml파일 작성
    * on
        * Event type(Event 기반 발생 타입)
        * push, pull_request
        * https://help.github.com/en/actions/reference/events-that-trigger-workflows
    * jobs/build
        * runs-on
            * 작동 컴퓨터
        * steps
            * 실제 벌어지는일
            * uses, name, run
### Example 1(default)
* main.yaml 
  * ![image](https://user-images.githubusercontent.com/20143765/76146563-30bab900-60d7-11ea-95f4-b716b08d0139.png)
      * uses
          * 다른사람이 만든 actions을 실행하고 싶을때 사용
          * actions/checkout@v2
              * https://github.com/actions/checkout
              * checkout이라는 action의 저장소가 actions
              * action이 실행하고 있는 저장소를 clone하고 checkout하는 action
          * 이외 다른사람꺼 사용하기
              * Marketplace의 todo-actions
* Push 결과
  * ![image](https://user-images.githubusercontent.com/20143765/76146566-34e6d680-60d7-11ea-9293-90cd8483cacb.png)
      * /home/runner/work/{repository}… 라는 컴퓨터에서 작동
      
### Example 2(uses 사용하기)
* GitHub-checkout.yml
  * ![image](https://user-images.githubusercontent.com/20143765/76146570-3912f400-60d7-11ea-8fea-13975e1d8de4.png)
* Push 결과
  * ![image](https://user-images.githubusercontent.com/20143765/76146572-3dd7a800-60d7-11ea-9ae5-cac2824c0983.png)
  
### Example 3(GitHub actions context)
* main.yml
  * ![image](https://user-images.githubusercontent.com/20143765/76146579-44661f80-60d7-11ea-88dd-3da7f4af3b78.png)
* Push 결과
  * ![image](https://user-images.githubusercontent.com/20143765/76146575-40d29880-60d7-11ea-8a3c-d5af4b6f9e01.png)
  
### Example 4(Github actions context2)
* https://help.github.com/en/actions/reference/context-and-expression-syntax-for-github-actions
* context.yml
  * ![image](https://user-images.githubusercontent.com/20143765/76146581-48923d00-60d7-11ea-80cd-26a51be44dc1.png)
* Push 결과
  * ![image](https://user-images.githubusercontent.com/20143765/76146584-4c25c400-60d7-11ea-8cf9-f54e128cc94a.png)
  
### Example 5(Secret)
* password.yml
  * ![image](https://user-images.githubusercontent.com/20143765/76146591-50ea7800-60d7-11ea-84fd-ee0abd78ba0b.png)
  * Secret password는 settings/secrets에서 생성
* Push 결과
  * ![image](https://user-images.githubusercontent.com/20143765/76146593-547dff00-60d7-11ea-8c1b-83caf7a52403.png)
