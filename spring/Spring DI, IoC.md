<div align="center">
  <br />
  <h1>Spring DI, IoC</h1>
  <br />
</div>

## 목차

1. [**IoC & DI**](#1)
2. [**DI**](#2)
3. [**IoC**](#3)

<br />

<div id="1"></div>

## IoC & DI

일반적으로 의존성에 대한 제어권은 객체 자기 자신이 갖는다. 아래의 코드는 Sample이라는 클래스에서 Apple 객체를 불러오는 예제이다. 의존관계는 간단히 말해 new라는 키워드를 통해 생성된다.

```java
class Sample{
    private Apple apple = new Apple();
}
```

아래는 SampleTest라는 클래스에서 Apple 객체를 생성한 뒤 Sample 클래스의 생성자로 주입시켜 준다. 여기서는 Sample이 직접 Apple을 생성하는 것이 아니라 생성자로 주입받는다.

```java
class Sample{
    private Apple apple;

    public Sample(Apple apple){
    	this.apple = apple;
    }
}

class SampleTest{

    Apple apple = new Apple();
    Sample sample = new Sample(apple);

}
```

이처럼 첫 번째 예시에서는 Apple 객체의 제어권이 Sample에게 있었다면, 두 번째 예시에서는 Sample에게 있는 것이 아니라 SampleTest에게 있다. 이처럼 의존성을 역전시켜 제어권을 직접 갖지 않는 것을 **IoC**라고 하며, 의존성을 외부에서 주입시켜 주는 것을 **DI**라고 한다.

<br />

<div id="2"></div>

## DI(Dependency Injection)

의존 관계 주입 기능으로 객체를 직접 생성하는 게 아니라 외부에서 생성한 후 주입 시켜주는 방식이다.

DI(의존성 주입)를 통해서 모듈 간의 결합도가 낮아지고 유연성이 높아진다.

![https://media.vlpt.us/images/gillog/post/08489bda-549e-4dae-851b-8ae1734bf85e/21373937580AEF9B37.jpg](https://media.vlpt.us/images/gillog/post/08489bda-549e-4dae-851b-8ae1734bf85e/21373937580AEF9B37.jpg)

첫번째 방법은 A객체가 B와 C객체를 New 생성자를 통해서 직접 생성하는 방법이고,

두번째 방법은 외부에서 생성 된 객체를 setter()를 통해 사용하는 방법이다.

이러한 두번째 방식이 의존성 주입의 예시인데, A 객체에서 B, C객체를 사용(의존)할 때 A 객체에서 직접 생성 하는 것이 아니라 외부(IOC컨테이너)에서 생성된 B, C객체를 조립(주입)시켜 setter 혹은 생성자를 통해 사용하는 방식이다.

![https://media.vlpt.us/images/gillog/post/41f2eb24-fce2-4b7e-b9ac-d5c3ce97d213/22535642580C4AF12C.jpg](https://media.vlpt.us/images/gillog/post/41f2eb24-fce2-4b7e-b9ac-d5c3ce97d213/22535642580C4AF12C.jpg)

스프링에서는 객체를 Bean이라고 부르며, 프로젝트가 실행될때 사용자가 Bean으로 관리하는 객체들의 생성과 소멸에 관련된 작업을 자동적으로 수행해주는데 객체가 생성되는 곳을 스프링에서는 IOC 컨테이너라고 부른다.

<br />

<div id="3"></div>

## IoC(Inversion of Control)

IoC(Inversion of Control)란 "제어의 역전" 이라는 의미로, 말 그대로 메소드나 객체의 호출작업을 개발자가 결정하는 것이 아니라, 외부에서 결정되는 것을 의미한다.

IoC는 제어의 역전이라고 말하며, 간단히 말해 "제어의 흐름을 바꾼다"라고 한다.

객체의 의존성을 역전시켜 객체 간의 결합도를 줄이고 유연한 코드를 작성할 수 있게 하여 가독성 및 코드 중복, 유지 보수를 편하게 할 수 있게 한다.

기존에는 다음과 순서로 객체가 만들어지고 실행되었다.

1. 객체 생성
2. 의존성 객체 생성클래스 내부에서 생성
3. 의존성 객체 메소드 호출

하지만, 스프링에서는 다음과 같은 순서로 객체가 만들어지고 실행된다.

1. 객체 생성
2. 의존성 객체 주입스스로가 만드는것이 아니라 제어권을 스프링에게 위임하여 스프링이 만들어놓은 객체를 주입한다.
3. 의존성 객체 메소드 호출

스프링이 모든 의존성 객체를 스프링이 실행될때 다 만들어주고 필요한곳에 주입시켜줌으로써 Bean들은 싱글턴 패턴의 특징을 가지며,

제어의 흐름을 사용자가 컨트롤 하는 것이 아니라 스프링에게 맡겨 작업을 처리하게 된다.
