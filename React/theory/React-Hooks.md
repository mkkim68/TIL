# React Hooks
- class없이 state를 사용할 수 있는 기능
## 필요한 이유
- Class Component로 사용되어온 React에서 느껴왔던 불편함이나 문제점들을 해결하기 위해서 개발됨
### 기존 Class Component와의 비교
| Class Component | Functional Component |
| --------------- | -------------------- |
| 더 많은 기능 제공      | 더 적은 기능 제공           |
| 더 긴 코드 양        | 짧은 코드 양              |
| 더 복잡한 코드        | 더 심플한 코드             |
| 더딘 성능           | 더 빠른 성능              |
### 함수형 컴포넌트에서 클래스 컴포넌트에 비해 사용하지 못했던 기능
#### 리액트의 생명주기
- Mounting `componentDidMount`
- Updating `componentDidUpdate`
- Unmounting `componentWillUnmoung`
## Hooks의 장점
### 간결한 코드
- 생명주기를 이용할 때 다 다르게 처리해줘야 했던 클래스 컴포넌트와 다르게 리액트 훅을 사용할 때는 `useEffect` 안에서 다 처리 가능하기 때문
### HOC 컴포넌트를 Custom React Hooks로 대체
- 많은 Wrapper 컴포넌트를 줄일 수 있음
#### HOC(Higher Order Component)
- 화면에서 재사용 가능한 로직만을 분리해서 component로 만들고 재사용 불가능한 UI와 같은 다른 부분들은 parameter로 받아서 처리하는 방법
#### Custom Hooks
- 재사용하는 로직은 따로 Custom Hooks를 이용해 컴포넌트를 만들어서 처리함
### 더 나은 가독성