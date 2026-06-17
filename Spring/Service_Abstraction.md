# 서비스 추상화(Service Abstraction)

> "환경과 기술의 차이를 추상화하여 비즈니스 로직이 기술에 의존하지 않도록 만드는 것"

- 서비스 추상화의 essence는 "비즈니스 로직은 그대로 두고, 사용하는 기술(DB, 메일, 트랜잭션 등)을 바꿀 수 있도록 추상화하는 것" 이다

### 서비스 추상화가 필요한 이유

##### JDBC 서비스 추상화

- DB Connection을 구현해야 할 떄 큰 회사 서비스 일수록 여러개의 DB(MySQL, Oracle, PostgreSQL)을 사용하게 된다. 

> 비즈니스 로직이 JDBC 기술에 의존

```java
Connection conn =
    DriverManager.getConnection(...);
```

- Spring은 이 문제를 해결하기 위해 JDBC를 추상화

```java
JdbcTemplate jdbcTemplate;
```

- 이로써 개발자는 JDBCTemplate만 사용해서 여러 DB에 접근 가능

```java
jdbcTemplate.query(...)
```

##### 트랜잭션 서비스 추상화

> "단위 작업(Unit of Work)"이라고 한다

- 비즈니스 로직에서 여러 DAO작업을 묶어서 처리하기 위한 방식

```java
PlatformTransactionManager
```

```java
transactionManager.commit(status);
```