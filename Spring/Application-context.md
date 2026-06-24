# ApplicationContext

> 객체(Bean)를 생성하고 , 연결하고, 관리해주는 공장 + 관리자 역할

- Aplication-context = Ioc Container = Bean factory

- 빈(객체)을 생성하고 관리

- 빈들 사이의 의존관계를 설정

- Spring framework의 핵심 Container

### ApplicationContext의 핵심 역할

- Bean 생성 : 객체 생성

- DI 수행 : 의존성 주입

- Singleton 관리 : 객체 재사용

- 생명주기 관리 : 초기화 소멸

- AOP 지원 : 프록시 생성

### Bean 작성 방식

- XML 방식

```xml

<bean id="userDao" class="com.example.UserDao" />

<bean id="userService" class="com.example.UserService">
    <property name="userDao" ref="userDao" />
</bean>

```

- Java Config 방식

```java
@Configuration
public class AppConfig {

    @Bean
    public UserDao userDao() {
        return new UserDao();
    }

    @Bean
    public UserService userService() {
        UserService userService = new UserService();
        userService.setUserDao(userDao());
        return userService;
    }
}
```

- 애노테이션 방식

```java
@Repository
public class UserDao {
}

@Service
public class UserService {

    private final UserDao userDao;

    public UserService(UserDao userDao) {
        this.userDao = userDao;
    }
}
```

### Aplication-context 동작 방식

![ApplicationContext 동작 방식](image-1.png)

1) Spring 실행 

2) ApplicationContext 생성 

3) ApplicationContext 설정 정보 읽기

4) Bean 객체 생성

5) 의존성 주입(DI) 

6) Bean 컨테이너 저장

→ 필요할 때 getBean()으로 꺼내 쓰거나 자동 주입받음

### Bean 등록 예시

1) 빈으로 사용할 클래스 작성

```java
public class UserDao {
    public void save() {
        System.out.println("user 저장");
    }
}
```

```java
public class UserService {

    private final UserDao userDao;

    public UserService(UserDao userDao) {
        this.userDao = userDao;
    }

    public void join() {
        userDao.save();
    }
}
```

2) 설정 클래스에서 빈 정의 

- UserDao , UserService 객체를 스프링이 관리하도록 등록해야 합니다.

##### @Configuration 

- "이 클래스는 스프링 설정 클래스다" 라는 것을 의미

##### @Bean 
  
- "이 메서드가 반환하는 객체를 스프링 빈으로 등록하겠다" 라는 것을 의미

- 메서드 이름이 기본적으로 빈 이름이 됨

```java
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

@Configuration
public class AppConfig {

    @Bean
    public UserDao userDao() {
        return new UserDao();
    }

    @Bean
    public UserService userService() {
        return new UserService(userDao());
    }
}
```

3) ApplicationContext 생성

- new AnnotationConfigApplicationContext(AppConfig.class)를 통해 AppConfig 클래스를 읽어서 빈 정보를 파악하고 그 빈들을 생성해서 스프링 컨테이너에 삽입

```java
import org.springframework.context.ApplicationContext;
import org.springframework.context.annotation.AnnotationConfigApplicationContext;

public class Main {
    public static void main(String[] args) {
        ApplicationContext context =
                new AnnotationConfigApplicationContext(AppConfig.class);
    }
}
```

4) 컨테이너에서 빈 꺼내 사용하기

```java
import org.springframework.context.ApplicationContext;
import org.springframework.context.annotation.AnnotationConfigApplicationContext;

public class Main {
    public static void main(String[] args) {
        ApplicationContext context =
                new AnnotationConfigApplicationContext(AppConfig.class);

        UserService userService = context.getBean("userService", UserService.class);
        userService.join();
    }
}
```

### ApplicationContext 장점

- 클라이언트는 구체적인 팩토리 클래스를 알 필요가 없다

- 애플리케이션 컨텍스트는 종합 IoC서비스를 제공한다

- 애플리케이션 컨텍스는 빈을 검색하는 다양한 방법을 제공한다

