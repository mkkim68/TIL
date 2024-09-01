# 0. To Do List
### useState로 만든 변수에 바로 접근 불가능
- 항상 setState 함수를 사용하는데 그 안에 함수로 이전 값에 접근해서 원하는 동작을 할 수 있다.
### map을 이용해서 배열 내 요소 `li` 태그로 변환 후 출력
```js
  <ul>
	{toDos.map((item, index) => (
	  <li key={index}>{item}</li>
	))}
  </ul>
```
- React.js 는 element에 key 값을 줘야 함
# 2. Coin Tracker
```js
import { useEffect, useState } from "react";

function App() {
  const [loading, setLoading] = useState(true);
  const [coins, setCoins] = useState([]);
  useEffect(() => {
    fetch("https://api.coinpaprika.com/v1/tickers")
      .then((response) => response.json())
      .then((json) => {
        setCoins(json);
        setLoading(false);
      });
  }, []);
  return (
    <div>
      <h1>The Coins! {loading ? "" : `(${coins.length})`}</h1>
      {loading ? (
        <strong>Loading...</strong>
      ) : (
        <select>
          {coins.map((coin) => (
            <option>
              {coin.name} ({coin.symbol}): ${coin.quotes.USD.price}
            </option>
          ))}
        </select>
      )}
    </div>
  );
}


export default App;
```
- coins API를 이용해 select 만들기
- API를 받아오는 동안 Loading... 메시지가 뜨고 API를 다 받아오면 select 태그가 뜨도록 함
# 3-4. Movie App
- [https://yts.mx/api/v2/list_movies.json?minimum_rating=9&sort_by=year](https://yts.mx/api/v2/list_movies.json?minimum_rating=9&sort_by=year)
- movie API 사용
```js
import { useEffect, useState } from "react";

function App() {
  const [loading, setLoading] = useState(true);
  const [movies, setMovies] = useState([]);
  const getMovies = async () => {
    const json = await (
      await fetch(
        `https://yts.mx/api/v2/list_movies.json?minimum_rating=9&sort_by=year`
      )
    ).json();
    setMovies(json.data.movies);
    setLoading(false);
  };
  useEffect(() => {
    getMovies();
  }, []);
  console.log(movies);
  return (
    <div>
      {loading ? (
        <h1>Loading...</h1>
      ) : (
        <div>
          {movies.map((movie) => (
            <div key={movie.id}>
              <img src={movie.medium_cover_image} />
              <h2>{movie.title}</h2>
              <p>{movie.summary}</p>
              <ul>
                {movie.genres.map((g) => (
                  <li key={g}>{g}</li>
                ))}
              </ul>
              <hr />
            </div>
          ))}
        </div>
      )}
    </div>
  );
}
```
- 전에 배운 것이랑 같음
	- *key값 필수 조심*
## 파일 분리
- `src`내에 `routes, components` 폴더 생성 (vue와 비슷한 흐름름)
	- routes : 각각 다른 url 경로마다 보여줄 파일
	- components : 요소
### routes/Home.js
- Movie List
```js
import { useEffect, useState } from "react";
import Movie from "./components/Movie";

function Home() {
  const [loading, setLoading] = useState(true);
  const [movies, setMovies] = useState([]);
  const getMovies = async () => {
    const json = await (
      await fetch(
        `https://yts.mx/api/v2/list_movies.json?minimum_rating=9&sort_by=year`
      )
    ).json();
    setMovies(json.data.movies);
    setLoading(false);
  };
  useEffect(() => {
    getMovies();
  }, []);
  console.log(movies);
  return (
    <div>
      {loading ? (
        <h1>Loading...</h1>
      ) : (
        <div>
          {movies.map((movie) => (
            <Movie
              key={movie.id}
              coverImg={movie.medium_cover_image}
              title={movie.title}
              summary={movie.summary}
              genres={movie.genres}
            />
          ))}
        </div>
      )}
    </div>
  );
}

export default Home;
```
### routes/Detail.js
- Movie Detail
```js
function Detail() {
  return <h1>Detail</h1>;
}

export default Detail;
```
### components/Movie.js
- Movie List의 각 Item 요소
- Props 사용
```js
import PropTypes from "prop-types";

function Movie({ coverImg, title, summary, genres }) {
  return (
    <div>
      <img src={coverImg} alt={title} />
      <h2>{title}</h2>
      <p>{summary}</p>
      <ul>
        {genres.map((g) => (
          <li key={g}>{g}</li>
        ))}
      </ul>
      <hr />
    </div>
  );
}

Movie.propTypes = {
  coverImg: PropTypes.string.isRequired,
  title: PropTypes.string.isRequired,
  summary: PropTypes.string.isRequired,
  genres: PropTypes.arrayOf(PropTypes.string),
};

export default Movie;
```
# 5. Router
```
npm i react-router-dom@latest
```
- 강의에서는 5.3.0 버전으로 다운받으라고 했는데 현재 react 버전과 충돌
	- 그래서 가장 최신 버전으로 받음
	- 강의에서 (버전 5에서) `Switch` → 최신 버전(6.23.0)에서 `Routes`
	- `Route` 컴포넌트 사이에 자식 컴포넌트를 넣는 방식이 아닌 element prop에 자식 컴포넌트를 할당하도록 변경됨 
	- `<Route path='경로' element={<컴포넌트 />} />`
```js
import { BrowserRouter as Router, Routes, Route } from "react-router-dom";
import Home from "./routes/Home";
import Detail from "./routes/Detail";
function App() {
  return (
    <Router>
      <Routes>
        <Route path="/movie" element={<Detail />} />
        <Route path="/" element={<Home />} />
      </Routes>
    </Router>
  );
}

export default App;
```
### `BrowserRouter`
- Router 사용 시 가장 바깥쪽
### `Routes`
- Route 들을 묶는 태그
### `Route`
- 실제 경로를 적고 그 경로에서 띄우고 싶은 요소들을 정의해줌
	- `path` : 경로 작성 (string)
	- `element` : 컴포넌트나 html 요소들
### BrowserRouter와 HashRouter 차이
- hashrouter는 url 뒤에 \#을 붙임
# 6. Parameters
- `:변수이름` 방식으로 parameter 지정
- parameter이름을 각 components에 지정
## parameter 받아오기
```js
import { useParams } from "react-router-dom"
```
- useParams 불러오기
```js
const x = useParams();
console.log(x);
```
- parameter로 보낸 변수가 있는 Object가 출력
- ES6 이용해서 변수를 바로 가져와서 사용 가능
# 7. Publishing
### 준비
```
npm i gh-pages
```
- gh-pages : 결과물을 github pages에 업로드 할 수 있게 해주는 패키지
	- github pages: github에서 제공하는 무료 서비스
```
npm run build
```
- 이 script를 실행하면 웹사이트의 production ready code를 생성함
	- browser가 이해할 수 있는 형태로 `build` 폴더 및 파일들 생성
### homepage 추가
```json
{
	...,
	"homepage": "https://{github계정이름}.github.io/{현재 project 코드가 있는 레포지토리 이}"
}
```
- package.json에 추가
### deploy 추가
- deploy: 설치한 gh-pages 실행, `build`라는 디렉토리 가져감
- package.json의 scripts에 추가
```json
  "scripts": {
	  ...,
	"deploy": "gh-pages -d build",
    "predeploy": "npm run build"
  },
```
- `npm run deploy`를 실행시키면 predeploy가 먼저 실행된 후 deploy 실행
- 그 다음 홈페이지 링크 들어가면 됩니다요
# 참고
- breaking change: 버전이 업그레이드드 되면서 깨진 코드를 수정하는 것