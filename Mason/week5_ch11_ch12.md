# 11장. 합성과 유연한 설계

- 346
  - 상속 관계는 __is-a 관계__ 라고 부르고, 합성 관계는 __has-a 관계__ 라고 부른다.
  - 상속과 합성은 코드의 재사용의 목적은 갖지만 구현 방법과 변경을 다루는 방식에서의 차이가 발생
  - 상속의 단점
    - 부모 클래스의 내부 구현에 대해 상세하게 알아야 한다.
  - 합성은 구현에 의존하지 않는다는 점이 상속과 다르다. > 퍼블릭 인터페이스에 의존한다.
- 347
  - 코드 작성 시점에 결정한 상속 관계는 변경이 불가능하지만, 합성 관계는 실행시점에 동적으로 변경할 수 있다.
  - **물론 상속보다 합성을 이용하는 것이 구현 관점에서는 좀 더 번거롭고 복잡하게 느껴질 수도 있지만 설계는 변경과 관련된 거싱라는 점을 기억하라.**
  - 상속과 합성은 재사용의 대상이 다르다.
    - 상속: 부모 클래스 안에 구현된 코드 자체를 재사용.
    - 합성: 포함되는 객체의 퍼블릭 인터페이스를 재사용.
- 348
  - 10장에서 살펴본 상속의 문제 3가지: 불필요한 인터페이스 상속문제, 메서드 오버라이딩의 오작용 문제, 부모 클래스와 자식 클래스의 동시 수정 문제
  - **348에서 상속문제를 해결하기 위한 합성 관계 변화는 상속 클래스 관계를 다른 클래스의 인스턴스 변수로 가지고 있게 하는 방법.** > 대신 퍼블릭 인터페이스를 통해서만 협력 가능
- 350
  - InstrumentedHashSet > HashSet이 제공하는 퍼블릭 인터페이스를 그대로 제공해야 함.
- 352
  - **몽키패치** : 현재 실행 중인 환경에만 영향을 미치도록 지역적으로 코드를 수정하거나 확장하는 것. 
  - 포워딩 메서드 보여줌.(**포워딩** : 기존 클래스의 인터페이스를 그대로 외부에 제공하면서 구현에 대한 결합 없이 일부 작동 방식을 변경하고 싶은 경우 사용할 수 있음)
- 352
  - 대부분의 경우 구현에 대한 결합보다는 인터페이스에 대한 결합이 더 좋다는 사실을 기억하라.
- 355
  - 조합이 필요한 경우에 대한 예시. 기본정책 + 부가정책
- 360
  - 추상메서드의 단점: 모든 자식 클래스에서 추상 메서드를 오버라이드 해야한다.(자바)
  - 해결방법 -> 기본 구현 제공하는 것
    - 스위프트에서 프로토콜에 protocol default implementation와 같은 느낌임.
  - **훅 메서드: ** 추상 메서드와 동일하게 자식 클래스에서 오버라이딩할 의도로 메서드를 추가했지만 편의를 위해 기본 구현을 제고하는 메서드를 훅 메서드(hook method)라고 한다. 
- 364
  - 결국 이렇게 하더라도 조합이 증가함에 따라 중복 코드가 발생하게 된다.
- 367
  - 결국 클래스 폭발... 그림 11.6 참조
- 370
  - Phone과 RatePolicy 관계를 잘 기억할것. 합성!
    - RatePolicy의 메서드 인터페이스는 Phone을 사용하고 Phone은 내부적으로 RatePolicy(인터페이스)를 참조하고 있다.
    - Phone은 RatePolicy에 대해 의존성 주입받음. > 런타임. > 다양한 종류의 객체와 협력하기 위해 합성 관계를 이용해서 객체의 타입을 인터페이스나 추상클래스로 선언.
- 372
  - 그림 11.7과 그 아래 합성 하는 방법 코드 참조.
- 377
  - 합성을 이용했을 때 새로운 정책 추가하는 그림 참조.
- 379
  - 믹스인 :  상속과 합성으 ㅣ특성을 모두 보유하고 있는 독특한 코드 재사용 방법.
  - 객체를 생성할 때 코드 일부를 클래스 안에 섞어 넣어 재사용하는 기법.
  - 믹스인은 뭔가 와닿질 않네요... 어렵다...





# 12장. 다형성

- 389
  - 상속을 사용하는 목적이 코드를 재사용하기 위함인가? 클라이언트들 관점에서 인스턴스들을 동일하게 행동하는 그룹으로 묶이 위해서인가?
    - 코드 재사용이라면 상속을 사용하지 말아야 한다.
