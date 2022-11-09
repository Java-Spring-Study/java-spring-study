# Tomcat & Apache

![image](https://user-images.githubusercontent.com/97498405/200717471-8b627cc2-ec8e-419e-983f-2fad6ba95146.png)

### Q . 브라우저에서 localhost:8080을 입력했을 때 웹 페이지가 생성되는 과정을 공부하고 싶습니다. ( 톰캣과 아파치에서의 처리 과정을 살펴보고 싶습니다. )

# 아파치(Apache)

`오픈 소스 소프트웨어 프로젝트`를 운영하는 비영리 단체

주요 프로젝트

- **Apache HTTP Server**
- **Tomcat**
- Maven
- 하둡과 그 파생 프로젝트 : 빅 데이터 프로세싱을 위한 프로그램.
- …등등

---

## 1.1 Apache HTTP Server

**정의** : 

아파치 소프트웨어 재단에서 만든 `웹 서버` 프로그램이다.

**특징**

- 오픈소스 및 크로스 플랫폼 웹 서버이다. (무료 서버)
- Apache + PHP + MySQL을 통틀어 "APM"이라고 통칭하면서 웹 서버를 돌리기 위한 기본 3종 세트 !
  
    ( 물론 다른 언어와 다른 DBMS도 지원하지만, 저 조합이 가장 인지도가 높다. )
    
- [JSP](https://namu.wiki/w/JSP) 의 경우에도 [톰캣](https://namu.wiki/w/%ED%86%B0%EC%BA%A3)과 연동하여 돌릴 수 있다.
- **정적타입**
(HTML, CSS, 이미지 등)의 데이터만을 처리하기 때문에 톰캣이란 것이 등장한 것 같다.

**용어**

- `웹 서버`
  
    : 웹 브라우저와 같은 웹 페이지를 반환하는 컴퓨터 프로그램.  
    
    ( HTTP 또는 HTTPS를 통해 웹브라우저에서 요청하는 HTML 문서나 오브젝트(이미지 파일)을 전송해주는 서비스 프로그램 )
    

## 1.2 톰 캣( Tomcat )

**정의** : 아파치 소프트웨어 재단에서 개발하는 Java기반의 `서블릿 컨테이너` 이자 `웹서버` 프로그램이다.

**특징** 

- JSP/Spring 으로 웹사이트를 구축한다면 톰캣을 거의 사용된다고 보면 된다.
- 톰캣은 오로지 서블릿/JSP 및 HTTP처리 엔진만 들어 있다.
- 톰캣의 존재로 JSP 사용자가 늘어나 ASP는 쓰는 사람만 쓰는 언어가 되었다?
- Apache HTTP Server 와는 다르게 DB연결, 다른 응용프로그램과 상호 작용 등 동적인 기능들을

사용할 수 있다.

**용어**

- `ASP`
  
    MS에서 내놓은 Active Server Page이다.
    
    이것은 [윈도우](https://namu.wiki/w/Microsoft%20Windows)에 최적화되어 있고, 다른 OS는 정식으로 지원하지 않는다.
    
    [아파치 HTTP 서버](https://namu.wiki/w/%EC%95%84%ED%8C%8C%EC%B9%98%20HTTP%20%EC%84%9C%EB%B2%84)에서 Apache::ASP라는 모듈을 사용하면 아주 제한적으로 PerlScript 기반의 ASP를 구동할 수 있지만, [리눅스](https://namu.wiki/w/Linux)환경에선 [PHP](https://namu.wiki/w/PHP), [JSP](https://namu.wiki/w/JSP), [Python](https://namu.wiki/w/Python) 등의 경쟁자들이 많아서...
    
    물론 한국에서 이렇다… 정부 표준이 자바 웹개발이기 때문!
    
- `서블릿`
  
    클라이언트의 요청을 받고 요청을 처리하여 결과를 클라이언트에게 제공하는 자바 인터페이스.java.servlet.package에 정의된 인터페이스로서 서블릿의 라이프 사이클을 위한 세 가지 필수적인 메소드들을 정의한다.
    
    - init()
    - service()
    - destory()

---

## **아파치 톰 캣으로 부르는 이유?**

기본적으로 위처럼**아파치**와**톰캣**의 기능은 나뉘어져 있지만, **톰캣 안에 있는 컨테이너**를 통해 **일부**의 기능을 발휘하기 때문에 보통 **아파치 톰캣**으로 합쳐서 부르곤 한다.

![image](https://user-images.githubusercontent.com/97498405/200717532-a14c9a58-da55-4329-9653-5ddcb8fcc742.png)

## **사용자가 웹사이트 정보를 받아오는 과정**

**1. `웹사이트` 의 url을 주소창에 직접적으로 입력하거나 또는 간접적으로 입력하는 방식을 따른다.**

**2. `웹 브라우저`가 url을 읽고 해당 `웹 서버`에 가서 request를 한다.**

**3. request를 받은 `웹 서버`는 `웹 브라우저`가 필요한 정보를 주어 response를 한다.**

[www.naver.com](http://www.naver.com) → 202.179.177.22 

[localhost](http://localhost) → 127.0.0.1 

---

[**Ref**](https://namu.wiki/w/%EC%95%84%ED%8C%8C%EC%B9%98%20%EC%86%8C%ED%94%84%ED%8A%B8%EC%9B%A8%EC%96%B4%20%EC%9E%AC%EB%8B%A8)

[https://velog.io/@kdhyo/Apache-Tomcat-둘이-무슨-차이지](https://velog.io/@kdhyo/Apache-Tomcat-%EB%91%98%EC%9D%B4-%EB%AC%B4%EC%8A%A8-%EC%B0%A8%EC%9D%B4%EC%A7%80)

[https://namu.wiki/w/아파치 소프트웨어 재단](https://namu.wiki/w/%EC%95%84%ED%8C%8C%EC%B9%98%20%EC%86%8C%ED%94%84%ED%8A%B8%EC%9B%A8%EC%96%B4%20%EC%9E%AC%EB%8B%A8)
