# Java 8에서 추가된 기능

## 1. Lambda 표현식

- Lambda(람다) 익명함수로 이름과 식별자가 없는 함수를 말한다. 람다를 사용하면 코드를 간결하게 작성이 가능하다
- -> 화살표를 쓰는 코드를 본적이 있다면 이것이 람다식을 쓴 코드라고 할 수 있다

```java
// 일반적인 람다식 구문 
(parameters) -> expression
//예제
(x, y) -> x +y
```

### 람다 표현식 작성 규칙

1. 람다 식에는 매개변수가 0 개, 1개 이상 있을 수 있음 (매개변수 없어도 됨)
    
    ```java
    ( ) -> expression
    ```
    
2. 매개 변수가 여러개이면 괄호로 묶고, 쉼표로 구분
    
    ```java
    ( param1, param2, param3, param4 ) -> expression
    ```
    
3. 매개 변수가 1개인 경우 괄호를 반드시 쓰지 않아도 됨
    
    ```java
    x -> x + x
    ```
    
4. 람다 식의 본문이 단일 문인 경우 중괄호는 필수가 아니지만, 둘 이상의 명령문이 있는 경우 중괄호를 사용해야 함

## 2. Optional

- Optional을 사용하면 NullPointException을 걱정하지 않아도 된다.
- 기존에 null을 체크하기 위해서 if 문을 많이 사용했지만 Opitonal을 사용하면 Null을 핸들링 할 수 있게 된다.
- 옵셔널은 null이나 null이 아닌 값을 담을 수 있는 클래스이다.
- 옵셔널을 사용하면 DB를 조회하고 null인 경우 orElseThrow 메소드를 사용하여 에러를 던지거나 ifpresent 메소드로 분기처리를 하는 등 null 처리를 세련되게 할 수 있게 된다.

```java
//일반 null 처리
String str = "name";

if (str != null) {
	System.out.println("name : " + str);
}

// Optional 처리 
String str2 = "name";

Optional<String> opt = Optional.ofNullable(str);
opt.ifPresent(s -> System.out.println("name : " + str));
```

## 3. Stream API

- 필터링, 변환 등 다양한 방식으로 배열이나 컬렉션 (List, Map 등) 을 반복적으로 처리하는 스트림 API 추가되었다.
- 컬렉션을 다루기 위한 API로 컬렉션의 요소를 람다식으로 처리하여 복잡한 구조의 데이터 처리를 간단하게 해주어 코드의 복잡도를 낮출 수 있다.
- 기존에 for 문을 돌리면서 처리하던 것을 Stream으로 변환하고, mapping, sorting, filtering 등 을 메서드로 할 수 있게 해준다.
- 스트림 API를 사용하면 기존 코드보다 가독성이 좋게 데이터 처리, 가공이 가능하다.

```java
//자바8 이전 버전
@Test
void test() {
    // java 7
    List<String> nameList = Arrays.asList("apple", "pie", "banana", "cake", "coffee", "latte");
    List<String> aNameList = new ArrayList<>();

    for (String name : nameList) {
        if (name.contains("a")) {
            aNameList.add(name);
        }
    }

    for (String a : aNameList) {
        System.out.println(a);
    }
}

//자바8 이후 
@Test
void test2() {
    // java 8
    List<String> nameList = Arrays.asList("apple", "pie", "banana", "cake", "coffee", "latte");
    nameList.stream() //스트림생성
            .filter(name -> name.contains("a")) //중개연산, 리턴값이 없다
            .forEach(a -> System.out.println(a));//주어진 객체에서 루프를 돌면서 명령을 수행한다
}
```

## 4. Default Method

- 원래 interface를 구현하는 클래스에서는 interface에 있는 메소드를 모두 구현하여야 컴파일 오류가 발생하지 않는다.
- 이와는 다르게 default를 사용하여 interface에 선언한 메소드는 필수가 아닌 선택적으로 구현여부를 정할 수 있다.
- 이렇게 만든 이유는 과거에 만든 소스가 많은 개발자들에게 사용되는 상황에서 기존의 interface에 새로운 메소드를 추가해야하는 상황이발생했기 때문이다. 기능 추가는 가능하되 컴파일 에러를 피할 수 있다.

## 5. 함수형 인터페이스

- 함수형 인터페이스는 SAM Interface (Single Abstract Method Interface) 라고도 한다.
- 단 1개의 추상 메소드를 가지고 있는 인터페이스를 말하며, @FuntionalInterface 어노테이션을 이용해 만들 수 있다.

```java
@FunctionalInterface
public interface WorkFunctionalInterface {
    public void work();
}
```

## 6. 날짜 관련 클래스 추가

- Date 클래스가 아니라 LocalDate, LocalTime, LocalDateTime 클래스를 사용하게 된다.
- 기존에 직관적이지 않던 date 처리가 자바 8에서 Date, time API 변경으로 직관적으로 변경되었다.
- 날짜 TimeZone 설정, 날짜 계산 등 편리하게 이용 가능해졌다.

```java
LocalDate localDate = LocalDate.now();

System.out.println(localDate.toString());                // 2021-05-12
System.out.println(localDate.getDayOfWeek().toString()); // WEDNESDAY
System.out.println(localDate.getDayOfMonth());           // 12
System.out.println(localDate.plusDays(12).toString());   // 2021-05-24
```

## 7. **Method Reference**

- static 메소드 참조( 클래스 내에 선언된 static 메소드를 참조할 수 있다. 클래스명::메소드명)
- 특정 객체의 인스턴스 메소드 참조 ( System 클래스의 out에 저장된 printStream의 객체를 참조하여 println()을 호출한다.)
- 특정 유형의 임의의 객체에 대한 인스턴스 메소드 참조
- 생성자 참조
