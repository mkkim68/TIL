# 0. Introduction
- Typescript란?
	- JS를 기반으로 한 프로그래밍 언어
	- strongly-typed된 언어
- 기존 js에서는 오류를 안 알려줌 (undefined된 변수 등)
	- 이런 단점을 커버 (변수나 인자의 type을 설정해줘야함)
```typescript
const plus = (a:number, b:number) => a + b;
```
- 인자의 type을 설정해야함
# 1. DefinitelyTyped
## 프로젝트 새로 설치
```
npx create-react-app my-app --template typescript
```
- styled-components 설치
```
npm i styled-components --legacy-peer-deps
```
## 기존 프로젝트 변경
- 확장자 `.js` -> `.tsx`
- react에서 사용하는 몇 라이브러리를 typescript는 인식하지 못할 수 있음
```
npm install @types/styled-components
```
- 이 명령어로 typescript에서도 styled-components 사용 가능
## DefinitelyTyped Repository
- npm package를 모아놓은 github 레포지토리
- 사용자가 직접 typescript에서 사용하고 싶으면 올려도됨
# 2. Typing the Props
- props를 그냥 사용하면 에러남
	- interface를 해줘야함
## interface
```ts
// Circle.tsx
import styled from "styled-components";

interface ContainerProps {
  bgColor: string;
}

const Container = styled.div<ContainerProps>`
  width: 200px;
  height: 200px;
  background-color: ${(props) => props.bgColor};
  border-radius: 100px;
`;

interface CircleProps {
  bgColor: string;
}

function Circle({ bgColor }: CircleProps) {
  return <Container bgColor={bgColor} />;
}

export default Circle;

interface PlayerShape {
  name: string;
  age: number;
}

const sayHello = (playerObj: PlayerShape) =>
  `Hello ${playerObj.name}. You are ${playerObj.age} years old`;

```
- js에서 뜨지 않은 오류가 뜬다