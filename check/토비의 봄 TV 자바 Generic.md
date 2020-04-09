# Chapter별 Check List
- [x] 1편: 자바 Generics
- [x] 2-1편: Generics에서 와일드카드 활용법
- [ ] 2-2편: 람다와 인터섹션 타입을 이용한 동적인 기능확장법

출처: (토비의 봄 TV, 백기선) - 유튜브
# Chapter별 Summary
## 1편: 자바 Generics
* 지네릭 메서드(메소드 레벨)
    * static, instance메서드 둘다 사용 가능
    * 지네릭 메서드가 static 메서드일경우 메소드 매개변수의 타입파라미터는 클레스 레벨의 타입파라미터를 이용할수 없다.
        * 지네릭 메서드는 메소드 레벨이므로
        * ![image](https://user-images.githubusercontent.com/20143765/76697180-4a5f9000-66d7-11ea-9359-3560994bfef4.png)

    * 지네릭 메서드가 instance메서드일경우에는 두개다(T: 클래스 레벨 타입 파라미터, S: 메소드 레벨 타입 파라미터) 사용가능
        * ![image](https://user-images.githubusercontent.com/20143765/76697182-4fbcda80-66d7-11ea-860e-ef2146c27562.png)        
    * 생성자에서도 타입파라미터 사용가능
        * ![image](https://user-images.githubusercontent.com/20143765/76697184-53506180-66d7-11ea-8945-50f2b03143ef.png)
* Bounded Type Parameter
    * Multiple bound(and 조건)
        * ![image](https://user-images.githubusercontent.com/20143765/76697187-577c7f00-66d7-11ea-921a-fca4f9ba8cbf.png)
    * Array, 기준값을 매개변수로 array에서 기준값보다 큰 요소를 찾는 메서드 구현
        * ![image](https://user-images.githubusercontent.com/20143765/76697188-5b100600-66d7-11ea-91c0-4e5e8dd6fc94.png)
        * > 부등호 비교는 number타입만 가능하기 때문에 compareTo로 비교해야한다. 그러기 위해선 Compareble을 구현한 타입으로 제한해야 한다.
* 타입 파라미터의 상속 관계는 적용이 된 지네릭 타입의 상속관계의 영향을 주지 않는다.
    * ![image](https://user-images.githubusercontent.com/20143765/76697189-5f3c2380-66d7-11ea-98c2-764b1fa55b77.png)
        * List를 상속하므로 타입파라미터 P가 추가되도 대입 가능
* 타입 추론 제공
    * ![image](https://user-images.githubusercontent.com/20143765/76697192-63684100-66d7-11ea-85c6-3dc1a2a95ac9.png)
        * static 지네릭 메서드 타입 추론 정보 제공 
* ?(와일드카드
    * List<?> = List<? extends Object>
    * ![image](https://user-images.githubusercontent.com/20143765/76697196-66fbc800-66d7-11ea-9a3c-78af525cc20f.png)
        * printList와 printList2의 차이점
            * List를 넘겨줄때 차이가 남
            * printList(Arrays.asList(1,2,3) => X
            * printList2(Arrays.asList(1,2,3) => O
    * ![image](https://user-images.githubusercontent.com/20143765/76697198-6a8f4f00-66d7-11ea-9d81-3126b0550633.png)
        * ?로 List를 유연하게 받을수 있지만.. 제약조건이 있음. add할때 등
      
---

## 2-1편: Generics에서 와일드카드 활용법
* 와일드카드 활용법
    * ?(와일드카드)의 제한
        * List의 메서드는 (size(), clear(), iterator등) 사용가능
    * isEmpty 메소드 구현하기
        * ![image](https://user-images.githubusercontent.com/20143765/76703021-a21aed00-6711-11ea-9e3a-77e1604303ba.png)
            * 해당 지네릭 메서드를 와일드 카드로 변경 가능
    * 언제 지네릭 메소드와 와일드카드를 써야하나?
        * 지네릭 메소드 쓰는경우
            * 타입파라미터로 정의되있는 List의 원소에 관심이 있을때 사용
        * 와일드 카드 쓰는 경우
            * List의 원소에 관심이 없는 경우(List 메서드를 사용할경우) 사용
    * Max 메소드 구현
        * 지네릭 메소드 이용
            * ![image](https://user-images.githubusercontent.com/20143765/76703024-a810ce00-6711-11ea-8431-f5f38e390da8.png)
        * 와일드 카드 이용하기
            * ![image](https://user-images.githubusercontent.com/20143765/76703029-acd58200-6711-11ea-981b-8e64f1f402a7.png)
                * compareTo안에는 T의 하위타입도(꼭 같은타입으로 비교할필요 없음) 들어갈수 있으므로 List<? Extends T>가 올바름
                * ![image](https://user-images.githubusercontent.com/20143765/76703033-b232cc80-6711-11ea-8659-0649fae6eecb.png)
    * 언제 super, extends사용할까?
        * 메서드 내부에서 사용하면 extends, 메서드 외부에서 사용하면 super
        * copy가 대표적인 예제
            * ![image](https://user-images.githubusercontent.com/20143765/76703036-b5c65380-6711-11ea-9039-897b3aa33f98.png)
                * input에 해당하는 src는 Upper bound인 extends, output에 해당하는 dest는 Lower bound인 super
    * 와일드 카드의 Capture
        * 이 타입이 뭔지 몰라 정의한건데 필요에 따라서 타입 추론해야 할때 caputure한다고 표현함
        * Capture하는 Helper메서드 예제(By 자바 언어 진영)
            * ![image](https://user-images.githubusercontent.com/20143765/76703043-bbbc3480-6711-11ea-8914-32b63be3be42.png)
        * 자바 API 진영에선 capture 없이 row타입 사용
            * ![image](https://user-images.githubusercontent.com/20143765/76703047-bfe85200-6711-11ea-970f-44ca0fc672e5.png)
* [Share] Java 제네릭 바운디드 와일드 카드 활용 참고 
    * ? extends T : read만 가능하다 => get만 가능하다
    * ? super T : writer만 가능하다 => add만 가능하다.
    * ![image](https://user-images.githubusercontent.com/20143765/76703057-cecf0480-6711-11ea-9845-f4ecb2a0985f.png)
        * error
    * ![image](https://user-images.githubusercontent.com/20143765/76703060-d4c4e580-6711-11ea-9c94-680103a94870.png)
        * Ok
    * ![image](https://user-images.githubusercontent.com/20143765/76703063-dbebf380-6711-11ea-9ef5-fcbef3b626fe.png)
    
---

## 2-2편: 람다와 인터섹션 타입을 이용한 동적인 기능확장법
