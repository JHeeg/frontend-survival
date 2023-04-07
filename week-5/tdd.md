## TDD (Test Driven Development)

> 💡 테스트 코드를 먼저 작성하는, 구현보다 인터페이스와 스펙을 먼저 정의함으로써 개발을 진행하는 방식.

- [테스트 주도 개발](http://wiki.c2.com/?TestDrivenDevelopment)
- [TDD FAQ](https://github.com/ahastudio/til/blob/main/blog/2016/12-03-tdd-faq.md)

### TDD Cycle

1. `Red`: 실패하는 테스트 코드를 작성, 인터페이스와 스펙에 집중
2. `Green`: 올바른 방법이 아니어도 테스트를빠르게 통과시킨다.
3. `Refactor` : 리팩터링을 통해서 코드를 깔끔하고 바르게 만든다. TDD에서 가장 중요한 부분이지만, 관과할 때가 많다.

작은 단위에서부터 반복하면서 코드에서 피드백을 얻는다. TDD cycle이 익숙해지지 않으면 일반적인 개발이나 클린 코드를 작성하는 것 조차 힘들어진다.

## Jest

- [Jest](https://jestjs.io/)
- [Jest를 이용한 간단한 TDD 예제](https://github.com/ahastudio/til/blob/main/jest/20201204-simple-tdd-example.md)

facebook 에서 만든 테스팅 도구.

테스트 케이스를 정의하는 방법

1. test 함수로 개별 테스트를 나열

```typescript
function add(x: number, y:number): number {
  return x + y;
}

test('add', () => {
  expect(add(1, 2)).toBe(3);
})
```

2. BDD 스타일로 주체-행위 중심으로 테스트를 조직화하는 방식

```typescript
describe('add', () => {
  it('returns sum of two numbers', () => {
    expect(add(1, 2)).toBe(3);
  })
})
```


3. Describe - Context - It 패턴

```typescript
const context = describe;

describe('add', () => {
  context('with no argument', () => {
    it('returns zero', () => {
      expect(add()).toBe(0);
    });
  });

  context('with only one number', () => {
    it('returns the same number', () => {
      expect(add(1)).toBe(1);
    });
  });

  context('with two numbers', () => {
    it('returns sum of two numbers', () => {
      expect(add(1, 2)).toBe(3);
    });
  });

  context('with three numbers', () => {
    it('returns sum of three numbers', () => {
      expect(add(1, 2, 3)).toBe(6);
    });
  });
});
```

<br />

> 💡 Jest에서 TypeScript 사용하려면 **`jest.config.js`** 파일을 작성해야한다.
>
> ```typescript
>module.exports = {
> testEnvironment: 'jsdom',
> setupFilesAfterEnv: [
>   '@testing-library/jest-dom/extend-expect',
> ],
> transform: {
>   '^.+\\.(t|j)sx?$': ['@swc/jest', {
>     jsc: {
>       parser: {
>         syntax: 'typescript',	
>         jsx: true,
>         decorators: true,
>       },
>       transform: {	
>         react: {
>           runtime: 'automatic',
>         },
>       },
>     },
>   }],
> },
>};
>```
>

## 단위테스트

단위 테스트(Unit Test)는 하나의 모듈을 기준으로 독립적으로 진행되는 가장 작은 단위의 테스트이다. 모듈은 애플리케이션에서 작동하는 하나의 기능 또는 메소드이다.
웹 애플리케이션에서 로그인 메소드에 대한 독립적인 테스트가 1개의 단위테스트가 될 수 있다.

즉, 단위 테스트는 애플리케이션을 구성하는 하나의 기능이 올바르게 동작하는지를 독립적으로 테스트하는 것으로, `"어떤 기능이 실행되면 어떤 결과가 나온다"` 정도로 테스트를 진행한다.

### 단위 테스트의 장점

- 테스팅에 대한 시간과 비용을 절감할 수 있다.
- 새로운 기능 추가 시에 수시로 빠르게 테스트 할 수 있다.
- 리팩토링 시에 안정성을 확보할 수 있다.
- 코드에 대한 문서가 될 수 있다.

### 좋은 단위 테스트란

- 1개의 테스트 함수에 대해 assert를 최소화한다.
- 1개의 테스트 함수는 1가지 개념만을 테스트 한다.