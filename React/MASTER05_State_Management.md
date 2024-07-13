# 0-1. Dark Mode
## Recoil 사용x 다크모드 만들기
- `ThemeProvider`를 `index.tsx`에서 `App.tsx`로 옮기기
```tsx
// App.tsx

function App() {
  return (
    <>
      <ThemeProvider theme={theme}>
        <GlobalStyle />
        <Router />
        <ReactQueryDevtools initialIsOpen={true} />
      </ThemeProvider>
    </>
  );
}
```
- theme 두 개 만들기
```tsx
// theme.ts

export const darkTheme: DefaultTheme = {
  bgColor: "#2f3640",
  textColor: "#f5f6fa",
  accentColor: "#9c88ff",
};

export const lightTheme: DefaultTheme = {
  bgColor: "whitesmoke",
  textColor: "black",
  accentColor: "#9c88ff",
};
```
- theme을 토글할 변수, 함수, 버튼 만들기
```tsx
// App.tsx

function App() {
  const [isDark, setIsDark] = useState(false);
  const toggleDark = () => setIsDark((current) => !current);
  return (
    <>
      <ThemeProvider theme={isDark ? darkTheme : lightTheme}>
        <button onClick={toggleDark}>Toggle Mode</button>
        <GlobalStyle />
        <Router />
        <ReactQueryDevtools initialIsOpen={true} />
      </ThemeProvider>
    </>
  );
}
```
- `App.tsx`의 Router에 `toggleDark` 함수 넘겨주기
```tsx
// App.tsx

function App() {
	...
        <Router toggleDark={toggleDark} />
	...
}
```
- `Router.tsx` 수정
	- toggleDark 정의
	- Coins에 toggleDark 넘겨주기
```tsx
// Router.tsx

interface IRouterProps {
  toggleDark: () => void; // toggleDark라는 함수를 받고자 한다고 말함
}

function Router({ toggleDark }: IRouterProps) {
  return (
		...
        <Route path="/" element={<Coins toggleDark={toggleDark} />} />
	    ...
  );
}
```
- `Coins.tsx` 에 토글 버튼 만들기
- `Router.tsx`에서 넘겨받은 toggleDark 함수 사용
	- 정의도 해줌
```tsx
// Coins.tsx

interface ICoinsProps {
  toggleDark: () => void;
}

function Coins({ toggleDark }: ICoinsProps) {
	...
      <Header>
        <Title>C O I N S</Title>
        <button>Toggle Dark Mode</button>
      </Header>
    ...
}
```
- Chart도 적용
	- `App.tsx`의 `isDark` 변수를 보내서 Chart의 mode도 바꿔줌
## Global State
: 어플리케이션 전체에서 공유되는 state
- 어플리케이션이 무언가를 인지해야 할 때 사용
- 특정 value에 접근해야 할 때 사용
# 2-3. Introduction to Recoil
## Recoil
- React JS에서 사용할 수 있는 state management library
```
npm install recoil
```
## useRecoilValue()
- 설치 후 `index.tsx`에 추가
```tsx
// index.tsx

import { RecoilRoot } from "recoil";

const root = ReactDOM.createRoot(
  document.getElementById("root") as HTMLElement
);
root.render(
  <React.StrictMode>
    <RecoilRoot>
      <QueryClientProvider client={queryClient}>
        <App />
      </QueryClientProvider>
    </RecoilRoot>
  </React.StrictMode>
);
```
- `atoms.ts` 추가
	- key: 이름
	- default: 초기값
```ts
// atoms.ts

import { atom } from "recoil";

export const isDarkAtom = atom({
  key: "isDark",
  default: false,
});
```
- `App.tsx`
```tsx
// App.tsx

import { useRecoilValue } from "recoil";
import { isDarkAtom } from "./atoms";

function App() {
  const isDark = useRecoilValue(isDarkAtom)
...
}
```
- `useRecoilValue` 를 이용해서 atom을 불러와줌
	- 변수에 할당해서 사용
## useSetRecoilState()
- Coins.tsx
```tsx
// Coins.tsx

import { useSetRecoilState } from "recoil";
import { isDarkAtom } from "../atoms";


const setterFn = useSetRecoilState(isDarkAtom);
```
- `setterFn`은 React의 `setState`와 같은 방식으로 작동
```tsx
<button onClick={() => setterFn((prev) => !prev)}>Toggle Mode</button>
```
- 더 깔끔하게 수정
```tsx
  const setDarkAtom = useSetRecoilState(isDarkAtom);
  const toggleDarkAtom = () => setDarkAtom((prev) => !prev);
  
        <button onClick={toggleDarkAtom}>Toggle Mode</button>

```
