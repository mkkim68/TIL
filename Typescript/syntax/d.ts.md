# .d.ts
- 모듈 선언 파일
## uuid.d.ts
- 어떠한 객체가 있는데 그 객체에 유니크한 식별자를 주기 위해서 UUID라는 라이브러리를 이용해서 유니크한 값을 만들 수 있음
- uuid.d.ts 정의
```ts
declare module 'uuid' {
	const v4: () => string;
	
	export { v4 };
}
```
- 컴포넌트에서 사용
```tsx
import { v4 } from 'uuid';

function App() {
	console.log(v4());
	return <div></div>
}
```