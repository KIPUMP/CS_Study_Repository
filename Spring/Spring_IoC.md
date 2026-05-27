# Spring IoC 용어 정리

### Bean(빈. bean Object)

- bean은 Spring이 IoC 방식으로 관리하는 오브젝트라는 뜻이다.

- Spring이 직접 생성과 제어를 담당하는 오브젝트

### Bean factory(빈 팩토리)

- Spring의 IoC를 담당하는 핵심 컨테이너를 가리킨다.

- Bean을 등록하고, 생성하고, 조회하고, 돌려주고, 추가적인 Bean을 관리하는 기능을 담당한다.

### Application-context(애플리케이션 컨텍스트)

- Bean Factory를 확장한 IoC 컨테이너이다

- Application-Context는 BeanFactory를 상속한다

### Configuration metadata(설정정보/매타정보)

- Application-context 또는 Bean-factory가 IoC를 적용하기 위해 사용하는 메타정보

