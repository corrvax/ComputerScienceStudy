<div align="center">
  <br />
  <h1>JVM 구조와 Java 실행과정</h1>
  <br />
</div>

## 목차

1. [**JVM이란**](#1)
2. [**JVM 특징**](#2)
3. [**JVM 구조**](#3)
4. [**Java 실행과정**](#4)

<br />

<div id="1"></div>

## JVM이란

Java Virtual Machine으로 Java와 OS 사이에서 중간자 역할을 수행한다.

자바 컴파일러(javac)에 의해 소스코드 (.java)로 부터 변환된 자바 바이트코드(. class)를 해당 OS에 맞게 해석해주는 역할을 수행한다.

<img src="https://user-images.githubusercontent.com/56222478/147563265-d7fc4fb6-d270-4121-8aa5-64a609f31332.png" style="width:350px;height:350px"/>

이때, 자바 컴파일러에 의해 생성되는 자바 바이트 코드는 기계어가 아니기때문에 OS에서 바로 해석할 수 없다.

C와 같은 언어 방식은 소스를 컴파일하면 OS에서 바로 실행될 수 있는 실행파일 즉 기계어로 컴파일되어 운영체제가 바뀔때 마다 그에 맞는 실행 가능한 파일을 만들어줘야 한다.

반면에 자바는 JVM이 해석할 수 있는 바이트코드로의 변환 과정을 추가하여, 이러한 불편한 점을 해소했다.

결과적으로 OS에 종속적이지 않고 Java 파일 하나만 만들면 어느 디바이스든 JVM 위에서 실행할 수 있다.

<br />

<div id="2"></div>

## JVM 특징

- 스택 기반의 가상 머신
- 단일 상속 형태의 객체 지향 프로그래밍을 가상 머신 수준에서 구현
- 포인터를 지원하되 C와 같이 주소 값을 임의로 조작이 가능한 포인터 연산이 불가능
- 가비지 컬렉션 사용
- 모든 기본 타입의 정의를 명확히 함으로써 플랫폼 독립성 보장
- 데이터 흐름 분석(Data flow analysis)에 기반한 자바 바이트코드 검증기(Verifier)를 통해 스택 넘침, 명령어 피연산자의 타입 규칙 위반, 필드 접근 규칙 위반, 지역 변수의 초기화 전 사용 등 많은 문제를 실행 전에 검증하여 실행 시 안전을 보장하고 별도의 부담을 줄여줌
- 명령어에서 스택에서 가져올 피연산자의 타입을 명령어에 지정(예: 정수 덧셈은 iadd, 단정도 실수 덧셈은 fadd)

<br />

<div id="3"></div>

## JVM 구조

![image](https://user-images.githubusercontent.com/56222478/147563517-33b5d4e5-28b8-414d-bf72-71bfbcd0c266.png)

### **Class Loader**

JVM내로 class를 로드하고 Link를 통해 적절히 배치하는 일련의 작업을 수행하는 모듈.

Runtime 시에 동적으로 클래스를 로드한다. jar파일 내 저장된 클래스들을 JVM위에 탑재하고 사용하지 않는 클래스들은 메모리에서 삭제한다.

### **Execution Engine**

class loader를 통해 JVM 내의 런타임 데이터 영역에 배치된 바이트 코드는 실행 엔진에 의해 실행, 실행 엔진은 자바 바이트 코드를 명령어 단위로 읽어서 실행. 바이트 코드를 실제로 JVM내부에서 기계가 실행할 수 있는 형태로 변경한다. Interpreter와 JIT 방식이 있다.

- **Interpreter** : 명령어를 하나하나 실행하게 된다. 하나의 메서드가 여러 번 호출될 때마다 매번 새로운 해석이 요구된다는 단점이 있어 느리다.
- **JIT(Just-In-Time) Compiler** : JIT 컴파일러는 Just In Time 컴파일러로 인터프리터 방식의 단점을 보완하기 위해 도입되었다. 실행 시점에 인터프리터 방식으로 기계어 코드를 생성 하면서 그것을 따로 캐싱해둔다. 나중에 동일한 부분이 호출된다면 캐싱해둔 코드를 불러다가 쓴다. 이러한 경우에는 인터프리터 방식보다 빠르다고 볼 수 있다.

### **Garbage Collector**

JVM은 Garbage Collector를 통해 자동화된 메모리 관리 기능을 제공.

Garbage Collection을 수행하는 모듈 쓰레드. Application이 생성한 객체의 생존 여부를 판단해서 더 이상 사용되지 않는 객체를 해제함으로써 메모리 관리가 자동화 되도록 한다.

### **Runtime Data Areas**

JVM이라는 프로그램이 운영체제 위에서 실행되면서 할당받는 메모리 영역. 런타임 데이터 영역은 6개의 영역으로 나뉜다.

<img src="https://user-images.githubusercontent.com/56222478/147563610-2d081443-bd8b-4426-9e02-0ebe3d078fcb.png" style="width:550px;height:650px"/>

**메모리에 load 하고 heap stack 등 메모리 영역을 할당하는 것은 OS. 하지만 어떻게 JVM이 runtime area를 자바 프로그램에게 할당하는지?**

이유는 **OS가 JVM에게 메모리 할당 권한을 주기 때문** 따라서 OS위에서 메모리를 받아 실행되는 다른 프로그램들과 다르게 자바 애플리케이션의 경우 JVM에게 메모리를 할당받아 실행된다. **즉, 자바 애플리케이션은** OS가 아닌 **JVM에 종속적**이라는 뜻.

![https://blog.kakaocdn.net/dn/Pj5z2/btqRjgFHsJw/hWVdVDfuQFNvw31uWxVzzk/img.png](https://blog.kakaocdn.net/dn/Pj5z2/btqRjgFHsJw/hWVdVDfuQFNvw31uWxVzzk/img.png)

java 프로그램을 구동하기 위해는 jre, api, jvm이 포함된 jdk를 설치해야 한다. jdk를 설치할 때는 각자 OS환경에 맞는 것을 선택해야 하는데 이렇게 OS마다 다른 JVM이 제공되기 때문에 별개로 작동하게 된다.

<br />

<div id="4"></div>

## Java 실행과정

![image](https://user-images.githubusercontent.com/56222478/147563701-80d3c956-a22d-4b95-832a-5f4e685c606d.png)

1. 프로그램이 실행되면 JVM은 OS로부터 이 프로그램이 필요로 하는 메모리를 할당받는다.
    
    JVM은 이 메모리를 용도에 따라 여러 영역으로 나누어 관리한다.
    
2. 자바 컴파일러(javac)가 자바 소스코드(.java)를 읽어들여 자바 바이트코드(.class)로 변환시킨다.
3. Class Loader를 통해 class파일들을 JVM으로 로딩한다.
4. 로딩된 class파일들은 Execution engine을 통해 해석된다.
5. 해석된 바이트코드는 Runtime Data Areas 에 배치되어 실질적인 수행이 이루어지게 된다.
    
    이러한 실행과정 속에서 JVM은 필요에 따라 Thread Synchronization과 GC같은 관리작업을 수행한다.
