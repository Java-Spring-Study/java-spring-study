# Stream & Lambda !!

java 8의 주요 변경 사항 중 하나!!

**람다식 표현**과 **스트림**으로 인하여 객체지향 언어인 java에 함수형 프로그래밍이 더욱 자연스럽게 가능하다.

함수형 프로그래밍의 참조의 투명성으로 프로그램이 더욱 직관적이게 되었다.



## <span style="color:blue">0. 람다식</span>

메서드를 하나의 식으로 표현 한 것.

java에서는 모든 메서드는 클래스에 포함되어야 하므로 클래스도 새로 만들어야하고, 

객체도 생성해야만 비로소 이 메서드를 호출 할 수 있다. 

그러나 람다식은 이 모든 과정 없이 오직 람다식 자체만으로도 이 메서드의 역할을 대신할 수 있다.



### 0.1 람다식의 특징

1.  람다식은 메서드의 **매개변수로 전달 되어지는 것이 가능**하고, **메서드의 결과값으로 반환**되어지는 것 또한 가능하다.

   즉, 메서드를 변수처럼 사용이 가능해 진 것이다.



### 0.2 람다식 문법

````java
반환 타입 메서드이름(매개변수 선언){		//일반적인 메서드 표현
    구현부
}

(매개변수 선언) -> { 구현부 }				//람다식으로 표현
````



**예시**

< 일반적인 메서드 표현 >

```java
int max(int a, int b){
    return a > b ? a : b; 
}
```

 

< 람다식 표현 >

```java
(a, b) -> a > b ? a : b
```

🔅조금 더 상세한 문법이 있지만 이는 직접 사용을 하며 익히자! (다른 문서의 도움을...)



### 0.3 람다식의 숨겨진 진실

>  (타입) f = (a, b) -> a >  b ? a : b

위 처럼 람다식을 다른 변수에 할당하게 되면 **변수 f**는 **참조변수 타입**으로 정의 되어야 할 것이다.

그렇다면 그 <u>참조 변수 타입은 무엇일까 ?</u>



정답은 ?

람다식을 위한 `함수형 인터페이스`이다. 

함수형 인터페이스는 오직 하나의 추상 메서드만 정의되어 있어야 한다는 제약이 있다.  그래야 람다식과 인터페이스의 메서드가 1:1 로 연결이 가능하기 때문이다.



예시

```java
interface MyFunction{
    public abstract max(int a, int b);
}

Myfunction f = new Myfunction(){
    public int max(int a, int b){
        return a > b ? a : b;
    }
};

int big = f.max(5, 6); // 익명 객체의 메서드를 호출 !!   
```

````java
@FunctionalIterface
interface MyFunction{
    public abstract max(int a, int b);
}

Myfunction f = (int a, int b) -> a > b ? a : b; //익명 객체를 람다식으로 대체
````

하나의 메서드가 선언된 인터페이스 (함수형 인터페이스)를 정의해서 람다식을 다루는 것이 기존의 자바 규칙들을 어기지 않으면서도 자연스럽다.



### 0.4 람다식의 더 간결한 표현 : 메서드 참조

메서드 참조가 탄생 나왔을까 ? 

( 주의, 개인적인 생각이 곁들여졌습니다 ) 

 함수를 매개변수로써 사용하고 싶다 ?! 👉 람다식을 이용해 겠음 👉 근데 사용하고 싶은 그 함수가 이미 잘 구현되어 있음.

👉 그렇다면 그걸 쓰면 ? 람다식이 wrapper역할만 수행함 👉 조금더 간결하게 만들어보자. wrapper 벗겨! 👉 메서드 참조 탄생



**예시**

```java
(String s) -> Integer.parseInt(s);	//람다식은 그냥 다른 함수를 호출해주는 역할만 하고 있음. 의미없는 겉포장지 느낌 ?

Integer::parseInt;					//메소드 참조
```

위의 예시 둘다 같은 인터페이스를 반환한다.



**상세한 문법**

