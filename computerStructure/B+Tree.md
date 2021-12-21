<div align="center">
  <br />
  <h1>B+Tree</h1>
  <br />
</div>

## 목차

1. [**B+Tree란**](#1)
2. [**삽입과정**](#2)
3. [**삭제과정**](#3)

<br />

<div id="1"></div>

## B+Tree란

B+Tree는 B-Tree의 확장 개념으로 , B-Tree인 경우 internal 또는 branch노드에 key와 data를 담을 수 있다.
하지만 B+Tree의 경우 브랜치 노드에 key만 담아두고 data는 담지 않는다. 
오직 리프노드에만 key와 data를 저장하고 리프노드끼리 LinkedList로 연결되어 있다.

### B+Tree 장점
1. 리프 노드를 제외하고 데이터를 담아두지 않기 때문에 메모리를 더 확보함으로써 더 많은 key들을 수용할 수 있다.***하나의 노드에 더 많은 key들을 담을 수 있기에 트리의 높이는 더 낮아진다.(cache hit를 높일 수 있음)

2. 풀 스캔 시, B+tree는 리프 노드에 데이터가 모두 있기 때문에 한 번의 선형탐색만 하면 되기 때문에 B-tree에 비해 빠르다. B-tree의 경우에는 모든 노드를 확인해야 한다. 

### InnoDB(MySQL의 DB engine)
MySQL의 InnoDB는 B+Tree로 이루어져 있다.
<div>
  <img width="680" alt="스크린샷 2021-12-20 오후 5 34 46" src="https://user-images.githubusercontent.com/54795404/146737406-a9446fc1-296a-425f-9b0f-7f50ca839765.png">
</div>
InnoDB에서 B+tree는 단순하게 설명한 B+tree보다 더 복잡하게 구현된 것 같다. 
같은 레벨의 노드들끼리는 Linked List가 아닌 Double Linked List를 사용했고, 자식 노드로는 Single Linked List로 연결되어있다.
key의 범위마다 찾아가야할 페이지 넘버(포인터)가 있는데, 해당 페이지 넘버를 통해 곧바로 다음 노드로 넘어간다.
그리고 리프 노드에 다다랐을 때 디스크에 존재하는 데이터의 주소값을 구할 수 있고, Linked List를 통해 탐색도 가능하다. 

### B-Tree VS B+Tree
|구분|	B-tree	|B+tree|
|---|---|---|
|데이터 |저장	리프 노드, 브랜치 노드 모두 데이터 저장 가능|	오직 리프 노드에만 데이터 저장 가능
|트리의 높이|	높음	|낮음(한 노드 당 key를 많이 담을 수 있음)|
|풀 스캔 시, 검색 속도|	모든 노드 탐색	|리프 노드에서 선형 탐색 |
|키 중복	|없음	|있음(리프 노드에 모든 데이터가 있기 때문)|
|검색	|자주 access 되는 노드를 루트 노드 가까이 배치할 수 있고, 루트 노드에서 가까울 경우, 브랜치 노드에도 데이터가 존재하기 때문에 빠름	|리프 노드까지 가야 데이터 존재|
|링크드 리스트|	없음|	리프 노드끼리 링크드 리스트로 연결|

### DB 인덱싱
실제 DB의 인덱싱은 B+Tree로 이루어져 있다. 다음 그림은 인덱싱을 나타낸 것이다.
인덱싱은 어떠한 자료를 찾는데 key값을 이용해 효과적으로 찾을 수 있는 기능이다.
<div>
  <img width="850" alt="스크린샷 2021-12-20 오후 5 44 34" src="https://user-images.githubusercontent.com/54795404/146738698-24ffdcd1-d63f-4dd0-b5ff-9fbc2253629a.png">
</div>
위와 같은 인덱싱을 B+Tree로 나타내면 아래 그림과 같다.
<div>
  <img width="850" alt="스크린샷 2021-12-20 오후 5 46 08" src="https://user-images.githubusercontent.com/54795404/146738932-8bfe2fd9-b416-4f0c-a6ea-14f67f690079.png">
</div>

1.모든 key, data가 리프노드에 모여있다. B트리는 리프노드가 아닌 각자 key마다 data를 가진다면, B+트리는 리프 노드에 모든 data를 가진다.

2.모든 리프노드가 연결리스트의 형태를 띄고 있다. B트리는 옆에있는 리프노드를 검사할 때, 다시 루트노드부터 검사해야 한다면, B+트리는 리프노드에서 선형검사를 수행할 수 있어 시간복잡도가 굉장히 줄어든다.


### B+Tree 특징(M차 B+Tree)
- 노드는 M/2개 부터 M개 까지의 자식을 가질 수 있다.
- 노드에는 [M/2]−1개 부터 [M-1]개의 키가 포함될 수 있다.
- 노드의 키가 x개라면 자식의 수는 x+1개 이다.
- 최소차수는 자식수의 하한값을 의미하며, 최소차수가 t라면 M=2t−1을 만족한다. (최소차수 t가 2라면 3차 B트리이며, key의 하한은 1개입니다.)


<br />

<div id="2"></div>

## 삽입과정

검색과정은 B-Tree설명과 같다.(앞의 [B-Tree](https://github.com/corrvax/ComputerScienceStudy/edit/main/computerStructure/BTree.md)참고)

### Case1) 분할이 일어나지 않고, 삽입 위치가 리프노드의 가장 앞 key자리가 아닌경우
B-Tree와 동일하게 수행한다.

### Case2) 분할이 일어나지 않고, 삽입 위치가 리프노드의 가장 앞 key자리인 경우
삽입 후 부모 key를 삽입된 key로 갱신하고, data를 넣는다.
<div>
  <img width="850" alt="스크린샷 2021-12-21 오전 10 57 09" src="https://user-images.githubusercontent.com/54795404/146858054-47d3bc42-a8ef-448b-9701-9aaae032f81f.png">
</div>

### Case3) 분할이 일어나는 삽입과정
1.분할이 일어나는 노드가 리프노드가 아니라면 기존 B트리와 똑같이 분할을 진행한다. 중간 key를 부모 key로 올리고, 분할한 두개의 노드를 왼쪽, 오른쪽 자식으로 설정한다.

2.분할이 일어나는 노드가 리프노드라면 중간 key를 부모 key로 올리지만, 오른쪽 노드에 중간 key를 포함하여 분할한다. 또한 리프노드는 연결리스트이기 때문에 왼쪽 자식노드와 오른쪽 자식 노드를 이어줘 연결리스트 형태를 유지한다. 해당 부분이 B트리의 분할과 다른 점이다.

<div>
  <img width="850" alt="스크린샷 2021-12-21 오전 11 01 26" src="https://user-images.githubusercontent.com/54795404/146858422-ccfcfde2-24b1-4adb-918c-84d0d7150cfb.png">
</div>
  <img width="850" alt="스크린샷 2021-12-21 오전 11 01 46" src="https://user-images.githubusercontent.com/54795404/146858451-89a90bff-e2c4-4fc0-b94f-5bbab7265cb9.png">
<div>
  <img width="850" alt="스크린샷 2021-12-21 오전 11 09 38" src="https://user-images.githubusercontent.com/54795404/146859141-271ddd90-9224-47de-b4bd-c08c12e082b6.png">
</div>

<br />

<div id="3"></div>

## 삭제과정

삭제과정 또한 B-Tree와 유사하다. 하지만 삭제할 key k가 무조건 리프노드에 존재하는 점과 k를 삭제하기 위해 검색하는 과정에서 index에 존재할 수 있다는 점이 다르다.
### Case1) 삭제할 key k 가 index에 없고, 리프노드의 가장 처음 key가 k가 아닌 경우
기존 B-Tree삭제과정과 동일하다.
<div>
  <img width="687" alt="스크린샷 2021-12-21 오전 11 12 13" src="https://user-images.githubusercontent.com/54795404/146859368-25401764-964f-4f6f-9e0d-6f2291a2cba6.png">
</div>

### Case2) 삭제할 key k가 리프노드의 가장 처음 key인 경우
삭제할 key k가 리프노드의 가장 처음 key인 경우에는 항상 k가 index내에 존재한다.

1.먼저 리프노드의 k를 삭제하는 과정을 수행한다. key의 개수가 최소 key의 개수라면 B트리의 삭제 과정 중 형제노드의 key를 빌려오는 경우나 부모key와 병합하는 등 과정들은 동일하게 수행한다. 단, 리프노드가 병합할 때는 부모key와 오른쪽 자식의 처음 key가 동일하기 때문에 부모key를 가져오는 과정만 생략하고 왼쪽 자식과 오른쪽 자식을 병합만 하면 된다.

2.리프노드의 k를 삭제한 후, index내의 k를 inorder successor(오른쪽 자손에서 가장 작은 key)로 변경한다.
<div>
  <img width="850" alt="스크린샷 2021-12-21 오후 12 43 05" src="https://user-images.githubusercontent.com/54795404/146867559-c0532bee-494c-41d6-bb63-ba32c443bc80.png">
</div>
<div>
  <img width="850" alt="스크린샷 2021-12-21 오후 12 43 50" src="https://user-images.githubusercontent.com/54795404/146867623-ad882949-4d3e-49c4-ab90-cbbbf3763cc0.png">
</div>
<div>
  <img width="850" alt="스크린샷 2021-12-21 오후 12 44 10" src="https://user-images.githubusercontent.com/54795404/146867652-e381c835-6210-4527-a3ca-b8618038b646.png">
</div>
