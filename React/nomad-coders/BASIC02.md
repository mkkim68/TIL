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
# JSX
: javascript를 확장한 문법
```jsx
const Title = <h3 id="title" onMouseEnter={() => console.log("mouse enter")}>hello, I'm a title</h3>
```
- html처럼 요소를 만들어주면 됨 (eventlistener도 property에 넣어주면 된다)
### Babel 설치해야함
- JSX를 기본적으로 이해하지 못함
```html
<script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
<script type="text/babel"></script>
```
- 작성하는 파일 script로 type 정의해줘야됨
### 다른 요소 담기
```jsx
const Button = () => (

      <button

        style={{

          backgroundColor: "teal",

        }}

        onClick={() => console.log("i'm clicked")}

      >

        Click me

      </button>

    );

function Title() {  <!-- 위에랑 같지만 다른 방식 -->

      return (

        <h3 id="title" onMouseEnter={() => console.log("mouse enter")}>

          hello, I'm a title.

        </h3>

      );

    }
    
const Container = (

      <div>

        <Title /> <Button />

      </div>

    );
```
- 요소를 함수로 만들고 <이름 /> 을 넣어준다
- 컴포넌트의 첫 글자는 *대문자!!!!*
	- 소문자로 하면 html요소로 헷갈릴 수 있음
	- 따로 요소 안만들고 html요소를 바로 넣어주는 것도 가능