- 390
  - 유니버셜 다혓엉, 임시(Ad Hoc) 다형성, 매개변수 다형성, 포함 다형성, 오버로딩 다형성, 강제 다형성...
    - 하나의 클래스 안에 동일한 이름의 메서드가 존재하는 경우 : **오버로딩 다형성**
    - 언어가 지원하는 자동적인 타입 변환이나 사용자가 직접 구현한 타입 변환을 이용해 동일한 연산자를 다양한 타입에 사용할 수 있는 방식 : **강제 다형성**
    - 클래스의 인스턴스 변수나 메서드의 매개변수 타입을 임의의 타입으로 선언한 후 사용하는 시점에 구체적인 타입으로 지정하는 방식 : **매개변수 다형성** (제네릭 프로그래밍과 연관)
    - 메시지가 동일하더라도 수신한 객체의 타입에 따라 실제로 수행되는 행동이 달라지는 능력을 의미한다. : **포함 다형성** (서브타입 다형성)
    - **포함 다형성** 을 구현한 가장 일반적인 방법 > 상속
      - 두 클래스를 상속 관계로 연결하고 자식 클래스에서 부모 클래스의 메서드를 오버라이딩한 후 클라이언트는 부모 클래스만 참조하면 포함 다형성을 구현할 수 있음

#### 상속의 양면성

- 393

  - 상속의 목적은 프로그램을 구성하는 개념들을 기반으로 다형성을 가능하게 하는 타입 계층을 구축하기 위한 것.(재사용이 아니다.)
  - 상속의 메커니즘 (업캐스팅, 동적 메서드 탐색, 동적 바인딩, self 참조, super 참조)

- 401

  - LSP
  - 어떻게 부모 클래스에서 구현한 메서드를 자식 클래스의 인스턴스에서 수행할 수 있는 것일까?
    - 런타임에 시스템이 자식 클래스에 정의되지 않은 메서드가 있을 경우 이 메서드를 부모 클래스 안에서 탐색하기 때문.
  - ex) class A: B 
    B().method를 햇는데 이 메서드가 B에 정의되어 있지 않으면 부모 클래스에서 탐색을 한다.
    - 객체의 경우 서로 다른 상태를 저장할 수 있도록 각 인스턴스별로 독립적인 메모리를 할당받아야한다. 하지만 메서드의 경우에는 동일한 클래스의 인스턴스끼리 공유가 가능하기 때문에 클래스는 한 번만 메모리에 로드하고 각 인스턴스별로 클래스를 가리키는 포인터를 갖게 하는 것이 경제적이다.

- 405

  - 부모 클래스 타입으로 선언된 변수에 자식 클래스의 인스턴스를 할당하는 것이 가능하다. **업캐스팅**
  - 선언된 변수 타입이 아니라 메시지를 수신하는 객체의 타입에 따라 실행되는 메서드가 결정된다. 이것은 객체지향 시스템이 메시지를 처리할 적절한 메서드를 컴파일 시점이 아니라 실행 시점에 결정하기 때문에 가능하다. 이를 **동적바인딩** 이라고 한다. 
    - 동일한 수신자에게 동일한 메시지를 전송하는 동일한 코드를 이용해 서로 다른 메서드를 실행할 수 있는 이유는 어배스팅과 동적 메서드 탐색이라는 기반 메커니즘이 존재하기 때문.

- 406

  - 반대로 부모 클래스의 인스턴스를 자식 클래스 타입으로 변환하기 위해서는 명시적인 타입 캐스팅이 필요한데 이를 **다운 캐스팅** 이라고 한다.

- 408

  - **self**
    - 객체가 메시지를 수신하면 컴파일러는 self 참조라는 임시 변수를 자동으로 생성한 후 메시지를 수신한 객체를 가리키도록 설정한다. 동적 메서드 탐색은 self가 가리키는 객체의클래스에서 시작해서 상속 계층의 역방향으로 이뤄지며 메서드 탐색이 종료되는 순간 self 참조는 자동으로 소멸된다. 시스템은 앞에서 설명한 class 포인터와 parent포인터와 함께 self참조를 조합해서 메서드를 탐색한다.

- 410

  - 스위프트의 프로토콜과 확장 메커니즘은 상속 계층에 독립적으로 메시지를 위임할 수 있는 대표적인 장치.

- 417

  - 자신이 자신에게 다시 메시지를 전송하는 self 전송
    - 현재 클래스의 메서드를 호출하는 것이 아니라 **현재 객체에게 메시지를 전송하는 것**
    - 현재 객체란 바로 self 참조가 가리키는 객체.

- 429

  - 포워딩과 위임: 다른 객체에게 요청을 처리할 때 인자로 self참조를 전달하지 않는 경우를 포워딩, self참조를 전달하는 경우에 위임. 

- 430~434

  - 프로토타입 기반의 객체지향 언어.

  

----

### Discussion

- 