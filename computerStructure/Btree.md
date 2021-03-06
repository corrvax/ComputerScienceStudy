<div align="center">
  <br />
  <h1>B-Tree</h1>
  <br />
</div>

## 목차

1. [**B-Tree란**](#1)
2. [**검색 과정**](#2)
3. [**삽입 과정**](#3)
4. [**삭제 과정**](#4)

--> B+Tree란?? [B+Tree](https://github.com/corrvax/ComputerScienceStudy/blob/main/computerStructure/B%2BTree.md)
<br />

<div id="1"></div>

## B-Tree란

B트리는 이진트리와 다르게 하나의 노드에 많은 수의 정보를 가지고 있을 수 있다. 최대 M개의 자식을 가질 수 있는 B트리를 M차 B트리라고 하며 다음과 같은 특징을 같는다.

- 각 내부노드의 자식노드 개수는 [M/2]이상 M이하 이다.
- 노드에는 [M/2]−1개 부터 M-1개의 키가 포함될 수 있다.
- 노드의 키가 x개라면 자식의 수는 x+1개 이다.
- 최소차수는 자식수의 하한값을 의미하며, 최소차수가 t라면 M=2t−1을 만족한다. (최소차수 t가 2라면 3차 B트리이며, key의 하한은 1개 이다.)
- 모든 단말노드는 동일한 높이를 갖는다.

다음은 차수가 3인 B트리 이다. 파란색 부분은 각 노드의 key를나타내며, 빨간색 부분은 자식 노드들을 가르키는 포인터이다. 
key들은 노드 안에서 항상 정렬된 값을 가지며, 이진검색 트리처럼 각 key들의 왼쪽 자식들은 항상 key보다 작은 값을, 오른쪽은 큰 값을 가진다.
<div>
 <img width="850" alt="스크린샷 2021-12-20 오전 11 08 04" src="https://user-images.githubusercontent.com/54795404/146702005-efdb0668-44bc-4afa-b546-779bb07a840e.png">
</div>

### B-Tree 복잡도
이진 트리는 구조의 간결함과 균형만 맞다면 ***검색, 삽입, 삭제 모두 O(logN)*** 의 성능을 보이는 장점이 있다.
B-Tree는 스스로 균형을 맞추는 트리로 최악의 경우에도 O(logN)의 검색 성능을 보인다.(탐색을 제외한 작업에서는 재정렬 작업 때문에 일반 Tree보다 성능이 좋지 않다.)

### B-Tree 특징
B-Tree는 트리의 균형을 자동으로 맞추어준다. 이런 균형 로직은 단순하면서도 효율적이다.
대량의 데이터를 처리해야 하는 검색 구조인 경우 하나의 노드에 많은 데이터를 가질 수 있다는 큰 장점이 있다.
대량의 데이터는 메모리보다 하드디스크나 SSD에 저장되어야 하는데 이런 외부 기억 장치들은 블럭단위로 입출력을 하기 때문이다.
예를 들어 한블럭이 1024바이트라면 2바이트를 읽으나 1024바이트를 읽으나 입출력에 대한 비용은 동일하다.
따라서 하나의 노드를 1024바이트가 되도록 조절한다면 입출력 면에서 매우 효율적인 구성이된다.
-->실제 B-Tree는 많은 데이터베이스 시스템의 인덱스 저장 방법으로 쓰이고 있다.

### B-Tree 장점
1. 트리 내 모든 데이터가 항상 정렬된 상태로 유지되기 때문에 등호(=) 연산뿐만 아니라 부등호(>,<)연산처리도 가능하다.
2. 포인터 접근 방식이 적어 매우 많은 데이터가 있어도 속도 이슈가 적다.
3. 데이터탐색뿐 아니라, 삽입 및 수정 및 삭제에도 항상 O(long N)의 시간 복잡도를 갖는다.
<br/>

<div id="2"></div>

## 검색 과정

루트노드에서 시작하여 하향식으로 검색을 수행한다. 검색하고자 하는 key를 k(아래그림에서 [18])라고 하였을 때 검색 과정이다.

루트 노드에서 시작하여 key들을 순회하면서 검사한다.
1-1. 만일 k와 같은 key를 찾았다면 검색을 종료한다.
1-2. 검색하는 값과 key들의 대소관계를 비교한다. 어떠한 key들 사이에 k가 들어간다면 해당 key들 사이의 자식노드로로 내려간다.

해당 과정을 리프노드에 도달할 때까지 반복한다. 만일 리프노드에도 k와 같은 key가 없다면 검색을 실패한다.
<div>
  <img width="850" alt="스크린샷 2021-12-20 오전 11 17 42" src="https://user-images.githubusercontent.com/54795404/146702645-2a95909f-ec72-4324-83c4-1344b271cdc6.png">
</div>

<div>
  <img width="850" alt="스크린샷 2021-12-20 오전 11 18 10" src="https://user-images.githubusercontent.com/54795404/146702675-fb29f8eb-63e8-4595-9269-c7211b49dc7f.png">

</div>
  <img width="850" alt="스크린샷 2021-12-20 오전 11 20 06" src="https://user-images.githubusercontent.com/54795404/146702795-4a5512c2-bfd0-4512-bf0e-254b5bd61c11.png">
<div>
 
</div>

<br />

<div id="3"></div>

## 삽입 과정

key를 삽입하기 위해서는 
1. 요소 삽입에 적절한 리프 노드를 검색하고
2. 필요한 경우 노드를 분할해야 한다.
**리프노드 검색은 하향식**이지만 <b>노드 분할의 과정은 상향식</b>으로 이루어진다고 볼 수 있다. 
다음은 삽입하고자 하는 값을 k(아래 그림에서[9])로 하였을 때 삽입 과정이다.
트리가 비어있으면 루트 노드를 할당하고 k를 삽입한다. 
만일 루트노드가 가득 찼다면, 노드를 분할하고 리프노드가 생성된다.
이후부터는 삽압하기에 적절한 리프노드를 찾아 k를 삽입한다. 삽입위치는 노드의 key값과 k값을 검색 연산과 동일한 방법으로 비교하면서 찾는다.

삽입과정은 두 가지 경우로 나뉘게 된다.
### Case1) 분할이 일어나지 않는 경우
리프노드가 가득차지 않았으면 오름차순으로 k를 삽입합니다.
<div>
  <img width="850" alt="스크린샷 2021-12-20 오후 1 44 02" src="https://user-images.githubusercontent.com/54795404/146713211-26b9459d-a581-47b9-8254-92c72aa7b8e0.png">

</div>
  <img width="850" alt="스크린샷 2021-12-20 오후 1 44 15" src="https://user-images.githubusercontent.com/54795404/146713232-8dd8de23-589b-497a-a591-b5a81c5a9d08.png">

### Case2) 분할이 일어나는 경우
만일 리프노드에 key노드가 가득 찬 경우, 노드를 분할해야 한다.
오름차순으로 요소를 삽입한다. 노드가 담을 수 있는 최대 key 개수를 초과하게 된다.
중앙값에서 분할을 수행한다. 중앙값은 부모 노드로 병합하거나 새로 생성된다. 왼쪽 키들은 왼쪽 자식으로, 오른쪽 키들은 오른쪽 자식으로 분할된다.

부모 노드를 검사해서 또 다시 가득 찼다면, 다시 부모노드에서 위 과정을 반복한다.
<div>
  <img width="850" alt="스크린샷 2021-12-20 오후 1 58 17" src="https://user-images.githubusercontent.com/54795404/146714218-f9478eff-18e1-4ad4-ae9d-9b13105a0333.png">
</div>
<div>
  <img width="850" alt="스크린샷 2021-12-20 오후 1 59 17" src="https://user-images.githubusercontent.com/54795404/146714272-75ff0b4b-3325-4fb9-9344-aee5fe07b7cb.png">
</div>
<div>
  <img width="850" alt="스크린샷 2021-12-20 오후 2 01 04" src="https://user-images.githubusercontent.com/54795404/146714391-c53c0d3d-3ad5-49d0-96ca-f153197d6577.png">
</div>
<div>
  <img width="850" alt="스크린샷 2021-12-20 오후 2 02 36" src="https://user-images.githubusercontent.com/54795404/146714506-3994a9e9-dfb3-4fc7-ba92-4ff4be9253a2.png">
</div>
<div>
  <img width="851" alt="스크린샷 2021-12-20 오후 2 03 18" src="https://user-images.githubusercontent.com/54795404/146714554-432b361a-4452-4acc-960f-44239eb7c168.png">
</div>
<br />

<div id="4"></div>

## 삭제 과정 

요소를 삭제하기 위해선 1. 삭제할 키가 있는 노드 검색, 2. 키 삭제, 3. 필요한 경우, 트리 균형 조정을 해야한다.
삭제 과정을 이해하기 위해서 몇가지 용어를 정의해본다.
***inorder predecessor : 노드의 왼쪽 자손에서 가장 큰 key
inorder successor : 노드의 오른쪽 자손에서 가장 작은 key
부모key: 부모노드의 key들 중 왼쪽 자식으로 본인 노드를 가지고 있는 key값이다. 단, 마지막 자식노드의 경우에는 부모의 마지막 key이다.***

### Case 1) 삭제할 key k가 리프에 있는 경우
***Case 1.1) 현재 노드의 key 개수가 최소 key 개수보다 크다면***
다른 노드들에 영향 없이 해당 k를 단순 삭제한다.
<div>
  <img width="850" alt="스크린샷 2021-12-20 오후 2 08 53" src="https://user-images.githubusercontent.com/54795404/146714951-094ea297-810d-4fdb-a022-1e32a2d64929.png">
</div>

***Case 1.2) 왼쪽 또는 오른쪽 형제 노드의 key가 최소 key 개수 이상라면***
부모 key 값으로 k를 대체한다.
최소키 개수 이상의 키를 가진 형제 노드가 ***왼쪽 형제라면 가장 큰 값을, 오른쪽 형제라면 가장 작은 값***을 부모 key로 대체한다.
<div>
  <img width="850" alt="스크린샷 2021-12-20 오후 2 36 32" src="https://user-images.githubusercontent.com/54795404/146717191-78637d16-8a82-46a5-a204-39df708752f9.png"> 
</div>
<div>
  <img width="850" alt="스크린샷 2021-12-20 오후 2 37 03" src="https://user-images.githubusercontent.com/54795404/146717234-453ec8d9-05b5-4f93-88a2-9031588b69ca.png">
</div>

***Case 1.3) 왼쪽, 오른쪽 형제 노드의 key가 최소 key 개수이고, 부모노드의 key가 최소개수 이상이면***
k를 삭제한 후, 부모key를 형제 노드와 병합한다.
부모노드의 key개수를 하나 줄이고, 자식 수 역시 하나를 줄여 B-Tree를 유지한다.
<div>
  <img width="850" alt="스크린샷 2021-12-20 오후 2 40 40" src="https://user-images.githubusercontent.com/54795404/146717556-f812dfb7-31f4-497a-86d9-1cce21ad1b16.png">
</div>
<div>
  <img width="850" alt="스크린샷 2021-12-20 오후 2 41 10" src="https://user-images.githubusercontent.com/54795404/146717597-8781d8f6-9a88-48f6-a000-1e8bf3fd88e5.png">
</div>

***Case 1.4) 자신과 형제, 부모 노드의 key 개수가 모두 최소 key 개수라면***
부모노드를 루트노드로 한 부분 트리의 높이가 줄어드는 경우이기 때문에 재구조화의 과정이 일어난다. case3의 2번 과정으로 이동한다.

### Case2) 삭제할 key k 가 내부 노드에 있고, 노드나 자식에 키가 최소 키 개수보다 많을 경우
현재 노드의 inorder predecessor 또는 inorder successor와 k의 자리를 바꿉니다.
리프노드의 k를 삭제하게 되면, 리프노드가 삭제 되었을 때의 조건으로 변한다. 삭제한 리프노드에 대해서 case 1 조건으로 이동한다.

<div>
  <img width="648" alt="스크린샷 2021-12-20 오후 4 50 50" src="https://user-images.githubusercontent.com/54795404/146731848-cd28e91a-8ad5-488f-be3e-8fa54afc1834.png">
</div>

## Case3) 삭제할 key k 가 내부 노드에 있고, 노드에 key 개수가 최소 key 개수만큼, 노드의 자식 key 개수도 모두 최소 key 개수인 경우

삭제할 key k가 있는 노드도 최소, 자식노드들도 최소의 key 개수를 가지므로, k를 삭제하면 트리의 높이가 줄어들어 재구조화가 일어나는 경우이다. 재구조화의 과정은 다음과 같다.

<div>
  <img width="850" alt="스크린샷 2021-12-20 오후 5 08 15" src="https://user-images.githubusercontent.com/54795404/146733990-53396729-0f7c-4ca3-8ea3-3a24e4866a5c.png">
</div>
<div>
  <img width="850" alt="스크린샷 2021-12-20 오후 5 08 25" src="https://user-images.githubusercontent.com/54795404/146734014-cd54814f-1b78-4132-bbff-6c6f6473f63c.png">
</div>
새로운 트리 예시

<div>
  <img width="850" alt="스크린샷 2021-12-20 오후 5 09 35" src="https://user-images.githubusercontent.com/54795404/146734143-93c32831-5a28-4d6e-8d56-337d21ebaae8.png">
</div>
<div>
  <img width="850" alt="스크린샷 2021-12-20 오후 5 09 46" src="https://user-images.githubusercontent.com/54795404/146734172-c60daff6-88dc-4223-bb97-e1e169ea3b28.png">
</div>
