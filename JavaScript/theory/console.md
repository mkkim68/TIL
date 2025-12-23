# Console 객체
- 브라우저의 *디버깅 콘솔(Firefox 웹 콘솔 등)에 접근할 수 있는 메서드를 제공*
- 동작 방식은 브라우저마다 다르지만, 사실상 표준으로 여겨지는 기능도 여럿 있음

- 아무 전역 객체에서나 접근 가능
- 브라우징 문맥에선 Window, 워커에서는 WorkerGlobalScope(en-US)이 속성으로 포함
- Window.console의 형태로 노출되어 있으므로 간단하게 console로 참조 가능

- `log`
- `table`
- `error`
- `warn`
- `time`, `timeEnd` : time, timeEnd 사이 시간 얼마나 걸리는지
- `clear`