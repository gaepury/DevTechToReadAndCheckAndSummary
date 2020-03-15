# Chapter별 Check List
- [x] 1편: 자바 Generics
- [ ] 2편: Generics에서 와일드카드 활용법, 람다와 인터섹션 타입을 이용한 동적인 기능확장법


# Chapter별 Summary
## 1편: 자바 Generics
* 지네릭 메서드(메소드 레벨)
    * static, instance메서드 둘다 사용 가능
    * 지네릭 메서드가 static 메서드일경우 매개변수의 T타입파라미터는 클레스 레벨의 T타입파라미터를 이용할수 없다.
        * 지네릭 메서드는 메소드 레벨이므로
        * ![image](https://user-images.githubusercontent.com/20143765/76697182-4fbcda80-66d7-11ea-860e-ef2146c27562.png)
    * 지네릭 메서드가 instance메서드일경우에는 두개다(타입파라미터S,T) 사용가능
        * ![image](https://user-images.githubusercontent.com/20143765/76697180-4a5f9000-66d7-11ea-9359-3560994bfef4.png)
        * T는 클래스레벨, S는 메소드 레벨 타입 매개변수
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
* ?(와일드카드)과 T(타입파라미터) 차이점
    * List<?> = List<? extends Object>
    * ![image](https://user-images.githubusercontent.com/20143765/76697196-66fbc800-66d7-11ea-9a3c-78af525cc20f.png)
        * printList와 printList2의 차이점
            * List를 넘겨줄때 차이가 남
            * printList(Arrays.asList(1,2,3) => X
            * printList2(Arrays.asList(1,2,3) => O
    * ![image](https://user-images.githubusercontent.com/20143765/76697198-6a8f4f00-66d7-11ea-9d81-3126b0550633.png)
        * ?로 List를 유연하게 받을수 있지만.. 제약조건이 있음. add할때 등
        
## 2편: Generics에서 와일드카드 활용법, 람다와 인터섹션 타입을 이용한 동적인 기능확장법
