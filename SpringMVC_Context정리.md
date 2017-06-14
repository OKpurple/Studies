###기본
/src/main/wepapp/WEB-INF/web.xml 에서 

__rootApplicationContext__를 설정

~~~
<!-- The definition of the Root Spring Container shared by all Servlets and Filters -->
<context-param>
	<param-name>contextConfigLocation</param-name>
	<param-value>/WEB-INF/spring/root-context.xml</param-value>
</context-param>
	
<!-- Creates the Spring Container shared by all Servlets and Filters -->
<listener>
	<listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
</listener>
~~~

__servlet-context__를 설정

~~~
<!-- Processes application requests -->
<servlet>
	<servlet-name>appServlet</servlet-name>
	<servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
	<init-param>
		<param-name>contextConfigLocation</param-name>
		<param-value>/WEB-INF/spring/appServlet/servlet-context.xml</param-value>
	</init-param>
		<load-on-startup>1</load-on-startup>
</servlet>
		
<servlet-mapping>
	<servlet-name>appServlet</servlet-name>
	<url-pattern>/</url-pattern>
</servlet-mapping>
~~~

두 설정 모두 init-param구문에서 contextConfigLocation을 지정했는데 지정하지 않으면 기본적으로 root는 WEB-INF\applicationContext.xml 를 찾게 되고, 자식은 WEB-INF\ {servlet-name}-applicationContext.xml를 찾게된다.

---

/src/main/wepapp/WEB-INF/spring/__root-context.xml__이 있고
root-context.xml의 자식인
servlet-context.xml이

/src/main/wepapp/WEB-INF/spring/__appServlet/servlet-context.xml__ 있다.

기본적인 applicationContext 설정은 다음의 규칙을 따른다.

- DI를 위한 bean을 찾을때, 자신의 applictionContext에서 먼저 찾는다. bean이 없는 경우 부모(root)의 applicationContext 에서 bean을 찾는다.
- 따라서, 같은 bean 을 가지고 있더라도, 자신이 가진게 우선시 된다.
- 반면, 자식이 가지고있는 applicationContext에서 bean을 찾지는 않으며, 같은 level(형제)의 applicationContext bean도 검색하지 않는다.

root ApplicationContext에는 DB관련 설정정보를 담고, servlet(자식) ApplicationContext는 application에서 사용하는 bean설정정보를 담는 것이 일반적이라고 할 수 있다. 잠깐 생각해보면 하나의 웹어플리케이션에서 여러개의  servlet(자식) 이context단위로 존재할 수 있고, 각각 동일한 DB를 바라본다고 하면 이해하기 쉬울 것이다. 

그런데 Spring에서 제공되는 Dispatcher servlet이 프론트 컨트롤러역할을 하므로 실제로 하나의 웹어플리케이션에서 여러개의 servlet를 설정할 이유가 특별히 없다.
그래서 대부분 root-ApplicationContext와 그 자식인 servelt –ApplicationContext 두 개의 설정만 존재한다고 봐도 무방하다.

스프링을 사용한다고 해서 반드시 스프링 기술을 이용할 필요는 없기에 이런식으로 계층 구조를 통해 접근하게 하는 것이다.  결국 우리는 스프링이외의 기술을 잘 사용하지 않기에 단일 servelt-ApplicationContext만 가지고 있는 구조가 되는 것이다. 

 만일 다른 기술을 이용하여 스프링bean을 가져오려면 applicationContext.getBean() 메서드를 통해 스프링 빈에 접근할 수 있고, root ApplicationContext에 선언된 bean도 접근할 수 있게 되는 것이다.	// 부모의 context는 접근 가능하므로 

---

root와 servlet(자식) context 모두
`<context:component-scan>`을 가지고 있다

parent(=root)/child 구조로 bean을 스캔하는 이유는 bean의 의존관계에 영향을 미친다. 특히 AOP등의 transaction 은 bean설정을 통해 point-cut이 결정되는데 parent/child 두군데 bean이 등록되어있다면 transaction을 처리못하는 경우가 종종 발생한다.

따라서 명시적으로 child는 웹애플리케이션 컨텍스트를 담당하므로 웹요청에 응답해주는 Controller가 위치하는 것이 맞고,  parent의 경우 Service 레이어와 Repository, DB 관련 bean 설정을 담고있어야 하는 것이 올바른 설정이라고 할 수 있겠다.

---

###결론

####WEB-INF/web.xml
:	root(부모)와 servlet(자식) context를 설정 (위치포함)

####WEB-INF/spring/[servletName]/serlvet
:	웹요청과 관련된 Controller의 __context:component-scan__ 위치
	ViewResolver와 같은 웹에 관련된 bean 등록

####WEB-INF/spring/root-context.xml
:	spring 프레임워크에 관련된 DAO나 Service의 __context:component-scan__이 위치
Database, Transaction과 같은 bean 등록 속성 설정을 함






