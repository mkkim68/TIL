# Lookup Types(Indexed Access Types)
- Typescript에서는 다른 Type의 속성 Type을 재사용할 수 있음
```ts
interface Car {
	id: number;
	name: string;
	brand: {
		popularity: number;
		logo: string;
		history: number;
	}
}

function updateCarBrand(id: Car['id'], newBrand: Car['brand']) {}
```
