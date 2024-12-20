# BFS

---

### BFS(너비 우선 탐색) 개념:

- BFS는 그래프나 트리를 탐색하는 알고리즘  
- 시작 노드에서 가까운 노드부터 차례대로 탐색  
- 같은 레벨의 모든 노드를 탐색한 후 다음 레벨로 넘어감  

### 큐(Queue) 사용:

- BFS는 큐 자료구조를 사용하여 구현  
- 큐는 선입선출(FIFO) 방식으로 동작  
- 탐색할 노드를 큐에 넣고, 순서대로 꺼내며 탐색  

### 방문 체크:

- 이미 방문한 노드를 다시 방문하지 않도록 방문 여부를 체크  
- `visited` 리스트를 사용하여 각 노드의 방문 상태를 관리  

### 인접 노드 탐색:

- 현재 노드와 연결된 모든 인접 노드를 확인  
- 방문하지 않은 인접 노드를 큐에 추가  

### 그래프 표현:

- 이 코드에서는 인접 행렬을 사용하여 그래프를 표현  
- `G[i][j] = 1`은 노드 i와 j가 연결되어 있음을 의미  

### 탐색 순서:

- 시작 노드부터 가까운 순서대로 노드를 탐색  
- 결과적으로 시작 노드로부터의 거리 순으로 노드를 방문  

### 구현 과정:

- 시작 노드를 큐에 넣고 방문 표시를 - 큐가 빌 때까지 다음 과정을 반복:  
  a) 큐에서 노드를 하나 꺼낸다.  
  b) 꺼낸 노드의 인접 노드 중 방문하지 않은 노드를 모두 큐에 넣고 방문 표시를 한다.

### 1차원 예제:

```python
'''
7 8
4 2 1 2 1 3 5 2 4 6 5 6 6 7 3 7
'''

def bfs(s, V):  # 시작정점 s, 마지막 정점 V
    visited = [0] * (V+1)   # visited 생성
    q = []          # 큐 생성
    q.append(s)     # 시작점 인큐
    visited[s] = 1  # 시작점 방문표시
    while q:        # 큐에 정점이 남아있으면 front != rear
        t = q.pop(0)    # 디큐
        print(t)        # 방문한 정점에서 할일
        for w in adj_l[t]:  # 인접한 정점 중 인큐되지 않은 정점 w가 있으면
            if visited[w]==0:
                q.append(w)     # w인큐, 인큐되었음을 표시
                visited[w] = visited[t] + 1

V, E = map(int, input().split()) # 1번부터 V번 정점, E개의 간선
arr = list(map(int, input().split()))
# 인접리스트 -------------------------
adj_l = [[] for _ in range(V+1)]
for i in range(E):
    v1, v2 = arr[i*2], arr[i*2+1]
    adj_l[v1].append(v2)
    adj_l[v2].append(v1)    # 방향이 없는 경우
# 여기까지 인접리스트 -----------------
bfs(1, 7)
```

### 2차원 예제:

```python
def bfs(s, V):  # 시작정점 s, 마지막 정점 V
    visited = [0] * (V + 1)  # visited 생성
    q = []  # 큐 생성
    q.append(s)  # 시작점 인큐
    visited[s] = 1  # 시작점 방문표시
    while q:  # 큐가 비어있지 않은 동안 반복
        t = q.pop(0)  # 디큐
        print(t)  # 방문한 정점 출력
        for w in range(1, V + 1):  # 모든 노드에 대해
            # 현재 노드와 연결되어 있고, 아직 방문하지 않은 노드라면
            if adj_m[t][w] == 1 and visited[w] == 0:
                q.append(w)  # w 인큐, 인큐 되었음을 표시
                visited[w] = visited[t] + 1
    # print(visited)


V, E = map(int, input().split())  # 1번부터 V번 정점, E개의 간선
arr = list(map(int, input().split()))  # 간성 정보

# 인접행렬
adj_m = [[0] * (V + 1) for _ in range(V + 1)]

for i in range(E):
    v1, v2 = arr[i * 2], arr[i * 2 + 1]
    adj_m[v1][v2] = 1
    adj_m[v2][v1] = 1  # 방향이 없는 경우

bfs(1, V)
```
