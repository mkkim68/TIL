- 간선 가중치가 0 또는 1만 있는 그래프에서 최단 거리를 구하는 BFS 변형
## 조건
- 간선 가중치가 0 또는 1
- 음수 없음
## 목표
- 어떤 정점까지의 최소 비용
## 다익스트라와 비교
### 다익스트라
- 우선순위 큐 사용
- `O((N+M) log N)`
### 0-1 BFS
- deque 사용
- `O(N+M)`
## 코드
```python
from collections import deque

dist = [INF] * N
dq = deque()

dist[start] = 0
dq.append(start)

while dq:
    u = dq.popleft()
    for v, cost in edges[u]:
        if dist[v] > dist[u] + cost:
            dist[v] = dist[u] + cost
            if cost == 0:
                dq.appendleft(v)
            else:
                dq.append(v)
```
- 가중치 0일땐 `appendleft()`
- 가중치 1일땐 `append()`
- 큐에서 꺼내는 순서가 항상 거리 증가 순서가 됨
## 백준
### [32197 절연 구간 최소화](https://www.acmicpc.net/problem/32197)
```python
import sys  
from collections import deque  
input = sys.stdin.readline  
  
N, M = map(int, input().split())  
edges = [[] for _ in range(N+1)]  
for _ in range(M):  
    s, e, t = map(int, input().split())  
    edges[s].append([e, t])  
    edges[e].append([s, t])  
  
A, B = map(int, input().split())  
  
INF = 1e9  
dist = [[INF, INF] for _ in range(N+1)]  
q = deque()  
q.append([A, 0])  
q.append([A, 1])  
dist[A][0] = 0  
dist[A][1] = 0  
  
while q:  
    now, way = q.popleft()  
  
    for n, t in edges[now]:  
        cost = abs(way-t)  
        next_cnt = dist[now][way] + cost  
  
        if dist[n][t] <= next_cnt:  
            continue  
  
        dist[n][t] = next_cnt  
        if cost == 0:  
            q.appendleft([n, t])  
        else:  
            q.append([n, t])  
  
  
print(min(dist[B]))
```