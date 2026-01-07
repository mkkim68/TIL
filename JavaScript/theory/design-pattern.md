# Design Pattern
- 소프트웨어 설계의 주어진 콘텍스트 내에서 일반적으로 발생하는 문제에 대한 일반적이고 재사용 가능한 솔루션
- 프로그래머가 응용 프로그램이나 시스템을 디자인할 때 일반적인 문제를 해결하는 데 사용할 수 있는 공식화된 모범 사례
## 장점
- 최고의 솔루션
- 재사용성 
- 풍부한 표현력
- 향상된 의사 소통
- 필요없는 코드 리팩토링
- 코드베이스 크기 감소
# Singleton Pattern
- 클래스의 인스턴스화를 하나의 객체로 제한하는 디자인 패턴
- 고전적으로 싱글톤 패턴은 클래스가 존재하지 않는 경우 클래스의 새 인스턴스를 생성하는 메서드로 클래스를 생성하여 구현할 수 있음
- 인스턴스가 이미 존재하는 경우 해당 개체에 대한 참조 반환
```js
let instance;

class Counter {
	constructor() {
		if(instance) {
			throw new Error('이미 인스턴스 존재');
		}
		instance = this;
	}
}

const singletonCounterA = new Counter();
const counterB = new Counter(); // error
```
# Factory Pattern
- 팩토리 패턴을 사용하면 특수 함수인 팩토리 함수를 사용하여 비슷한 객체를 많이 만들 수 있음
	- 비슷한 객체를 반복적으로 생성해야하는 경우 사용
```js
const createBook = (title, author, isbn) => ({
	title,
	author,
	isbn,
});

const book1 = createBook('book1', 'author1', 'ab123')
const book2 = createBook('book2', 'author2', 'cd123')
```
- 속성 쉽게 변경 가능
# Mediator Pattern
- 중재자 패턴
- 객체 그룹에 대한 중앙 권한 제공
```js
class Participant {
	constructor(name) {
		this.name = name;
		this.chatRoom = null;
		this.messages = [];
	}
	
	// 생략
	
	send(message, to) {
		this.chatRoom.send(message, this, to);
	
	receive(message, from) {
		this.messages.push({message, from});
	}
}

class ChatRoom { // mediator
	constructor() {
		this.participants = {}
	}
	
	// 생략
	
	send(message, participant, to) {
		this.participants[to.name].receive(message, participant);
	}
}
```
- 모든 참가자가 보내는 메시지가 채팅방을 거쳐서 전송됨
	- 참가자를 보호하기 위해 '정크 필터'와 같은 복잡한 규칙을 추가할 수 있게 된다
# Observer Pattern
- 특정 Subject를 관찰하는 많은 Observer가 있음
- Observer는 기본적으로 Subject에 대한 관심이 있고 변경 사항이 있을 떄 알림을 받기를 원함
	- 그 Subject에 스스로를 등록(register)
- Subject에 대한 관심을 잃으면 단순히 해당 Subject에서 등록 취소
	- 게시자-구독자 (Publisher-Subscriber) 모델이라고도 함
# Module Pattern
- 코드를 더 작고 재사용 가능한 조각으로 분할하는 것을 도와줌
```html
<body>
	<script src="index.js" type="module"></script>
</body>
```
## 일반 스크립트와 모듈의 차이
- 항상 엄격 모드로 실행됨
- 모듈 레벨 스코프
- 지연 실행
- 인라인 모듈 스크립트도 비동기 처리 가능
- 외부 오리진에서 스크립트를 불러오려면 Cors 헤더 필요
- 중복 스크립트 무시