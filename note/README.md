# 무작정 정리
19/01/08
### 1. Framework
소프트웨어의 구체적인 부분에 해당하는 설계와 구현을 재사용이 가능하게끔
일련의 협업화된 형태로 클래스들을 제공하는 것

 **장점**
 1) 효율적.
시간과 비용이 훨씬 절약되며 생산성이 좋아짐
2) Quality 향상
다수의 개발자 -> 검증된 코드
3) 유지 보수
코드가 체계적이라 유지보수에 안정적

 **단점**
 1) 긴 학습기간
 습득하고 이해하는데 오랜 시간이 걸림
 2) 제작자의 의도된 제약 사항
 자유롭고 유연하게 개발하는 데 한계
 
---
### 2. Maven
자바 프로젝트를 자동으로 빌드해주는 빌드 툴
### 3. Build
소스코드 파일을 컴퓨터에서 실행할 수 있도록 바꾸는 것
### 4. Dependency
```java
public class Order{
 private Customer customer;
 
 public Order() {
	 coustomer = new Customer(); //의존?
	 //tightly coupled
 }
}

public class Customer(){
 private String name;
 private Address address;
 private String email;
 // getter, setter etc..
}
```


하나의 프로그램은 여러 개의 Class를 가진다.
가령 Class Order 내부에서 new Customer , 즉 새로운 인스턴스를 만들게 되면
Order Class 는 Customer Class에 대해 의존성을 가지게 된다(?)

**해결 방법**
1) Interface 도입
```java
public interface CustomerServies{
	void setName(String name);
	String getName();
	//...
}
Class Customer implements CustomerServie{
	private String name;
}
public class Order{
	private CustomerServie customer;
	public Order() {
		customer = new Customer();
		//loosely coupled 하지만 여전히 Order Class에서 Customer를 Instance를 생성
	}
}
```
2) 의존성 주입(Dependency Injection, DI)
프로그래머가 직접 new Object 를 하지 않음 -> IoCContainer(Framework)
컨테이너가 인스턴스의 생명주기를 관리하며, 생성된 인스턴스들에게 추가적인 기능을 제공

```java
public class Order{
	private CustomerServies customer;
	public Order() {
		customer = new Customer();
	}
}
public class IoCContainer{
	public Order getOrder() {
	 CustomerService customer = new Customer();
	 return new Order(custumer);
	}
}
```

### 5. POJO (Plain Old Java Object)
**스프링은 POJO 프레임워크 중 하나**
* '평범한 구식 자바 객체'
* 특정 규약(contract)에 종속되지 않는다.
* 특정 환경에 종속되지 않는다.
* 객체지향원리에 충실해야 한다.

**POJO를 사용하는 이유**
* 코드의 간결함
* 자동화 테스트에 유리
* 객체지향적 설계의 자유로운 사용

### 6. J2EE(Java2 Enterprise Edtion)
* 서버 기반의 자바 기술
* Servlet, JSP 레벨의 최소한의 서버 프로그래밍 인터페이스만 가지고는 복작한 엔터프라이즈 애플리케이션을 제작하기 어려움

### 7. REST API(Representational State Transfer API)
**REST** : 자원을 이름으로 구분하여 해당 자원의 상태(정보)를 주고 받는 모든 것

*자원 ex) 문서, 그림, 데이터 , etc*
*상태ex) 요청되는 시점에 따른  자원의 상태 (정보)
JSON 혹은 XML를 통해 데이터를 주고 받는 것이 일반적* 

1) REST 구성
* 자원(RESOURCE) - URI
* 행위(Verb) - HTTP METHOD
* 표현(Representaions)

**API** : 데이터와 기능의 집찹을 제공하여 컴퓨터 프로그램간 상호작용을 촉진하면, 서로 정보를 교환 가능 하도록 하는 것
**REST API** : REST기반으로 서비스 API를 구현한것`
