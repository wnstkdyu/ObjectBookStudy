# 14장 일관성 있는 협력 

객체는 협력을 위해 존재한다. 협력은 객체가 존재하는 이유와 문맥을 제공한다. 잘 설계된 애플리케이션은 이해하기 쉽고, 수정이 용이하며 재사용 가능한 협력의 모임이다. 객체지향 설계의 목표는 적절한 책임을 수행하는 객체들의 협력을 기반으로 결합도가 낮고 재사용 가능한 코드 구조를 창조하는 것이다. 

유사한 요구사항을 계속 추가해야 하는 상황에서 각 협력이 서로 다른 패턴을 따를 경우에는 전체적인 설계의 일관성이 서서히 무너진다. 

객체지향 패러다임의 장점은 설계를 재사용할 수 있다는 점이다. 재사용을 위해서는 객체들의 협력 방식을 일관성 있게 만들어야 한다. 일관성은 설계에 드는 비용을 감소시킨다. 

일관성이 있는 설계가 가져다 주는 더 큰 이익은 코드가 이해하기 쉬워진다는 것이다. 가능하면 유사한 기능을 구현하기 위해 유사한 협력 패턴을 사용하라. 



## 1. 핸드폰 과금 시스템 변경하기 

> p471~483 코드 참고. 

현재 구현의 가장 큰 문제점은 이 클래스들이 유사한 문제를 해결하고 있음에도 불구하고 설계에 일관성이 없다는 것이다. 이 클래스들은 기본 정책을 구현한다는 고통의 목적을 공유한다. 하지만 정책을 구현하는 방식은 완전히 다르다. 다시 말해서 개념적으로는 연관돼 있지만 구현 방식에 있어서는 완전히 제각각이라는 것이다. 

비일관성은 두 가지 상황에서 발목을 잡는다. 

- 새로운 구현을 추가해야 하는 상황
  - 새로운 기본 정책을 추가하면 추가할수록 코드 사이의 일관성은 점점 어긋나게 된다. 
- 기존의 구현을 이해해야 하는 상황
  - 유사한 요구사항이 서로 다른 방식으로 구현돼 있다면 요구사항이 유사하다는 사실 자체도 의심하게 될 것. 
  - 유사한 요구사항을 구현하는 서로 다른 구조의 코드는 이해하는 데 심리적인 장벽을 만든다. 

결론은 유사한 기능을 서로 다른 방식으로 구현해서는 안 된다는 것이다. 

유사한 기능은 유사한 방식으로 구현해야 한다. 객체지향에서 기능을 구현하는 유일한 방법은 객체 사이의 협력을 만다는 것뿐이므로 유지보수 가능한 시스템을 구축하는 첫걸음은 협력을 일관성 있게 만든 것이다. 



> **코드 재사용을 위한 상속은 해롭다**
>
> 코드 재사용을 위해 상속을 사용하게 되면 두 클래스 사이의 강한 결합도가 생기게 되고 이런 강한 결합도는 설계 개선과 새로운 기능의 추가를 방해한다. 



## 2. 설계에 일관성 부여하기 

일관성 있는 설계를 만드는 데 가장 훌륭한 조언은 다양한 설계 경험을 익히라는 것. 

일관성 있는 설계를 위한 두 번째 조언은 널리 알려진 디자인 패턴을 학습하고 변경이라는 문맥 안에서 디자인 패턴을 적용해 보라는 것이다. 디자인 패턴은 특정한 변경에 대해 일관성 있는 설계를 만들 수 있는 경험 법칙을 모아놓은 일종의 설계 템플릿이다. 

협력을 일관성 있게 만들기 위해 다음과 같은 기본 지침을 따르는 것이 도움이 될 것. 

- **변하는 개념을 변하지 않는 개념으로부터 분리하라.**
- **변하는 개념을 캡슐화하라.**

