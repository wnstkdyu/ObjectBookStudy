#  객체분해

- p216

- 실제로 문제를 해결하기 위해 사용하는 저장소는 장기기억이 아니라 단기기억이다.

- p217

  - 불필요한 정보를 제거하고 현재의 문제 해결에 필요한 핵심만 남기는 작업을 추상화라고 부른다.
  - 일반적인 추상화 방법은 한 번에 다뤄야 하는 문제의 크기를 줄이는 것이다 
    - = `분해`

- p218

  ### 프로시저 추상화와 데이터 추상화

  - 프로시저 추상화

    - 무엇을 해야하는지가 중점
    - 기능분해 = 알고리즘 분해

  - 데이터 추상화

    - 타입 추상화(추상 데이터 타입)

    - 데이터를 중심으로 프로시저 추상화(객체지향)

      > 데이터를 `중심`으로 프로시저 추상화 하는것이 객체지향 이라고 하는데, `데이터` != 상태
      > 역할을 수행할 수 있는 정보를 의미? 
      >
      > 추상화메커니즘에서 프로시저 추상화와 데이터추상화에서의 프로시저 추상화는 어떤 차이가있나

  - 프로그래밍 관점에서 객체지향이란 데이터를 중심으로 데이터 추상화와 프로시저 추상화를 통합한 객체를 이용해 시스템을 분해하는 방법이다.

    - 클래스

- p218

  ### 프로시저 추상화와 기능 분해

  - **메인 함수로서의 시스템**

    - 프로시저 중심의 기능 분해 관점에서 시스템은 필요한 더 작은 작업으로 분해될 수 있는 하나의 커다란 메인함수다.
      - ?
    - 하향식 접근법
      - 시스템을 구성하는 가장 최상위 기능을 정의하고, 이 최상위 기능을 좀 더 작은 단계의 하위기능으로 분해해 나가는 방법을 말한다.

  - **급여 관리 시스템**

    - `직원의 급여를 계산한다` 에서부터 시작하며, 필요한 정보를 중심으로 추상화 한다.

    - 단계별로 추상화 수준을 감소시켜 가며 프로그래밍 가능한 상태를 도출할 수 있는 단계까지 진행

    - 기능분해의 결과(p221)는 최상위 기능을 수행하는데 필요한 절차들을 실행되는 시간순서에 따라 나열한것

    - `목차` 

    - 기능 분해를 위한 하향식 접근법은 먼저 필요한 기능을 생각하고 이 기능을 분해하고 정제하는 과정에서 필요한 데이터의 종류와 저장 방식을 식별한다.

      > 책임,역할을 우선 고려하면서 나아가는 과정

- p225

  - 하향식 기능 분해 방식은 `트리` 구조
  - **하향식 기능 분해의 문제점** 

- P226

- 하나의 메인 함수라는 비현실적인 아이디어 

  - 현대의 시스템은 동등한 수준의 다양한 기능으로 구성된다.
  -  실제 시스템에 정상(top)이란 존재하지 않음

- p227

- 메인 함수의 빈번한 재설계

  - 새로운 기능을 추가 할 때마다 메인 함수를 수정해야함 

- P229

- 비즈니스 로직과 사용자 인터페이스의 결합

  - 하향식 접근법은 비즈니스 로직을 설계하는 초기 단계부터 입력 방법과 출력 양식을 함께 고민하도록 강요한다

    > 설계시 상태를 우선 고려했을 때 나타나는 문제점과 유사?
    > 다양한 상황에 대해서 필요한 값들을 우선 고려 햇을 시 

- P230

- 성급하게 결정 된 실행 순서

  - 하향식 접근법의 첫 번째 질문은 무엇이 아니라 어떻게다.
  - 강하게 결합된 시스템은 아주 사소한 변경만으로도 전체 시스템을 요동치게 만들 수 있다.

- p231

  - 데이터 변경으로 인한 파급효과
    - 하향식 기능 분해의 가장 큰 문제점은 어떤 데이터를 어떤 함수가 사용하고 있는지 추적하기 어렵다.

- p234

  - 데이터 변경으로 인한 영향을 최소화하려면 데이터와 함께 변경되는 부분과 그렇지 않은 부분을 명확하게 분리해야한다.
  - 잘 정의된 퍼블릭 인터페이스를 통해 데이터에 대한 접근을 통제해야하는 것이다. 이것이 의존성 관리의 핵심

- p235

  - 언제 하향식 분해가 유용한가

  - 프로젝트 초기에 설계된 본질적인 측면을 무시하고 사용자 인터페이스 같은 비본질적인 측면에 집중하게 만든다.

    > 처음 시작할 때 입력과 출력을 우선 생각하고있는것 같음..

- p235

  ### 모듈

  - 정보 은닉과 모듈
    - 정보 은닉은  외부에 감춰야 하는 비밀에 따라 시스템을 분할하는 모듈 분할 원리다.
    - 모듈은 변경될 가능성이 있는 비밀을 내부로 감추고, 잘 정의되고 쉽게 변경되지 않을 퍼블릭 인터페이스를 외부에 제공해서 내부의 비밀에 함부로 접근하지 못하게 한다.

- p238

  - 모듈의 장점과 한계
    - 모듈 내부의 변수가 변경되더라도 모듈 내부에만 영향을 미친다
    - 비즈니스 로직과 사용자 인터페이스에 대한 관심사를 분리한다
    - 전역 변수와 전역 함수를 제거함으로써 네임스페이스 오염을 방지한다

- p239

  - 메인 함수를 정의하고 필요에 따라 더 세부적인 함수로 분해하는 하향식 기능 분해와 달리 모듈은 감춰야 할 데이터를 결정하고 이 데이터를 조작하는데 필요한 함수를 결정한다.

    > 위 설명을 봤을 땐 감춰야할 데이터를 결정하고 이 데이터를 조작하는 데 필요한 함수를 결정하는것이 기존에 책에서 주장햇던 것들과 차이가 있다고 생각?

- P241

  - ### 데이터 추상화와 추상 데이터 타입

    - 추상 데이터 타입을 구현할 수 있는 언어적인 장치를 제공하지 않는 프로그래밍 언어에서도 추상데이터 타입을 구현하는 것은 가능하다.

      > Swift 에서는? extension Protocol?

- p247

  - 실제로 내부에서 수행되는 절차는 다르지만 클래스를 이용한 다형성은 절차에 대한 차이점을 감춘다.

  - > 절차가 의미하는것이 어떤것인가.

- p250

  - ### 변경을 기준으로 선택하라

    - 메서드 내에서 타입을 명시적으로 구분하는 방식은 객체지향을 위반하는 것

      - p242,251 코드참고

    - 클라이언트가 객체의 타입을 확인한 후 적절한 메서드를 적절한 메서드를 호출하는 것이 아니라, 객체가 메시지를 처리할 적절한 메서드를 선택한다

      - > 정보 전문가에게 메시지를 전송하여 책임을 수행시키듯?

- p251

  - 설계는 변경과 관련된 것
  - 설계의 유용성은 변경의 방향성과 발생 빈도에 따라 결정된다
    - 타입 추가라는 변경의 압력이 더 강한경우 : 객체지향
      - 상속을 통해 편리하게 추가가 가능
    - 오퍼레이션을 추가하는 압력이 더 강한경우 : 추상 데이터 타입
      - 객체지향일 경우, 상속구조에 해당하는 모델에 오퍼레이션 추가가 필요