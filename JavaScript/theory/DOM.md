# DOM이란?
- Document Object Model
- 메모리에 웹 페이지 문서 구조를 트리구조로 표현해서 웹 브라우저가 HTML 페이지를 인식하게 해줌
- 웹 페이지를 이루는 요소들을 자바스크립트가 이용할 수 있게 브라우저가 **트리구조로 만든 객체 모델**
![](../../img/251229_1.png)
1. DOM 트리 생성: 렌더 엔진이 문서를 읽어들임 → 파싱하고 어떤 내용을 페이지에 렌더링할 지 결정
2. Render Tree 생성: 브라우저가 DOM과 CSSOM을 결합하는 곳, 스타일 정보를 포함한 최종 렌더링 트리 출력
3. Layout(reflow): 브라우저가 페이지에 표시되는 각 요소의 크기와 위치 계산
4. Paint: 실제 화면에 그리기
```javascript
let val;

val = document; // document 객체

val = document.baseURI; // 웹 페이지의 절대 URI 반환
val = document.head; // head 태그 반환
val = document.forms; // 모든 form 태그 반환
val = document.scripts; // script 태그 반환
```
# DOM Navigation
- DOM에 수행하는 모든 연산은 document 객체에서 시작
- document 객체는 DOM에 접근하기 위한 '진입점'
- 진입점을 통과하면 어떤 노드에도 접근 가능
## Node Name
```js
val = list.childNodes; // NodeList 반환, line break도 포함
val = list.childNodes[3].nodeType;

// 1 - Element
// 2 - Attribute (deprecated)
// 3 - Text Node
// 8 - Comment Node
// 9 - Document itself
// 10 - Doctype

// children element nodes 반환
val = list.children; // HTML Collection 반환 (line break X)
```

| 모든 노드에 적용 가능한 탐색 프로퍼티                                                              | 요소 노드에만 적용 가능한 탐색 프로퍼티                                                                                          |
| ---------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------- |
| `parentNode` `childNodes` `firstChild` `lastChild` `previousSibling` `nextSibling` | `parentElement` `children` `firstElementChild` `lastElementChild` `previousElementSibling` `nextElementSibling` |
# DOM Collection
- childNodes는 배열같아 보이지만 배열이 아님
	→ iterable할 유사 배열 객체인 **컬렉션(collection)**
## 특징
1. `for..of` 사용 가능 
	- `forEach()` 사용 가능
	- `for...in` 사용 불가능
2. 배열이 아니기 떄문에 배열 메서드 사용 불가능