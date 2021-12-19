### 트라이 (Trie)란

> 문자열을 빠르게 탐색하기 위한 트리구조의 자료구조
> 

![https://upload.wikimedia.org/wikipedia/commons/thumb/b/be/Trie_example.svg/375px-Trie_example.svg.png](https://upload.wikimedia.org/wikipedia/commons/thumb/b/be/Trie_example.svg/375px-Trie_example.svg.png)

- **자동완성 기능, 사전 검색 등 문자열을 탐색하는데 특화되어있는 자료구조**라고 한다.
- 래딕스 트리(radix tree) or 접두사 트리(prefix tree) or 탐색 트리(retrieval tree)라고도 한다. 트라이는 re**trie**val tree에서 나온 단어이다.
- 예를 들어 'Datastructure'라는 단어를 검색하기 위해서는 제일 먼저 'D'를 찾고, 다음에 'a', 't', ... 의 순서로 찾으면 된다. 이러한 개념을 적용한 것이 트라이(Trie)이다.
- 위에 보이는 트리의 루트에서부터 자식들을 따라가면서 생성된 문자열들이 트라이 자료구조에 저장되어 있다고 볼 수 있다. 저장된 단어는 끝을 표시하는 변수를 추가해서 저장된 단어의 끝을 구분할 수 있다.
- **DFS** 형태로 검색을 해보면 사진의 번호에 나와있듯이 to, tea, ted, ten, A, i, in, inn이라는 단어들이 자료구조에 들어가 있음을 알 수 있습니다.


### 트라이 장단점

장점

- 트라이(Trie)는 문자열 검색을 빠르게 한다.
- 문자열을 탐색할 때, 하나하나씩 전부 비교하면서 탐색을 하는 것보다 시간 복잡도 측면에서 훨씬 더 효율적이다.

단점

- 각 노드에서 자식들에 대한 포인터들을 배열로 모두 저장하고 있다는 점에서 저장 공간의 크기가 크다는 단점도 있다. (메모리 측면에서 비효율적일 수 있음!)


### 트라이 시간복잡도

- 제일 긴 문자열의 길이를 L 총 문자열들의 수를 M이라 할 때 시간복잡도는 아래와 같다.
- 생성시 시간복잡도: **O(M*L)**, 모든 문자열들을 넣어야하니 M개에 대해서 트라이 자료구조에 넣는건 가장 긴 문자열 길이만큼 걸리니 L만큼 걸려서 **O(M*L)**만큼 걸립니다. 물론 삽입 자체만은 **O(L)**만큼 걸립니다.
- 탐색시 시간복잡도: **O(L)**, 트리를 타고 들어가봤자 가장 긴 문자열의 길이만큼만 탐색하기 때문에 **O(L)**만큼 걸립니다.


### 트라이 작동원리

![https://media.vlpt.us/images/kimdukbae/post/9b4e8997-8c66-4509-9349-cf336b6e8a27/image.png](https://media.vlpt.us/images/kimdukbae/post/9b4e8997-8c66-4509-9349-cf336b6e8a27/image.png)

'abc', 'ab', 'car' 단어들을 'abc'부터 트라이에 저장한다고 가정해보자.

1. **'abc' 트라이(Trie)에 삽입**
    
    ![https://media.vlpt.us/images/kimdukbae/post/ff402294-b59d-4866-910e-2b3ba4c423cb/image.png](https://media.vlpt.us/images/kimdukbae/post/ff402294-b59d-4866-910e-2b3ba4c423cb/image.png)
    
    - 첫 번째 문자는 'a'이다. 초기에 트라이 자료구조 내에는 아무것도 없으므로 Head의 자식노드에 'a'를 추가해준다.
    - 'a'노드에도 현재 자식이 하나도 없으므로, 'a'의 자식노드에 'b'를 추가해준다.
    - 'c'도 마찬가지로 'b'의 자식노드로 추가해준다.
    - 'abc' 단어가 여기서 끝남을 알리기 위해 현재 노드에 abc라고 표시한다. (Data)
2. **'ab' 트라이(Trie)에 삽입**
    
    ![https://media.vlpt.us/images/kimdukbae/post/22168fdf-62e5-4cea-9969-6fd5d687d2a7/image.png](https://media.vlpt.us/images/kimdukbae/post/22168fdf-62e5-4cea-9969-6fd5d687d2a7/image.png)
    
    - 현재 Head의 자식노드로 'a'가 이미 존재한다. 따라서 'a'노드를 추가하지 않고, 기존에 있는 'a'노드로 이동한다.
    - 'b'도 'a'의 자식노드로 이미 존재하므로 'b'노드로 이동한다.
    - 'ab' 단어가 여기서 끝이므로 현재 노드에 ab를 표시한다.
    
3. **'car' 트라이(Trie)에 삽입**
    
    ![https://media.vlpt.us/images/kimdukbae/post/8d819895-5389-4b31-8b6b-a133e4ab3396/image.png](https://media.vlpt.us/images/kimdukbae/post/8d819895-5389-4b31-8b6b-a133e4ab3396/image.png)
    
    - Head의 자식노드로 'a'만 존재하고, 'c'는 존재하지 않는다. 따라서 'c'를 자식노드로 추가한다.
    - 'c'의 자식노드가 없으므로 마찬가지로 'a'를 추가한다.
    - 'a'의 자식노드가 없으므로 마찬가지로 'r'을 추가한다.
    - 'car' 단어가 여기서 끝이므로 현재 노드에 car를 표시한다.
