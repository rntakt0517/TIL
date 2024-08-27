# Tree

[자료구조 트리](#자료구조-트리)

[이진 트리](#이진-트리)

[순회(traversal)](#순회traversal)

[연습문제](#연습문제)

[어려운 버전](#어려운 버전)

[인접리스트](#인접리스트)

---

## 자료구조 트리

- 개념
  
  - 비선형 구조 : 순서 X. idx 사용이 제한됨
    
    > 선형 : 스택, 큐, 덱, 연결리스트
    > 
    > 비선형 : 딕셔너리, set, 해쉬, **그래프**
  
  - 원소들 간에 1:n 관계를 가지는 자료구조
  
  - 원소들 간에 **계층관계**를 가지는 계층형 자료구조
  
  - 상위 원소에서 하위 원소로 내려가면서 확장되는 트리(나무)모양의 구조

- 정의
  
  - 한 개 이상의 노드로 이루어진 유한 집합
    
    > - 노드 중 취상위 노드를 루트(root)라고 함
    > 
    > - 나머지 노드들은 n(>=0)개의 분리 집합으로 분리
  
  - 각각 하나의 트리가 되며(재귀적 정의) 루트의 서브트리(subtree)라 함.

- 용어
  
  - **노드**(node) : 트리의 원소
  
  - **간선**(edge) : 노드를 연결하는 선. 부모 노드와 자식 노드를 연결
  
  - **루트 노드**(root node) : 트리의 시작 노드
  
  - **형제 노드**(sibling nod) : 같은 부모 노드의 자식 노드들
    
    > 형제 노드끼리 연결할 수 없음 (트리는 사이클이 없음)
  
  - **조상 노드** : 간선을 따라 루트 노드까지 이르는 경로에 있는 모든 노드들
  
  - **자손 노드** : 서브 트리에 있는 하위 레벨의 노드들
  
  - **차수**(degree) : 노드에 연결된 자식 노드의 수
    
    - 단말 노드(리프 노드) : 차수가 0인 노드. 자식 노드가 없는 노드
  
  - **높이** : 루트에서 노드에 이르는 간선의 수 노드의 레벨 (위에서부터 0)

---

## 이진 트리

모드 노드들이 2개의 서브트리를 갖는 특별한 형태의 트리

- 특성
  
  - 각 노드가 자식 노드를 최대 2개까지만 가질 수 있는 트리
    
    > 왼쪽 자식 노드(left child node), 오른쪽 자식 노드(right child node)
  
  - 레벨 i에서의 노드의 최대 개수는 2**i개
  
  - h+1 <= 높이가 h인 이진 트리가 가질 수 있는 노드 <= 2**(h+1)-1

- **<mark>포화 이진 트리</mark>**(Full Binary Tree)
  
  - 모든 레벨에 노드가 포화상태로 차 있는 이진 트리
  
  - 높이가 h일 때, 최대의 노드 개수인 2**(h+1)-1의 노드를 가진 이진 트리
  
  - 루트를 1번으로 하여 2**(h+1)-1까지 정해진 위치에 대한 노드 번호를 가짐

- **<mark>완전 이진 트리</mark>**(Commplete Binary Tree)
  
  - 포화 이진 트리의 노드 번호 1번부터 n번까지 빈 자리가 없는 이진 트리

- **<mark>편향 이진 트리</mark>**(Skewed Binary Tree)
  
  - 높이 h에 대한 최소 개수의 노드를 가지면서 한쪽 방향의 자식 노드만을 가진 이진 트리
    
    > 왼쪽 편향 이직 트리, 오른쪽 편향 이진 트리

---

## 순회(traversal)

트리의 각 노드를 중복되지 않게 전부 방문(visit)하는 것

- **전위순회**(preorder traversal) : VLR
  
  부모노드 방문 후, 자식노드를 **좌**, 우 순서로 방문

- **중위순회**(inorder traversal) : LVR
  
  왼쪽 자식노드, 부모노드, 오른쪽 자신노드 순으로 방문

- **후위순회**(postorder traversal) : LRV
  
  자식노드를 좌우 순서로 방문한 후, 부모노드로 방문

---

## 연습문제

```python
'''
13
1 2 1 3 2 4 3 5 3 6 4 7 5 8 5 9 6 10 6 11 7 12 11 13
'''
# 전위 순회(나 -> 왼쪽 -> 오른
def pre_order(T):
    if T:
        print(T, end = ' ')
        pre_order(left[T])
        pre_order(right[T])

N = int(input())        # 1번부터 N번까지인 정점
E = N-1
arr = list(map(int, input().split()))
left = [0]*(N+1)        # 부모를 인덱스로 왼쪽 자식번호 저장
right = [0]*(N+1)       # 부모를 인덱스로 오른쪽 자식번호 저장
# ex) left[3] = 2 -> 3번 부모의 왼쪽 자식은 2다.
par = [0]*(N+1)         # 자식을 인덱스로 부모 저장

for i in range(E):
    parent, child = arr[i*2], arr[i*2+1]
# for i in range(0,E*2, 2):
#         p, c = arr[i], arr[i + 1]
    if left[parent]==0:          # 왼쪽자식이 없으면
        left[parent] = child
    else:                        # 왼쪽자식은 없는데, 오른쪽 자식이 없다면
        right[parent] = child
    par[child] = parent

child = N
while par[child]!=0:        # 부모가 있으면
    child = par[child]          # 부모를 새로운 자식으로 두고
root = child                # 더이상 부모가 없으면 root
print(root)
pre_order(root)
```

---

## 어려운 버전

```python
from collections import deque

class TreeNode:
    def __init__(self, key):
        self.key = key  # 노드의 값
        self.left = None  # 왼쪽 자식 노드를 가리킴
        self.right = None  # 오른쪽 자식 노드를 가리킴

class BinaryTree:
    def __init__(self):
        self.root = None  # 트리의 루트 노드

    # 새로운 노드를 삽입하는 함수 (레벨 순서 삽입)
    def insert(self, key):
        new_node = TreeNode(key)
        if self.root is None:
            self.root = new_node
            return

        # 레벨 순서로 트리를 탐색하기 위해 큐를 사용
        queue = deque([self.root])

        while queue:
            node = queue.popleft()

            # 왼쪽 자식이 비어있으면 삽입
            if node.left is None:
                node.left = new_node
                break
            else:
                queue.append(node.left)

            # 오른쪽 자식이 비어있으면 삽입
            if node.right is None:
                node.right = new_node
                break
            else:
                queue.append(node.right)

    def inorder_traversal(self):
        # 중위 순회를 통해 트리의 노드들을 출력하는 함수
        return self._inorder_traversal(self.root, [])

    def _inorder_traversal(self, node, result):
        if node:
            self._inorder_traversal(node.left, result)
            result.append(node.key)
            self._inorder_traversal(node.right, result)
        return result

# 예제 사용법
if __name__ == "__main__":
    tree = BinaryTree()
    tree.insert(50)
    print("Inorder Traversal:", tree.inorder_traversal())
    tree.insert(30)
    print("Inorder Traversal:", tree.inorder_traversal())
    tree.insert(20)
    print("Inorder Traversal:", tree.inorder_traversal())
    tree.insert(40)
    print("Inorder Traversal:", tree.inorder_traversal())
    tree.insert(70)
    print("Inorder Traversal:", tree.inorder_traversal())
    tree.insert(60)
    print("Inorder Traversal:", tree.inorder_traversal())
    tree.insert(80)

    print("Inorder Traversal:", tree.inorder_traversal())
```

---

## 인접리스트

```python
'''
13
1 2 1 3 2 4 3 5 3 6 4 7 5 8 5 9 6 10 6 11 7 12 11 13
'''

def dfs(node):
    if node == -1:
        return

    preorder.append(node)
    dfs(graph[node][0])
    inorder.append(node)
    dfs(graph[node][1])
    postorder.append(node)



N = int(input())
E = N - 1
arr = list(map(int, input().split()))
graph = [[] for _ in range(N + 1)]
# append 를 통해 갈 수 있는 경로를 추가하기
for i in range(E):
    p, c = arr[i * 2], arr[i * 2 + 1]
    graph[p].append(c)

# 없는 경우 -1로 데이터를 저장하기 위한 코드("좌우 경로가 있는가 ?")
# 탐색 시 index 오류를 방지하기 위해 없는 경로를 -1로 저장하였습니다.
for i in range(N + 1):
    while len(graph[i]) < 2:
        graph[i].append(-1)


preorder = []
inorder = []
postorder = []

dfs(1)

print(*inorder)
print(*preorder)
print(*postorder)
```
