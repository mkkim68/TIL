# Infer
```ts
type SomeType = T extends infer U ? U : Y;
```
- Typescript가 U의 타입을 추론해서 T가 U에 할당 가능하면 SomeType은 U 아니면 Y 
- T가 U에 최대한 할당 가능하게 U의 타입을 Typescript에게 추론하라고 하는 것
- `extends`와만 함께 사용 가능
## 예제 1
```ts
type AType<T> = T extends infer R ? R : null
const a: AType<number> = 1; // number
```
## 예제 2
```ts
type BType<T> = T extends {a: infer A; b: 1} ? A : any;
type Inferred = BType<{a: 'hi'; b: 1}>; // 'hi'
```
## 예제 3
```ts
type CType<T> = T extends {a: infer A; b: infer B} ? A & B : any;
type Inferred2 = CType<{a: {someProps: 1}; b: {someBProps: 2}}>
// { someProps: 1 } & { someBProps: 2 }
```
