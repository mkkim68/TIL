# 준비
## 두 가지 코드 import
### react 
- [https://unpkg.com/react@17.0.2/umd/react.production.min.js](https://unpkg.com/react@17.0.2/umd/react.production.min.js)
- 어플리케이션이 interactive하도록 만들어주는 library
### react-dom
- [https://unpkg.com/react-dom@17.0.2/umd/react-dom.production.min.js](https://unpkg.com/react-dom@17.0.2/umd/react-dom.production.min.js)
- 모든 React element를 HTML body에 둘 수 있게 해주는 library(혹은 package)
# 기본문법
## React
### `.createElement()`
- HTML 요소 만들기
- 아무도 안쓰고 어려운 방식이다.
```javascript
const elementName = React.createElement("span", {property: "property-name"}, "content");
```
#### property
- `class`
- `id`
- `style`
- `onClick` : eventListener를 바로 property에 넣어줄 수 있음!!! *이름은 기존 js같이 click이 아닌 on을 붙여야함*
#### content
- 요소의 내용
- 내부에 여러 요소를 넣고 싶으면 array안에 순서대로 담으면 됨
## ReactDOM
### `.render()`
- React element를 HTML로 만들어 배치(사용자에게 보여줌)
```javascript
ReactDOM.render(elementName, parentElement)
```
- 부모 요소 안에 넣어줌