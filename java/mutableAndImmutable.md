
<div align="center">
  <br />
  <h1>Mutable 객체와 Immutable 객체의 차이점에 대해 설명해주세요</h1>
  <br />
</div>

## 목차

1. [**Immutable 객체**](#1)
2. [**Mutalbe 객체**](#2)


<br />

<div id="1"></div>

## Immutalble Object(불변 객체)

# Immutable Object란?

---

> 객체 지향 프로그래밍에 있어서 불변객체(immutable object)는 생성 후 그 상태를 바꿀 수 없는 객체를 말한다. 반대 개념으로는 가변(mutable) 객체로 생성 후에도 상태를 변경할 수 있다. 객체 전체가 불변인 것도 있고, C++에서 const 데이터 멤버를 사용하는 경우와 같이 일부 속성만 불변인 것도 있다. 또, 경우에 따라서는 내부에서 사용하는 속성이 변화해도 외부에서 그 객체의 상태가 변하지 않은 것 처럼 보인다면 불변 객체로 보기도 한다. 예를 들어, 비용이 큰 계산의 결과를 캐시하기 위해 메모이제이션(Memoization)을 이용하더라도 그 객체는 여전히 불변하다고 볼 수있다. 불변 객체의 초기 상태는 대개 생성 시에 결정되지만 객체가 실제로 사용되는 순간까지 늦추기도 한다.불변 객체를 사용하면 복제나 비교를 위한 조작을 단순화 할 수 있고, 성능 개선에도 도움을 준다. 하지만 객체가 변경 가능한 데이터를 많이 가지고 있는 경우엔 불변이 오히려 부적절한 경우가 있다. 이 때문에 많은 프로그래밍 언어에서는 불변이나 가변 중 하나를 선택할 수 있도록 하고 있다.-위키백과
> 

제가 공부한 바로 불변 객체를 한마디로 표현하자면 다음과 같습니다.

> 불변객체는 재할당은 가능하지만, 한번 할당하면 내부 데이터를 변경할 수 없는 객체
> 

즉, 객체에 값을 할당하면 내부 데이터를 변경시킬 수 없다는 것입니다. 대표적인 예로 String, Integer, Boolean 등이 있습니다.String은 `String str="a"`, `str="ab"` 이런 식으로 사용하기 때문에 값이 변경한다고 생각하여 불변객체가 아닌 것으로 착각하기 쉽습니다.하지만 이것은 str가 처음에 참조하고 있는 "a"값이 "b"로 변경되는 것이 아니라 "b"라는 새로운 객체를 만들고 그 객체를 str이 참조하게 하는 것입니다.

아래 코드는 불변이 아닌 클래스입니다.

```java
class MutablePerson {
   public int age;
   public int name;

   public MutablePerson(int age, int name) {
    	this.age = age;
        this.name = name;
    }
}
```

그 이유는 외부에서 age나 name을 **변경할 수 있기 때문**입니다.그럼 이 클래스를 불변 클래스로 만들어보겠습니다.

```java
class ImmutablePerson {
    private final int age;
    private final int name;

    public ImmutablePerson(int age, int name) {
    	this.age = age;
        this.name = name;
    }
}
```

위와 같이 만들면 외부에서 **값을 수정할 수 없습니다. 따라서 불변객체가 됩니다.**(final 변수이므로 당연히 Setter 메서드를 작성할 수 없습니다)일반 객체들을 불변객체로 만드는 방법들은 뒤에 추가적으로 보여드리겠습니다.

# Immutable Object의 장단점

**장점**

- 객체에 대한 신뢰도가 높아집니다. 객체가 한번 생성되어서 그게 변하지 않는다면 transaction 내에서 그 객체가 변하지 않기에 우리가 믿고 쓸 수 있기 때문입니다.
- 생성자, 접근메소드에 대한 방어 복사가 필요없습니다.
- 멀티스레드 환경에서 동기화 처리없이 객체를 공유할 수 있습니다.

**단점**

- 객체가 가지는 값마다 새로운 객체가 필요합니다. 따라서 메모리 누수와 새로운 객체를 계속 생성해야하기 때문에 성능저하를 발생시킬 수 있습니다.

# Immutable Object 만들어보기

---

Immutable Object를 만드는 기본적인 아이디어는 필드에 `final`을 사용하고, `Setter`를 구현하지 않는 것입니다.이 아이디어는 불변객체의 필드가 모두 원시 타입일 경우에만 가능하고, 참조 타입일 경우엔 추가적인 작업이 필요합니다.

이제 필드가 원시 타입만 있는 객체와 참조 타입이 있는 객체를 불변객체로 만들어봅시다.

## 원시 타입만 있는 경우

**➡️ 변경 전**

```java
public class BaseObject {

    private int value;

    public BaseObject(final int value) {
        this.value = value;
    }

    public void setValue(int newValue) {
    	this.value = newValue;
    }

    // getter는 생략 했음
}
```

위 객체는 **불변객체가 아닙니다**. 앞서 설명드렸지만, 외부에서 Setter를 통해 int형 필드 value의 값을 변경할 수 있기 때문입니다.

필드가 원시 타입만 있으므로 이는 **`final` 키워드를 사용해서 불변객체로 만들 수 있습니다.**

**➡️ 변경 후**

```java
public class BaseObject {

    private final int value;

    public BaseObject(final int value) {
        this.value = value;
    }

    // getter는 생략 했음
}
```

필드에 `final` 키워드를 사용했으므로 Setter를 구현하는 것은 당연히 불가능합니다.따라서 이 객체의 value를 변경하려면 재할당하는 방법밖에 없습니다.

## 참조 타입이 있는 경우

참조 타입이 있는 경우의 대부분은 **final을 사용하고, Setter를 작성하지 않는 것으로는 불변객체를 만들 수 없습니다.**아래의 예를 보겠습니다.

```java
public class Animal {

    private final Age age;

    public Animal(final Age age) {
        this.age = age;
    }

    public Age getAge() {
    	return age;
    }
}

class Age {

    private int value;

    public Age(final int value) {
        this.value = value;
    }

    public void setValue(final int value) {
        this.value = value;
    }

    public int getValue() {
    	return value;
    }
}
```

Animal 클래스는 final을 사용하고, Setter를 구현하지 않았지만 불변객체가 될 수 없습니다. 왜냐하면 Animal 클래스의 필드인 Age의 값을 아래처럼 변경할 수 있기 때문입니다.

```java
public static void main(String[] args) {
    Age age = new Age(1);
    Animal animal = new Animal(age);

    System.out.println(animal.getAge().getValue());
    // Output: 1

    animal.getAge().setValue(10);
    System.out.println(animal.getAge().getValue());
    // Output: 10
}
```

즉, **불변 객체의 참조 변수 또한 불변이어야 합니다**.필드에 참조 타입이 있는 경우는 여러가지 상황이 있을 수 있습니다. 대표적으로 (1)객체를 참조할 수도 있고, (2)Array나 (3)List 등을 참조할 수 있습니다.이 세가지 상황에 대해 불변 객체를 만들어보겠습니다.

### (1) 참조 변수가 일반 객체인 경우

이 상황은 위의 예제를 고쳐보면 될 것입니다.따라서 이는 참조 변수인 Age도 불변객체로 만들어 해결할 수 있습니다.

```java
public class Animal {

    private final Age age;

    public Animal(final Age age) {
        this.age = age;
    }

    // getter
}

class Age {

    private final int value;

    public Age(final int value) {
        this.value = value;
    }

    // getter
}
```

이 상황을 보면 결국 **"참조 변수도 불변 객체이어야 한다"**라는 결론이 나옵니다.

### (2) Array일 경우

```java
public class ArrayObject {

    private final int[] array;

    public ArrayObject(final int[] array) {
        this.array = Arrays.copyOf(array,array.length);
    }

    public int[] getArray() {
        return (array == null) ? null : array.clone();
    }
}
```

배열일 경우에는 생성자에서 **배열을 받아 copy해서 저장하도록** 했고,getter를 **clone을 반환하도록** 하면 됩니다.배열을 **그대로 참조하거나, 그대로 반환할 경우 외부에서 배열 내부값을 변경시킬 수 있기 때문에, clone을 반환하게 되면 외부에서 값을 변경시킬 수 없습니다.**만약 **원시 타입 배열이 아니고, `Animal[]`과 같은 형태라면 해당 객체는 불변객체이어야 합니다.**

```java
public static void main(String[] args) {
	int[] array = {1, 2, 3};
  
	ArrayObject arrayObject = new ArrayObject(array);

     for (int num : arrayObject.getArray()) {
            System.out.print(num + " ");
     }
     // 결과: 1 2 3

     System.out.println();
     array[0] = 999; // arrayObject의 배열 값은 변하지 않는다.

     for (int num : arrayObject.getArray()) {
         System.out.print(num + " ");
     }
     // 결과: 1 2 3
}
```

### (3) List인 경우

List인 경우에도 Array와 마찬가지로 **생성시 생성자 인자를 그대로 참조하지 않고, 새로운 List를 만들어 값을 복사하도록 해야합니다.** 그리고 **getter를 통해 값 추가/삭제가 불가능하도록 Collection의 unmodifiableList 메서드를 사용했습니다.**

여기서 `Animal`은 앞서 만든 불변객체입니다.

```java
import java.util.Collections;
import java.util.List;

public class ListObject {

    private final List<Animal> animals;

    public ListObject(final List<Animal> animals) {
        this.animals = new ArrayList<>(animals);
    }

    public List<Animal> getAnimals() {
        return Collections.unmodifiableList(animals);
    }
}
```

**결과**

```java
public static void main(String[] args) {
    List<Animal> animals = new ArrayList<>();
    animals.add(new Animal(new Age(1)));

    ListObject listObject = new ListObject(animals);

    for (Animal animal : listObject.getAnimals()) {
        System.out.print(animal.getAge().getValue());
    }
    System.out.println();
    // Output: 1

    animals.add(new Animal(new Age(2))); // List인 animals에는 추가되지만 listObject의 List에는 추가되지 않는다

    for (Animal animal : listObject.getAnimals()) {
        System.out.print(animal.getAge().getValue());
    }
    System.out.println();
    // Output: 1
}

```

# 결론

- 불변객체는 한번 할당하면 필드 값을 변경할 수 없는 객체입니다.
- 하지만 재할당은 가능합니다.
- 필드가 원시 타입일 경우엔 **final** 사용으로 불변객체를 만들 수 있고, 참조 타입일 경우엔 추가적인 작업이 필요합니다.

<br />

<div id="2"></div>

## Muttable Object(가변 객체)

### Mutable이란?

Java에서는 **가변(mutable)성**을 가지는 **StringBuffer** / **StringBuilder** 클래스를 도입했습니다.

String 과는 반대로 StringBuffer/StringBuilder 는 가변성 가지기 때문에 .append() .delete() 등의 API를 이용하여 **동일 객체내에서 문자열을 변경**하는 것이 가능합니다. 따라서 **문자열의 추가,수정,삭제가 빈번하게 발생할 경우**라면 String 클래스가 아닌 **StringBuffer/StringBuilder를 사용**하셔야 합니다.

`StringBuffer sb= new StringBuffer("hello");
sb.append(" world");`

[https://t1.daumcdn.net/cfile/tistory/9923A9505E2F133608](https://t1.daumcdn.net/cfile/tistory/9923A9505E2F133608)

****| StringBuffer  vs  StringBuilder**

그렇다면 동일한 API를 가지고 있는 **StringBuffer, StringBuilder의 차이점**은 무엇일까요?

가장 큰 차이점은 **동기화의 유무**로써 **StringBuffer**는 동기화 키워드를 지원하여 **멀티쓰레드 환경에서 안전하다는 점(thread-safe)** 입니다.  참고로 **String**도 ****불변성을 가지기때문에 마찬가지로  **멀티쓰레드 환경에서의 안정성(thread-safe)**을 가지고 있습니다.

반대로 **StringBuilder**는 **동기화를 지원하지 않기**때문에 멀티쓰레드 환경에서 사용하는 것은 적합하지 않지만 동기화를 고려하지 않는 만큼 **단일쓰레드에서의 성능은 StringBuffer 보다 뛰어납니다**.

출처:

[https://ifuwanna.tistory.com/221](https://ifuwanna.tistory.com/221)

<br />


