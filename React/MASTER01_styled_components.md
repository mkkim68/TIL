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