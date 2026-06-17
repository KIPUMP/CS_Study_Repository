# AOP(Aspect Oriented Programming)

> 핵심 비즈니스 로직과 공통 관심사를 분리하는 기술

- Ioc/DI , 서비스 추상화와 더불어 스프링의 3대 기반 기술

- 여러 서비스를 구현할 때, 공통된 로직을 분리하여 중복을 막는다.

- AOP는 OOP만으로 모듈화하기 힘든 부가기능을 효과적으로 모듈화하도록 도와주는 기술

- AOP 적용 전

```java
public void reserve() {

    long start = System.currentTimeMillis();

    reservationDao.save();

    long end = System.currentTimeMillis();

    System.out.println(end - start);
}
```

- AOP 적용 후

```java
public void reserve() {

    reservationDao.save();
}
```

```java
@Aspect
@Component
public class TimeTraceAop {

    @Around("execution(* com.careerbridge..*(..))")
    public Object execute(ProceedingJoinPoint joinPoint)
            throws Throwable {

        long start = System.currentTimeMillis();

        try {
            return joinPoint.proceed();
        } finally {
            long end = System.currentTimeMillis();

            System.out.println(end - start);
        }
    }
}
```