| 종류                           | 람다식                     | 메서드참조        |
| :----------------------------- | :------------------------- | :---------------- |
| static 메서드 참조             | (x) -> ClassName.method(x) | ClassName::method |
| instance 메서드 참조           | (obj, x) -> obj.method(x)  | ClassName::method |
| 특정 객체 instance 메서드 참조 | (x) -> obj.method(x)       | obj::method(x)    |
| 생성자 메서드 참조             | ( ) -> new ClassName( )    | ClassName::new    |



## <span style="color:blue">1. 스트림</span>

1. 스트림 소스 대상 → **배열, 컬렉션, 임의의 수**
2. 스트림이 소스를 제작해서 사용하는 방법 



### 1.1 컬렉션 to 스트림

컬렉션의 최고 조상인 Collection에는 stream( )이 정의 되어 있다.

>  Stream<T> Collection.stream( )

```java
//예시 
List<Integer> list = Arrays.asList(1,2,3,4,5);
Stream<Integer> intStream = list.stream( );

intStream.forEach(System.out::println); //스트림의 모든 요소를 출력.
intStream.forEach(System.out::println); //에러, 스트림이 이미 닫힘.
```

🔅 스트림 요소를 한번더 출력하려면 스트림을 새로 생성해야한다. 



### 1.2 배열 to 스트림

배열을 소스로하는 스트림을 생성하는 메서드는**Stream**과 **Arrays**에 static 메서드로 정의되어 있다.

```java
//예시
//문자열 스트림
Stream<String> strStream = Stream.of("A", "B", "C");
Stream<String> strStream = Stream.of(new String[]{"A", "B", "C"});
Stream<String> strStream = Array.stream(new String[]{"A", "B", "C"});
Stream<String> strStream = Array.stream(new String[]{"A", "B", "C"},0, 3);
```

```java
//예시
//int, long, double과 같은 기본형 배열을 소스로 하는 스트림을 생성하는 메서도 있음.
IntStream IntStream.of(int...values)
IntStream IntStream.of(int[])
IntStream Arrays.stream(int[])
IntStream Arrays.stream(int[] array, int startInclusive, int endExclusive)
```

IntStream과 LonStream은 지정된 범위의 연속된 정수를 스트림을 생성해서 반환하는 range( )와 rangeClosed( )를 가지고 있다.

```java
IntStream intStream = IntStream.range(1,5); //결과, 1,2,3,4
IntStream intStream = IntStream.rangeClosed(1,5); //결과, 1,2,3,4,5
```



### 1.3 임의의 수 to 스트림

Random 클래스에는 `Random::ints( )`, `Random::longs( )`, `Random::doubles( )` 가 포함되어있다.

**무한 스트림**

```java
IntStream intstream = new Random().ints(); //무한 스트림 생성

intstream.limit(5).forEach(System.out::println); // 5개의 요소만 출력
```

 ⇒ `limit()` 를 이용하면 무한스트림의 크기를 제한 할 수 있음.

**유한 스트림** 

```java
//ints(long StreamSize, int begin(<=), int end(>=))
IntStream intstream = new Random().ints(5, 0, 10)

intstream.forEach(System.out::println);       //1부터 10까지의랜덤 정수 5개 출력.
```



### 1.4 스트림이이 직접 소스 제작!!

Stream클래스의 **iterate( )**와 **generate( )**는 람다식을 매개변수로 받아서, 무한 스트림을 만들어준다.

위에서 **임의의 수** 파트 처럼 Stream클래스에서 자체적으로 조건에 맞는 스트림을 직접 제작해준다.



>  Stream<T> iterate( T seed, UnaryOperator<T> f )

```java
Stream<Integer> evenStream = Stream.iterate(0, n->n+2); // 0부터 2씩 증가하는 정수들 생성.
```



>  Stream<T> generate( Supplier<T> s )

```java
Stream<Double> randomStream = Stream.generate(Math::Random); //랜덤 실수 생성.
```



