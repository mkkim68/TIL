# 0. Setup
## coinpaprika API
- 암호화폐 관련 API
## React Query
- 데이터 fetch 할 수 있는 패키지
## setting
```
npm i react-router-dom react-query
```
- 설치
	- react-router-dom
	- react-query
- src/
	- routes/
		- Coins.tsx
		- Coin.tsx
	- Router.tsx
```ts
// Coins.tsx
function Coins() {
  return <h1>Coins</h1>;
}

export default Coins;
```
```ts
// Coin.tsx
function Coin() {
  return <h1>Coin</h1>;
}

export default Coin;
```
```ts
// Router.tsx
import { BrowserRouter, Routes, Route } from "react-router-dom";
import Coins from "./routes/Coins";
import Coin from "./routes/Coin";

function Router() {
  return (
    <BrowserRouter>
      <Routes>
        <Route path="/:coinId" element={<Coin />} />
        <Route path="/" element={<Coins />} />
      </Routes>
    </BrowserRouter>
  );
}
export default Router;
```
- typescript에서 router 사용할 수 있게 설치
```
npm i --save-dev @types/react-router-dom
```
```tsx
// App.tsx
import Router from "./Router";

function App() {
  return <Router />;
}

export default App;
```

```ts
// Coin.tsx
import { useParams } from "react-router-dom";

function Coin() {
  const { coinId } = useParams();
  return <h1>Coin : {coinId}</h1>;
}

export default Coin;

```
# 1. Styles
## 기본 style 초기화
https://github.com/zacanger/styled-reset/blob/master/src/index.ts
### styled-reset 사용
- 설치 후 import
## Fragment
- 일종의 유령 컴포넌트
- `<> </>`
```ts
import { createGlobalStyle } from "styled-components";
import Router from "./Router";

const GlobalStyle = createGlobalStyle`
  body {
    color: red;
  }
`;

function App() {
  return (
    <>
      <GlobalStyle />
      <Router />
    </>
  );
}

export default App;
```
## 기본 css 세팅
```ts
html, body, div, span, applet, object, iframe,
h1, h2, h3, h4, h5, h6, p, blockquote, pre,
a, abbr, acronym, address, big, cite, code,
del, dfn, em, img, ins, kbd, q, s, samp,
small, strike, strong, sub, sup, tt, var,
b, u, i, center,
dl, dt, dd, menu, ol, ul, li,
fieldset, form, label, legend,
table, caption, tbody, tfoot, thead, tr, th, td,
article, aside, canvas, details, embed,
figure, figcaption, footer, header, hgroup,
main, menu, nav, output, ruby, section, summary,
time, mark, audio, video {
  margin: 0;
  padding: 0;
  border: 0;
  font-size: 100%;
  font: inherit;
  vertical-align: baseline;
}
/* HTML5 display-role reset for older browsers */
article, aside, details, figcaption, figure,
footer, header, hgroup, main, menu, nav, section {
  display: block;
}
/* HTML5 hidden-attribute fix for newer browsers */
*[hidden] {
    display: none;
}
body {
  line-height: 1;
}
menu, ol, ul {
  list-style: none;
}
blockquote, q {
  quotes: none;
}
blockquote:before, blockquote:after,
q:before, q:after {
  content: '';
  content: none;
}
table {
  border-collapse: collapse;
  border-spacing: 0;
}
```
- 리셋시키기 위해 GlobalStyle 컴포넌트에 입력
- 구글 폰트 사용 가능
```ts
body {
	font-family: 'Source Sans Pro', sans-serif;
}
```
- 추가 기본 설정
	- 모든 요소 `border-box` 
	- 모든 a tag 밑줄 제거
