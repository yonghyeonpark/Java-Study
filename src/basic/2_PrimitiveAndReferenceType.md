# 기본형과 참조형
## 기본형(Primitive Type)

- int, long, double, boolean처럼 변수에 사용할 값을 직접 넣을 수 있는 데이터 타입을 의미합니다.
- 실제 값이기 때문에 매개변수로 넘겨 메서드 내부에서 값을 변경하더라도 호출자의 변수 값에는 영향이 없습니다.
- null을 할당할 수 없습니다.

## 참조형(Reference Type)

- String처럼 데이터에 접근하기 위한 참조 값(주소)를 저장하는 데이터 타입을 의미합니다.
- 기본형과 마찬가지로 대입이 가능합니다.(실제 객체가 아닌 참조값이 복사)
  ```java
  A a1 = new A();
  A a2 = a1;
  ```
- 참조 값이기 때문에 객체를 매개변수로 넘겨 메서드 내부에서 객체의 멤버 변수를 변경하면, 호출자의 객체도 변경됩니다.
- null을 할당할 수 있습니다.

<br>

### 📌 GC(Garbage Collection)
자바는 아무도 참조하지 않는 인스턴스가 있으면, JVM의 GC가 더이상 사용하지 않는 인스턴스라 판단하여 해당 인스턴스를 자동으로 메모리에서 제거해줍니다.

# 변수와 초기화

## 멤버 변수(필드)
- 클래스에 선언
- 생성 시 자동으로 초기화됩니다.
  - 숫자 = 0
  - boolean = false
  - 참조형 = null

## 지역 변수
- 메서드에 선언, `매개변수`도 지역 변수의 한 종류입니다.
- 항상 직접 초기화해야 합니다.

# NullPointerException
- null인 객체를 참조할 때 발생하는 예외입니다.

```java
public class A {
    int value;
}

public class Main {
    public static void main(String[] args) {
        A a = null;
        System.out.println(a.value); // NullPointerException 발생
    }
}
```

<br>

📌 Scanner로 숫자 입력받을 때 주의사항

```java
Scanner scanner = new Scanner(System.in);
int a = scanner.nextInt();
int b = scanner.nextInt();
scanner.nextLine(); // 입력 버퍼를 비우기 위함
```

nextInt()는 정수를 읽지만 엔터 키를 처리하지 않기 때문에 다음에 나올 nextLine()이 문제없이 작동하도록 nextLine()을 통해 줄 바꿈 문자(\n)를 소비해 줍니다.