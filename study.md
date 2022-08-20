* 스프링의 중심에는 IoC(Inversion Of Control, 제어의 역전) 컨테이너가 있다.
* IoC 컨테이너는 DI(Dependency Injection, 의존 관계 주입) 기능을 제공한다.
   
* 핵심 컨테이너
    - 스프링 기반을 이루는 모듈을 제공한다.
    - 이 그룹에 spring-core와 spring-beans 모듈은 스프링 DI 기능과 IoC 컨테이너 구현을 제공한다.
    - spring-expression 모듈은 스프링 애플리케이션에서 애플리케이션 객체 설정에 사용하는 SpEL(Spring Expression Language) 지원을 제공한다.
   
* AOP와 계측
    - spring-aop 모듈은 AOP 기능을, spring-instrument 모듈은 클래스 계측 지원을 제공한다.

* 메시징
    - 메시지 기반 애플리케이션을 쉽게 개발하도록 도와주는 spring-messaging 모듈을 포함한다.

* 데이터 접근/통합
    - 데이터베이스나 메시징 공급자와의 상호 작용을 쉽게 해주는 모듈을 포함한다.
    - spring-jdbc 모듈은 JDBC를 사용한 데이터베이스 사용을 단순화해주고, 
    - spring-orm 모듈은 하이버네이트나 JPA와 같은 ORM(Object Relational Mapping) 프레임워크 통합을 제공한다.
    - spring-jms 모듈은 JMS 공급자와의 상호 작용을 쉽게 만들어 준다.
    - spring-tx 모듈은 프로그램을 통해 트랜잭션 관리를 선언적으로 할 수 있다.
   
* 웹
    - spring-mvc 모듈은 서블릿 기반의 웹 애플리케이션과 RESTful 웹 서비스 개발을 쉽게 해주며,
    - spring-webflux 모듈은 반응형 웹 애플리케이션과 RESTful 웹 서비스 개발을 쉽게 해준다.
    - spring-websocket 모듈은 웹소켓 프로토콜을 사용하는 웹 애플리케이션 개발을 지원하며,
    - spring-web 모듈은 모든 웹 모듈이 공통으로 사용하는 클래스와 인터페이스를 제공한다.

* 테스트
    - 단위테스트와 통합테스트를 도와주는 spring-test 모듈이 있다.

### 스프링 배포판 명명규칙
'''spring-<짧은 모듈 이름>-<스프링 버전>.jar'''
- <짧은 모듈 이름>은 스프링 모듈 이름으로
    - aop
    - beans
    - context
    - expressions
- <스프링 버전>은 스프링 버전이다.

* DI는 객체 간의 의존관계를 생성자 인수(Constructor argument)나 세터 메서드 인수(Setter method argument)로 명시하고 객체를 생성할 때 생성자나 세터를 통해 의존 관계를 주입하는 방식을 따르는 디자인 패턴이다.

* 스프링 IoC 컨테이너(이를 '스프링 컨테이너'라고도 한다)는 스프링 애플리케이션에서 애플리케이션에 존재하는 객체를 생성하고 의존관계를 주입하는 일을 담당한다.

* 스프링 컨테이너가 생성하고 관리하는 애플리케이션 객체르를 빈(Bean)이라고 부른다.

