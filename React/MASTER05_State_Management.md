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
# 5. To Do Setup
- `toDoList.tsx`
```tsx
import React, { useState } from "react";

function ToDoList() {
  const [toDo, setTodo] = useState("");
  const onChange = (event: React.FormEvent<HTMLInputElement>) => {
    const {
      currentTarget: { value },
    } = event;
    setTodo(value);
  };
  const onSubmit = (event: React.FormEvent<HTMLFormElement>) => {
    event.preventDefault();
    console.log(toDo);
  };
  return (
    <div>
      <form onSubmit={onSubmit}>
        <input onChange={onChange} value={toDo} placeholder="Write a to do" />
        <button>Add</button>
      </form>
    </div>
  );
}

export default ToDoList;
```
- input이 많아지면 일일히 그 input에 따른 state를 관리할 변수, 함수를 생성해야함
# 6. Forms
## React Hook Form
- React에서 Form을 쉽게 관리하게 해주는 라이브러리
```
npm install react-hook-form
```
## useForm()
### register
- 이벤트 핸들러, props 등 역할을 해주는 함수
```tsx
// ToDoList.tsx

import { useForm } from "react-hook-form";

const {register} = useForm();
```
- `register` 함수를 사용하면 `onChange` 이벤트 핸들러가 필요 없음
- register("toDo")를 console창에 찍은 결과
```
1. name: "toDo"
2. onBlur: async event => {…}
3. onChange: async event => {…}
4. ref: ref => {…}
```
```tsx
        <input {...register("toDo")} placeholder="Write a to do" />
```
### watch
- form의 입력값들의 변화를 관찰할 수 있게 해주는 함수
	- console창에 찍어보면 입력값 변화를 감지함
```tsx
console.log(watch())

// {toDo: 'ㅁㄴㅇㄹㅇㄹ'}
```
# 7. Form Validation
## useForm()
### handleSubmit
- validation 담당
- 두 개의 인자
	- `onValid` : 유효할 때 쓰는 함수 (필수)
	- `onInvalid` : 유효하지 않을때 쓰는 함수 (선택)
- 자동으로 invalid한 input으로 focus를 옮겨준다.
#### \[tip] validation
```tsx
<input {...register("email")} required placeholder="Email" />

<input {...register("email", { required: true })} placeholder="Email" />
```
- 위처럼 HTML 자체에서 required를 하면 여러가지 문제가 생길 수 있음
	- 사용자가 지원하지 않는 브라우저, 모바일에 있을 때
	- 소스코드를 임의로 수정하는 경우
- 이를 보호하기 위해 JS에서 validation을 수행함
```tsx
<input
  {...register("username", { required: true, minLength: 10 })}
  placeholder="Username"
/>
```
- 이런 으로 간단히 적어주기만 하면 유효성 검사를 알아서 해줌!
### formState
```tsx
console.log(formState.errors)
```
- 어떤 에러가 발생했는지 나옴
	- type: 'required'
	- type: 'minLength'
	- 등 어떤 조건을 불충족했는지 나온다
- 보낼 메시지도 설정 가능
	- value, message 설정
```tsx
<input
  {...register("username", {
	required: "Username is required",
	minLength: {
	  value: 5,
	  message: "Your username is too short.",
	},
  })}
  placeholder="Username"
/>
```
# 8. Form Errors
- 정규식 [https://regex101.com/](https://regex101.com/)
- `pattern`에 정규식을 넣어줌
	- `~~@naver.com` 이어야 한다는 듯
```tsx
<input
  {...register("email", {
	required: "Email is required",
	pattern: {
	  value: /^[A-Za-z0-9._%+-]+@naver.com$/,
	  message: "Only naver.com emails allowed",
	},
  })}
  placeholder="Email"
/>
```
- 에러 메시지 출력
	- type 설정을 해줘야 함
```tsx
type IFormData = {
  errors: {
    email: {
      message: string;
    };
  };
  username: string;
  firstName: string;
  lastName: string;
  email: string;
  password: string;
  password2: string;
};

  const {
    register,
    watch,
    handleSubmit,
    formState: { errors },
  } = useForm<IFormData>();

<span>{errors?.email?.message}</span>
```
- `interface` 이용
	- 위에랑 뭐가 다른지..?
	- + default 값 이용
```tsx
interface IForm {
  username: string;
  firstName: string;
  lastName: string;
  email: string;
  password: string;
  password2: string;
}

  const {
    register,
    watch,
    handleSubmit,
    formState: { errors },
  } = useForm<IForm>({
    defaultValues: {  // 이 부분 덕분에 email 입력 창에 알아서 @naver.com이 들어가있음
      email: "@naver.com",
    },
  });
```
# 9. Custom Validation
- 에러를 trigger 시키는 방법
- `iForm` 을 이용해서 data의 type 설정
```tsx
  const onValid = (data: IForm) => {
    console.log(data);
  };
```
## useForm()
### setError
- 원하는 특정 항목에 error 발생 가능
- 발생하는 문제에 따라 추가적으로 에러를 설정할 수 있게 도와줌
```tsx
  const onValid = (data: IForm) => {
    if (data.password !== data.password2) {
      setError("password2", { message: "Passwords are not the same" });
    }
    setError("extraError", { message: "Server Offline" });
  };
```
#### shouldFocus
- 오류가 발생한 특정 부분에 자동으로 focus되게 함
```tsx
  const onValid = (data: IForm) => {
    if (data.password !== data.password2) {
      setError(
        "password2",
        { message: "Passwords are not the same" },
        { shouldFocus: true }
      );
    }
    setError("extraError", { message: "Server Offline" });
  };
```
### register
#### validate
- 함수를 값으로 가짐
	- value를 인자로 받음
	- boolean 값을 반환
		- `true` : validation 통과
		- `false` : validate 오류 발생
	- 특정 값을 return하면 에러 메세지를 리턴한다는 뜻
	- 삼항연산자 사용 시 조건 + 에러메시지 둘 다 사용 가능
```tsx
        <input
          {...register("firstName", {
            required: "write here",
            validate: (value) =>
              value.includes("nico") ? "No NICOs allowed" : true,
          })}
          placeholder="First Name"
        />
```
- 여러가지 객체를 가질 수 있음
	- 여러 조건 검사 가능
```tsx
validate: {
  noNico: (value) =>
	value.includes("nico") ? "No NICOs allowed" : true,
  noNick: (value) =>
	value.includes("nick") ? "No NICKs allowed" : true,
},
```
# 10. Recap
## react-hook-form
### register
`<input {...register("이름")} />`
- pattern : 정규식 검사
- validate : 만든 함수로 검사
### handleSubmit
`<form onSubmit={handleSubmit(내 함수)}></form>`
### setValue
`setValue("이름", 값)`
