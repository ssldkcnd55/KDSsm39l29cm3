# KDSsm39l29cm3

워크스페이스에 한글 no
공백도 no

UTF-8설정
General - Workspace 
General - Editor - Text Editor - Spelling
JSON -JSON Files
Web - CSS,HTML,JSP

Maven 3.3.9다운
Maven폴더안에 repository 폴더 생성
Maven-conf-settings.xml에서
<localRepository>D:\apache-maven-3.5.3\repository</localRepository> 추가

Eclipse에서
preferences - Maven - User Settings - User Settings를 Maven-conf-settings.xml로 설정

git에서 target제외
Window - preferences - Team - Ignored Resources - Add Pattern - */target/* 추가

Help - Eclipse MarketPlace - STS검색후 설치


프로젝트 생성
Spring Legacy Project - 프로젝트이름은 웹루트명이며 패키지명이여서 소문자로 입력
Spring MVC Project 선택
최상위 패키지 지정 시 : 최소 3개 이상의 레벨로 지정 마지막 패키지는 루트명이랑 같이
ex)com.kh.first

프로젝트 생성 후 Properties에서
Project Facets - Java 버전 1.8 로 변경
오른쪽의 Runtimes 탭 - 톰캣 8.5로 선택(만들어 놓은 서버)

prom.xml
prom.xml 탭에서
11번째 줄 Java Version 1.8로 
12번째줄 spring version 5.0.4로

http://mvnrepository.com/에서
버전을 찾아야한다..?
prom.xml에서 138번째줄 artifactId에 있는 값으로 검색 후 찾..아야한다?

src - main - webapp - WEB-INF 가 우리가 쓰던 web폴더
모든게 WEB-INF에 있어야된다?
이미지같은것들은 webapp - resources안에

jstl-1.2.jar를 연결을 잘 못 시켜줘서
webapp - WEB-INF아래에 lib폴더 만들어서 jar파일 넣어준다.


2.MVC구조?

바로 서블릿으로 가는게아니라
web.xml에서 front controller 역할을 하는 서블릿을 따로 만들어서 
front controller로 넘긴다.?

front controller가 DispatcherServlet..?
근데 그게 servlet-context.xml..?
뭐래는거야

front controller만 xml로 만들고 나머지는 java로 만든다.
근데 기본제공된다/..?

프론트컨트롤러의 주소는 web.xml의 <servlet-name>appServlet</servlet-name>

web.xml에서 servlet - url-pattern을 *.do로 지정..(자주쓰이는..?)

<servlet>안에 <load-on-startup>1</load-on-startup> 첫번째로 시작되는 서블릿이라는 뜻

모놀리식..(한곳에 다때려박는..?)
분산 아키텍쳐를 써도되고?

servlet-context.xml 프론트컨트롤러에 context:component-scan 
선언이 되어있지 않다면 오류가 발생한다

<context:component-scan base-package에서  base-package는 찾는 위치이고 base-package="com.kh.first" 는 com.kh.first 밑에서 찾아라는 뜻이다

”com.kh.hello/**/controller” 이런식으로 하면 controller에서만 컴파일이 되고 dao나 service에서는 컴파일이 발생되지않아서 오류가 발생한다.

스프링에서 서블릿 단위는 메소드로 바뀌었다.
login메소드는 로그인 logout메소드는 로그아웃

Model은 request와 response를 합쳐놓은 객체?
new,포워딩 모든걸 Spring이 대신해준다..?
(model은 request와 response를 합쳐놓은것이다)

매개변수에 객체를 쓰면 스프링은 자동으로 객체생성(의존성주입(did))가 되므로 new를 쓰지않아도 된다

서블릿에서 리턴하는값은 view파일의 이름?을 리턴한다
리턴된값은 servlet-context.xml로오는데 ViewResolver가 받아서 관리..? view로 연결해준다?
bean이 클래스
ViewResolver가 view관리자?

