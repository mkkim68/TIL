# React Testing Library
## React Testing Library란?
- `create-react-app`으로 리액트 앱 생성시 기본적으로 테스팅할 때 사용(즉시 지원)
	- 없다면 npm을 통해 추가 가능
	- `npm install --save-dev @testing-library/react`
- React 구성 요소 작업을 위한 API를 추가하여 DOM Testing Library 위에 구축됨
- DOM Testing Library란
	- DOM 노트를 테스트하기 위한 매우 가벼운 솔루션
- 행위 주도 테스트(Behavior Driven Test)
	- 기존의 구현 주도 테스트 기반 툴(Enzyme)을 대처하는 솔루션
## api
- 앱을 키고 기본 테스트 진행 
	- a
	- q quit
- App.test.js : 기본 테스트가 진행되는 곳
### "render" 함수
- DOM에 컴포넌트를 렌더링하는 함수
- 인자로 렌더링할 React 컴포넌트가 들어감
### FireEvent API
- 유저가 발생시키는 액션(이벤트)에 대한 테스트를 해야하는 경우 사용