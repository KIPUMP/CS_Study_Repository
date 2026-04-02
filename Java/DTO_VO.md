# DTO와 VO

### DTO (Data Transfer Object)

#### 개념
계층 간 또는 시스템 간에 **데이터를 전달하기 위한 객체**입니다.

예: Controller ↔ Service ↔ Client

#### 특징
- 데이터 전달 목적
- 보통 getter/setter를 가짐
- 일반적으로 가변 객체(mutable)
- 직렬화(JSON 변환 등)에 자주 사용
- 비즈니스 로직은 최소화하거나 없음

#### 예시
```java
public class UserDTO {
    private String name;
    private int age;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }
}
```

#### 언제 사용하나
- API 요청/응답 객체
- Controller와 Service 사이 데이터 전달
- 화면과 서버 간 통신

#### 한 줄 정리
**DTO는 데이터를 전달하기 위한 객체입니다.**

---

### VO (Value Object)

#### 개념
값 그 자체를 표현하는 객체로, **불변성**을 가지는 것이 일반적입니다.

#### 특징
- 값 자체가 중요함
- 보통 식별자보다 값 비교가 중요함
- 불변 객체(immutable)로 설계하는 경우가 많음
- `equals()`와 `hashCode()`가 중요함
- setter 없이 생성자로 값 설정

#### 예시
```java
public class Money {
    private final int amount;

    public Money(int amount) {
        this.amount = amount;
    }

    public int getAmount() {
        return amount;
    }
}
```

#### 언제 사용하나
- 금액, 주소, 날짜 범위 등 값 자체가 의미 있는 경우
- 도메인 모델 설계에서 값 객체 표현 시

#### 한 줄 정리
**VO는 값을 표현하는 불변 객체입니다.**

---

### DTO vs VO 비교

| 구분 | DTO | VO |
|------|-----|----|
| 목적 | 데이터 전달 | 값 표현 |
| 변경 가능 여부 | 가능(Mutable) | 불가능(Immutable)인 경우가 많음 |
| 로직 | 거의 없음 | 값 관련 로직 포함 가능 |
| 식별성 | 보통 없음 | 값 자체로 비교 |
| setter | 있음 | 보통 없음 |

#### 면접용 한 줄
**DTO는 데이터를 전달하기 위한 객체이고, VO는 값을 표현하는 불변 객체입니다.**

---

## 빠른 암기 포인트
- **DTO**: 데이터 전달용 객체
- **VO**: 값 표현용 객체

---

## 실무/면접용 짧은 답변 예시

### DTO vs VO
“DTO는 Controller와 Service 간 데이터를 주고받기 위해 사용하고, VO는 금액이나 주소처럼 변경되지 않는 값을 표현할 때 사용합니다.”
