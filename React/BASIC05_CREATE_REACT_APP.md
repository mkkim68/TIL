# create-react-app
### 준비사항
- node-js 설치
	- 콘솔에 node -v 입력후 설치 확인 (버전이 나와야함)
- 폴더 하나 만들고
- `npx create-react-app .` 실행
	- 현재 위치에 앱을 만드려면 . 필수
	- 현재 위치가 아니라 폴더를 새로 만들거면 . 자리에 원하는 폴더명 입력
- `npm start` : 서버 켜기
### 시작
- src 파일에 `App.js`, `index.js` 빼고 삭제
	- 불필요한 css와 App 함수 내에 필요없는 부분도 삭제
```js
// App.js
function App() {
  return (
    <div>
      <h1>Welcome</h1>
    </div>
  );
}

export default App;
```
```js
// index.js
import React from "react";
import ReactDOM from "react-dom/client";
import App from "./App";

const root = ReactDOM.createRoot(document.getElementById("root"));
root.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>
);
```
# Tour of CRA
## 파일 분리
- Button.js 생성
```js
import PropTypes from "prop-types";

function Button({ text }) {
  return <button>{text}</button>;
}

Button.propTypes = {
  text: PropTypes.string.isRequired,
};

export default Button;
```
- `npm i prop-types` 설치
- 기존에 했던 방식으로 Button 함수 만들어서 export
```js
import Button from "./Button";

function App() {
  return (
    <div>
      <h1>Welcome</h1>
      <Button text={"Continue"} />
    </div>
  );
}

export default App;
```
- App.js 에서 Button import 후 사용
## style을 모듈로 사용하기
- `원하는이름.module.css` 파일 생성
- css 파일에 스타일을 정의할 클래스 만들기
```css
/* Button.module.css */

.btn {
  color: white;
  background-color: aquamarine;
}
```
- 이 파일을 import 해서 (styles라는 이름으로) 스타일 적용을 원하는 요소에 className으로 `{styles.클래스명}` 을 넣어주면 적용됨
```js
import PropTypes from "prop-types";
import styles from "./Button.module.css";

function Button({ text }) {
  return <button className={styles.btn}>{text}</button>;
}

Button.propTypes = {
  text: PropTypes.string.isRequired,
};

export default Button;
```
- 렌더하는 과정에서 클래스명은 랜덤으로 바꿔서 html에 적용됨!! 