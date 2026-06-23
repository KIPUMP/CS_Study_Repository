# TDD 

> 테스트가 개발을 주도한다(Test Driven Development)

- 테스트를 먼저 작성하고, 그 테스트를 통과시키기 위한 최소한의 코드만 구현하는 개발 방법론

- 소프트웨어를 개발 또는 설계할 때, 요구사항에서 유도 가능한 선제적(prior) 테스트를 도출하여 작성한 후, 실제적인 구현 착수보다 우선하는 소프트웨어 개발 방법론

- 구현해야 될 소프트웨어의 규모가 커지고 복잡해짐에 따라 소프트웨어의 확장가능성, 개방적 구조를 위한 개발 방법론

### TDD 장점

- 설계 품질을 향상시켜 코드의 유지보수가 용이해진다. 

- 빠른 피드백 : ./gradlew test만 실행하면 어느 API에서 문제가 있는지 확인가능

- 디버깅 시간 단축

- 문서화 : 테스트 이름만 봐도 기능을 이해할 수 있다.

### 테스트 코드 패턴(Given - When - Then)

- Given : 테스트를 위한 데이터 준비

```java
JobCategory category =
        new JobCategory(1L, "개발");
```

- When : 실제 동작 수행

```java
List<JobCategory> result =
        service.getJobCategories();
```

- Then : 결과 검증

```java
assertThat(result)
        .hasSize(1);
```

```java
@Test
void 카테고리를_조회할_수_있다() {

    // Given
    JobCategory category =
            new JobCategory(1L, "개발");

    // When
    List<JobCategory> result =
            service.getJobCategories();

    // Then
    assertThat(result).hasSize(1);
}
```

### AssertJ

- AssertJ 라이브러리에서 제공하는 검증 메서드

- 테스트 검증을 더 읽기 쉽게 만들어주는 라이브러리

- assertThat()과 관련된 다양한 검증 메서드

```java
assertThat(10).isEqualTo(10);         // 같으면 성공, 다르면 실패

assertThat(result).isNull();          // Null 확인

assertThat(categories).hasSize(3);    // 리스트 크기 확인

assertThat(categories).contains(category1);   // 리스트 포함 여부

assertThat(categories).contains(category1, category2);    // 여러 값 포함

assertThat(categories).containsExactly(category1, category2);   // 순서 검증
```

### JUnit

- Java에서 테스트 코드를 작성하고 실행하기 위한 테스트 프레임워크

```java

@Test
void 두수를_더할수있다() {

    Calculator calculator = new Calculator();

    int result = calculator.add(3, 5);

    assertEquals(8, result);
}
```

##### JUnit 주요 어노테이션

- @Test : 테스트 메서드임을 의미

```java

@Test
void 회원가입_성공() {

}

```

- @BeforeEach : 각 테스트 실행 전 수행

```java
@BeforeEach
void setUp() {
    service = new UserService();
}
```

- @AfterEach : 각 테스트 종료 후 수행

```java
@AfterEach
void tearDown() {

}
```

- assertEquals() : JUnit에서 제공하는 기본 검증 메서드

```java
assertEquals(10, result);
```

