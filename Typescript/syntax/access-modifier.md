# 접근제어자
```ts
class Post {
	id: number = 0; // public
	title: string = "";  // public
	constructor(id: number, title: string) {
		this.id = id;
		this.title = title;
	}
	
	getPost() {
		return `postId ${this.id}, postTitle: ${this.title}`;
	}
}

const post: Post = new Post(1, "title 1");
```

| name      | description                |
| --------- | -------------------------- |
| public    | default, 어디서나 접근 가능        |
| protected | 클래스 내, 상속받은 자식 클래스에서 접근 가능 |
| private   | 클래스 내에서만 접근 가능             |
## public
```ts
console.log(post.id); // 1
console.log(post.title); // "title 1"
```
## protected
```ts
console.log(post.id); // 보호된 속성
console.log(post.title); // 보호된 속성
```
- 하위 클래스에서 사용 가능
```ts
class Post {
	id: number = 0;
	protected title: string = "";
	constructor(id: number, title: string) {
		this.id = id;
		this.title = title;
	}
	
	getPost() {
		return `postId ${this.id}, postTitle: ${this.title}`;
	}
}

class PostB extends Post {
	getPost() {
		return this.title;
	}
}
```
## private
```ts
class Post {
	private id: number = 0;
	protected title: string = "";
	constructor(id: number, title: string) {
		this.id = id;
		this.title = title;
	}
	
	getPost() {
		return `postId ${this.id}, postTitle: ${this.title}`;
	}
}

class PostB extends Post {
	getPost() {
		return this.id; // error
	}
}
```
## 간단하게 표현 가능
```ts
class Post {
	constructor(
		public id: number = 0,
		protected title: string
	) {}
}
```
- public 생략 불가
- 초기값 설정 가능