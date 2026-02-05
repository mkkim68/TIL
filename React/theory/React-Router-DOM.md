# React Router DOM
- 사용 시 웹 앱에서 동적 라우팅 구현 가능
- 라우팅이 실행 중인 앱 외부의 구성에서 처리되는 기존 라우팅 아키텍처와 달리 React Router DOM은 앱 및 플랫폼의 요구 사항에 따라 컴포넌트 기반 라우팅을 용이하게 함
## SPA (Single Page Application)
- 리액트는 SPA이기 때문에 하나의 index.html 템플릿 파일을 가짐
- 이 하나의 템플릿에 자바스크립트를 이용해서 다른 컴포넌트를 이 index.html에 넣으므로 페이지를 변경해주게 됨
- 이 때 React Router DOM 라이브러리가 새 컴포넌트로 라우팅/탐색을 하고 렌더링하는데 도움을 줌
## 설치
```
npm install react-router-dom --save
yarn add react-router-dom
```
## 설정
### `BrowserRouter`로 루트 컴포넌트 감싸주기
```jsx
import { BrowserRouter } from 'react-router-dom';

ReactDOM.render(
	<BrowserRouter>
		<App />
	</BrowserRouter>
	document.getElementById('root')
);
```
#### `BrowserRouter` 
- HTML5 History API를 사용하여 UI를 URL과 동기화된 상태로 유지해줍니다
### 여러 컴포넌트 생성 및 라우트 정의하기
```jsx
function App() {
	return (
		<div className="App">
			<Routes>
				<Route path='/' element={ <Home /> } />
			</Routes>
		</div>
	)
}
```
#### `Routes`
- 앱에서 생성될 모든 개별 경로에 대한 컨테이너/상위 역할을 함
- `Route`로 생성된 자식 컴포넌트 중에서 매칭되는 첫번째를 렌더링 해줌
#### `Route`
- 단일 경로를 만드는 데 사용됨
##### `path` 속성
- 원하는 컴포넌트의 URL 경로를 지정
- 경로 이름은 마음대로 설정 가능
- 경로 이름이 `'/'`인 컴포넌트는 앱이 처음 로드될 때마다 먼저 렌더링됨
##### `element` 속성
- 경로에 맞게 렌더링되어야 하는 컴포넌트 지정
### `<Link />`를 이용해 경로 이동하기
```jsx
import { Link } from "react-router-dom";

function Home() {
	return (
		<div>
			<h1>홈페이지</h1>
			<Link to="about">About 페이지를 보여주기</Link>
			<Link to="contact">Contact 페이지를 보여주기</Link>
		</div>
	)
}
```
#### `Link` 구성 요소
- HTML의 앵커 요소 (`<a />`)와 유사함
##### `to` 속성
- 링크가 당신을 데려가는 경로 지정
## APIs
### 중첩 라우팅 (Nested Routes)
- React Router의 가장 강력한 기능 중 하나이므로 복잡한 레이아웃 코드를 어지럽힐 필요가 없습니다
- 대부분의 레이아웃은 URL의 세그먼트에 연결되며 React Router는 이를 완전히 수용합니다
```jsx

<BrowserRouter>
	<Routes>
		<Route path='/' element={ <App /> } >
			<Route index element={ <Home /> } />
			<Route path='teams' element={ <Teams /> } >
				<Route path=':teamid' element={ <Team /> } />
				<Route path='new' element={ <NewTeamForm /> } />
			</Route>
		</Route>
	</Routes>
</BrowserRouter>

```
- `App` 컴포넌트에 Header, Footer 등 Layout
- localhose:3000/teams/13 => `Team` 컴포넌트
- localhose:3000/teams/new => `NewTeamForm` 컴포넌트
### Outlet
- 자식 경로 요소를 렌더링하려면 부모 경로 요소에서 `<Outlet>`을 사용해야 함
- 이렇게 하면 하위 경로가 렌더링될 때 중첩된 UI가 표시될 수 있음
- 부모 라우트가 정확히 일치하면 자식 인덱스 라우트를 렌더링하거나 인덱스 라우트가 없으면 아무것도 렌더링 X
- react-router-dom에서 가져와 사용
```jsx
function App() {
	return (
		<div>
			<Navigation />
			<div>
				<Outlet /> {/* 이 부분 */}
			</div>
			<Footer />
		</div>
	)
}
```
### 다양한 기능
#### `useNavigation()`
- 경로 바꿔줌
#### `useParams()`
- `:style` 문법을 path 경로에 사용하였다면 `useParams()`로 읽을 수 있음 (e.g. `:id`)
#### `useLocation()`
- 현재 위치 객체 반환
- 현재 위치가 변경되 때마다 일부 side effect를 수행하려는 경우에 유용
#### `useRoutes()`
- `<Routes>`와 기능적으로 동일하지만 `<Route>`요소 대신 JS 객체를 사용하여 경로 정의
- `<Route>`와 동일한 속성을 갖지만 JSX 필요 없음