```ts
* {
  box-sizing: border-box;
}
a {
  text-decoration: none;
}
```
## theme
- [https://flatuicolors.com/](https://flatuicolors.com/)
	- 컬러 팔레트 사이트
	- 테마 컬러 선택
- `accentColor` 추가 후 적용
```ts
//theme.ts
import { DefaultTheme } from "styled-components/dist/types";

export const theme: DefaultTheme = {
  bgColor: "#40407a",
  textColor: "#f7f1e3",
  accentColor: "#ffda79",
};
```
```ts
//styled.d.ts

// import original module declarations
import "styled-components";

// and extend them!
declare module "styled-components" {
  export interface DefaultTheme {
    textColor: string;
    bgColor: string;
    accentColor: string;
  }
}
```
# 2. Home part One
```ts
// Coins.tsx
import { Link } from "react-router-dom";
import styled from "styled-components";

const Container = styled.div`
  padding: 0px 20px;
`;

const Header = styled.header`
  height: 10vh;
  display: flex;
  justify-content: center;
  align-items: center;
`;

const CoinsList = styled.ul``;

const Coin = styled.li`
  background-color: ${(props) => props.theme.textColor};
  color: ${(props) => props.theme.bgColor};
  border-radius: 15px;
  margin-bottom: 10px;
  a {
    padding: 20px;
    transition: color 0.2s ease-in;
    display: block;
  }
  &:hover {
    a {
      color: ${(props) => props.theme.accentColor};
    }
  }
`;

const Title = styled.h1`
  font-size: 48px;
  color: ${(props) => props.theme.accentColor};
`;

const coins = [
  {
    id: "btc-bitcoin",
    name: "Bitcoin",
    symbol: "BTC",
    rank: 1,
    is_new: false,
    is_active: true,
    type: "coin",
  },
  {
    id: "eth-ethereum",
    name: "Ethereum",
    symbol: "ETH",
    rank: 2,
    is_new: false,
    is_active: true,
    type: "coin",
  },
  {
    id: "hex-hex",
    name: "HEX",
    symbol: "HEX",
    rank: 3,
    is_new: false,
    is_active: true,
    type: "token",
  },
];

function Coins() {
  return (
    <Container>
      <Header>
        <Title>코인</Title>
      </Header>
      <CoinsList>
        {coins.map((coin) => (
          <Coin key={coin.id}>
            <Link to={`/${coin.id}`}>{coin.name} &rarr;</Link>
          </Coin>
        ))}
      </CoinsList>
    </Container>
  );
}

export default Coins;
```
## Link
- parameter로 `coin.id`를 넘겨주어 코인마다 디테일 페이지로 넘어갈 수 있도록 함
# 3. Home part Two
## interface 정의
- API로 받아오는 정보라도 interface로 각 데이터 속성을 정의해 주어야 함
```tsx
interface CoinInterface {
  id: string;
  name: string;
  symbol: string;
  rank: number;
  is_new: boolean;
  is_active: boolean;
  type: string;
}
```
```ts
  const [coins, setCoins] = useState<CoinInterface[]>([]);
```
- coins가 coin으로 이루어진 array라고 선언해줌
### 함수를 바로 실행하는 tip
```ts
(함수)();
```
- 코드에 적용
```ts
    (async() => {
      fetch("https://api.coinpaprika.com/v1/coins")
    })()
```
- 코인 API로 정보 받아오기
	- loading 까지 구현
```ts
function Coins() {
  const [coins, setCoins] = useState<CoinInterface[]>([]);
  const [loading, setLoading] = useState(true);
  useEffect(() => {
    (async () => {
      const response = await fetch("https://api.coinpaprika.com/v1/coins");
      const json = await response.json();
      setCoins(json.slice(0, 100));
      setLoading(false);
    })();
  }, []);
  console.log(coins);
  return (
    <Container>
      <Header>
        <Title>코인</Title>
      </Header>
      {loading ? (
        <Loader>"Loading..."</Loader>
      ) : (
        <CoinsList>
          {coins.map((coin) => (
            <Coin key={coin.id}>
              <Link to={`/${coin.id}`}>{coin.name} &rarr;</Link>
            </Coin>
          ))}
        </CoinsList>
      )}
    </Container>
  );
}
```