# javascript
```js
let farm = [];
let visited = [];

const row = [0, 0, -1, 1];
const col = [1, -1, 0, 0];

const dfs = (j, k, N, M) => { // j: 행, k: 열
	visited[j][k] = true;
	for (let i = 0; i < 4; i++) {
		newJ = j + row[i];
		newK = k + col[i];
		if (newJ >= 0 && newJ < N && newK >= 0 && newK < M) {
			if (farm[newJ][newK] === 1 && visited[newJ][newK] === false) {
			dfs(newJ, newK, N, M);
			}
		}
	}
};
```