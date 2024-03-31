> 가중치가 음수가 가능한 경우 사용 (다익스트라는 가중치가 모두 양수)

-  (정점-1)번의 매 단계마다 모든 간선을 전부 확인하면서 모든 노드간의 최단 거리를 구함
- 음수 간선이 있어도 최적의 해를 찾을 수 있다.
- 시간 복잡도가 느림
## 알고리즘
1. 출발 노드 설정
2. 최단 거리 테이블 초기화
3. 다음의 과정을 V-1번 반복
	1. 모든 간선 E개를 하나씩 확인
	2. 각 간선을 거쳐 다른 노드로 가는 비용을 계산하여 최단 거리 테이블을 갱신
- 만약 음수 간선 순환이 발생하는지 체크하고 싶으면 3번 과정을 한 번 더 수행
	- *음수 간선 순환이 존재하면 비용을 무한히 줄일 수 있다*
## 코드
### 백준 11657 [타임머신](https://www.acmicpc.net/problem/11657)
```python
import sys  
input = sys.stdin.readline  
INF = int(1e9)  
  
  
def bellman_ford(start):  
    # 시작 노드 초기화  
    distance[start] = 0  
    # 전체 v-1번의 라운드를 반복  
    for i in range(V):  
        # 매 반복마다 모든 간선 확인  
        for j in range(E):  
            cur_node = adj[j][0]  
            next_node = adj[j][1]  
            weight = adj[j][2]  
            # 현재 간선을 거쳐서 다른 노드로 이동하는 거리가 더 짧은 경우  
            if distance[cur_node] != INF and distance[cur_node] + weight < distance[next_node]:  
                distance[next_node] = distance[cur_node] + weight  
                # v번째 라운드에서도 값이 갱신된다면 음수 순환이 존재  
                if i == V-1:  
                    return True  
    return False  
  
V, E = map(int, input().split())  
adj = []  
distance = [INF] * (V+1)  
  
for _ in range(E):  
    s, e, w = map(int, input().split())  
    adj.append([s, e, w])  
  
ans = bellman_ford(1)  
if ans:  
    print(-1)  
else:  
    for i in range(2, V+1):  
        if distance[i] == INF:  
            print(-1)  
        else:  
            print(distance[i])
            
```
### 백준 1865 [웜홀](https://www.acmicpc.net/problem/1865)
```python
import sys  
input = sys.stdin.readline  
INF = int(1e9)  
  
  
def bf(start):  
    distance[start] = 0  
    for i in range(N):  
        for j in range(len(adj)):  
            now, to, cost = adj[j][0], adj[j][1], adj[j][2]  
            if distance[now] + cost < distance[to]:  
                distance[to] = distance[now] + cost  
                if i == N-1:  
                    return "YES"  
    return "NO"  
  
  
T = int(input())  
for tc in range(1, T+1):  
    N, M, W = map(int, input().split())  # 노드 개수, 도로 개수, 웜홀 개수  
    adj = []  
    for _ in range(M):  # 도로  
        s, e, w = map(int, input().split())  
        adj.append([s, e, w])  
        adj.append([e, s, w])  
    for _ in range(W):  # 웜홀  
        s, e, w = map(int, input().split())  
        w = -w  
        for arr in adj:  
            if arr[0] == s and arr[1] == e:  
                adj.remove(arr)  
                break  
        adj.append([s, e, w])  
    distance = [INF] * (N + 1)  
    ans = bf(1)  
    print(ans)  
```
- 1과 연결되지 않은 노드가 있을 수 있음
	-  그 노드에서 시작해서 음수 간선 순환 가능할수도 있다
	- 따라서 위의 코드와 다르게` distance[now] != INF` 의 조건을 뺴줌