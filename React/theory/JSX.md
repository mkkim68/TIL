# Javascript Syntax eXtension
- 자바스크립트의 확장 문법
- 리액트에서 이 JSX를 이용해서 화면에서 UI가 보이는 모습 나타냄
## `createElement`를 쉽게 사용하기 위해 사용
- 모든 UI를 만들 때 마다 `createElement`를 사용해서 컴포넌트를 만들 수는 없음
- JSX 사용 후 바벨이 다시 `createElement`로 바꿔 사용
## 주의해야 할 문법들 (규칙)
- 컴포넌트에 여러 엘리먼트 요소가 있다면 반드시 부모 요소 하나로 감싸줘야 함
- 