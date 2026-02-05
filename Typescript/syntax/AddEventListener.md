# AddEventListener를 위한 타입 생성
```ts
interface MyMouseEvent {
	x: number;
	y: number;
}

interface MyKeyBoardEvent {
	key: string;
}

interface MyEventObjects {
	click: MyMouseEvent;
	keypress: MyKeyBoardEvent;
}

function handleEvent<K extends keyof MyEventObjects>(
	eventName: K, 
	callback: (e: MyEventObjects[K]) => void
	) {

}

handleEvent('click', (e) => {}) // MyMouseEvent
handleEvent('keypress', (e) => {}) // MyKeyBoardEvent
```