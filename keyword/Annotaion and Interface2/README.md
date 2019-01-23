### 1. @EnableWebSecurity

**@EnableWebSecurity** 애너테이션은 웹 보안을 활성화 한다. 하지만 그자체로는 유용하지 않고, 스프링 시큐리티가 **WebSecurityConfigurer**를 구현하거나 컨텍스트의 **WebSebSecurityConfigurerAdapter**를 확장한 빈으로 설정되어 있어야 한다.

하지만 **WebSebSecurityConfigurerAdapter**를 확장하여 클래스를 설정하는 것이 가장 편하고 자주 쓰이는 방법이다.



### 2. WebSecurityConfigurerAdapter

| 메소드                                  | 설명                                                         |
| --------------------------------------- | ------------------------------------------------------------ |
| configure(WebSecurity)                  | 스프링 시큐리티의 필터 연결을 설정하기 위한 오버라이딩이다.  |
| configure(HttpSecurity)                 | 인터셉터로 요청을 안전하게 보호하는 방법을 설정하기 위한 오버라이딩이다. |
| configure(AuthenticationManagerBuilder) | 사용자 세부 서비스를 설정하기 위한 오버라이딩이다.           |

### 3. HttpServletRequest

하나의 요청에서 HttpServletRequest 객체가 소멸하기 까지 상태정보를 유지하고자 할 때, 한번의 요청으로 실행된 페이지끼리 정보를 공유하고자 할 때 사용되며, 디스패처에 의한 요청재지정을 하기 전 HttpServletRequest 객체의 setAttribute( ) 메소드로 데이터를 등록하고 요청 재지정으로 HttpServletRequest 객체가 전달된 페이지에서 getAttribute( ) 메소드로 추출할 수 있다.

### 4. XFrameOptionsHeaderWriter

X-Frame-Options <iframe>,  <object>에서 렌더링할 수 있는지 여부를 나타내는데 사용

사이트 내 콘텐츠들이 다른 사이트에 포함되지 않도록 하여 <u>클릭제킹</u> 공격을 막기 위해 이 헤더를 사용한다.

**클릭재킹**(Clickjacking, User Interface redress attack, UI redress attack, UI redressing)은 웹 사용자가 자신이 클릭하고 있다고 인지하는 것과 다른 어떤 것을 클릭하게 속이는 악의적인 기법으로써 잠재적으로 공격자는 비밀 정보를 유출시키거나 그들의 컴퓨터에 대한 제어를 획득할 수 있게 된다. [[1\]](https://ko.wikipedia.org/wiki/%ED%81%B4%EB%A6%AD%EC%9E%AC%ED%82%B9#cite_note-1) [[2\]](https://ko.wikipedia.org/wiki/%ED%81%B4%EB%A6%AD%EC%9E%AC%ED%82%B9#cite_note-2) [[3\]](https://ko.wikipedia.org/wiki/%ED%81%B4%EB%A6%AD%EC%9E%AC%ED%82%B9#cite_note-3) [[4\]](https://ko.wikipedia.org/wiki/%ED%81%B4%EB%A6%AD%EC%9E%AC%ED%82%B9#cite_note-4) 이것은 다양한 웹 브라우저들과 컴퓨팅 플랫폼들에서의 취약점으로서 브라우저 보안 이슈이다. 클릭재킹은 사용자의 인식 없이 실행될 수 있는 임베디드 코드나 스크립트의 형태를 갖는다.

**Syntax**

1. X-Frame-Options: deny
2. X-Frame-Options: sameorigin
3. X-Frame-Options: allow-from https://example.com/

`deny`는 같은 사이트 내에서 frame을 통한 접근도 막습니다.
`sameorigin`를 명시할 경우에는 frame에 포함된 페이지가 페이지를 제공하는 사이트와 동일한할 경우 계속 사용할 수 있습니다.

`allow-from uri`지정된 프레임에만 페이지를 표시

### 5. CharacterEncodingFilter
스프링은 웹 요청과 응답에 대한 인코딩 처리를 위해 CharacterEncodingFilter를 제공합니다.

인코딩 필터의 경우 모든 프로젝트에서 사용가는 공통적인 기능이므로 스프링프레임워크 측에서 번거로움을 피하기 위해 제공하는것 같습니다.

CharacterEncodingFilter 클래스는 Servlet 표준 스펙인 javax.servlet.Filter 인터페이스를 구현한 클래스이기 때문에 기존의 Servlet, JSP 에서 사용하던 필터와 똑같이 사용 가능함

### 6. CsrfFilter

**CSRF(Cross Stie Request Forgery) : 사이트간 요청 위조**

웹 애플리케이션 취약점 중 하나로 사용자가 자신의 의지와 무관하게 공격자가 의도한 행동을 하여 특정 웹페이지를 보안에 취약하게 한다거나 수정, 삭제 등의 작업을 하게 만드는 공격방법을 의미한다 - 나무위키