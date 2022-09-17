> java.lang.System 클래스는 자바 프로그래밍을 할 때 정말 자주 사용하는 클래스입니다.System 클래스의 모든 것을 정리해 볼 수는 없지만,
> 
> - 클래스 변수 `in`, `out`, `err`
> - 환경 변수를 찾는 방법
> - 배열 복사 방법
> - 그 외 알아둘 특징
> 
> 정도를 한번 정리해보고 싶습니다!
> 

## System 클래스

- `실행시간` 환경과 관련된 속성과 메서드를 제공
- 모든 필드와 메서드는 `static`으로 구성
- 대표적인 기능
    - 표준 입출력
    - *환경 변수 읽기 : 운영체제에 설정되어 있는 환경 변수를 읽어옴*
    - 시스템 프로퍼티 읽기 : 프로그램의 환경 모드를 프로퍼티 형태로 읽고 쓰는 기능
    - 현재 시각 측정 : 시스템 시계로부터 현재 시각을 읽어오는 기능
    - 프로그램 실행 관련 기능 : 프로그램을 끝내는 기능과 가비지 컬렉터 관련 기능
    - 보안 설정 기능 : 자바 프로그램의 보안 관리자 설정 기능
    - 그 밖의 유용한 기능 : *배열을 효율적으로 복사하는 기능*

![image](https://user-images.githubusercontent.com/92802207/190862302-d3824445-9646-448d-9b67-586a41cc57de.png)

## System 변수? (클래스 변수)

`final static InputStream` `in` : 표준 입력에 사용된다.

`final static PrintStream` `out` : 표준 출력에 사용된다. print(), println() 매개변수를 받아 모니터에 출력을 수행한다.

`final static PrintStream` `err` : 에러 출력에 사용된다. print(), println() 매개변수를 받아 모니터에 에러 출력을 수행한다.

## System 클래스의 주요 메서드

- static void arraycopy(Object src, int srcPos, Object dest, int destPos, int length)
    - 배열을 복사한다. src와 dest은 복사될 배열의 변수이고, srcPos와 destPos는 복사가 시작될 위치이고, length는 복사될 배열의 크기이다.
- static long currentTimeMillis()
    - 1970년 1월 1일 자정부터 현재까지의 시간을 밀리초로 반환한다.
- static void exit(int status)
    - 현재 수행적인 응용 프로그래을 종료시킨다. status로 종료 상태를 반환한다. 보통 마이너스(-)는 비정상 종료를 뜻한다.
- static void gc()
    - 가비지 콜렉션(garbage collection)을 실행시킨다.
- static String getPropertys()
    - 시스템 환경 변수 목록을 얻어온다.
- static String getProperty(String key)
    - 시스템 환경 변수를 얻어온다.
- static String getProperty(String key, String def)
    - 프로그램 환경 변수를 설정한다.

## 덧붙일 말

강의 PPT에서는 환경 변수를 찾는 방법, 배열 복사 방법 등이 꽤 중요한 듯이 적혀있었으나, 정리하며 이것 저것 찾아 보니 크게 중요한 부분이 아니라고 생각된다.
