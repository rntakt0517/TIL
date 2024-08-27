# DP

[동적 계획 알고리즘](#동적-계획-알고리즘)

[피보나치 수 DP 적용](#피보나치-수-dp-적용)

[DFS 깊이우선탐색](#dfs-깊이우선탐색)

---

## 동적 계획 알고리즘

Dynamic Programming : 최적화 문제를 해결하는 알고리즘

1. 먼저 입력 크기가 작은 부분 문제들을 모두 해결

2. 그 해들을 이용하여 보다 큰 크기의 부분 문제들을 해결

3. 최종적으로 원래 주어진 입력의 문제를 해결

> **<mark>구현 방식</mark>**
> 
> - recursive 방식
> 
> - iterative 방식
> 
> - memoization을 재귀적 구조에 사용하는 것보다 반복적 구조로 DP를 구현하는 것이 성능 면에서 보다 효율적
> 
> - 재귀적 구조는 내부에 시스템 호출 스택을 사용하는 오베헤드가 발생하기 때문

---

## 피보나치 수 DP 적용

피보나치 수는 부분 문제의 답으로부터 본 문제의 답을 얻을 수 있으므로 최적 부분 구조

1. 문제를 부분 문제로 분할

2. 부분 문제로 나누는 일을 끝냈으면 가장 작은 부분 문제부터 해 구하여 테이블에 저장

3. 테이블에 저장된 부분 문제의 해를 이용하여 상위 문제 해결

```python
def fibo(n):
    # n이 0 또는 1일 때는 그 값을 바로 반환
    if n <= 1:
        return n
    # n+1 크기의 리스트를 만들어서 DP 테이블을 초기화
    dp = [0] * (n + 1)
    dp[0] = 0
    dp[1] = 1
    # DP 테이블을 사용하여 피보나치 수를 계산
    for i in range(2, n + 1):
        dp[i] = dp[i - 1] + dp[i - 2]
    return dp[n]
# n=7로 피보나치 수를 계산
n = 7
print(f"{fibo(n)}")
```

---

## DFS 깊이우선탐색

> 비선형구조인 그래프 구조는 그래프로 표현된 모든 자료를 빠짐없이 검색하는 것이 중요
> 
> - **깊이 우선 탐색(Depth First Search, <mark>DFS</mark>)**
> 
> - **너비 우선 탐색(Breadth First Search, <mark>BFS</mark>)**

- 막히면 가장 마지막에 만났던 갈리길의 정점으로 되돌아가서 다시 깊이 우선 탐색 반복

- 후입선출 구조의 스택 사용

- 예시 문제

![image](https://github.com/user-attachments/assets/178a3c73-cacb-40b0-afb2-5fa6da163d92)

```python
'''
1
7 8
1 2 1 3 2 4 2 5 4 6 5 6 6 7 3 7
'''
# 함수 정의
def DFS(s, l):                  # s시작정점, l정점개수(1번부터인 정점의 마지막 정점)
    visited = [0]*(l+1)         # 방문한 정점을 표시
    stack = []                  # 스택생성
    print(s, end=' ')
    visited[s] = 1              # 시작정점 방문표시
    v = s
    while True:
        for w in adjL[v]:       # v에 인접하고, 방문안한 w가 있으면
            if visited[w] == 0:
                stack.append(v) # push(v) 현재 정점을 push하고
                v = w           # w에 방문
                print(v, end=' ')
                visited[w] = 1  # w에 방문 표시
                break           # for w, v부터 다시 탐색
        else:                   # 남은 인접정점이 없어서 break가 걸리지 않은 경우
            if stack:           # 이전 갈림길을 스택에서 꺼내서... if TOP > -1
                v = stack.pop()
            else:               # 되돌아갈 곳이 없으면 남은 갈림길이 없으면 탐색종료
                break           # while True:
# 실행 시작
T = int(input())
for tc in range(1, T+1):
    V, E = map(int, input().split())        # 정점개수와 ? 입력 받기
    adjL = [[]for _ in range(V+1)]          # 연결 정보 받을 리스트 생성
    arr = list(map(int, input().split()))   # 연결 정보 받기
    # 연결 정보 옮기기
    for i in range(E):
        v1, v2 = arr[i*2], arr[i*2+1]
        adjL[v1].append(v2)
        adjL[v2].append(v1)
    DFS(1, V)                               # 1 2 4 6 5 7 3 
```
