# `tsconfig.json`
- 디렉터리에 이 파일이 있으면 해당 디렉터리가 TypeScript의 루트임을 나타냄
- 프로젝트를 컴파일하는데 필요한 루트 파일과 컴파일러 옵션 지정
## 전체 구성
```json
{
	// 컴파일러 옵션 지정
	"compilerOptions": {},
	// 컴파일할 개별 파일 목록(확장자 이름 필수)
	"files": [
		"node_modules/library/index.ts"
	],
	// 컴파일러를 이용해서 변환할 폴더 경로를 지정
	"include": [
		"src/**/*",
		"tests/**/*"
	],
	// 컴파일러를 이용해서 변환하지 않을 폴더 경로를 지정
	"exclude": [
		"node_modules",
		"dist"
	],
	// 상속해서 사용할 다른 TS 구성파일 지정
	"extends": "main_config.json"
}
```
## compilerOptions
### lib
- 라이브러리 설정
- lib 지정시 배열 안에 있는 라이브러리만 사용
- 미지정시 기본 값
### moduleResolution
- 타입스크립트 컴파일러가 모듈을 찾는 방법
1. 모듈 import가 relative인지 non-relative인지 구분함
2. Classic 또는 Node 전략 중 하나를 이용해서 컴파일러에서 moduleA를 찾을 위치를 알려줌
### baseUrl
- 이 프로퍼티 지정 시 non-relative import의 모듈 해석 과정에 하나의 과정 추가
```json
"baseUrl": "./"
```
- 사용하면 TS는 tsconfig.json과 동일한 폴더에서 시작하는 파일 찾음
### paths
```json
"paths": {
	"@src/*": [
		"src/*"
	]
}
```
```ts
import { bar } from "../../../../bar"
// 아래처럼 가독성 있게 바꿀 수 있음
import { bar } from '@src/bar'
```
### isolatedModules
- true로 설정하면 프로젝트 내에 모든 각각의 소스코드 파일을 모듈로 만들기를 강제함
- 소스코드 파일에서 import 또는 export를 사용하면 그 파일은 모듈이 되지만 만약 import / export를 하지 않으면 그 파일은 전역 공간으로 정의되고 모듈이 아니기에 에러가 나게 됨
```ts
export {}
```
### removeComments
- 컴파일 시에 주석 모두 제거
### allowJs
- JS도 함께 사용하며 개발 가능
### checkJs
- allowJs와 함께 작동
- 활성화되면 JS 파일에 오류 보고됨
- 아래 사용과 똑같이 동작
```js
// @ts-check
```
### forceConsistentCasingInFileNames
- 파일의 이름을 대소문자 판별하게 하는 옵션
### declaration
- true로 설정하면 TS 파일을 JS로 컴파일하는 과정에서 JS파일과 함께 d.ts 선언 파일이 생성됨
- 타입만 따로 관리 가능
### strict
- 모든 엄격한 유형 검사 옵션 활성화
```json
"nolmplicitAny": true, /* 명시적이지 않은 'any' 유형으로 표현식 및 선언 사용 시 오류 발생 */ 
"strict ullChecks": true, /* 엄격한 null 검사 사용 */ 1/"strictFunctionTypes": true, /* 엄격한 함수 유형 검사 사용 */ 1/"strictBindCallApply": true, /* 엄격한 'bind', 'call, apply' 함수 메서드 사용 */*
"strictPropertyInitialization": true, /* 클래스에서 속성 초기화 엄격 검사 사용 */
"nolmplicitThis": true, /* 명시적이지 않은 'any'유형으로 'this' 표현식 사용 시 오류 발생 */
"alwaysStrict": true, /* 엄격모드에서 구문 분석 후, 각 소스 파일에 "use strict" 코드를 출력 */
```