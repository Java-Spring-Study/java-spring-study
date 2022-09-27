```java
class A{
	A() {
		f();
	}
	public void f() {
		System.out.println("A::f()");
	}
}

class B extends A{
	int a = 2;
	public void f() {
		System.out.println("B::f()");
		System.out.println(a);
	}
}

public class Main {
	public static void main(String[] args) {
		A obj = new B();
	}
}
```
>출력
>
>B::f()
>
>0

왜 이런 일이 발생하는 걸까요?

A생성자에서 호출한 f는, 상속에 의해 B::f 로 변경되었고, B::a의 초기화는 A의 생성자 호출 이후에 발생하기 때문입니다.

C++에서는 약간 다릅니다.

```cpp
#include <iostream>

using std::cout;

class A{
public:
	A() {
		f();
	}
	virtual void f() {
		cout << "A::f()\n";
	}
};

class B: public A{
	int a = 2;
public:
	virtual void f() {
		cout << "B::f()\n";
		cout << a << "\n";
	}
};

int main()
{
	A* obj = new B;
	delete a;
}
```
> 위의 java소스와 동일합니다.
>
> 출력
>
> A::f()

C++의 경우 B의 생성 이전에는 가상화되었더라도 호출하지 못합니다.
C++의 상속 모델은 부모 객체 생성 후에 자식 객체로 부모 객체를 넘겨 껍질을 감싸는 형태로 진행되기 때문입니다.
그럼 장단점을 알아봅시다.

C++:
- 타입 안정성
  - 생성자를 통해 항상 자원이 초기화됨이 보장됩니다. 예를 들어, 자바 소스에서 B::a가 Database의 커넥션일 경우,
    메소드들은 해당 객체가 살아있는 동안에는 별다른 검사 없이 커넥션 객체가 존재한다고 assert할 수 있습니다.
    만약 java의 방식을 따른다면, 메소드는 생성자 호출을 가정할 수 없습니다.
    또, 불변 클래스의 경우에도 getter가 다른 값을 반환할 수 있어 사실상 불변성을 보장하기도 어렵습니다.

Java:
- 초기화 전파
  - 사실 장점이라고 보기엔 단점이 너무나 큰 설계로 보이지만, 어쨌든 상위 클래스에서 하위 클래스에 대한 초기화를 수행할 수 있습니다.

이처럼 생성자에서 non-static method를 호출하는건 주의해야합니다.
