## Fetch API

네트워크 통신을 포함한 리소스 취득을 위한 인터페이스가 정의되어 있고 `XMLHttpRequest` 보다 강력하고 유연한 조작이 가능

### 사용 방법

- Fetch 에는 `Request`와 `Response`가 포함되어 있다.
- `fetch()`를 불러들이는 경우 취득하고자 하는 리소스를 반드시 인수로 지정해야 한다.
- `fetch()`는 `Promise` 객체를 반환한다.
- `fetch()`의 두번째 인수는 초기화에 사용되는 객체를 정의 (생략 가능)
- Request와 Response를 직접 작성할 수 있지만 또다른 API를 불러들이는 작업이 수행되어야 하므로 지양하는 것이 좋다.

__기본적인 Fetch 요청__
```typescript
fetch('http://example.com/movies.json')
  .then((response) => response.json())
  .then((data) => console.log(data))
```

다른 HTTP Method를 쓰고 싶은 경우

```typescript
// POST 메서드 구현 예제
async function postData(url = '', data = {}) {
  // 옵션 기본 값은 *로 강조
  const response = await fetch(url, {
    method: 'POST', // *GET, POST, PUT, DELETE 등
    mode: 'cors', // no-cors, *cors, same-origin
    cache: 'no-cache', // *default, no-cache, reload, force-cache, only-if-cached
    credentials: 'same-origin', // include, *same-origin, omit
    headers: { // 많이 사용됨
      'Content-Type': 'application/json',
      // 'Content-Type': 'application/x-www-form-urlencoded',
    },
    redirect: 'follow', // manual, *follow, error
    referrerPolicy: 'no-referrer', // no-referrer, *no-referrer-when-downgrade, origin, origin-when-cross-origin, same-origin, strict-origin, strict-origin-when-cross-origin, unsafe-url
    body: JSON.stringify(data), // body의 데이터 유형은 반드시 "Content-Type" 헤더와 일치해야 함, json 넘겨 줄 때
  });
  return response.json(); // JSON 응답을 네이티브 JavaScript 객체로 파싱
}

postData('https://example.com/answer', { answer: 42 }).then((data) => {
  console.log(data); // JSON 데이터가 `data.json()` 호출에 의해 파싱됨
});
```

## Promise

비동기 작업의 완료 또는 실패와 그 결과 값을 나타낸다.
`Promise`는 생성된 시점에는 알려지지 않았을 수도 있는 값을 위한 대리자로, `비동기 연산이 종료된 이후에 결과 값과 실패 사유를 처리하기 위한 처리기를 연결`, 프로미스를 사용하면 비동기 메서드에서 마치 동기 메서드처럼 값을 반환할 수 있다. 다만 최종 결과를 반환하는 것이 아니고, 미래의 어떤 시점에 결과를 제공하겠다는 '약속'(프로미스)을 반환한다.

### 프로미스의 상태
- 대기(pending): 이행/거부가 아닌 초기 상태
- 이행(fulfilled):연산 성공
- 거부(rejected): 연산 실패

## ReadableStream
Streams API의 `ReadableStream`인터페이스는 byte 데이터를 읽을 수 있는 스트림을 제공한다. Fetch API는 Response 객체의 body 속성을 통하여 ReadableStream의 구체적인 인스턴스를 제공한다.

### Constructor
ReadableStream() : 읽을 수 있는 스트림 객체를 생성 후 리턴
```javascript
new ReadableStream()
new ReadableStream(underlyingSource)
new ReadableStream(underlyingSource, queuingStrategy)
```
### Properties
ReadableStream.locked : `locked는 ReadableStream이 reader에 고정되어 있는지 확인하는 getter 이다.
```javascript
const stream = new ReadableStream({
  // ...
})

const reader = stream.getReader();

stream.locked;
```

###  Method

- cancel()
- getReader()
- pipeThrough()
- pipeTo()
- tee()

## Unicode
- 문자 인코딩의 표준
- 16진수로 표기
- 조합형은 크기가 너무 커져서 완성형으로 주로 사용한다.

### 인코딩
용량이 큰 유니코드를 보완하기 위해 가변길이 문자 인코딩으로, 자주 쓰이는 문자 테이블을 1바이트(UTF-8) 또는 2바이트(UTF-16)으로 표현할 수 있는 대신 자주 쓰이지 않는 문자 테이블을 표현하는데 더 많은 바이트가 필요해 진다. `UTF-8`은 흔히 웹 브라우저의 인코딩을 설정할 때 자주 접할 수 있다.


> [텍스트 디코더와 인코더](https://ko.javascript.info/text-decoder)

#### 디코더 : 이진 데이터를 자바스크립트 문자열로 읽을 수 있게 변환

```javascript
let decoder = new TextDecoder([label], [options]);
```

- label : 기본적인 인코딩 방식은 `utf-8`
- options
  - fatal : `true`의 경우 디코딩이 불가능한 글자를 대상으로 예외처리. `false(기본값)`의 경우 글자를 **\uFFFD**로 대체
  - ingnoreBOM : `true`인 경우 사용되지 않는 바이트 순서 표식을 무시

```javascript
let str = decoder.decode([input], [options]);
```
- input : 디코딩할 BufferSource를 입력
- options
  - stream : 많은 양의 데이터를 `decoder`를 반복적으로 호출/실행. 이 경우 멀티 바이트 문자가 분할될 수 있기 때문에 이를 방지하기 위해 TextDecoder에 "unfinished" 문자를 입력시켜 다음 데이터가 오면 디코딩하도록 지시한다.

#### 인코더 : 문자열을 바이트로 변환

```javascript
let encoder = new TextEncoder();
```

- 인코딩 시 'uff-8'만 지원
- encode(str) : `Unit8Array`(BufferSource)에 문자열을 반환
- encodeInto(str, destination) : Unit8Array 구조 형태로 문자열을 인코딩

```javascript
let encoder = new TextEncoder();

let uint8Array = encoder.encode("Hello");
alert(uint8Array); // 72,101,108,108,111
```

## CORS란?

웹 브라우저는 **Same Origin Policy**에 따라 웹 페이지와 리소스를 요청한 출처가 다를 때 서버에서 얻은 결과를 사용할 수 없게 막는다. 서버에 요청하고 응답을 받아오는 것까지는 이미 진행이 다 된 상황이란 점에 주의!

REST API 서버에서 Headers에 “Access-Control-Allow-Origin” 속성을 추가하면 된다.

- Express에선 CORS 미들웨어 사용

```typescript
import express from 'express';
import cors from 'cors';

const app = express();

app.use(cors());
```