# 4. Testing Library

## [Jest](https://jestjs.io/)

Javascript 테스트 프레임워크로, Babel, TypeScript, Node, React, Angular, Vue 등 다양한 프로젝트에서 사용 가능하다.

* 기본 사용법

```javascript
test('add', () => {
  expect(add(1, 2)).toBe(3);
});
```

* BDD 스타일 사용법
* 표현력이 좋아지며, 좀 더 고민해볼 수 있다.

```javascript
describe('add', () => {
  it('returns sum of two numbers', () => {
    expect(add(1, 2)).toBe(3);
  });
});
```

\


## [React Testing Library](https://testing-library.com/docs/react-testing-library/intro/)

* UI 테스트에 특화된 라이브러리
* “F/E 테스트 = only React 컴포넌트 테스트”가 되면 쓸데없이 너무 많은 테스트 코드를 작성할 위험이 있고, 유지보수가 더 힘들어질 수 있기 때문에 주의해야 한다.
