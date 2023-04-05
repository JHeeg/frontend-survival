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