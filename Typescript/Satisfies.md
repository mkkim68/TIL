# Satisfies 연산자
```ts
type Colors = 'red' | 'green' | 'blue';
type RGB = [red: number, green: number, blue: number];

const palette: Record<Colors, string | RGB> = {
	red: [255, 0, 0],
	green: "#00ff00",
	bleu: [0, 0, 255] // Error
}

const redComponent = palette.red.at(0);

const greenNormalized = palette.green.toUpperCase(); // Error: string | RGB 형식에 'toUpperCase' 속성 없음
```
- Satisfies 적용
```ts
type Colors = 'red' | 'green' | 'blue';
type RGB = [red: number, green: number, blue: number];

const palette = {
	red: [255, 0], // Error
	green: "#00ff00",
	bleu: [0, 0, 255], // Error
	platypus: false // Error (value 타입 안맞음)
} satisfies Record<string, string | RGB>

const redComponent = palette.red.at(0);

const greenNormalized = palette.green.toUpperCase(); // Error 사라짐
```
