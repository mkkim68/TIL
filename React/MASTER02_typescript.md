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
# 3. Optional Props
- 필수가 아닌 props 사용
```ts
interface CircleProps {
  bgColor: string;
  borderColor?: string; // ? 사용 -> 선택적 props
}
```
- 하지만 Circle 내부의 Container의 borderColor는 필수임
	- 그냥 사용하면 에러가 난다!
```ts
interface ContainerProps {
  bgColor: string;
  borderColor: string;
}

const Container = styled.div<ContainerProps>`
  width: 200px;
  height: 200px;
  background-color: ${(props) => props.bgColor};
  border-radius: 100px;
  border: 1px solid ${(props) => props.borderColor};
`;

function Circle({ bgColor, borderColor }: CircleProps) {
  return <Container bgColor={bgColor} borderColor={borderColor ?? bgColor} />;
}
```
- `borderColor={borderColor ?? bgColor}` : ?? 뒤에 default 
- 함수 인자에서도 default 값을 정해줄 수 있음(ES6)
	- `인자명 = 디폴트로 원하는 값`
# 4. State
 - state + typescript
```ts
  const [value, setValue] = useState<number|string>(1);
```
- `value`가 number, string 모두 될 수 있다는 의미
- 보통 state는 같은 타입으로 계속 쓰기 때문에 이건 잘 쓸 일이 없다.
# 5. Forms
```ts
import React, { useState } from "react";

function App() {
  const [value, setValue] = useState("");
  const [message, setMessage] = useState("");
  const onChange = (event: React.FormEvent<HTMLInputElement>) => {
    const {
      currentTarget: { value },
    } = event;
    setValue(value);
  };
  const onSubmit = (event: React.FormEvent<HTMLFormElement>) => {
    event.preventDefault();
    setMessage("Hello, " + value);
  };
  return (
    <div>
      <h1>{message}</h1>
      <form onSubmit={onSubmit}>
        <input
          value={value}
          onChange={onChange}
          type="text"
          placeholder="username"
        />
        <button>Log in</button>
      </form>
    </div>
  );
}
```
- event를 보호 가능
	- `event: React.FormEvent<HTMLInputElement>` 형식
# 6. Themes
- `styled-components` 설치
- `styled.d.ts` 파일 생성
```ts
// styled.d.ts

// import original module declarations
import "styled-components";

// and extend them!
declare module "styled-components" {
  export interface DefaultTheme {
    textColor: string;
    bgColor: string;
  }
}
```
- `theme.ts` 파일 생성
```ts
import { DefaultTheme } from "styled-components/dist/types";

export const lightTheme: DefaultTheme = {
  bgColor: "white",
  textColor: "black",
};

export const dartTheme: DefaultTheme = {
  bgColor: "black",
  textColor: "white",
};
```
- `DefaultTheme` 내의 속성만 정의해서 테마 뚝딱
```ts
// index.tsx
import React from "react";
import ReactDOM from "react-dom/client";
import App from "./App";
import { ThemeProvider } from "styled-components";
import { lightTheme } from "./theme";

const root = ReactDOM.createRoot(
  document.getElementById("root") as HTMLElement
);
root.render(
  <React.StrictMode>
    <ThemeProvider theme={lightTheme}>
      <App />
    </ThemeProvider>
  </React.StrictMode>
);
```
- `ThemeProvider` 와 `lightTheme` 이용
```ts
import styled from "styled-components";

const Container = styled.div`
  background-color: ${(props) => props.theme.bgColor};
`;
const H1 = styled.h1`
  color: ${(props) => props.theme.textColor};
`;

function App() {
  return (
    <div>
      <Container>
        <H1>hi</H1>
      </Container>
    </div>
  );
}
```
- [!] 원래 theme 속성 부분 오타나면 빨간 줄 떠야되는데 안뜸;;; 왜지
	- 변수명 오타나면 적용 안되긴 함 (JS랑 같아짐)