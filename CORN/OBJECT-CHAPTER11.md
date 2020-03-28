## 11장 합성과 유연한 설계

상속에서 부모 클래스와 자식 클래스 사이의 의존성은 컴파일 타임에 해결되지만 합성에서 두 객체 사이의 의존성은 런타임에 해결된다. 상속 관계는 **is-a** 관계라 부르고 합성 관계는 **has-a** 관계라고 부른다. 

상속을 제대로 활용하기 위해서는 부모 클래스의 내부 구현에 대해 상세하게 알아야 하기 때문에 자식 클래스와 부모 클래스 사이의 결합도가 높아질 수 밖에 없다. 

합성은 내부에 포함되는 객체의 구현이 아닌 퍼블릭 인터페이스에 의존한다. 따라서 합성을 이용하면 포함된 객체의 내부 구현이 변경되더라도 영향을 최소화할 수 있기 때문에 변경에 더 안정적인 코드를 얻을 수 있게 된다. 

상속 관계는 클래스 사이의 정적인 관계, 합성 관계는 객체 사이의 동적인 관계

코드 작성 시점에 결정한 상속 관계는 변경이 불가능하지만 합성 관계는 실행 시점에 동적으로 변경 가능. 따라서 상속 대신 합성을 사용하면 변경하기 쉽고 유연한 설계를 얻을 수 있다. 

상속과 합성은 재사용의 대상이 다르다. 상속은 부모 클래사 안에 구현된 코드 자체를 재사용하지만 합성은 포함되는 객체의 퍼블릭 인터페이스를 재사용한다. 상속 대신 합성을 사용하면 구현에 대한 의존성을 인터페이스에 대한 의존성으로 변경할 수 있다. 

> 화이트박스 재사용 
>
> - 서브클래싱에 의한 재사용
> - 내부가 공개된다.
>
> 블랙박스 재사용
>
> - 합성에 의한 재사용
> - 내부는 공개되지 않고 인터페이스를 통해서만 재사용



### 상속을 합성으로 변경하기

상속을 남용했을 때 직면할 수 있는 세 가지 문제점

- 불필요한 인터페이스 상속 문제
- 메서드 오버라이딩의 오작용 문제
- 부모 클래스와 자식 클래스의 동시 수정 문제

합성을 통해 위의 세 가지 문제점을 해결할 수 있다.

**합성 방법**

1. 자식 클래스에 선언된 상속 관계를 제거
2. 부모 클래스의 인스턴스를 자식 클래스의 인스턴스 변수로 선언

```
책의 코드 참고
```



### 상속으로 인한 조합의 폭발적인 증가

상속으로 인해 결합도가 높아지면 코드를 수정하는 데 필요한 작업의 양이 과도하게 늘어나는 경향이 있다. 과도한 상속의 두 가지 문제점은 다음과 같다.

- 하나의 기능을 추가하거나 수정하기 위해 불필요하게 많은 수의 클래스를 추가하거나 수정해야 한다.
- 단일 상속만 지원하는 언어에서는 상속으로 인해 오히려 중복 코드의 양이 늘어날 수 있다. 



설계는 다양한 조합을 수용할 수 있도록 유연해야 한다. 

부모 클래스의 메서드를 재사용하기 위해 **`super` 호출**을 사용하면 원하는 결과를 쉽게 얻을 수는 있지만 **자식 클래스와 부모 클래스 사이의 결합도가 높아**지고 만다. **결합도를 낮추는 방법**은 자식 클래스가 부모 클래스의 메서드를 호출하지 않도록 **부모 클래스에 추상 메서드를 제공하는 것**.

**하지만**, 부모 클래스에 추상 메서드를 추가하면 **모든 자식 클래스들이 추상 메서드를 오버라이딩해야** 하는 문제가 발생. 그렇기 때문에 추상 메서드가 동일한 방식으로 구현된다면 추상 메서드의 **기본 구현을 제공하자**. (이를 **훅 메서드**라고 부른다.)

상속의 남용으로 하나의 기능을 추가하기 위해 필요 이상으로 많은 수의 클래스를 추가해야 하는 경우를 가리켜 **클래스 폭발** 문제 또는 **조합의 폭발** 문제라고 부른다. 

