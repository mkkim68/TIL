# ESLint
## ESLint란?
- 개발자들이 특정한 규칙을 가지고 코드를 깔끔하게 짤 수 있게 도와주는 라이브러리
- 자바스크립트를 쓰는 가이드라인 제시, 문법에 오류가 나면 알려주는 역할 등등
- formatter 역할도 하지만 주요 기능은 문법 오류 잡는 것
## 사용 방법
### ESLint 익스텐션 설치
- `create-react-app`으로 리액트를 설치하면 기본으로 eslint가 설정되긴 함
	- VSCode에서 바로 에러 확인은 불가능
	- 앱 시작 시 터미널 상에서 볼 수 있음
- 따라서 설치를 해야 앱을 켜지 않아도 에러 확인 가능
### eslint 설정 파일 생성
- package.json에 eslintConfig 부분 지우고 `.eslintrc.json` 파일 생성
### testing에 특화된 ESLint 설치 (ESLint Testing Plugins)
```
npm install eslint-plugin-testing-library eslint-plugin-jest-dom
```
- testing-library: render로 DOM 그리는 부분
- jest-dom: expect-matcher로 테스트
#### Plugins 란?
- eslint에서 기본으로 제공하지 않는 다양한 규칙을 플러그인을 통해 사용할 수 있음
- 예를 들어 react에 관련된 린트 설정을 위해서는 eslint-plugin-react를 사용하면 되며, react hooks에 관련된 규칙을 적용시켜주려면 eslint-plugin-react-hooks를 사용
### 내부 설정
```json
{
	"plugins": ["testing-library", "jest-dom"],
	"extends": [
		"react-app",
		"react-app/jest",
		"plugin:testing-library/react",
		"plugin:jest-dom/recommended"
	]
}
```
#### plugins 항목
- 플러그인 추가
- 추가할 때 `eslint-plugin-` 부분 생략 가능
#### extends 항목
- 플러그인 추가한 후, **규칙을 정해야** 사용 가능
	- 이 항목에 규칙 설정
- react를 위한 규칙
- recommended는 추천이 되는 걸 사용
- **규칙 변경하고자** 할 때는 rule 항목 추가
### lint가 잘 작동하는지 확인
# Prettier
## Prettier란?
- 주로 코드 형식을 맞추는데 사용
- 작은따옴표를 사용할지 큰 따옴표를 사용할지, Indent 값을 2로 줄지 등등, 에러 찾는 것이 아닌 코드 포맷터 역할
## 사용 방법
### 설치
- npm으로 설치 -> 여러 개발자와 같은 포맷 유지에 더 좋음
- VSCode로 익스텐션 설치 -> 혼자서 편하게 설치해서 사용하기 좋음