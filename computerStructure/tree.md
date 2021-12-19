## 자료구조-Tree

### 트리란
트리란 노드들이 나무 가지처럼 연결된 비선형 계층적 자료구이다.
트리는 다음과 같이 나무를 거꾸로 뒤집어 놓은 모양과 유사하다.

<img width="497" alt="스크린샷 2021-12-19 오후 7 15 03" src="https://user-images.githubusercontent.com/54795404/146671446-441dc47f-504b-4898-b9b9-3c98e26e1503.png">

트리는 또한 트리 내에 다른 하위 트리가 있고 그 하위 트리 안에는 또 다른 하위 트리가 있는 재귀적 자료구조이기도 하다.

eg)컴퓨터의 directory구조

<img width="497" alt="스크린샷 2021-12-19 오후 7 16 24" src="https://user-images.githubusercontent.com/54795404/146671488-3c4ba6db-0fb0-4290-a6c8-77edffd19043.png">

트리 구조에서 사용되는 기본 용어

<img width="517" alt="스크린샷 2021-12-19 오후 7 18 11" src="https://user-images.githubusercontent.com/54795404/146671538-5fc21997-1366-4143-b07d-3a4770e7a50c.png">

### 노드 (Node)
트리를 구성하고 있는 기본 요소
노드에는 키 또는 값과 하위 노드에 대한 포인터를 가지고 있음.
A, B, C, D, E, F, G, H, I, J

### 간선 (Edge)
노드와 노드 간의 연결선

### 루트 노드 (Root Node)
트리 구조에서 부모가 없는 최상위 노드
root node : A

### 부모 노드 (Parent Node)
자식 노드를 가진 노드
H, I에 부모 노드는 D

### 자식 노드 (Child node)
부모 노드의 하위 노드
노드 D의 자식 노드는 H, I

### 형제 노드 (Sibling node)
같은 부모를 가지는 노드
H, I는 같은 부모를 가지는 형제 노드

### 외부 노드(external node, outer node), 단말 노드 (terminal node), 리프 노드(leaf node)
자식 노드가 없는 노드
H, I, J, F, G

### 내부 노드 (internal node, inner node), 비 단말 노드 (non-terminal node), 가지 노드 (branch node)
자식 노드 하나 이상 가진 노드
A, B, C, D, E

### 깊이 (depth)
루트에서 어떤 노드까지의 간선(Edge) 수
루트 노드의 깊이 : 0
D의 깊이 : 2

### 높이 (height)
어떤 노드에서 리프 노드까지 가장 긴 경로의 간선(Edge) 수
리프 노드의 높이 : 0
A 노드의 높이 : 3

<img width="420" alt="스크린샷 2021-12-19 오후 7 20 52" src="https://user-images.githubusercontent.com/54795404/146671623-fe75bcc5-8ba2-418d-9fb2-129dff699708.png">

### 트리의 특징
- 하나의 루트노드와 0개 이상의 하위 트리로 구성되어 있다.
- 데이터를 순차적으로 저장하지 않기 때문에 비선형 자료구조이다.
- 트리내에 또 다른 트리가 있는 재귀적 자료구조이다.
- 단순 순환(Loop)을 갖지 않고, 연결된 무방향 그래프 구조이다.
- 노드가 n개인 트리는 항상 n-1개의 간선을 가진다.
<img width="461" alt="스크린샷 2021-12-19 오후 7 31 49" src="https://user-images.githubusercontent.com/54795404/146671915-b3251f6e-cc8f-47d7-803f-95d7df266792.png">

다음은 트리가 아닌경우이다.(루트 노드가 두 개가 있으므로 트리가 아닙니다.)
<img width="456" alt="스크린샷 2021-12-19 오후 7 32 25" src="https://user-images.githubusercontent.com/54795404/146671934-40b070b1-b59c-4d57-8936-e2f0b4b0975d.png">


<img width="515" alt="스크린샷 2021-12-19 오후 7 37 59" src="https://user-images.githubusercontent.com/54795404/146672056-97043261-6976-4a1f-8aa7-b4ed132470c2.png">


## 이진트리(Binary Tree)
이진트리는 각 노드가 최대 두 개의 자식을 갖는 트리를 뜻한다. 
1. 공집합 이거나
2. 루트와 왼쪽 서브트리, 오른쪽 서비트리로 구성된 노드들의 유한 집합

<img width="489" alt="스크린샷 2021-12-19 오후 7 50 32" src="https://user-images.githubusercontent.com/54795404/146672421-4f403e6c-3e35-4cda-b96b-8c4b042ba2aa.png">


이진 트리는 전위 순회, 중위 순회, 후위 순회를 통해 탐색할 수 있다.

### 중위 순회(inorder traversal) 
LVR 탐색이 이루어진다.(왼쪽 서브 트리 - 루트 노드 - 오른쪽 서브트리 )
<img width="503" alt="스크린샷 2021-12-19 오후 7 44 06" src="https://user-images.githubusercontent.com/54795404/146672252-ffccd5ed-7370-4164-a2fa-4a0340f9a4d5.png">
A B C D E F G H I

### 전위 순회(Preorder Traversal)
VLR 탐색이 이루어진다. (루트 노드 - 왼쪽 서브 트리- 오른쪽 서브 트리)

<img width="500" alt="스크린샷 2021-12-19 오후 7 47 57" src="https://user-images.githubusercontent.com/54795404/146672363-e7e999a1-370e-412c-9da0-c5b3f2a759fb.png">

### 후위 순회(Postorder Traversal)
LRV 탐색이 이루어진다. ( 왼쪽 서브 트리 - 오른쪽 서브 트리 - 루트 노드)
<img width="483" alt="스크린샷 2021-12-19 오후 7 48 59" src="https://user-images.githubusercontent.com/54795404/146672386-004c2d4c-fc2f-4ce9-b349-86d7c0835da8.png">