클래스 폭발 문제는 자식 클래스가 부모 클래스의 구현에 강하게 결합되도록 강요하는 상속의 근본적인 한계 때문에 발생하는 문제다. 컴파일 타임에 결정된 자식 클래스와 부모 클래스 사이의 관계는 변경될 수 없기 때문에 자식 클래스와 부모 클래스의 다양한 조합이 필요한 상황에서 유일한 해결 방법은 조합의 수만큼 새로운 클래스를 추가하는 것뿐.

추가할 때뿐만 아니라 기능을 수정할 때도 문제. 모든 클래스를 찾아 동일한 방식으로 수정해야 



### 합성 관계로 변경하기

상속 관계는 컴파일 타임에 결정되고 고정되기 때문에 코드를 실행하는 도중에는 변경할 수 없다. **합성은 컴파일 타임 관계를 런타임 관계로 변경**함으로써 이 문제를 해결한다. **합성을 사용하면 구현이 아닌 퍼블릭 인터페이스에 대해서만 의존할 수 있기 때문에 런타임에 객체의 관계를 변경할 수** 있다. 

합성을 사용하면 컴파일 타임 의존성과 런타임 의존성을 다르게 만들 수 있다. 

합성을 사용하면 구현 시점에 정책들의 관계를 고정시킬 필요가 없으며 실행 시점에 정책들의 관계를 유연하게 변경할 수 있게 된다. 

상속이 조합의 결과를 개별 클래스 안으로 밀어 넣는 방법이라면 합성은 조합을 구성하는 요소들을 개별 클래스로 구현한 후 실행 시점에 인스턴스를 조립하는 방법을 사용하는 것.  

**컴파일 의존성에 속박되지 않고 다양한 방식의 런타임 의존성을 구성할 수 있다는 것이 합성이 제공하는 가장 커다란 장점.** 

컴파일 타임 의존성과 런타임 의존성의 거리가 멀면 멀수록 설계의 복잡도가 상승하기 때문에 이해하기 어려워지는 것 역시 사실. 하지만 **설계는 변경과 유지보수를 위해 존재한다는 사실**. 

변경에 따르는 고통이 복잡성으로 인한 혼란을 넘어서고 있다면 유연성의 손을 들어주는 것이 현명한 판단.

```
합성 예시는 책의 코드 참조.
```

합성을 사용하면 요구사항을 변경할 때 오직 하나의 클래스만 수정해도 된다. 



#### 객체의 합성이 클래스 상속보다 좋은 방법이다. 

상속은 부모 클래스의 세부적인 구현에 자식 클래스를 강하게 결합시키기 때문에 코드의 진화를 방해

코드를 재사용하면서도 건전한 결합도를 유지할 수 있는 더 좋은 방법은 합성을 이용하는 것. 

**상속을 사용해야 하는 경우는 언제인가? 상속을 구현 상속과 인터페이스 상속, 두 가지로 나눠야 한다는 사실을 이해햐야 한다.**



### 믹스인

우리가 원하는 것은 코드를 재사용하면서도 납득할 만한 결합도를 유지하는 것. 

상속과 클래스를 기반으로 하는 재사용 방법을 사용하면 클래스의 확장과 수정을 일관성 있게 표현할 수 있는 추상화의 부족으로 인해 변경하기 어려운 코드를 얻게 된다. 

**구체적인 코드를 재사용하면서도 낮은 결합도를 유지할 수 있는 유일한 방법은 재사용에 적합한 추상화를 도입하는 것.**

믹스인(mixin)은 객체를 생성할 때 코드 일부를 클래스 안에 섞어 넣어 재사용하는 기법.

합성이 실행 시점에 객체를 조합하는 재사용 방법이라면 믹스인은 컴파일 시점에 필요한 코드 조각을 조합하는 재사용 방법.

상속의 진정한 목적은 자식 클래스를 부모 클래스와 동일한 개념적인 범주로 묶어 is-a 관계를 만들기 위한 것. 반면 믹스인은 말 그대로 코드를 다른 코드 안에 섞어 넣기 위한 방법.  

 상속은 정적이지만 믹스인은 동적이다. 상속은 부모 클래스와 자식 클래스의 관계를 코드를 작성하는 시점에 고정시켜 버리지만 믹스인은 제약을 둘뿐 실제로 어떤 코드에 믹스인될 것인지를 결정하지 않는다.

> 믹스인에서 `extends`는 상속을 의미하는 것이 아닌 문맥을 제한하는 것. 
>
> `super`로 참조되는 코드 역시 고정되지 않는다. 

상속은 재사용 가능한 문맥을 고정시키지만 믹스인은 문맥을 확장 가능하도록 열어 놓는다. 




