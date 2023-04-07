
## React Testing Library

- [공식 사이트](https://testing-library.com/docs/react-testing-library/intro/)
- [깃헙](https://github.com/testing-library/react-testing-library)

React 컴포넌트를 사용자 입장에 가깝게 테스트할 수 있는 도구로, 컴포넌트를 사용하는 코드를 작성하면서 해당 컴포넌트의 인터페이스를 점검할 수 있다.

- [jest-dom](https://github.com/testing-library/jest-dom) : 자체적인 test runner와 test util 제공, 리액트에서 DOM 시뮬레이션을 하기 위한 도구

```javascript
import { render, screen } from '@testing-library/react';

import TextField from './TextField';

test('TextField', () => {	
	const text = 'Tester';
	const setText = () => {
		// do nothing...
	};

	render((	
		<TextField
			label="Name"
			placeholder="Input your name"
			text={text}
			setText={setText}		
		/>
	));
	
	screen.getByLabelText('Name');
});
```

## given - when - then 패턴

테스트 코드를 작성하는 표현 방식.
[준비 - 실행 - 검증]

> 💡 마틴 파울러의 [GivenWhenThen](https://martinfowler.com/bliki/GivenWhenThen.html)

1. Given (준비)

테스트를 위해 준비하는 과정. 테스트에 사용하는 변수, 입력 값 등을 정의하거나 Mock 객체(테스트 대상)를 정의하는 구문이 포함된다.

2. When (실행)

실제로 액션을 위한 테스트를 실행하는 과정.
하나의 메서드만 수행하는 것이 좋다. 가장 중요하지만 가장 짧은 구문.

3. Then (검증)

테스트를 검증하는 과정. 예상한 값, 실제 실행을 통해서 나온 값을 검증한다.

## Mocking

테스트하고자 하는 코드가 의존하는 function이나 class에 대해 모조품을 만들어 `'일단'` 돌아가게 하는 것.
단위 테스트를 작성할 때, 해당 코드가 의존하는 부분을 대체할 가짜를 만드는 기법이다.

### 🤔 왜 mocking을 하는가?

1. 테스트하고자 하는 기능이 다른 기능들과 엮여있을 경우 정확한 테스트를 하기 힘들기 때문에.
2. 외부 API가 정상적으로 작동하지 않아서.
3. 외부 API를 호출할 때 비용이 발생하는 경우.

## Test fixture

테스트를 위해 변경되지 않는 상태나 데이터를 미리 만들어 두는 작업을 `Test Fixture`를 만든다고 한다.

### 🤔 왜 Fixture를 만들어야 할까?

외부 요인의 간섭을 최대한 없애야 한다.
외부 DB나 API등 대상 서버의 네트워크, 정기작업 이슈가 있다면 테스트를 진행할 수 없기 때문이다.

- 중복 발생되는 행위를 고정시켜 한 곳에서 관리
- 테스트에서 같은 구성의 Data Set을 사용하고자 할 때 유용(재사용)
- 객체 형태로 설정하여 테스트 가능

