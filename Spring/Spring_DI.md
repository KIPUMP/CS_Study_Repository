#  의존성 주입(Dependency Injection)

### 의존성(Dependency)

> 한 객체가 다른 객체를 필요로 하는 관계

- 파라미터나 리턴값 또는 지역변수 등으로 다른 객체를 참조하는 것

- A가 B를 의존한다 → 의존 대상인 B가 변하면 A에 영향을 미친다(의존성 전이)

- 의존성은 객체 간 협력을 위해 필수적이지만 의존성을 최소화 해야 한다.

### DI(의존성 주입)

- 아래 코드에서 Car 클래스는 Engine 클래스가 반드시 있어야 하고 Engine 클래스 변환 시, Car 클래스가 영향 받도록 되어있다.
→ 전체(Car)가 부분(Engine)에 의존

```java
class Engine {
    public void start() {
        System.out.println("시동");
    }
}

class Car {

    private Engine engine;

    public Car() {
        this.engine = new Engine();
    }

    public void drive() {
        engine.start();
    }
}
```

- DI를 적용한 개선 코드 : 이제는 Car가 직접 new를 사용해서 Engine 클래스를 만들지 않음

```java
class Car {

    private Engine engine;

    public Car(Engine engine) {
        this.engine = engine;
    }
}
```

### 의존성 주입 방법

##### 생성자 주입

- 생성자의 호출시점에 1회 호출되는 것이 보장

- 주입받은 객체가 변하지 않거나, 반드시 객체의 주입이 필요한 경우에 강제하기 위해 사용

- 생성자 주입의 장점

    - 객체 생성 시점에 의존성이 반드시 주입됨

    - final을 사용해서 불변성을 보장할 수 있음

    - 순환 참조 발견 가능

```java
@Service
public class OrderService {

    private final PaymentService paymentService;

    public OrderService(PaymentService paymentService)  {
        this.paymentService = paymentService;
    }
}
```

- Lombok 사용시 

```java
@Service
@RequiredArgsConstructor
public class OrderService {
    private final PaymentService paymentService;
}
```

##### 수정자 주입(Setter 주입)

- 필드 값을 변경하는 Setter를 통해서 의존관계 주입

- 주입 받는 객체가 변경될 가능성이 있는 경우

- 수정자 주입의 장점

    - 선택적인 의존성 주입 가능

    - 주입 누락 가능

```java

@Service
public class OrderService {

    private PaymentService paymentService;

    @Autowired
    public void setPaymentService(
            PaymentService paymentService) {

        this.paymentService = paymentService;
    }
}
```

##### 필드 주입

- 필드에 바로 의존관계 주입

- 외부에서 접근이 불가능하다는 단점

- 필드 주입은 테스트가 어렵고 의존성(DI)이 명확히 드러나지 않아 실무에서는 지양

```java

@Service
public class OrderService {

    @Autowired
    private PaymentService paymentService;
}

```

##### 일반 메서드 주입

- 일반 메서드를 통해 의존관계를 주입

```java
@Service
public class OrderService {

    private PaymentService paymentService;
    private DiscountService discountService;

    @Autowired
    public void init(
            PaymentService paymentService,
            DiscountService discountService) {

        this.paymentService = paymentService;
        this.discountService = discountService;
    }
}

```


