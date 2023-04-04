## Express
- Nodejs의 서버 웹 프레임워크

간단한 서버 앱 npm 패키지 세팅

1. 프로젝트 생성

```bash
mkdir express-demo-app
cd mkdir express-demo-app
```

2. .gitignore 작성 및 패키지 초기화
```bash
touch .gitignore
echo "/node_modules/" > .gitignore

npm init -y
```

3. 패키지 초기화
```bash
npm i -D typescript
npx tsc --init
```

4. ESLint 설치
```bash
npm i -D eslint
npx eslint --init
```

5. ts-node 설치 
```bash
npm i -D ts-node
```

6. Express 설치
```bash
npm i express
npm i -D @types/express
```

7. package.json script 추가
```json
 "scripts": {
    "start": "nodemon app.ts",
    "lint": "eslint --fix ."
  },
```

8. nodemon 설치

Node.js 개발 시 자바스크립트 파일을 수정할 때마다 `ctrl+c`를 통해 node를 종료한 후 다시 실행해주는 번거로움을 덜어준다. 파일들을 모니터링하고 있다가 변경이 발생하는 경우 서버를 자동으로 재실행 시켜준다.

```bash
npm i -D nodemon
npx nodemon app.ts

# nodemon 실행방법
# nodemon app.js
```

### express 예제
```ts
import express from 'express';

const port = 3000;

const app = express();

// app.get('주소', (요청, 응답) => {
//   응답
// })
app.get('/', (req, res) => {
	res.send('Hello, world!!');
});

app.listen(port, () => {
	console.log(`Server running at http://localhost:${port}`);
});
```

```bash
# ts-node로 실행
npx ts-node app.ts
```


## URL 구조

URL은 하이퍼텍스트와 HTTP에서 핵심 개념이며, 웹에 게시된 리소스를 검색하기 위해 브라우저에서 사용하는 메커니즘이다.

__URL의 예__

```docs
https://developer.mozilla.org
https://developer.mozilla.org/en-US/docs/Learn/
https://developer.mozilla.org/en-US/search?q=URL
```

![URL구조](https://developer.mozilla.org/en-US/docs/Learn/Common_questions/Web_mechanics/What_is_a_URL/mdn-url-all.png)

- scheme(스키마): 브라우저가 리소르를 요청하는 데 사용해야 하는 `프로토콜(데이터를 교환하거나 전송하기 위한 설정)`
- domain name(도메인네임): 요청하는 웹 서버, IP주소를 사용할 수도 있다.
- port(포트): 웹 서버의 리소스에 접근하는 데 사용되는 '게이트', 생략 가능
- path(경로): 웹 서버의 파일 위치, 최근에는 물리적 실체가 없는 웹 서버가 처리한다.
- parameter(매개변수): 웹 서버에 제공되는 추가 키/값. 리소르를 반환하기 전 매개변수를 사용하여 추가 작업을 수행할 수 있다.
- anchor(앵커): 리소스 내부에서 '책갈피'역할로, 브라우저에 해당 지점의 콘텐츠를 표시하도록 지시한다.

__절대 URL vs 상대 URL__

|절대URL|상대URL|
|:---:|:---:|
|브라우저의 주소 표시줄에서 사용|HTML 페이지와 같은 문서 내에서 사용되는 경우|
|URL의 경로가 "`/`"로 시작하는 경우|URL의 경로가 "`/`"로 시작하지 `않는` 경우|
|`https://developer.mozilla.org/ko/docs/Learn`|`Skills/Infrastructure/Understanding_URLs`|
|`/ko/docs/Learn`|`../CSS/display`|

__시맨틱 URL__

기술적 노하우와 상관없이 누구나 이해할 수 있는 고유의 의미를 가진 단어 사용

- URL을 쉽게 조작할 수 있다.
- 사용자에게 현재 위치와 하는 일, 상호작용 등에 대해 명확하게 설명할 수 있다.
- 검색엔진에서 관련 페이지의 분류를 개선할 수 있다.


## REST API

> API란?

-  응용 프로그램에서 사용할 수 있도록, 운영체제나 프로그래밍 언어에서 제공하는 기능을 제어할 수 있게 해주는 인터페이스
- 어플리케이션 간에 지정된 형식으로 요청과 응답할 수 있도록 연결
- ex. 카셰어링앱, 맛집예약앱 등 실시간 지도 API(구글/네이버 maps)

> REST API

- 다른 컴퓨터나 프로그램과의 소통이 쉽다.
- 인터넷 식별자 URI와 HTTP를 기반으로 한다.
- 브라우저 간 호환성이 좋은 `JSON` 형식 사용
- 각 요청이 어떤 정보나 동작을 위한 것인지 모습자체만으로 추론 가능
- REST: 문서, 그림, 데이터 등의 자원을 이름으로 구분하여 해당 자원에 대한 상태와 정보를 주고받는 것, `HTTP 메소드를 활용해 CRUD를 적용`
- GET, POST, PUT, DELETE, PATCH 를 주로 사용


> CRUD: 
`C`reate(삽입)
`R`read(읽기)
`U`pdate(갱신)
`D`elete(삭제)

## Fetch API

네트워크 통신을 포함한 리소스 취득을 위한 인터페이스가 정의되어 있고 `XMLHttpRequest` 보다 강력하고 유연한 조작이 가능

### 사용 방법

- Fetch 에는 `Request`와 `Response_(en-US)`가 포함되어 있다.
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

## ReableStream

## Unicode

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