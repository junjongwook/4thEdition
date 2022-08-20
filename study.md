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

* 스프링 기반 애플리케이션에서 애플리케이션 객체와 그들의 의존 관계의 정보는 설정 메타데이터(Configuration metatdata)를 사용해 지정한다.

* 스프링 시큐리티는 자바 애플리케이션을 안전하게 만들기 위해 필요한 사용자 인증(authentication)과 권한 부여(authorization) 기능을 제공한다.

### Maven 으로 실행하기
    mvn compile exec:java -Dexec.mainClass=sample.spring.chapter01.bankapp.BankApp

* 설정 메타데이터를 스프링 컨테이너에 전달하는 방법은 XML 파일을 이용하는 방법과 POJO 클래스에 애너테이션을 설정하는 방법이 있다.

* 스프링 3.0부터는 스프링 @Configuration 애너테이션을 설정한 자바 클래스를 사용해 스프링 컨테이너에 설정 메타데이터를 제공할 수 있다.

* <beans>는 Root Element 이다.

* 각 <bean> Element는 스프링 컨테이너가 관리할 애플리케이션 객체를 설정한다.
    - 스프링 용어로 <bean> Element를 빈 정의(Bean Deifinition)라고 부르고,
    - 스프링 컨테이너가 빈 정의에 따라 만들어낸 객체를 빈(Bean)이라고 부른다.
    - id 속성은 빈의 유일한 이름을 지정하며,
    - class 속성은 빈 클래스의 전체 이름(full-qualified class name)을 지정한다.
    - <bean> Element에 name 속성을 넣어서 빈에 별명(alias)을 지정할 수도 있다.

* 일반적으로 스프링 컨테이너는 도메인 객체를 관리하지 않는다.
    - 도메인 객체는 애플리케이션이 사용하는 ORM 프레임워크(하이버네이트 등)가 생성하거나 직접 new 연산자를 사용해 사용한다.

* <property> Element는 스프링 컨테이너가 의존관계(또는 설정 프로퍼티)를 설정하기 위해 호출할 자바빈 스타일 세터(Setter) 메서드와 대응된다.

### <property> 엘리먼트를 이용한 의존관계 정의하기
```xml
	<bean id="controller"
		class="sample.spring.chapter01.bankapp.FixedDepositController">
		<property name="fixedDepositService" ref="service" />
	</bean>
```
    - <property> 엘리먼트의 name 속성의 경우 빈 클래스의 자바빈 스타일의 세터(Setter) 메소드 이름과 대응하며, 스프링 컨테이너는 빈 생성 시 이 세터 메소드를 호출한다.
    - <property> 엘리먼트의 ref 속성은 인스턴스를 생성한 다음 자바빈 스타일 세터 메소드에 전달할 빈을 가르킨다.
        - 이 ref 속성값은 설정 메타데이터에 있는 <bean> 엘리먼트 중 하나의 id 속성값(또는 name에 지정된 이름 중 하나)과 일치해야 한다.

* 스프링 컨테이너가 빈을 생성하는 순서는 applicationContext.xml 파일에 빈이 정의된 순서에 따라 결정된다.
    - 스프링 컨테이너는 세터(Setter) 메소드가 호출하기 전에 빈이 의존하는 다른 빈들을 완전히 설정되도록 보장한다.

* 빈 정의를 이름(id 속성값)이나 타입(class 속성값) 또는 빈 클래스가 구현하는 인터페이스 이름으로 부르는 경우가 흔하다.

* 스프링 ApplicationContext 객체는 스프링 컨테이너 인스턴스를 표현한다.
    - 스프링은 ClassPathXmlApplicationContext, FileSystemXmlApplicationContext, XmlWebApplicationContext, AnnotationConfigWebAppicationContext 등 몇가지 ApplicationContext 인터페이스 구현을 제공한다.
    - 어떤 ApplicationContext를 선택하느냐는 설정 메타데이터의 정의 방법(XML, 에너테이션, 자바 코드 등)과 애플리케이션 유형(웹 또는 독립형)에 따라 달라진다.
        - ClassPathXmlApplicationContext, FileSystemXmlApplicationContext 클래스는 설정 메타데이터를 XML 형태로 정의한 독립 실행 애플리케이션에 적합하고,
        - XmlWebApplicationContext 클래스는 설정 메타데이터를 XML 형태로 정의한 웹 애플리케이션에 적합하며,
        - AnnotationConfigWebApplicationContext 클래스는 자바 코드를 통해 설정 메타데이터를 정의하는 웹 애플리케이션에 적합하다.

* getBean에 넘기는 인수는 스프링 컨테이너에서 가져오려는 빈의 이름이다.
    - getBean 메소드에 전달하는 빈 이름은 반드시 가져오려는 빈의 id나 name 속성과 같아야 한다.
    - 스프링 컨테이너에 등록된 이름과 지정한 이름이 일치하는 빈을 찾을 수 없으면 getBean 메소드가 예외를 발생시킨다.

    

