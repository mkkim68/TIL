# 0. Why Styled Components
- 기존의 방식은 불편한 점이 많음
	1. 태그에 style 적용 -> 너무 한정적이고 불편
	2. module.css 사용 -> class 이름을 일일히 복붙해야하고 class 여러개를 줘야할때 불가
# 1. Our First Styled Component
```
npm i styled-components
```
- styled-components 설치
```jsx
import styled from "styled-components";
```
- App.js 에 styled 불러오기
```jsx
const Father = styled.div`
  display: flex;
`;

function App() {
  return (
    <Father>
      ...
	</Father>
  );
}
```
- `styled.` 뒤에 element를 작성 후 백틱 사용
- 백틱 안에 요소의 style 속성을 정의하면 됨
- 그리고 정의한 변수명을 html 요소처럼 사용 가능
# 2. Adapting and Extending
## 특정 컴포넌트 설정
- 특정 style 요소만 유동적으로 변경하고 싶을 때
	- props 사용
```jsx
const Box = styled.div`
  background-color: ${(props) => props.bgColor};
  width: 100px;
  height: 100px;
`;

function App() {
  return (
    <Father>
      <Box bgColor="teal" />
      <Box bgColor="tomato" />
    </Father>
  );
}
```
## 컴포넌트 확장
- 기존의 컴포넌트에 원하는 style 속성을 추가하기
```jsx
const Box = styled.div`
  background-color: ${(props) => props.bgColor};
  width: 100px;
  height: 100px;
`;

const Circle = styled(Box)`
  border-radius: 50px;
`;

function App() {
  return (
    <Father>
      <Box bgColor="teal" />
      <Circle bgColor="tomato" />
    </Father>
  );
}
```
- 원래 `Box`에 있는 props도 `Circle`에서 사용 가능하다
# 3. 'As' and Attrs
## As
```jsx
const Btn = styled.button`
  color: white;
  background-color: tomato;
  border: 0;
  border-radius: 15px;
`;

function App() {
  return (
    <Father>
      <Btn>Login</Btn>
      <Btn as="a" href="/">
        Login
      </Btn>
    </Father>
  );
}
```
- 한 component를 `as`를 이용해 다른 html 요소로 생상
## Attrs
```jsx
const Input = styled.input.attrs({ required: true, minLength: 10 })`
  background-color: tomato;
`;
```
- `attrs`를 사용함으로써 html 태그 안에 들어가야할 속성들 정의 가능
# 4. Animations and Pseudo Selectors
## Animation
- styled-components를 이용해서 애니메이션 만들기
```jsx
import styled, { keyframes } from "styled-components";

const animation = keyframes`
  0% {
    transform:rotate(0deg);
    border-radius: 0px;
  }
  50% {
    transform:rotate(180deg);
    border-radius: 100px;
  }
  100% {
    transform:rotate(360deg);
    border-radius: 0px;
  }
`;
```
- `keyframes` import 후 css 작성
## Pseudo Selectors
```jsx
const Box = styled.div`
  height: 200px;
  width: 200px;
  background-color: tomato;
  display: flex;
  justify-content: center;
  align-items: center;
  span {
    font-size: 35px;
    &:hover {
      font-size: 100px;
    }
  }
  &:hover {
    animation: ${animation} 1s linear infinite;
  }
`;

function App() {
  return (
    <Wrapper>
      <Box>
        <span>⚾</span>
      </Box>
    </Wrapper>
  );
}
```
- `Box` 내에 `span` 을 styled 내에서 선택 가능
- `hover` 같은 특성도 가능
	- `&` 을 이용해서 현재 요소 선택 후 css 작성
# 5. Pseudo Selectors part 2
```jsx
const Emoji = styled.span`
  font-size: 35px;
`;

const Box = styled.div`
  height: 200px;
  width: 200px;
  background-color: tomato;
  display: flex;
  justify-content: center;
  align-items: center;
  ${Emoji} {
    &:hover {
      font-size: 100px;
    }
  }
  &:hover {
    animation: ${animation} 1s linear infinite;
  }
`;

function App() {
  return (
    <Wrapper>
      <Box>
        <Emoji>⚾</Emoji>
      </Box>
    </Wrapper>
  );
}
```
- 기본 html 요소를 사용하면 다른 요소로 수정했을 때 pseudo selector를 이용해서 적용한 css가 반영이 안됨
	- styled 변수를 사용해서 pseudo selector를 사용하면 html 요소가 바뀌어도 계속 적용이 된다
# 7. Themes
```jsx
// index.js
import { ThemeProvider } from "styled-components";

const darkTheme = {
  textColor: "whitesmoke",
  backgroundColor: "#111",
};

const lightTheme = {
  textColor: "#111",
  backgroundColor: "whitesmoke",
};

const root = ReactDOM.createRoot(document.getElementById("root"));
root.render(
  <React.StrictMode>
    <ThemeProvider theme={darkTheme}>
      <App />
    </ThemeProvider>
  </React.StrictMode>
);
```
- `ThemeProvider` 이용
- 테마를 두 개 작성
	- 안의 내용은 똑같은 property로 작성해야함
- `App`을 `ThemeProvider`로 감싸줌
	- `ThemeProvider`에 `theme`이라는 props가 무조건 들어가야함 (테마를 넣어줌)
```jsx
// App.js
const Title = styled.h1`
  color: ${(props) => props.theme.textColor};
`;

const Wrapper = styled.div`
  display: flex;
  height: 100vh;
  width: 100vw;
  justify-content: center;
  align-items: center;
  background-color: ${(props) => props.theme.backgroundColor};
`;

function App() {
  return (
    <Wrapper>
      <Title>Hello</Title>
    </Wrapper>
  );
}
```
- `ThemeProvider`의 props를 사용 가능함
- `index.js`에서 `theme` props만 바꾸면 `App.js`를 수정하지 않아도 테마가 바뀜
