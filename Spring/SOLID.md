# 객체지향프로그래밍

## SOLID

> 로버트 마틴이 최초 정의한 SOLID는 객체지향 5가지 원칙의 앞글자를 딴 것


| 원칙 | 의미 |
|------|------|
| S | 단일 책임 원칙 (SRP, Single Responsibility Principle) |
| O | 개방-폐쇄 원칙 (OCP, Open-Closed Principle) |
| L | 리스코프 치환 원칙 (LSP, Liskov Substitution Principle) |
| I | 인터페이스 분리 원칙 (ISP, Interface Segregation Principle) |
| D | 의존 역전 원칙 (DIP, Dependency Inversion Principle) |


### SRP - 단일 책임의 원칙

> "클래스는 하나의 캑임만 가져야 한다"

- 클래스를 변경해야 하는 이유가 하나만 존재해야 한다는 의미

- 잘못된 예시 : 아래 클래스는 UserService에 사용자 저장과 이메일 발송 두가지 역할을 동시에 수행하므로 이를 개선해야 함

```java
public class UserService {

  public void saveUser() {
  // 사용자 저장
      }

  public void sendEmail() {
  // 이메일 전송
      }
}
```

- 개선

```java
// UserService에는 사용자에 관련된 기능만
public class UserService {
  public void saveUser() {}
}
// EmailService에는 이메일에 관련된 기능만
  public class EmailService {
  public void sendEmail() {}
}

```

- SRP의 장점 : 책임단위로 코드를 짜게 되면 아래의 장점이 있음
  - 유지보수성 강화
  - 테스트 용이
  - 변경 영향 감소

### OCP - 개방 폐쇄 원칙

> "확장에는 열려있고 변경,수정에는 닫혀 있어야 한다"

- 기존코드는 수정하지 않고 기능을 추가 할 수 있어야 함

- 예시 1 : DAO에서 DB 타입에 따라 다른 DatabaseConnection이 필요할 때 사용

- 잘못된 예시 : OCP를 준수하지 않으면 새로운 클래스가 추가될 때마다 기존 코드를 수정해야 함

```java
public class PaymentService {

  public void pay(String type) {

    if(type.equals("CARD")) {
    // 카드 결제
    }

    if(type.equals("KAKAO")) {
    // 카카오 결제
    }
  }
}
```

- 개선

```java
public interface Payment {
  void pay();
}

public class CardPayment implements Payment {
  public void pay() {}
}

public class KakaoPayment implements Payment {
  public void pay() {}
}

// NaverPayment, TossPayment가 추가되더리도 Service에서 수정할 필요가 없음
```

```java
public class PaymentService {

//Service가 구현체를 몰라야 함
private Payment payment;

// cardPayment나 KakaoPayment가 오면 자동으로 다운캐스팅
public PaymentService(Payment payment) {
  this.payment=payment;
  }

public void pay() {
  payment.pay();
  }
}
```

- OCP(개방-폐쇄 원칙)는 확장에는 열려 있고 수정에는 닫혀 있도록 설계하여, 결과적으로 '높은 응집도'와 '낮은 결합도'를 유지하도록 돕는 원칙이다.

- [소프트웨어_결합도_응집도](결합도_응집도.md)

- Spring의 전략패턴 + DI 구조가 대표적임

### LSP - 리스코프 치환 원칙

> "부모 객체를 자식 객체로 바꿔도 정상 동작해야 한다"

- 잘못된 예시 : 부모클래스(bird)의 규칙을 깸으로써 다형성이 깨짐

```java
class Bird {
  void fly() {}
}

class Penguin extends Bird {    
  @Override
  void fly() {          // 펭귄은 날 수 없음
  throw new UnsupportedOperationException();
  }
}
```

- 개선

```java

interface Flyable {
  void fly();
}

class Eagle implements Flyable {
  public void fly() {}
}

```

### ISP - 인터페이스 분리 원칙

> "부모 객체를 자식 객체로 바꿔도 정상 동작해야 한다"