# 상속

- 자바는 다중 상속을 지원하지 않습니다. (`extend`의 대상은 하나만 선택)

## 상속과 메모리 구조

- 상속 관계의 객체를 생성하면 그 내부에는 부모와 자식이 모두 생성됩니다.
- 상속 관계의 객체를 호출할 때, 대상 타입을 정해야 합니다.
- 현재 타입에서 해당 기능 혹은 변수를 찾지 못하면, 상위 부모 타입에서 찾아 실행해야 하고, 모든 타입에서 찾지 못하면 컴파일 에러가 발생합니다.<br>(부모 클래스 입장에서 보면 결국 외부에서 호출한 것과 같기 때문에, 접근 제어자의 영향을 받습니다.)
<br><br>

![image](https://github.com/yonghyeonpark/Java-Study/assets/126778700/4a5c9ca9-f243-4a5a-861c-4ce1c16c3a9c)
new 를 통해 인스턴스를 생성할 때, 해당 클래스뿐만 아니라 부모 클래스까지 포함하여 생성합니다. 즉, 하나의 참조 값에 두 가지 클래스 정보가 공존하는 상태입니다.
<br><br>

![image](https://github.com/yonghyeonpark/Java-Study/assets/126778700/68cdf20d-5c2f-41cd-bdba-94e89e3ff56f)
메서드를 호출했을 때, 호출하는 변수의 타입을 기준으로 선택합니다. 만약 자식 타입을 통해 호출했다면, 먼저 자식 타입에 해당 기능이 있는지 찾고, 없다면 부모 타입으로 올라가서 찾습니다.

## 상속과 메서드 오버라이딩

- 상속 받은 기능을 자식이 재정의하는 것을 메서드 오버라이딩이라고 합니다.
- 오버라이딩한 메서드 위에 `@Override` 애노테이션을 사용합니다.
  - 컴파일러가 애노테이션을 통해 정확히 오버라이드 되었는지 확인하고, 오버라이딩 조건을 만족시키지 않으면 컴파일 에러를 발생시킵니다.

### 메서드 오버라이딩 조건

- 메서드 이름이 같아야 합니다.
- 매개변수의 타입, 순서, 개수가 같아야 합니다.
- 반환 타입이 같아야 합니다. 단, 반환 타입이 하위 클래스 타입일 수 있습니다.
  ```java
  class Animal {
      
      Animal reproduce() {
          return new Animal();
      }
  }

  class Dog extends Animal {
      @Override
      Dog reproduce() {
          return new Dog();
      }
  }
  ```
  
- 오버라이딩 메서드의 접근 제어자는 상위 클래스의 메서드보다 더 제한적이어서는 안 됩니다.
- 오버라이딩 메서드는 상위 클래스의 메서드보다 더 많은 예외를 `throws`로 선언할 수 없습니다. 하지만 더 적거나 같은 수의 예외, 또는 하위 타입의 예외는 선언할 수 있습니다.
- `static`, `final`, `private` 키워드가 붙은 메서드는 오버라이딩 될 수 없습니다.
  - `static`은 클래스 레벨에서 작동하므로 인스턴스 레벨에서 사용하는 오버라이딩이 의미 없습니다.<br>(그냥 클래스 이름을 통해 필요한 곳에 직접 접근하면 됩니다)
- 생성자는 오버라이딩할 수 없습니다.

## super

- 부모 클래스에 대한 참조를 뜻합니다.

### super - 생성자

상속 관계의 인스턴스를 생성하면 결국 메모리 내부에는 자식과 부모 클래스가 각각 다 만들어지고, 이에 따라 각각의 생성자도 모두 호출되어야 합니다. 이러한 이유로, 상속 관계를 사용하면 자식 클래스의 생성자에서 부모 클래스의 생성자를 반드시 호출해야 한다는 규칙이 존재합니다.

- 상속을 받으면 생성자의 첫 줄에 `super`를 사용하여 부모 클래스의 생성자를 호출해야 합니다.
<br>(예외로 생성자 첫 줄에 `this`를 사용할 수는 있지만, 자식의 생성자 안에서 `super`를 언젠가는 반드시 호출해야 합니다.)
- 부모 클래스의 생성자가 기본 생성자인 경우에는 `super`를 생략할 수 있습니다.
- 여러 생성자가 있는 경우 하나만 선택해서 호출할 수 있습니다.

## final

- final이 사용된 클래스를 상속 받을 수 없습니다.
- final이 사용된 메서드를 오버라이딩할 수 없습니다.