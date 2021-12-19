# 원격 프로그램 실행

- 브라우저와 WAS가 있어야 원격 프로그램 실행 가능

- 브라우저에 URL을 입력하면 IP주소에 담긴 포트를 톰캣이 프로그램을 실행한다. 

- 외부에서 프로그램을 실행하려면

1. 프로그램 등록
2. URL과 프로그램을 연결 해야한다.

URL과 메인 메서드를 연결한다면

```Java
@Controller // 프로그램 등록
public class Hello {
    int iv = 10; // 인스턴스 변수
	static int cv = 20; // static 변수

    @RequestMapping("/hello")  // URL과 main()을 연결
	public void main() { // 인스턴스 메서드, iv, cv 둘 다 사용 가능
		System.out.println("Hello");
		System.out.println(cv); // ok
		System.out.println(iv); // ok
	}
    // 여기서 메서드를 private 으로 바꾸어도 외부에서 메서드를 호출하는 데에는 문제없다. (RequestMapping을 했기 때문에)
	
	public static void main2() { // static 메서드 - cv만 사용가능
		System.out.println(cv); // ok
//		System.out.println(iv); // 에러
	}

}
```
main 메서드는 인스턴스 메서드이다.
호출이 된다는 것은 과정에서 객체 생성을 한다는 뜻
url을 입력하면 톰캣이 내부에서 객체 생성을 해주고 메서드를 호출한다.


# sts 프로그램 생성

file - new - Spring legacy project

HomeController - 원격 호출 가능한 프로그램으로 등록

@RequestMapping - URL과 메서드 연결(맵핑,Mapping)

# Reflect API

만약 Hello 클래스의 main이 private이라면

```Java
public class Main {
	public static void main(String[] args) {
//		Hello hello = new Hello();
//		hello.main(); // private 이라서 외부 호출 불가
		
		// Reflection API를 사용 - 클래스 정보를 얻고 다룰 수 있는 강력한 기능 제곡
		// java.lang.reflect패키지를 제공
		// Hello클래스의 Class 객체(클래스의 정보를 담고 있는 객체)를 얻어온다.
		Class helloClass = Class.forName("com.fastcampus.ch2.Hello");
		
	}
}

```

# AWS에 배포하기

export - war 검색 - WAR file - ch2.war 다운로드
AWS의 원격 서버 Tomcat의 webapps에 war파일을 넣는다.

localhost:8080이 아닌 AWS서버의 ip주소:8080/ch2/hello로 URL에 접근 가능 하다.

# HTTP 요청과 응답

브라우저에 URL을 담고 서버에 호출하면 Tomcat은 HttpServletRequest 객체를 만든다. 요청한 정보를 담고 연결된 메서드의 파라미터로 HttpServletRequest를 넘긴다.

request 객체를 사용하여 요청 정보를 얻을 수 있다.





