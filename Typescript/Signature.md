# 호출 시그니처
```ts
interface getLikeNumber { // 호출 시그니처
	(like: number): number;
}

interface Post {
	id: number;
	title: string;
	getLikeNumber: getLikeNumber
}

const post1: Post = {
	id: 1,
	title: 'post 1',
	getLikeNumber(like: number) {
		return like
	}
}
```
# 인덱스 시그니처
## 객체 인덱스 시그니처
```ts
interface Post {
	id: number;
	title: string;
}

const post1: Post = {
	id: 1,
	title: 'post 1'
}

post1['description'] = 'post1 description';   // 오류
post1['pages'] = 300;                         // 오류
```
- 계속 속성이 더해져서 post1 객체에 모든 속성의 이름을 알지 못할 때 사용
```ts
interface Post {
	[key: string]: unknown;
	// ...
}
```
## 배열 인덱스 시그니처
```ts
interface Names {
	[item: number]: string; 
}

const userNames = ['John', 'Kim', 'Joe']
userNames[0] === 'John'
```