애플리케이션에서 달라지는 부분을 찾아내고, 달라지지 않는 부분으로부터 분리시킨다. 이것은 여러 설계 원칙 중에서 첫 번째 원칙이다. 즉, 코드에서 새로운 요구사항이 있을 때마다 바뀌는 부분이 있다면 그 행동을 바뀌지 않는 다른 부분으로부터 골라내서 분리해야 한다. 

"바뀌는 부분을 따로 뽑아서 캡슐화한다. 그렇게 하면 나중에 바뀌지 않는 부분에는 영향을 미치지 않고 채로 그 부분만을 고치거나 확장할 수 있다. "



### 조건 로직 대 객체 탐색 

조건에 따라 분기되는 어떤 로직들이 있다면 이 로직들이 바로 개별적인 변경이라고 볼 수 있다. 

객체지향에서 변경을 다루는 전통적인 방법은 조건 로직을 객체 사이의 이동으로 바꾸는 것이다. 

다형성은 바로 이런 조건 로직을 객체 사이의 이동으로 바꾸기 위해 객체지향이 제공하는 설계 기법이다. 

조건 로직을 객체 사이의 이동으로 대체하기 위해서는 커다란 클래스를 더 작은 클래스들로 분리해야 한다. **중요한 기준은 변경의 이유와 주기다.** 간단하게 말해서 단일 책임 원칙을 따르도록 클래스를 분리해야 한다. 

큰 메서드 안에 뭉쳐있던 조건 로직들을 변경의 압력에 맞춰 작은 클래스들로 분리하고 나면 인스턴스들 사이의 협력 패턴에 일관성을 부여하기가 더 쉬워진다. 유사한 행동을 수행하는 작은 클래스들이 자연스럽게 역할이라는 추상화로 묶이게 되고 **역할 사이에서 이뤄지는 협력 방식이 전체 설계의 일관성을 유지할 수 있게 이끌어주기 때문이다.**

따라서 협력을 일관성 있게 만들기 위해 따라야 하는 첫 번째 지침은 다음과 같다. 

- **변하는 개념을 변하지 않는 개념으로부터 분리하라.**
  - 변하는 개념을 별도의 서브타입으로 분리한 후 이 서브타입들을 클라이언트로부터 캡슐화한 것
- **변하는 개념을 캡슐화하라.**
  - 핵심은 훌륭한 추상화를 찾아 추상화에 의존하도록 만드는 것. 추상화에 대한 의존은 결합도를 낮추고 결과적으로 대체 가능한 역할로 구성된 협력을 설계할 수 있게 해준다. 
  - 추상화의 품질이 캡슐화의 품질을 결정한다. 

변경에 초점을 맞추고 캡슐화의 관점에서 설계를 바라보면 일관성 있는 협력 패턴을 얻을 수 있다. 



### 캡슐화 다시 살펴보기 

많은 사람들은 객체의 캡슐화에 관한 이야기를 들으면 반사적으로 데이터 은닉을 떠올린다. **그러나 캡슐화는 데이터 은닉 그 이상이다.**

설계에서 무엇이 변화될 수 있는지 고려하라. 설계에 변경을 강요하는 것이 무엇인지에 대해 고려하기보다는 재설계 없이 변경할 수 있는 것이 무엇인지 고려하라. 여기서 초점은 많은 디자인 패턴의 주제인 변화하는 개념을 캡슐화하는 것이다. 

**캡슐화란 변하는 어떤 것이든 감추는 것이다.**

캡슐화의 가장 대표적인 예는 객체의 퍼블릭 인터페이스와 구현을 분리하는 것이다. 자주 변경되는 내부 구현을 안정적인 퍼블릭 인터페이스 뒤로 숨겨야 한다. 

캡슐화의 종류

- **데이터 캡슐화** 
- **메서드 캡슐화** 
  - 외부에서는 메서드에 직접 접근할 수 없고 클래스 내부와 서브클래스에서만 접근이 가능
  - 클래스 외부에 영향을 미치지 않고 메서드를 수정할 수 있다. 
  - 클래스의 내부 행동을 캡슐화하고 있는 것.
