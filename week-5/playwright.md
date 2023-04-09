## Playwright

**웹 브라우저 기반의 E2E 테스트 자동화 도구**

## E2E(End to End) Test

Ednpoint 간의 테스트로 사용자의 입장에서 사 용자가 사용하는 상황을 가정하고 테스트 하는 것

- 웹이나 어플 등에서 GUI를 통해 시나리오, 기능 테스트 등을 수행
- 사용자에게 직접적으로 노출되는 부분을 점검
- 유닛 테스트로 불가능한 사용자 관점의 테스트가 가능
- 백엔드 관점에서 개발한 REST API를 테스트 하기 위해 실제로 서버에 요청을 보낸 뒤 클라이언트에서 원하는 데이터가 전송되는 지 확인
- E2E 프레임워크
  - 웹 환경 : selenium, testCafe, cypress, nightwatch 등
  - express 환경 : supertest

## Headless Chrome

>💡 Headless 란?
>
> **백그라운드에서 작동하는 브라우저**
>
> 일반 사용자가 브라우저를 사용할 때처럼 화면에 창이 시각적으로 나타나지는 않는다.

Headless 환경에서 Chrome 브라우저를 실행하는 방법으로, Chrome 59 버전에서 추가되었으며 이전에는 `PhantomJS`를 이용해서 Headless 테스트를 했다.

헤드리스 브라우저는 눈에 보이는 UI 셸이 필요하지 않은 자동화된 테스트 및 서버 환경을 위한 훌륭한 도구이다.

- 실제 웹 페이지에 대해 테스트를 실행
- PDF로 출력
- 브라우저가 URL을 렌더링하는 방법을 검사

## Puppeteer

**구글에서 개발한 노드 기반의 라이브러리**

### Puppeteer의 특징

- 여러 iframe이나 popup으로 이루어진 복잡한 화면을 제어하는것이 가능하다.
- DevTools 프로토콜을 이용하여 직접 Chrome을 제어하고 사용할 수 있다.
- DevTools 프로토콜로 마우스와 키보드뿐 아니라 브라우저의 스크린 크기, 쿠키 및 세션 스토리지, 서비스 워커를 제어할 수 있다.
- 직접 Chrome을 구동하여 사용자들이 직접 사용하는 환경과 비슷하게 동작하는 것을 직접 보면서 확인할 수 있다.

### Puppeteer의 기능

- SPA 화면의 렌더링이 가능하다
- 렌더링후 키보드, 마우스 입력을 제어할 수 있다.
- 웹페이지의 자동 테스트 도구를 만들 수 있다.
- 웹페이지 크롤링이 가능하다.
- 페이지를 캡처하거나 PDF로 출력할 수 있다.

## Playwright

**MS에서 만든 웹 테스트 자동화 라이브러리**

- 하나의 API로 Chrominum, Firfox, WebKit 까지 테스트 가능.
- Puppeteer보다 테스트에 특화되어있다.
- 크로스 브라우징 테스트가 가능해지고 자체 Test runner를 제공한다.([@playwright/test](https://github.com/microsoft/playwright/tree/main/packages/playwright-test))

### Playwright 설치 및 사용

1. 패키지 설치
```bash
npm i -D @playwright/test eslint-plugin-playwright
```

2. `playwright.config.ts` 작성

```javascript
import { PlaywrightTestConfig } from '@playwright/test';

const config: PlaywrightTestConfig = {
	testDir: './tests',
	retries: 0,
	use: {
		baseURL: 'http://localhost:8080',
		headless: !!process.env.CI,
		screenshot: 'only-on-failure',
	},
};

export default config;
```

3. `test/.eslintrc.js`

```javascript
module.exports = {
	env: {
		jest: false,
	},
	extends: ['plugin:playwright/playwright-test'],
	rules: {
		'import/no-extraneous-dependencies': 'off',
	},
};
```

4. `test/home.spec.ts` 작성

```javascript
import { test, expect } from '@playwright/test';

test('Filter products', async ({ page }) => {
	await page.goto('/');

	await expect(page.getByText('Apple')).toBeVisible();

	const searchInput = page.getByLabel('Search');

	await searchInput.fill('a');

	await expect(page.getByText('Apple')).toBeVisible();

	await searchInput.fill('aa');

	await expect(page.getByText('Apple')).toBeHidden();
});

test('Click the “Increase” button', async ({ page }) => {
	await page.goto('/');

	const count = 13;

	await Promise.all((
		[...Array(count)].map(async () => {
			await page.getByText('Increase').click();
		})
	));

	await expect(page.getByText(`${count}`)).toBeVisible();
});
```

5. 테스트 실행

```bash
npx playwright test
```

6. `.gitignore` 파일에 에러 상황의 스크린샷 등이 담기는 `test-results` 디렉터리 추가하여 관리

```bash
echo "/tst-results/" > .gitignore
```

## CodeceptJS

**인간 친화적인 E2E 테스팅 도구**

- [CodeceptJS](https://codecept.io/)
- [CodeceptJS 3 시작하기](https://github.com/ahastudio/til/blob/main/test/20201207-codeceptjs.md)
- [CodeceptJS 사용](https://github.com/ahastudio/CodingLife/tree/main/20211012/react#codeceptjs-사용)


