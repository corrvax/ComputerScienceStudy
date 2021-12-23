<div align="center">
  <br />
  <h1>Tree</h1>
  <br />
</div>

## 목차

1. [**트리**](#1)
2. [**특징**](#2)
3. [**종류**](#3)
4. [**사용 사례**](#4)


<br />

<div id="1"></div>

## 트리

트리 (Tree)란 노드들이 나무 가지처럼 연결된 비선형 계층적 자료구조입니다.

트리는 트리 내에 다른 하위 트리가 있고 그 하위 트리 안에는 또 다른 하위 트리가 있는 재귀적 자료구조이기도 합니다.

컴퓨터의 direcory구조가 트리 구조의 대표적인 예가 될 수 있습니다.

![https://blog.kakaocdn.net/dn/bl6Ecy/btq1yFCmshK/4uvfvvAxqX3TYlEN2P2eX1/img.png](https://blog.kakaocdn.net/dn/bl6Ecy/btq1yFCmshK/4uvfvvAxqX3TYlEN2P2eX1/img.png)

### 트리 구조에서 사용되는 기본 용어

---

![https://blog.kakaocdn.net/dn/cA6btV/btq1z5fVwht/96SGFKq5O3QtaUBabJKibK/img.png](https://blog.kakaocdn.net/dn/cA6btV/btq1z5fVwht/96SGFKq5O3QtaUBabJKibK/img.png)

- Node (노드) : 트리를 구성하고 있는 각각의 요소를 의미한다.
- Edge (간선) : 트리를 구성하기 위해 노드와 노드를 연결하는 선을 의미한다.
- Root Node (루트 노드) : 트리 구조에서 최상위에 있는 노드를 의미한다.
- Terminal Node ( = leaf Node, 단말 노드) : 하위에 다른 노드가 연결되어 있지 않은 노드를 의미한다.
- Internal Node (내부노드, 비단말 노드) : 단말 노드를 제외한 모든 노드로 루트 노드를 포함한다.
- Parent Node (부모 노드) : 자식 노드를 가진 노드
- Child Node (자식 노드) : 부모 노드의 하위 노드
- Sibling Node (형제 노드) : 같은 부모를 가지는 노드
- Depth (깊이) : 루트에서 어떤 노드까지의 간선(Edge) 수
- Height (높이) : 어떤 노드에서 리프 노드까지 가장 긴 경로의 간선(Edge) 수

<br />

<div id="2"></div>

## 특징

- 하나의 루트 노드와 0개 이상의 하위 트리로 구성되어 있습니다.
- 데이터를 순차적으로 저장하지 않기 때문에 비선형 자료구조입니다.
- 트리내에 또 다른 트리가 있는 재귀적 자료구조입니다.
- 단순 순환(Loop)을 갖지 않고, 연결된 무방향 그래프 구조입니다.
- 노드 간에 부모 자식 관계를 갖고 있는 계층형 자료구조이며 모든 자식 노드는 하나의 부모 노드만 갖습니다.
- 노드가 n개인 트리는 항상 n-1개의 간선(edge)을 가집니다.

![https://blog.kakaocdn.net/dn/vKvqg/btq1E9ODRk8/qXL8GehaRh0tgxiyrm8Q31/img.png](https://blog.kakaocdn.net/dn/vKvqg/btq1E9ODRk8/qXL8GehaRh0tgxiyrm8Q31/img.png)

다음은 트리가 아닌 경우입니다.

![https://blog.kakaocdn.net/dn/sXGwq/btq1ByPsA98/iAmWtKVq4WWdEV85sorkkk/img.png](https://blog.kakaocdn.net/dn/sXGwq/btq1ByPsA98/iAmWtKVq4WWdEV85sorkkk/img.png)

루트 노드가 2개(2, 8) 있으므로 트리가 아닙니다.

![https://blog.kakaocdn.net/dn/4pwtu/btq1By9I93O/zz7ZRsYNpUbKfCwCf0Jno0/img.png](https://blog.kakaocdn.net/dn/4pwtu/btq1By9I93O/zz7ZRsYNpUbKfCwCf0Jno0/img.png)

노드 6에는 2명의 부모 노드(8,5)가 있고 사이클(2-8-6-5)이 형성되므로 트리가 아닙니다.

<br />

<div id="3"></div>

## 종류

### 편향 트리 (skew tree)

- 모든 노드들이 자식을 하나만 가진 트리
- 왼쪽 방향으로 자식을 하나씩만 가질 때 left skew tree, 오른쪽 방향으로 하나씩만 가질 때 right skew tree라고 함.

![https://blog.kakaocdn.net/dn/bXGUbk/btq1E9gO4E7/v0vMMd9PYc0E2zH70ZC2eK/img.png](https://blog.kakaocdn.net/dn/bXGUbk/btq1E9gO4E7/v0vMMd9PYc0E2zH70ZC2eK/img.png)

### 이진트리 (Binary Tree)

- 각 노드의 차수(자식 노드)가 2 이하인 트리
    
    1. 포화 이진트리
    
    트리의 각 레벨에 노드가 꽉 차있는 이진트리를 의미한다.
    
    ![https://blog.kakaocdn.net/dn/AxJJn/btqAQM0Lep9/M07HUoFwctBUDMZDkN40Hk/img.png](https://blog.kakaocdn.net/dn/AxJJn/btqAQM0Lep9/M07HUoFwctBUDMZDkN40Hk/img.png)
    
    위와 노드가 비어있는 곳이 없고 꽉 차있는 상태를 말한다.
    
    2. 완전 이진트리
    
    높이가 k일 때 레벨 1부터 k-1까지는 노드가 모두 채워져 있고 마지막 레벨 k에서는 왼쪽부터 오른쪽으로 노드가 순서대로 채워져 있는 이진트리이다.
    
    ![https://blog.kakaocdn.net/dn/cfe2yQ/btqARxIBxkA/GREGxIDcTiyklRBZ8ka261/img.png](https://blog.kakaocdn.net/dn/cfe2yQ/btqARxIBxkA/GREGxIDcTiyklRBZ8ka261/img.png)
    
    위와 같이 왼쪽에서 부터 차례대로 노드가 배치되는 형태이다.
    
    3. 기타 이진트리
    
    기타 이진트리는 위의 두개의 특성을 제외하고 이진트리의 속성을 만족 시킨다면 다 기타 이진트리라고 할 수 있다.
    

### 이진 탐색 트리 (Binary Search Tree, BST)

- 순서화된 이진 트리
- 노드의 왼쪽 자식은 부모의 값보다 작은 값을 가져야 하며 노드의 오른쪽 자식은 부모의 값보다 큰 값을 가져야 함.

![image](https://user-images.githubusercontent.com/56222478/147184786-2503f507-003e-43ea-b97d-8c841295f23e.png)


### 다원 탐색 트리(m-way search tree)

- 최대 m개의 서브 트리를 갖는 탐색 트리
- 이진 탐색 트리의 확장된 형태로 높이를 줄이기 위해 사용함.

![image](https://user-images.githubusercontent.com/56222478/147184823-1dc95d39-47c0-4d12-948d-a287dd1a47af.png)

<br />

<div id="4"></div>

## 사용 사례

계층 적 데이터 저장

- 트리는 데이터를 계층 구조로 저장하는 데 사용됩니다.
- 예를 들어 파일 및 폴더는 계층적 트리 형태로 저장됩니다.

효율적인 검색 속도

- 효율적인 삽입, 삭제 및 검색을 위해 트리 구조를 사용합니다.

힙(Heap)

- 힙도 트리로 된 자료 구조입니다.

데이터 베이스 인덱싱

- 데이터베이스 인덱싱을 구현하는데 트리를 사용합니다.
- 예) B-Tree, B+Tree, AVL-Tree..

Trie

- 사전을 저장하는 데 사용되는 특별한 종류의 트리입니다.
