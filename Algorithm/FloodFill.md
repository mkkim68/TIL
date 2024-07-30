# 개념
- SeedFill이라고도 불린다.
- 배열에서 어떤 칸과 연결된 영역을 찾는 알고리즘
# BFS로 구현
- `idx` : 구역화
- 칸에서 같은 값을 가지고 있다면 같은 인덱스 값 부여
- `dr` : 열
- `dc` : 행
```python
from collections import deque

def flood_fill(r, c, idx):
	q = deque()
	visited = [[0] * N for _ in range(N)]
	q.append((r, c))
	indexedMap[r][c] = idx
	while q:
		nowr, nowc = q.popleft()
		for dr, dc in delta:
			nr, nc = dr + nowr, dc + nowc
			if 0 <= nr < N and 0 <= nc < N and visited[nr][nc] == 0 and board[nr][nc] != 0:
				visited[nr][nc] = 1
				indexedMap[nr][nc] = idx
				q.append((nr, nc))
				
```