뷰파일의 이름을 스트링형태로 리턴한다. 
뷰파일 이름앞에 밑에있는 <beans:property의 속성처럼 prefix 앞에 붙일 이름 /WEB-INF/views/ suffix뒤에 붙일 이름 .jsp 그래서 /WEB-INF/views/home.jsp로 내보내진다.

model.addAttribute("serverTime", formattedDate ); 보낸것을 home.jsp에서 
 ${serverTime}불러오는 방식

webapp이 컨텍츠디렉토리이다. /first 바로 밑에있는 폴더라는 뜻이다

src메인 쪽을 전부 classpath라고 한다

모든 view파일은 WEB-INF - views폴더안에 있어야되는데
그 밖에있으면 페이지간 이동에서 오류가 있을수있다.

Spring에서  welcome파일은 페이지 시작하는 역할만한다?

<jsp:forward> 포워드는 url은 그대로 있는데 페이지가 바뀐다?

@Component("member")
("member") 레퍼런스변수 - bean으로 등록
자동 의존성 주입 발동!
member타입으로 자동 new 객체생성
(스프링이 주관한다)
("member") 이렇게 쓰지않으면
member=new Member();을 써주어야한다.

첫번째 : 디스페처서블릿에 <bean>으로 등록한다
<bean id="member" class="com.kh.first.member.model.vo.Member"></bean> 이런식으로 등록한다

두번째: 어노테이션을 등록한다.
@Component("member") 이런식으로 등록한다.

스프링이 자동으로 setter getter가 작동하게 하려면 테이블의 컬럼명과 필드명을 동일하게 해야된다

자동으로 세터 게터가 발동되므로 하나라도 세터 게터가 없다면 오류가 발생하므로 꼭 만들어주어야한다.

implements java.io.Serializable(직렬화) 꼭 해주어야한다. 나중에 이유없이 오류가 발생할수도있다.
직렬화 번호가 중복되어도 오류가 발생한다.
번호는 항상 다르게 12345L등등

스프링에서는 메소드의 매개변수로 클래스명 레퍼런스 변수 선언하면 자동으로 해당클래스에 대한 객체 생성이 된다
(new 생성자())

컨트롤러에서 @Controller을 적어주면
디스페쳐서블릿 bean에 자동등록해준다.

컨트롤러를 만들고 나서
@RequestMapping("login.do") 이런식으로 적어준다.
이런식도 가능하다 = @RequestMapping(value = "login.do", method = RequestMethod.GET)
@RequestMapping(value = "login.do", method = RequestMethod.POST)

mv.setViewName("home");라고 쓰면
home으로 보낸다는 뜻이다.

핸들러매핑은 디스패처 서블릿에 들어있다.
.do라고 붙어있는 이름이 오면 핸들러매핑이 진짜이름과 비교 해서 연결해주는 역활을 한다.

loginCheck(Member member,ModelAndView mv)에서 Member member,ModelAndView mv가 매개변수이고 
매개변수로 선언된 객체를 Command 객체라고 한다.

미완성된이라는 뜻을가졌다. =  abstract

서비스에서 @Service를 적어주면
디스페쳐서블릿 bean에 자동등록해준다.

@Autowired라고 쓰면 자동으로 연결 되라는 뜻이다.
controller와 service같은걸 연결 할때 쓴다.

mv.addObject("member",returnMember);
mv.setViewName("home");
는 member라는 이름으로 returnmember을
home으로 보낸다는뜻이다.

<property name="dataSource" ref="dataSource">
name은 아무거나 적어도되지만 ref는 참조하는 아이디를 적어줘야한다.

스프링 시큐리티는 salt형식으로 랜덤으로 계속 돌아가면서 값을 계속 랜덤하게 암호화하는 암호화방식이다.
암호화된값을 확인하려면 matches라는 메소드로 matches(참조하기를 원하는 값,암호화한값)형식으로 하면 boolean값이 나온다.

