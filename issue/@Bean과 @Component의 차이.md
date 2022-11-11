## @ Bean ⇒ method 레벨에서 선언
> + Spring의 DI Container에 의해 관리되는 POJO(Plain Old Java Object)
> + 컨테이너에 의해 관리될 객체를 인스턴스화 하고, 구성하고, 초기화 하는 데 사용되는 method를 표시한다.
> + method에 적용하면 해당 method 반환 값 유형의 Bean을 ApplicationContext에 등록한다.
> + 일반적으로, 빈 이름 = method 이름!!
> +  @Bean은 @Component와 함께 사용할 수도 있지만 @Configuration와 빈을 함께 사용하는 게 일반적이다.



## @Configuration
> + class에 적용하면 class 수준 객체를 빈으로 등록
> + class 내부의 @Bean annotation이 적용된 method들 간에 서로 호출하면서 빈들 간의 종속성을 정의할 수 있다.
> + @Configuration class 내에서 @Bean을 사용했을 때만 같은 class 안의 종속성을 주입 받을 수 있다.
> + @Configuration이 적용되면 class 자체, 그리고 @Bean method들이 모두 빈으로 등록된다.



#### @Bean을 수동으로 등록하는 경우
1. 개발자가 직접 제어가 불가능한 라이브러리를 활용할 때
2. 애플리케이션 전 범위적으로 사용되는 class를 등록할 때
3. 다형성을 활용하여 여러 구현체를 등록해주어야 할 때


## @ Component ⇒ class레벨에서 선언
> + 수동으로 직접 빈을 등록하는 작업은 빈으로 등록하는 class가 많아질수록 상당히 많은 시간을 차지 ⇒ @Component이 있는 class들을 찾아서 자동으로 빈 등록!!
> + @Component를 갖는 annotation으로는 @Controller, @Service, @Repository @Configuration등이 있다.
> + Spring에서는 component scan을 통한 빈 등록 방식 권장
