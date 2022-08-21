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

### 스프링 5의 새로운 내용
- 자바 9와 호환된다.
    - 자바 9의 특징을 사용해 애플리케이션을 개발하고 자바 9로 배포(deploy)할 수 있다.
- 스프링 JAR를 자바 9의 모듈 경로나 클래스경로에 추가할 수 있다.
    - 스프링 JAR를 모듈 경로에 추가하면 자동으로 자동 모듈이 되어 JAR 내부의 모든 패키지를 외부에 노출시킨다.
- 비동기(asynchronous)와 넌블로킹(non-blocking) 애플리케이션 개발에 사용하는 반응형 프로그래밍 패러다임을 포함한다.
    - 스프링은 리액터 3.1과 RxJava 1.3이나 2.1 라이브러리에 정의된 반응형 타입을 지원한다.
- 스프링 5의 소스 코드는 이제 자바 8로 되어 있다.
- 스프링 5에서는 포틀릿, 벨로시티 템플릿, 자스퍼레포트 지원이 중단됐다.
- @Nullable, @NonNull, @NonNullApi, @NonNullFields 애너테이션을 사용해 스프링 애플리케이션에 null 안정성(null-safety)을 도입할 수 있다.
    - @Nullable은 필드, 메소드, 메소드 인수 또는 메소드 반환값이 null일 수 있다는 뜻이다.
    - @NonNull은 필드, 메소드,  메소드 인수 또는 메소드 반환값이 null일 수 없다는 뜻이다.
    - @NonNullApi는 패키지 수준의 애너테이션으로 메소드와 메소드 파라미터가 null일 수 없다는 뜻이다.
    - @NonNullFields는 패키지 수준의 애너테이션으로 필드가 null일 수 없다는 뜻이다.
    - 이런 애너테이션들을 (FindBugs와 같은) 정적 코드 분석 도구와 사용하면 프로그램에서 실행 시점에 java.lang.NullPointerException을 발생시킬 수 있는 잠재적인 문제를 찾아 낼 수 있다.
- AnnotationConfigApplicationContext 클래스에 새로 도입된 메소드를 통해 함수형으로 빈 등록과 커스텀화가 가능하다.
- 애플리케이션을 더 빠르게 시작하기 위해 (클래스경로를 스캔하는 대신) 파일에서 스프링 컴포넌트의 인덱스를 만들거나 읽을 수 있다.
- 서블릿 4.0에 javax.servlet.http.PushBuilder를 스프링 웹 MVC 애플리케이션에서 컨트롤러 메소드 인수로 사용할 수 있다.
    - PushBuilder를 사용하면 HTTP/2 프로토콜을 사용해 웹 클라이언트로 자원을 푸시할 수 있다.
- 새 웹 모듈인 spring-webflux를 도입했다. 
    - 이를 사용하면 RxJava나 리액터 라이브러리를 통해 반응형 웹 애플리케이션과 반응형 RESTful 웹 서비스를 개발할 수 있다.
- AsyncRestTemplate 지원은 사용을 금지하고, 그 대신 반응형 WebClient를 사용한다.

### 인터페이스를 사용하는 프로그래밍 programming to interface
    - 의존 중인 클래스가 의존 관계가 구현하는 인스턴스로 의존성을 만드는 설계 원칙
    - 의존 중인 클래스와 의존 관계 사이에 느슨한 결합을 만든다.
    - 의존 관계 클래스가 구현하는 인터페이스를 의존 관계 인터페이스(dependency interface)라고 부른다.

- Setter 기반 DI에서는 <property> 엘리먼트를 사용해 빈 의존 관계를 설정했다.

- Singleton scope는 XML파일에 정의된 모든 빈의 디폴트 스코프다.
    - singleton, prototype scope
    - 웹 애플리케이션에서는 request, session, websocket, application과 같은 몇 가지 스코프를 사용한다.

- Singleton 스코프 빈 인스턴스의 존재 범위는 한 스프링 컨테이너 인스턴스 내부로 제한된다.
    - 똑같은 설정 메타데이터로부터 2개의 스프링 컨테이너를 만들면 각 스프링 컨테이너마다 자신만의 싱글턴 빈 인스턴스를 갖게 된다.

- Singleton 스코프 빈은 기본적으로 사전-인스턴스화된다.
    - 스프링 컨테이너가 인스턴스를 생성할 때 싱글턴 스코프 빈의 인스턴스도 생성된다.

- 스프링 컨테이너에 싱글톤 빈을 처음으로 요청받았을 때 인스턴스를 생성하라고 지시할 수도 있다.
```xml
    <bean id="lazyBean" class="exmpale.LazyBean" lazy-init="true" />
```

- <beans> 엘리먼트의 defalut-lazy-init 속성을 지정하면 XML 파일에 빈 정의를 디폴트 초기화 전략을 설정할 수 있다. 
    - <bean> 엘리먼트의 lazy-init 속성이 <beans> 엘리먼트의 default-lazy-init와 다른 값을 가지면 lazy-init 속성에 지정한 값이 해당 빈에 적용된다.

- 프로토타입 스코프(Prototype scope) 빈이 싱글톤 스코프 빈과 다른 점은 스프링 컨테이너가 항상 프로토타입 스코프 빈의 새로운 인스턴스를 반환한다는 점이다.
    - 프로토타입 스코프 빈은 항상 지연 초기화된다. (lazy-init)

- 빈이 어떤 대화적 상태도 유지하지 않는다면(즉 애초에 상태가 없는 stateless 빈이라면) 싱글턴 스코프 빈으로 정의해야 하고,
    - 빈에 대화적 상태를 유지해야 한다면 프로토타입 스코프 빈으로 정의해야 한다.

- 애플이케이션에서 ORM 프레임워크(하이버네이트, 아이바티스 등)를 사용한다면 ORM 프레임워크가 도메인 객체를 생성하거나 직접 애플리케이션 코드에서 new 등의 프로그램을 사용해 도메인 객체를 생성한다.
    - 애플리케이션 영속화를 위해 ORM을 사용하는 경우에는 XML 파일 안에 도메인 객체를 정의하지 않는다.

- <bean> 엘리먼트의 abstract 속성을 true로 만들면 그 빈이 추상 빈이라는 뜻이다.
    - 스프링 컨테이너가 추상 빈 정의에 해당하는 빈을 생성하지 않는다.
    - 추상 빈에 의존하는 빈을 정의할 수 없다.
    - 추상 빈을 참조하는 <property>나 <constructor-arg> 엘리먼트에서 사용할 수 없다.
    - class 속성을 지정하지 않는 빈은 꼭 추상 빈으로 만들어야 스프링 컨테이너가 그 빈 인스턴스를 생성하지 않는다.

### 상속할 수 있는 Bean 정보
    - 프로퍼티 : <property> 엘리먼트로 설정
    - 생성자 인수 : <constructor-arg> 엘리먼트로 설정
    - 메서드 오버라이드
    - 초기화와 정리 메서드
    - 팩토리 메서드 : <bean> 엘리먼트의 factory-method 속성으로 설정

- parent bean 이 추상 bean 이 필요는 없다.


