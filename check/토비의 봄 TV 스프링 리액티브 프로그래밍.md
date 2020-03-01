
# Chapter별 Check List
- [x] 1편: Reactive Streams
- [x] 2편: Reactive Streams - Operators
- [x] 3편: Reactive Streams - Schedulers
- [ ] 4편: 자바와 스프링의 비동기 기술
- [ ] 5편: 비동기 RestTemplate과 비동기 MVC/Serlvet
- [ ] 6편: AsyncRestTemplate의 콜백 헬과 중복 작업 문제
- [ ] 7편: CompletableFuture
- [x] 8편: WebFlux
- [x] 9편: Mono의 동작방식과 block()
- [x] 10편: Flux의 특징과 활용방법
  
# Chapter별 Summary
## 1편(Reactive Streams)
https://www.youtube.com/watch?v=8fenTR3KOJo

#### iterable <—> observable(상대성)
   * Iterable: pull 방식
   * observable: push
####  옵저버 패턴의 부족한 점
   * Completed
   * Error
#### Reactive Streams
   * Publisher: Obervable 과 대응
   * Subscriber: Observer와 대응
   * Publisher.subscribe(Subscriber)
       * observable.addObserver와 대응
   * Subscription
       * publisher, subscriber 중계 역할
           * backpressure(publisher, subscriber 속도차 조절)
       * 전체 flow
            *  ![image](https://user-images.githubusercontent.com/20143765/70407835-31689280-1a89-11ea-8543-66395f6f62f9.png)
       * 최초 request(Subscription 메서드)는 onSubcribe에서 해야함(Subscriber)
       * Publisher를 병렬적으로 처리하고싶다고 멀티 스레드 환경처럼 하는것은 불가능
       
---

## 2편(Reactive Streams - Operators)
https://www.youtube.com/watch?v=DChIxy9g19o
#### Publisher -> [data1] -> op1 -> [data2] -> op2 -> [data3] -> Subscriber
   * ![image](https://user-images.githubusercontent.com/20143765/70407867-6248c780-1a89-11ea-9245-6bcfb09e289f.png) 
#### mapPub
   * ![image](https://user-images.githubusercontent.com/20143765/70408201-97a1e500-1a8a-11ea-8616-a14cb94c2a7f.png)
      * onSubscribe, onError, onCompleted는 그대로 중계
#### DelegateSub로 code refactoring
   * ![image](https://user-images.githubusercontent.com/20143765/70408209-9f618980-1a8a-11ea-9277-161177ddbf22.png)
#### sumPub
   * 어떻게 합계할것인가? onNext에서 어떻게 끝이라는걸 알지?
       * 모른다. onComplete에서 onNext호출
   * ![image](https://user-images.githubusercontent.com/20143765/70408220-aee0d280-1a8a-11ea-8a67-fea4514f024d.png)
#### reducePub
   * ![image](https://user-images.githubusercontent.com/20143765/70408239-be601b80-1a8a-11ea-9ff9-091a8092a4e6.png)
#### Generic method, class 변환
#### mapPub, reducePub 메서드의 generic화 
   * data type 변환(T -> R)
   * ![image](https://user-images.githubusercontent.com/20143765/70408244-c6b85680-1a8a-11ea-9af0-477dcb9bf01a.png)
#### Reactor
   * Flux(Publisher 구현)
   * Ex)
        * ![image](https://user-images.githubusercontent.com/20143765/70408256-cfa92800-1a8a-11ea-801e-6039e2bb5870.png)
        * log()로 onSubcribe, request, onNext등 메서드 로그를 볼수있음
   * map
        * ![image](https://user-images.githubusercontent.com/20143765/70408261-d9cb2680-1a8a-11ea-976b-ae59d1b38db1.png)
        * map operator에 의해 onSubscribe, onNext등이 두번씩 호출
   * 스프링 MVC에 적용
        * ![image](https://user-images.githubusercontent.com/20143765/70408266-df287100-1a8a-11ea-9c16-c5a4dd63b553.png)

--- 
## 3편(Reactive Streams - Operators)
https://www.youtube.com/watch?v=Wlqu1xvZCak

* consume이 느린경우 onNext, onError, onCompleted 메서드에 스케줄러를 매핑 및 중계해서 다른 스레드에서 돌도록 처리함
    * publishOn의 구현방법
* request의 과정이 느릴때(데이터 생성이 느릴떄)
    * subcribeOn의 구현방법
* 생명주기
    * 조립, 구독, 실행

* 요약
    * flux는 publisher의 구현체
    * subscribeOn: 데이터 생성이 느릴떄 사용해라
        * 직접 구현: subOnPub Operator
            * ![image](https://user-images.githubusercontent.com/20143765/73608027-12a5f880-4601-11ea-8db5-deeb6d8ab4a4.png)
            * 적용: subOnPub.subscribe(new Subscriber …{})
        * Slow Publisher, fast consumer
    * publishOn: 
        * 직접 구현: pubOnPub Operator
            * ![image](https://user-images.githubusercontent.com/20143765/73608031-16397f80-4601-11ea-85da-b1c2a15e3e95.png)
        * Fast publisher, slow consumer
    * subscribeOn + publishOn
        * ![image](https://user-images.githubusercontent.com/20143765/73608032-1b96ca00-4601-11ea-84cb-c06e26a4005d.png)
        * ![image](https://user-images.githubusercontent.com/20143765/73608035-205b7e00-4601-11ea-80f3-3d390df5e53c.png)
    * Thread name 지정하기
        * ![image](https://user-images.githubusercontent.com/20143765/73608036-24879b80-4601-11ea-99b8-e41ad285ade8.png)
            * 스프링이 제공하는 CustomizableThreadFactory 이용
    * reactor 에서 publishOn ,subsribeOn
        * ![image](https://user-images.githubusercontent.com/20143765/73608038-28b3b900-4601-11ea-85a9-23de96da63c6.png)
        * result
            * ![image](https://user-images.githubusercontent.com/20143765/73608039-2c474000-4601-11ea-9694-083e6d822633.png)
    * publishOn 스레드풀 셧다운
        * onError, onComplete에 구현
        * ![image](https://user-images.githubusercontent.com/20143765/73608041-2fdac700-4601-11ea-8b5e-88857a2c6573.png)
            * shundownNow (인터럽트 발생시켜 강제 셧다운)
    * Flux.interval
        * 데몬스레드여서 메인스레드 종료시 같이 종료됨
    * Take 구현
        * takePub
            * ![image](https://user-images.githubusercontent.com/20143765/73608043-336e4e00-4601-11ea-98ee-fa94b400053f.png)
        * subscription
            * ![image](https://user-images.githubusercontent.com/20143765/73608046-3701d500-4601-11ea-9902-4ac128489f57.png)
            
---
## 8편(WebFlux)
https://www.youtube.com/watch?v=ScH7NZU_zvk

* 단일 api 호출 By Mono 
    * ![image](https://user-images.githubusercontent.com/20143765/75626623-5f82ec00-5c0c-11ea-8da8-13605284d8cf.png)
    * 구독하는 코드가 별도로 없어도 Mono를 반환하면 Spring에서 Mono를 구독해줌.
* 멀티 api 호출 By Mono
    * ![image](https://user-images.githubusercontent.com/20143765/75626626-627ddc80-5c0c-11ea-90ff-deffa0ca12ae.png)
        * Netty에 worker 스레드에서 동작
* Service nonblocking으로 실행하기
    * @Async + (Future, ListenableFuture, CompletableFutue)
    *  CompletableFutue을 모노로 바꾸기
        * Mono.fromCompletionState
        * CompletableFuture는 CompletionState를 상속함
    * ![image](https://user-images.githubusercontent.com/20143765/75626628-66a9fa00-5c0c-11ea-8960-c7bcd903915d.png)

---
## 9편(Mono의 동작방식과 block())
https://www.youtube.com/watch?v=LK6NRV8tZBM

* .log()는 중간 퍼블리셔라고 생각하면 됨
    * Publisher -> publisher -> publisher -> subscriber
* doOnNext, .log() 코드 및 결과
    * ![image](https://user-images.githubusercontent.com/20143765/75627428-63663c80-5c13-11ea-937f-69c936ffe268.png)
    * ![image](https://user-images.githubusercontent.com/20143765/75627432-695c1d80-5c13-11ea-8e9e-1a487db4df84.png)
    * just내 함수가 호출되면 구독 전에 미리 호출됨, 레이지로 준비하려면 fromSupplier 메서드 사용.
* spring에서 해주기전에 미리 subsribe한다면?
    * mono나 flux같은 publisher들은 하나 이상의 subscriber를 가질수 있음.
    * Publisher source의 타입
        * hot: 구독하는 시점부터 실시간으로 발생하는 데이터만 가져온다.
        * cold: 어느 subscriber가 요청해도 동일한 결과가 고정되있음, 구독할때마다 데이터를 처음부터 다 끝까지 가져온다
    * 결과 => 로그가 두번찍힘.
* block()
    * block()메서드는 내부에서 subscribe를 함, 따라서 결과는 로그가 두번찍힘.
    * Api나 db호출이 있으면 block(), return할때 IO가 두번 일어날수 있으므로 비효율적, 따라서 가능한한 사용하지 않는것이 좋음. 
  
---
## 10편(Flux의 특징과 활용방법)
* Flux 간단 예제(Flux.just)
    * ![image](https://user-images.githubusercontent.com/20143765/75628368-b3e19800-5c1b-11ea-8ec1-0a6fb2d84a78.png)
    * Flux.just 인자론 여러개
* Mono.just안에 List vs Flux.just에 인자 여러개
    * ![image](https://user-images.githubusercontent.com/20143765/75628370-b80db580-5c1b-11ea-9743-e3fc6473574e.png)
    * 결과는 같다.
    * Mono.just로 할시 List 안에 Entity들을 조작,가공할때 reactor 라이브러리에 있는 operator를 이용할수 없음.
* HTTP 스트림을 지원하려면 Flux
    * MediaType 
    * ![image](https://user-images.githubusercontent.com/20143765/75628372-bb08a600-5c1b-11ea-9b4e-06988bb0ba30.png)
    * ![image](https://user-images.githubusercontent.com/20143765/75628377-bf34c380-5c1b-11ea-9ac2-9c74ba87526c.png)
* Stream을 이용해서 가져오기 + 특정 개수만큼 가져오기(take)
    * ![image](https://user-images.githubusercontent.com/20143765/75628379-c2c84a80-5c1b-11ea-9828-c1f05511b020.png)
* onNext로 오는것을 delay 걸기
    * ![image](https://user-images.githubusercontent.com/20143765/75628382-c65bd180-5c1b-11ea-89df-9730de701bfb.png)
    * delay는 백그라운드에서 blocking됨
* Flux의 generate 사용
    * generate(Consumer<SynchronousSink>)
        * sink
            * 데이터를 흘려보내는 역할
        * ![image](https://user-images.githubusercontent.com/20143765/75628384-ca87ef00-5c1b-11ea-93c6-99b856839607.png)
    * generate(Callable, BiFunction)
        * ![image](https://user-images.githubusercontent.com/20143765/75628385-ceb40c80-5c1b-11ea-94ab-c4bd04930f8c.png)
        * 첫번쨰 인자: 초기 상태값
        * 두번째 인자: 상태값과 sink을 보내서 다음 상태값을 return
* 여러 Flux 결합(merge)하기(with Flux interval)
    * Flux.zip 사용
    * Interval flux의 delay만 이용하고 es flux의 데이터만 가져오기
        * ![image](https://user-images.githubusercontent.com/20143765/75628387-d1aefd00-5c1b-11ea-95ca-e7c9a3e58c66.png)
    * id만들때 interval의 값 이용하기
        * ![image](https://user-images.githubusercontent.com/20143765/75628391-d673b100-5c1b-11ea-98dd-3d613ee98bf8.png)
    * zip의 효율적인 ex
        * 여러 서비스에서 데이터를 호출하고(사용자 프로파일 정보, 사용자 디테일정보등) 결합하여 제공
