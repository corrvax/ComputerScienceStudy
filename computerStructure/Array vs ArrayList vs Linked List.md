<div align="center">
  <br />
  <h1>Array vs ArrayList vs Linked List</h1>
  <br />
</div>

## 목차

1. [**Array**](#1)
2. [**ArrayList**](#2)
3. [**Linked List**](#3)

<br />

<div id="1"></div>

## Array
<br />

### **Array란**

**동일한 자료형(Data Type)의 데이터를 연속된 공간에 저장하기 위한 자료구조**이다. 배열은 연관된 데이터들을 하나의 그룹으로 묶어서 효율적으로 데이터들을 관리하기 위해서 사용된다.
배열에 저장되는 데이터는 순차적으로 저장되고 고유한 index 값을 가지고 있다.
하나의 배열을 구성하는 단위 데이터들을 'element', '원소'라고 부른다.

논리적 저장 순서와 물리적 저장 순서가 일치하기때문에 인덱스(index)로 해당 원소(element)에 접근할 수 있다.

### **Array 특징**

1. 삽입(insertion) 순서대로 저장된다. (즉, 새로 삽입되는 요소는 array의 새로운 꼬리가 된다.)
2. 이미 생성된 리스트도 수정 가능하다
3. 동일한 값도 여러번 삽입 가능하다.
4. Array의 요소가 array가 될 수 있다. 이러한 array를 다중차원(multi-dimensional) array라고 합니다. 일반적으로 2D (2차원) array가 많이 사용된다

### **Array 장점**

1. 구현이 쉽다.
2. 인덱스를 이용해 접근이 가능해 검색 성능이 좋다.
3. 데이터의 크기가 확정적일 때 배열을 사용하는 것이 메모리나 처리속도 면에서 좋다.
4. 연속된 메모리 공간에 존재하기 때문에 관리하기가 편하다.

### **Array 단점**

1. 삽입과 삭제가 어렵고 오래 걸린다.
    - 원소를 삽입하거나 삭제할 경우, 다음 항목의 모든 요소를 이동시켜야 한다. (연속된 메모리 공간)
    - 이를 위한 연산작업이 수행되어 비효율적이다.
    - 자료의 수에 비례하여 성능이 떨어지게 된다.
2. 배열의 크기를 바꿀 수 없다.
    - 크게 잡을 경우 메모리가 낭비된다.
    - 작게 잡을 경우 그 이상의 자료를 저장하지 못한다.
3. 메모리의 재사용이 불가능하다.
    - 배열은 초기 사이즈만큼의 메모리를 할당받아 사용하기
    - 데이터의 존재 유무와 관계없이 그 만큼의 메모리를 사용한다.
    - 이미 삭제된 데이터여도 (배열 요소 삭제)
    - 배열 자체를 제거하지 않는 이상 삭제된 공간의 메모리 재사용은 불가능하다.

### Array를 사용하는 경우

1. 순차열적인 데이터를 저장할 때
    - ex) 주식 가격. 어제의 2만원과 오늘의 2만원이 다름 >>> 값보다는 순서가 중요한 데이터
2. 다차원 데이터를 다룰 때
3. 어떠한 특정 요소를 빠르게 읽어야 할 때 (index를 통해 곧바로 읽을 수 있기 때문)
4. 데이터의 사이즈가 급변하게 자주 변하지 않을 때
5. 요소가 자주 삭제 되거나 추가되지 않을 때

### 시간 복잡도

1. 접근
    - 접근은 배열 내에서 n번째 인덱스에 해당하는 값을 찾아내는 연산이다.
    - **배열의 접근은 O(1)의 시간복잡도를 갖는다.** 따라서 찾고자 하는 값이 몇 번째 인덱스에 있는지 알고 있다면 굉장히 빠른 검색 속도를 갖는다. 배열의 첫번째 변수에는 시작 주소값이 저장되고, A[n]의 값을 찾아가기 위해 시작 주소값에서 단순 사칙연산이 수행되기 때문이다.
2. 검색
    - **배열의 검색은 순차검색이다.** 인덱스를 알지 못할 때 원하는 값을 찾기 위해 배열을 하나하나 확인해야한다.
        
        ![https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FebR7Gv%2FbtqUWtaBdb1%2FPsZJhqmDd2BUy8b9OpJfw1%2Fimg.jpg](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FebR7Gv%2FbtqUWtaBdb1%2FPsZJhqmDd2BUy8b9OpJfw1%2Fimg.jpg)
        
    - A[3]의 값을 찾기 위해 A[0], A[1]... 을 순서대로 검색한다. 따라서 최대 O(n)의 시간 복잡도를 가진다.
3. 삽입, 삭제
    - 추가와 삭제는 먼저 빈 공간이 마련되 있다를 전제로 한다.
        
        ![https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FctbBif%2FbtqU0xXor35%2Ftv2mfnmBKKakoWTN1FokYk%2Fimg.jpg](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FctbBif%2FbtqU0xXor35%2Ftv2mfnmBKKakoWTN1FokYk%2Fimg.jpg)
        
    - 추가, 삭제의 시간복잡도는 앞서 말한 접근과 검색의 방법 차이에 따라 시간복잡도가 나뉜다.
    - 배열의 원소를 삭제할 경우, 삭제한 원소보다 큰 인덱스를 값을 갖는 원소들을 1씩 옮겨줘야 하기 때문에 시간 복잡도는 O(n)이다.
    - 배열의 원소를 삽입할 경우, 배열의 크기가 충분할 때는 시간 복잡도는 O(1)이다. 여유 공간이 없을 경우, 확장이 필요하기 때문에 (새로운 원소를 추가하고 인덱스를 1씩 옮겨줘야 함)시간 복잡도는 O(n)이다.



### **Array 사용법**
- **선언**
    
    생성된 배열을 다루기 위한 참조 변수를 위한 공간이 만들어진다.
    
    ```java
    자료형[] 배열이름;
    ```
    
- **생성**
    
    배열을 생성해야 값을 저장할 수 있는 공간이 만들어진다.  배열의 길이는 값을 저장할 수 있는 공간의 개수다.  0을 포함한 양의 정수만 올 수 있다.
    
    ```java
    배열이름 = new 자료형[길이];
    자료형[] 배열이름 = new 자료형[길이];
    ```
    
- **초기화**
    
    ```java
    변수이름[0] = 값;
    변수이름[1] = 값;
    변수이름[2] = 값; ...
    ```
    
    배열은 생성과 동시에 자동적으로 자신의 타입에 해당하는  기본값으로 초기화(정수는 0, 실수는 0.0, 객체 배열은 null)  되므로 배열을 사용하기 전에 따로 초기화를 해주지 않아도 된다. 원하는 값을 저장하려면  각 요소마다  값을 덮어쓴다.
    
    생성된 배열의 각 저장 공간은  배열 이름[인덱스]  형식이다. 인덱스(index)는 배열의 요소마다 붙여진 일련번호로 각 요소를 구별하는데 사용된다. 인덱스 범위는  0부터 배열 길이 -1까지다.
    
    ```java
    자료형[] 변수이름 = {값, 값, 값, ...}
    
    자료형[] 변수이름;
    변수이름 = new 자료형[] { 값, 값, 값, ...}
    ```

<div id="2"></div>

## ArrayList

<br />


### ArrayList란

ArrayList는 List 인터페이스를 상속받은 클래스로 크기가 가변적으로 변하는 선형리스트이다. 일반적인 배열과 같은 순차리스트이며 인덱스로 내부의 객체를 관리한다는점등이 유사하지만 한번 생성되면 크기가 변하지 않는 배열과는 달리 ArrayList는 객체들이 추가되어 저장 용량(capacity)을 초과한다면 자동으로 부족한 크기만큼 저장 용량(capacity)이 늘어난다는 특징을 가지고 있다.

![https://t1.daumcdn.net/cfile/tistory/995E66395B1CFD7D10](https://t1.daumcdn.net/cfile/tistory/995E66395B1CFD7D10)

### ArrayList 특징

1. 데이터 순서 있음 (index), 동일 데이터 중복 저장 허용
2. 연속적인 메모리 할당
3. LinkedList 보다 검색 빠름
4. LinkedList 보다 데이터 추가 삭제 느림

### Array vs ArrayList

1. 배열은 크기가 고정되어있지만 arrayList는 사이즈가 동적인 배열이다.
2. 배열은 primitive type(int, byte, char 등)과 object 모두를 담을 수 있지만, arrayList는 object element만 담을 수 있다.
3. 배열은 제네릭을 사용할 수 없지만, arrayList는 타입 안정성을 보장해주는 제네릭을 사용할 수 있다.
4. 길이에 대해 배열은 length 변수를 쓰고, arrayList는 size() 메서드를 써야한다.
5. 배열은 element들을 할당하기 위해 assignment(할당) 연산자를 써야하고, arrayList는 add() 메서드를 통해 element를 삽입한다.

### **ArrayList** 시간 복잡도

1. 조회 (get / set)
    
    ![https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FemUNfi%2Fbtq2GR1DcGE%2FD1dwzwzlu6JJXjoqaFBA60%2Fimg.png](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FemUNfi%2Fbtq2GR1DcGE%2FD1dwzwzlu6JJXjoqaFBA60%2Fimg.png)
    
    배열의 index를 통해 접근하는 방식이기 때문에, random access속도가 빠르며 **get** / **set** 메소드는 **상수 시간**을 가지게 된다.
    
2. 삽입 (add)
    
    
    일반적인 add의 경우 마지막에 데이터가 삽입되며 시간복잡도는 O(1) 이다.
    
    ArrayList는 배열이기 때문에 중간에 값을 끼워넣는 연산이 불가능하다.
    
    만약 새로운 값을 추가하려고 할 때, List의 크기가 생성되어 있는 배열의 size(생성시 따로 설정하지 않았다면 size = 10인 배열이 생성된다)보다 커지게 되면, 이전 크기의 2배가 되는 배열을 생성해 배열 전체를 복사하여 새로운 배열에 복사하고 제일 뒤에 값을 추가해야 한다.
    
    따라서 기존에 있던 배열에서 추가하고 싶은 index부터 마지막 index까지 **한 칸씩 뒤로 미루는 연산**이 필요하다.
    
    따라서, 해당하는 인덱스를 찾아가는 시간(O(1)) + 배열을 복사하는 시간 **(O(n)) = O(n)**의 시간이 소요된다.
    
3. 삭제 (remove)
    
    **add**와 유사하게 remove는 삭제된 index + 1부터 마지막 index까지 **한 칸씩 앞으로 당기는 연산**을 하게 된다.
    
    따라서, **add**와 동일한 **O(n)**의 시간 복잡도를 가지게 된다
    

### **ArrayList 사용법**

- ArrayList 선언
    
    ```java
    ArrayList list = new ArrayList();	//타입 미설정 Object로 선언
    ArrayList<Student> members = new ArrayList<Student>();	//타입설정 Student객체만 사용가능
    ArrayList<Integer> num = new ArrayList<Integer>();	//타입설정 int타입만 사용가능
    ArrayList<Integer> num2 = new ArrayList<>();	//new에서 타입 파라미터 생략가능
    ArrayList<Integer> num3 = new ArrayList<Integer>(10);	//초기 용량(capacity)지정
    ArrayList<Integer> list2 = new ArrayList<Integer>(Arrays.asList(1,2,3));	//생성시 값추가
    ```
    
- ArrayList 값 추가
    
    ```java
    //case1
    ArrayList<Integer> list = new ArrayList<Integer>();
    list .add(Object value);	//ArrayList의 마지막 위치에 value 추가
    list .add(int index, Object value);	//ArrayList 해당 index에 value 추가=> list.add(1,10);
    list.add(null); //null값도 add가능
    
    //case2
    ArrayList<Student> members = new ArrayList<Student>();
    Student student = new Student(name,age);
    members.add(student);
    members.add(new Member("홍길동",15));
    ```
    
- ArrayList 값 삭제
    
    ```java
    ArrayList<Integer> list = new ArrayList<Integer>();
    list.remove(int index);	//index에 해당하는 데이터 제거
    list.claer();	//모든 데이터 제거
    ```
    
- ArrayList 크기 구하기
    
    ```java
    list .size();	//엘리먼트 개수 반환
    ```
    
- 조회, 수정
    
    ```java
    arrayList.get(int index);	//해당 index에 있는 데이터 가져옴
    arryList.set(int index, Object value);	//해당 인덱스의 데이터 value로 변경
    //인덱스 조회 indexOf(x)
    arrayList.indexOf(Object value);	//해당 값 없을 시 -1 반환
    ```
    
<div id="3"></div>

## Linked List

<br />

### Linked List란

![https://www.geeksforgeeks.org/wp-content/uploads/gq/2013/03/Linkedlist.png](https://www.geeksforgeeks.org/wp-content/uploads/gq/2013/03/Linkedlist.png)

LinkedList란 Collection 프레임워크의 일부이며 java.util 패키지에 소속되어 있다.

이 클래스는 데이터가 연속된 위치에 저장되지 않고 모든 데이터가 데이터 부분과 주소 부분을 별도로 가지고 있는 선형 데이터 구조이다. 

데이터는 포인터와 주소를 사용하여 연결합니다

각 노드는 **데이터 필드**와 **다음 노드에 대한 참조**를 포함하는 노드로 구성되어 있다.

### Linked List특징

1. 순차접근(sequential access)만 가능하다
2. n개의 자료를 저장할때 자료들을 저장공간에 불연속적인 단위로 저장
3. ArrayList처럼 뒤로 밀거나 채우는 작업 없이 주소만 서로 연결시켜 주면 되기 때문에 추가 삭제가 ArrayList보다 빠르고 용이함
4. 메모리 곳곳에 저장되어 있는 노드들을 접근하는데 ArrayList보다 시간 소모가 많다.
5. LinkedList는 참조자를 위해 추가적인 메모리를 할당해야한다.(자료들의 크기가 작은 리스트의 경우 참조자를 위한 추가 적인 메모리할당은 비실용적임)
6. 단방향성을 갖고 있어 인덱스를 이용해 자료를 검색하는 애플리케이션에 적합하지 않다.
7. 삽입삭제가 빈번하게 발생되는 프로세스의 경우 사용하기 좋다.
8. 순차접근도 참조의지역성(한번 참조한 데이터는 다시 참조될 가능성이 높음) 때문에 LinkedList보다 ArrayList가 훨씬 빠름.

> 데이터 검색이 빈번한 경우 **ArrayList** 를 사용하는 것이 좋다
> 삽입 및 삭제가 빈번한 경우 **LinkedList**를 사용하는 것이 좋다.

### Linked List시간복잡도

1. 삽입
    
  ![https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/bTqFl4/btq2IhL6sh8/6OOLAzpcszOKPvIHZ3zwJK/img.png](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/bTqFl4/btq2IhL6sh8/6OOLAzpcszOKPvIHZ3zwJK/img.png)
    
   - 맨 앞 , 맨 뒤 삽입은 위치를 찾지 않아도 되서 시간 복잡도 O(1)이다.
   - 중간 삽입은 이전 노드와 다음 노드의 위치를 알고 있는 경우 시간 복잡도는 O(1)이다.
   - 하지만 탐색을 해야하는 경우 시간 복잡도 O(n)이다.
2. 삭제
    
    ![enter image description here](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/ccCN4y/btq2EhzOKfI/jbiAFDCjlmLKlLLke9MGTk/img.png)
    
    - 삽입과 마찬가지로 맨 앞, 맨 뒤 삭제는 시간 복잡도 O(1)이다.
    - 중간 삭제는 시간 복잡도 O(n) 또는 O(1)이다. (삽입과 같음)
3. 접근
    - 특정 위치에 있는 원소에 바로 접근이 불가능하다. (주소를 바로 알 수 없기 때문)
    - 원하는 원소를 찾기 위해서 최소 한 번은 리스트를 순회해야하기 때문에 시간 복잡도는 O(n)이다.

[Array vs ArrayList vs LinkedList](https://www.notion.so/e0e64ff6c5844c8c8bd09cdb14bf3720)

### Linked List사용법

- 선언
    
    ```java
    LinkedList<Object> linkedList = new LinkedList<>(); //기본 메소드
    
    LinkedList list = new LinkedList();//타입 미설정 Object로 선언된다.
    LinkedList<Student> members = new LinkedList<Student>();//타입설정 Student객체만 사용가능
    LinkedList<Integer> num = new LinkedList<Integer>();//타입설정 int타입만 사용가능
    LinkedList<Integer> num2 = new LinkedList<>();//new에서 타입 파라미터 생략가능
    LinkedList<Integer> list2 = new LinkedList<Integer>(Arrays.asList(1,2));//생성시 값추가
    ```
    
- 값 추가
    
    ```java
    
    linkedList.add(Object value);	//LinkedList의 마지막 위치에 value 추가
    linkedList.add(int index, Object value);	//LinkedList 해당 index에 value 추가
    ```
    
- 삭제
    
    ```java
    linkedList.remove(int index);	//index에 해당하는 데이터 제거
    linkedList.claer();	//모든 데이터 제거
    ```
    
- 크기
    
    ```java
    linkedList.size();	//노드 개수 반환
    ```
    
- 조회, 수정
    
    ```java
    //데이터 검색
    arrayList.get(int index);	//해당 index에 있는 데이터 가져옴
    arryList.set(int index, Object value);	//해당 인덱스의 데이터 value로 변경
    //인덱스 조회
    arrayList.indexOf(Object value);	//해당 값 없을 시 -1 반환
    ```
    
- 비어있는 리스트 확인
    
    ```java
    arrayList.isEmpty();	//boolean값 반환
    ```
    

### Doubly Linked List

- Doubly Linked List에서의 Node는 Previous field, Data field, 그리고 Next field가 있다.
- Singly Linked List(LinkedList)와 동일하지만, Previous field는 이전 Node의 주소가 있다.
- 즉, 양방향 탐색이 가능하다
- Doubly Linked List는 양쪽 끝 모두에 Null 포인터를 사용한다.

![https://media.vlpt.us/images/weather1212/post/e9a7d6ad-2f62-483b-aaa6-c972a5af3ef9/610px-Doubly-linked-list.svg.png](https://media.vlpt.us/images/weather1212/post/e9a7d6ad-2f62-483b-aaa6-c972a5af3ef9/610px-Doubly-linked-list.svg.png)
