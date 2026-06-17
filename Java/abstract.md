# 추상화(abstract)

> "공통적인 특징만 남기고 구체적인 구현은 숨기는 것"

## 추상 클래스 (Abstract Class)

- 일부 구현 + 일부 미구현 제공
- `abstract` 키워드 사용
- 단일 상속만 가능 (`extends`)
- 필드(변수) 선언 가능
- 일반 메서드 + 추상 메서드 함께 사용 가능

- 추상클래스

``` java
public abstract class Car {

    public abstract void drive();

    public void stop() {
        System.out.println("정지");
    }
}
```
- 구현클래스

``` java
public class K5 extends Car {

    @Override
    public void drive() {
        System.out.println("K5 주행");
    }
}
```
---

## 인터페이스 (Interface)

-  기능의 규약(명세) 정의
-  `interface` 키워드 사용
-  다중 구현 가능 (`implements`)
-  메서드는 기본적으로 `public abstract`
-  변수는 `public static final` (상수만 가능)
-  Java 8 이후 `default`, `static` 메서드 사용 가능
- 인터페이스는 DI 등을 목적으로 Spring에서 더 많이 사용하고 있다
- [PSA](/CS_Study_Repository/Spring/Service_Abstraction.md)

``` java
public class KakaoPayService implements PaymentService {
    public void pay() {}
}

public class TossPayService implements PaymentService {
    public void pay() {}
}
```

- Spring DI

```java
private final PaymentService paymentService;
```

---

## Enum (열거형)

> "정해진 값만 사용할 수 있도록 제한하는 타입"

- 고정된 상수 집합을 표현하는 타입
- 문자열/숫자보다 타입 안정성이 높음
- 컴파일 시 타입 안전성 보장
- `switch`문 사용 가능
- 클래스처럼 필드, 생성자, 메서드 정의 가능

``` java
enum Status {
    READY, RUNNING, DONE
}
```
``` java
enum Status {
    READY("준비"),
    RUNNING("실행"),
    DONE("완료");

    private String description;

    Status(String description) {
        this.description = description;
    }

    public String getDescription() {
        return description;
    }
}
```