**🔅iterate( )와 generate( )의 차이:**

 둘다 람다식 계산 결과에 따른 무한 스트림을 생성하지만, 

iterate는 seed값을 시작으로 이전 결과를 이용해서 다음 결과를 계속 계산해나간다.

generate는 람다식에 매개변수가 없는 람다식만 허용된다. 

---



## <span style="color:blue">2. 스트림 연산자</span>

<span style='background-color:#fff5b1'>        </span> : **중간연산 ( Intermediate Operation )**

<span style='background-color:#dcffe4'>        </span> : **최종 연산 ( Terminal Operation )**



stream( )<span style='background-color:#fff5b1'>.filter( v -> v > 0)</span>

​				<span style='background-color:#fff5b1'>.map( v -> v * 2)</span>

​				<span style='background-color:#dcffe4'>.forEach( v -> System.out.println(v))</span>



### 2.1 중간 연산 종류( Intermediate Operation )

생성된 스트림은 `.` 을 이용한 메서드 호출로 연산이 가능하다. 

연산의 결과값을 다시 스트림으로 리턴한다. 

파이프라인처럼 쭉 쭉 이어 나가는 것이 가능하다. (메서드 체이닝, Pipelining)

| 중간 연산<br />(Intermediate Operation) | 반환 값<br />(Return Type) | 인자<br />(Argument) | 람다식을 이용한<br /> 예시 |
| --- | --- | --- | --- |
| .fiter( ) | Stream<T> | Predicate<T> | stream( ).filter( v→  v > 10) |
| .map( ) | Stream<T> | Function<T, R> | stream( ).map( v → v*2) |
| .limit( ) | Stream<T> | Integer | stream( ).limit( 5 ) |
| .sorted( ) | Stream<T> | Comparator<T> | stream( ).sorted( Comparator.comparing(String::length) ) |
| .distinct( ) | Stream<T> |  | stream( ).distinct( ) |
| 등등.. |  |  |  |

연산자이름으로 부터 충분히 역할 유추가 가능하므로 설명 생략.



### 2.2 **최종** 연산 종류( Terminal Operation )

스트림 파이프라인으로 부터 최종 결과를 만든다. 즉, 결과값이 스트림이 아니다.

| 중간 연산<br />(Intermediate Operation) | 반환 값<br />(Type) | 인자<br />(Argument) | 람다식을 이용한<br />예시 |
| --- | --- | --- | --- |
| .forEach( ) | void | Consumer<? super T> | stream( ).forEach(System.out::println) |
| .count( ) | Long |  | stream( ).count( ) |
| .reduce( ) | Optional<T> | BinaryOperator<T> | stream( ).( (a, b) → a > b ? a : b ) |
| .reduce( ) | T | T, BinaryOperator<T> | stream( ).( 0, (a, b) → a > b ? a : b )  // 0부터 비교 시작 |
| .collect( ) | <R, A>  | Collector<? super T, A, R> | stream( ).collect( Collectors.toList( ) ) |
| 등등.. |  |  |  |



🔅**스트림 연산 유의점 !!**

- stream에 올라간 data들의 타입이 **사용자 정의된 타입**(클래스 객체들)일 때,
  
    몇몇 스트림 연산자를 사용하기 위해선 스트림 연산자 내부 함수의 오버라이드가 필요하다. 
    
    

🔅**스트림 연산 익힐 때 !!**

- 스트림 연산자는 `.reduce( )` 와 같이 오버로딩 되어 있는 경우도 많아서, 이를 다 정리해서 공부하기보단, 필요에 따라 [공식문서]([https://docs.oracle.com/javase/8/docs/api/java/util/stream/Stream.html](https://docs.oracle.com/javase/8/docs/api/java/util/stream/Stream.html))를 보면서 사용할 줄 아는 것이 더 중요해 보인다.
- 매개변수와 리턴 값이 인터페이스로 되어 있어서 다양한 **함수형 인터페이스** 의 요구사항을 볼 줄 알아야 한다.

---



**[ 참고 ]**

자바의 정석2