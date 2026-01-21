# 함수 오버로딩
 - 매개변수가 다를 때 오버로딩을 이용해서 두 함수를 하나로 만들어줄 수 있음
 ```ts
 function add1(a: string, b:string): string {
	 return a + b;
 }
 
 function add2(a: number, b: number): number {
	 return a + b;
 }
 ```
- 타입 선언
```ts
function add(a: string, b: string): string;
function add(a: number, b: number): number;
```
- 함수 구현
```ts
function add(a: any, b: any): any {
	return a + b;
}

add("hello", "world");
add(1, 1);
```
