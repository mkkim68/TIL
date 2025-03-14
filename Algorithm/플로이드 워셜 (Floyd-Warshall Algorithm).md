- 모든 지점에서 다른 모든 지점까지의 최단 경로를 모두 구해야하는 경우
- 2차원 테이블에 최단 거리 정보 저장
- 시간복잡도 O(N³)
```python
INF = int(1e9)

N = int(input()) # 노드 개수
M = int(input()) # 간선 개수

graph = [[INF] * (N+1) for _ in range(N+1)]

for a in range(1, N+1):
	for b in range(1, N+1):
		if a == b:
			graph[a][b] = 0

for _ in range(M):
	a, b, d = map(int, input().split())
	graph[a][b] = d

for k in range(1, N+1):
	for a in range(1, N+1):
		for b in range(1, N+1):
			graph[a][b] = min(graph[a][b], graph[a][k] + graph[k][b])

for a in range(1, N+1):
	for b in range(1, N+1):
		if graph[a][b] == INF:
			print('INFINITY', end=' ')
		else:
			print(graph[a][b], end=' ')
	print()
```