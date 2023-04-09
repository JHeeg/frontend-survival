## MSW

- [MSW (Mock Service Worker)](https://mswjs.io/)
- [Service Worker API](https://developer.mozilla.org/ko/docs/Web/API/Service_Worker_API)

## Service Worker

- javascript로 작성된 이벤트 기반 워커
- 웹에서의 네트워크 요청 등의 이벤트를 가로채어 수정하고, 다시 페이지로 돌려보낸다.
- 서비스에서 사용하는 리소스를 캐싱할 수 있다.

![서비스 워커](https://fe-developers.kakaoent.com/static/fb5f782544bb2f92ee6fe4aa7746dffc/705cc/service-worker-layer-diagram.png)

- 브라우저와 네트워크 사이의 독립된 계층에 존재
- 오프라인 상태이거나 네트워크가 불안정한 경우 브라우저에 캐시 된 리소스를 전달 할 수 있다.

## MSW(Mock Service Worker)

서비스워커를 이용해 서버를 향한 실제 네트워크 요청을 가로채서 모의 응답을 보내주는 API Mocking 라이브러리.

**MSW의 장점**

- 직접 Mock 서버를 구현하지 않고 네트워크 수준에서 API Mocking을 할 수 있기 때문에 백엔드에서 API가 나오기 전에 개발을 먼저 시작할 수 있다.
- Mocking 테스트를 위한 노드환경, 개발 및 디버깅을 위한 브라우저 환경에서 모두 사용할 수 있다.
- 소스코드 수정 없이 모킹이 필요한 환경에서만 MSW 인스턴스를 실행해 API Mocking을 적용할 수 있다.

### MSW 사용해보기

1. MSW 설치

```bash
npm i -D msw
```

2. setting

`jest.config.js` 파일의 "setupFilesAfterEnv" 속성에 `setupTest.ts` 파일을 추가해준다.

```javascript
module.exports = {
  testEnvironment: 'jsdom',
  setupFilesAfterEnv: [
    '@testing-library/jest-dom/extend-expect',
    '<rootDir>/src/setupTests.ts',
  ],
  transform: {
    '^.+\\.(t|j)sx?$': ['@swc/jest', {
      jsc: {
        parser: {
          syntax: 'typescript',
          jsx: true,
          decorators: true,
        },
        transform: {
          react: {
            runtime: 'automatic',
          },
        },
      },
    }],
  },
};
```

3. `src/setupTests.ts` 생성

```javascript
import server from './mocks/server';

beforeAll(() => server.listen({ onUnhandledRequest: 'error' }));

afterAll(() => server.close());

afterEach(() => server.resetHandlers());
```

4. `src/mocks/server.ts` 생성

```javascript
import { setupServer } from 'msw/node';

import handlers from './handlers';

const server = setupServer(...handlers);

export default server;
```

5. `src/mocks/handlers.ts` 생성

```javascript
import { rest } from 'msw';

const BASE_URL = 'http://localhost:3000';

const handlers = [
  rest.get(`${BASE_URL}/products`, (req, res, ctx) => {
    const products = [
      {
        category: 'Fruits', price: '$1', stocked: true, name: 'Apple',
      },
    ];

    return res(
      ctx.status(200),
      ctx.json({ products }),
      );
    }),
  ];

export default handlers;
```

6. `App.test.ts`

```javascript
import { render, screen, waitFor } from '@testing-library/react';

import App from './App';

// jest.mock 불필요.

test('App', async () => {
  render(<App />);

  await waitFor(() => {
    screen.getByText('Apple');
  });
});
```

## polyfill(폴리필)

polyfill은 기본적으로 지원하지 않는 이전 브라우저에서 최신 기능을 제공하는 데 필요한 코드

IE11 을 사용할 때는 fetch API가 동작하지 않기 때문에, `polyfill`로 지원되지 않는 기능을 사용할 수 있게 해준다.

Node.js 환경에서는 작동하지 않으며, `웹 브라우저 전용`이다.
