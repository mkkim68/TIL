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