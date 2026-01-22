# `keyof` 연산자
- 제공된 타입의 키를 추출하여 새로운 Union 유형으로 반환
```ts
interface IUser {
	name: string;
	age: number;
	address: string;
}

type UserKeys = keyof IUser
```

```ts
const user = {
	name: "John",
	age: 20,
	address: "seoul"
}

type UserKeys = keyof typeof user
```

```ts
enum UserRole {
	admin,
	manager
}

type UserRoleKeys = keyof typeof UserRole
```