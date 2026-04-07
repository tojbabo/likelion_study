# DAY 9.
---
## 추상클래스와 인터페이스
### 추상클래스
*public abstract class 클래스명*

class  < concrete 클래스
abstract class < abstract 클래스(추상클래스)

> 일반 클래스는 method 동작이 구현되어 있는 상태 - 고정되어있음
> *어떤 기능처리를 할지 구체화되어 있는 상태, 완성된 클래스*

> 추상클래스틑 method 동작이 아직 미정인 상태 - 동적으로 변경될 수 있다
> **
>
> public abstract [return type] [function name] (parameter);  <이런식으로 선언만 되어있다. 함수 내부 구현이 없음.
>

특징
* new가 없다! 인스턴스 생성이 안된다 >> 미완성 클래스로 완성 클래스로 만든후에 사용이 가능하다
* 완성된 클래스 : 상속 + 오버라이딩 method를 이용해서 구현
* 추상 클래스를 상속하는 경우 추상메서드는 **반드시** 구현 해야한다

왜 필요하냐느냐? 추상 메서드는 반드시 구현해야하기 때문에 해당 함수 구현을 강제할 수 있다

### 인터페이스
*public interface 인터페이스명{}*

상수, 추상메서드, default 메서드, static 메서드를 가질 수 있다

* int num= 20;으로 멤버 변수 생성시 자동으로 static final로 지정된다(상수처리)
* void func();로 메서드 생성시 자동으로 abstract 셋팅됨 
* default void func(){} 로 기능을 구체화 할 수 있다. concrete 메서드 처럼 동작. *new 이후에 사용 가능*
* static void func(){}로 new 없이 동작이 가능한 static 메서드

> 불완전한 객체로 직접 new가 불가하다
> implements + 오버라이딩 메서드를 통해 
>
> 추상메서드 - concrete 클래스는 상속관계 : 실선화살표
> 인터페이스 - concrete 클래스는 구현관계 : 점선화살표
>
> 인터페이스의 추상메서드도 **반드시** 재정의해야함
>
> 상속관계에 비해 구현관계는 여러개를 가능하다 
>
> public class A extends B implements C, D{
> }
> 