- **객체 캡슐화**
  - 객체 사이의 관계를 변경하더라도 외부에는 영향을 미치지 않는다. 
  - 객체 캡슐화는 합성을 의미
- **서브타입 캡슐화**
  - 실제로 실행 시점에는 클래스들의 인스턴스와 협력
  - 서브타입의 종류를 캡슐화
  - 서브타입 캡슐화는 다형성의 기반이 된다.

코드 수정으로 인한 파급효과를 제어할 수 있는 모든 기법이 캡슐화의 일종이다. 

일반적으로 데이터 캡슐화와 메서드 캡슐화는 개별 객체에 대한 변경을 관리하기 위해 사용하고 객체 캡슐화와 서브타입 캡슐화는 협력하는 협력에 참여하는 객체들의 관계에 대한 변경을 관리하기 위해 사용한다. 

협력을 일관성 있게 만들기 위해 가장 일반적으로 사용하는 방법은 서브타입 캡슐화와 객체 캡슐화를 조합하는 것. 

서브타입 캡슐화는 인터페이스 상속을 사용하고, 객체 캡슐화는 합성을 사용한다.

서브타입 캡슐화와 객체 캡슐화를 적용하는 방법은 다음과 같다. 

- **변하는 부분을 분리해서 타입 계층을 만든다.**
  - 변하지 안흔 부분으로부터 변하는 부분을 분리
  - 변하는 부분들의 공통적인 행동을 추상 클래스나 인터페이스로 추상화
  - 변하는 부분들이 이 추사 클래스나 인터페이스를 상속받게 만든다. 
  - 변하는 부분은 변하지 않는 부분의 서브타입

- **변하지 않는 부분의 일부로 타입 계층을 합성한다.**
  - 앞에서 구현한 타입 계층을 변하지 않는 부분에 합성
  - 변하지 않는 부분에서 변경되는 구체적인 사항에 결합돼서는 안된다. 
  - 의존성 주입과 같이 결합도를 느슨하게 유지할 수 있는 방법을 이용해 오직 추상화에만 의존하게 만든다. 
  - 변경이 캡슐화된 것.



## 3. 일관성 있는 기본 정책 구현하기 

일관성 있는 협력을 만들기 위한 첫 번째 단계는 변하는 개념과 변하지 않는 개념을 분리하는 것. 



### 변경 캡슐화하기 

협력을 일관성 있게 만들기 위해서는 변경을 캡슐화해서 파급효과를 줄여야 한다. 



### 협력 패턴 설계하기 

변하는 부분과 변하지 않는 부분을 분리하고, 변하는 부분을 적절히 추상화하고 나면 변하는 부분을 생략한 채 변하지 않는 부분만을 이용해 객체 사이의 협력을 이야기할 수 있다. 추상화만으로 구성한 협력은 추상화를 구체적인 사례로 대체함으로써 다양한 상황으로 확장할 수 있게 된다. 다시 말해서 재사용 가능한 협력 패턴이 선명하게 드러나는 것이다. 

올바른 방향으로 나아가고 있는지 확인할 수 있는 유일한 방법은 협력을 직접 구현해 보는 것뿐이다. 



### 추상화 수준에서 협력 패턴 구현하기 

변하는 것과 변하지 않는 것을 분리하고 변하는 것을 캡슐화한 코드는 오로지 변하지 않는 것과 추상화에 대한 의존성만으로도 전체적인 협력을 구현할 수 있다. 

협력이 동작하기 위해서는 구체적이고 살아있는 컨텍스트로 확장돼야 한다. 



### 구체적인 협력 구현하기 

변하는 부분을 변하지 않는 부분으로부터 분리했기 때문에 변하지 않는 부분을 재사용할 수 있다. 

