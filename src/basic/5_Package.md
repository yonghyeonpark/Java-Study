# 패키지

- 폴더, 디렉토리와 같은 개념입니다.
- 패키지를 사용하는 경우 항상 코드 첫 줄에 패키지 이름을 적어주어야 합니다.
- 다음 줄에는 import를 사용할 수 있습니다.
  - 다른 패키지에 있는 클래스를 가져와서 사용할 수 있습니다.
  - 코드에서 패키지 명을 생략하고 클래스 이름만 적을 수 있습니다.
  - (*)을 사용하여 해당 패키지의 클래스들을 한 번에 import 할 수 있습니다.
    - ex) `import study.basic.*;`

## 클래스 이름 중복

패키지를 사용하면 이름이 같아도 패키지 이름으로 구분해서 같은 이름의 클래스를 사용할 수 있습니다.
```
study.basic.Java
study.advanced.Java
```
<br>
이렇게 패키지는 다르지만 이름이 같은 클래스를 둘 다 사용하는 경우가 가끔 있을 수 있는데, 이 때는 둘 중 하나만 선택하여 import 할 수 있습니다.
이 때는 자주 사용하는 클래스를 import하고 나머지는 패키지를 포함한 전체 경로를 적어주거나, 둘 다 전체 경로를 적어주면 됩니다.

```java
package study;

import study.basic.Java;

public class Main() {
    
    public static void main(String[] args) {
        Java java1 = new Java();
        study.advanced.Java java2 = new study.advanced.Java();
  }
}
```

## 규칙

- 패키지의 이름과 위치는 폴더 위치와 같아야 합니다. (필수)
- 패키지 이름은 모두 소문자를 사용합니다. (관례)
- 패키지 이름의 앞부분에는 일반적으로 회사의 도메인 이름을 거꾸로 사용합니다. (관례)
  - ex) com.company.myapp
  - 수많은 외부 라이브러리가 함께 사용되면 같은 패키지에 같은 클래스 이름이 존재할 수도 있는데, 이런 문제를 방지할 수 있습니다.
  - 오픈소스나 라이브러리를 직접 만들어서 외부에 제공한다면 꼭 지키는 것이 좋습니다.
  - 직접 만든 애플리케이션을 다른 곳에 공유하지 않고, 직접 배포한다면 지키지 않아도 보통 문제가 되지 않습니다.

## 계층 구조

- a
  - b
  - c

패키지는 보통 사람이 이해하기 쉽게 하기 위해 이런 식으로 계층 구조를 이룹니다.
이때, b와 c가 a의 하위 패키지라고 해서 import에 함께 묶이지 않습니다.
즉, a, a.b, a.c는 서로 완전히 다른 패키지이며, 각각 import 해서 사용해야 합니다.
마찬가지로 (*)을 사용하여 import 할 때도 해당 패키지의 클래스들만 import하고 하위 패키지까지 되지 않습니다.