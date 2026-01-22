# Mapped Types
- 맵드 타입을 이용하면 중복을 피하기 위해서 다른 타입을 바탕으로 새로운 타입을 생성할 수 있음
- type이 다른 type에서 파생되고 동기화 상태를 유지해야 하는 경우에 특히 유용
```ts
// 현재 사용자의 구성 값
type AppConfig = {
	username: string;
	email: string;
};

// 사용자에게 구성 값을 변경할 수 있는 권한이 있는지 여부
type AppPermissions = {
	changeUsername: boolean;
	changeEmail: boolean;
};
```
- 이런 경우엔 AppConfig와 AppPermissions 사이에 암시적 관계가 있기 때문에 문제가 있음
- 새 구성 값이 AppConfig에 추가될 때마다 AppPermissions에도 추가해야 함
- 이럴 때 Mapped Types 사용
## 사용 예제
```ts
type Users = 'John' | 'Han' | 'Kim';

type UserAge = { [K in Users]: number };
const userAgeInfo: UserAge = {
	John: 10,
	Han: 20,
	Kim: 30
}
```