새로운 기능을 추가하기 위해 오직 변하는 부분만 구현하면 되기 때문에 원하는 기능을 쉽게 완성할 수 있다. 

따라서 코드의 재사용성이 향상되고 테스트해야 하는 코드의 양이 감소한다. 

구조를 강제할 수 있기 때문에 기능을 추가하거나 변경할 때도 설계의 일관성이 무너지지 않는다. 

일관성 있는 협력은 개발자에게 확장 포인트를 강제하기 때문에 정해진 구조를 우회하기 어렵게 만든다. 

변하지 않는 부분은 모든 기본 정책에서 공통적이라는 것을 기억하라. 공통 코드의 구조와 협력 패턴은 모든 기본 정책에 걸쳐 동일하기 때문에 코드를 한 번 이해하면 이 지식을 다른 코드를 이해하는데 그대로 적용할 수 있다. 

일관성 있는 협력을 이해하고 나면 변하는 부분만 따로 때어내어 독립적으로 이해하더라도 전체적인 구조를 쉽게 이해할 수 있다. 

유사한 기능에 대해 유사한 협력 패턴을 적용하는 것은 객체지향 시스템에서 **개념적 무결성**을 유지할 수 있는 가장 효과적인 방법이다. 시스템이 일관성 있는 몇 개의 협력 패턴으로 구성된다면 시스템을 이해하고, 수정하고, 확장하는 데 필요한 노력과 시간을 아낄 수 있다. 



### 협력 패턴 맞추기 

고정요금 정책은 기존 협력 방식에서 벗어날 수밖에 없는 것이다. 

이런 경우에 또 다른 협력 패턴을 적용하는 것이 최선의 선택인가? 그렇지 않다. 가급적 기존의 협력 패턴에 맞추는 것이 가장 좋다. 전체적으로 일관성을 유지할 수 있는 설계를 선택하는 것이 현명하다. 



> **지속적으로 개선하라.**
>
> 협력은 고정된 것이 아니다. 만약 현재의 협력 패턴이 변경의 무게를 지탱하기 어렵다면 변경을 수용할 수 있는 협력 패턴을 향해 과감하게 리팩터링하라. 요구사항의 변경에 따라 협력 역시 지속적으로 개선해야 한다. 중요한 것은 현재의 설계에 맹목적으로 일관성을 맞추는 것이 아니라 달라지는 변경의 방향에 맞춰 지속적으로 코드를 개선하려는 의지다. 



### 패턴을 찾아라

일관성 있는 협력의 핵심은 변경을 분리하고 캡슐화하는 것이다. 변경을 캡슐화하는 방법이 협력에 참여하는 객체들의 역할과 책임을 결정하고 이렇게 결정된 협력이 코드의 구조를 결정한다. 

애플리케이션에서 유사한 기능에 대한 변경이 지속적으로 발생하고 있다면 변경을 캡슐화할 수 있는 적절한 추상화를 찾은 후, 이 추상화에 변하지 않는 공통적인 책임을 할당하라. 현재의 구조가 변경을 캡슐화하기에 적합하지 않다면 코드를 수정하지 않고도 원하는 변경을 수용할 수 있도록 협력과 코드를 리팩터링하라. 변경을 수용할 수 있는 적절한 역할과 책임을 찾다 보면 협력의 일관성이 서서히 윤곽을 드러낼 것이다. 

따라서 협력을 일관성 있게 만드는 것은 유사한 변경을 수용할 수 있는 협력 패턴을 발견하는 것이다. 

객체지향 설계는 객체의 행동과 그것을 지원하기 위한 구조를 계속 수정해 나가는 작업을 반복해 나가면서 다듬어진다.

협력 패턴과 관려해서 언급할 가치가 있는 두 가지 개념이 있다. 하나는 패턴이고 다른 하나는 프레임워크다. 이어지는 장에서 두 개념을 간단하게 살펴보자.


