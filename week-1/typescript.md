# 2. TypeScript

⭐️ [타입스크립트](https://www.typescriptlang.org/ko/) 공식문서

- [TypeScript for the New Programmer](https://www.typescriptlang.org/ko/docs/handbook/typescript-from-scratch.html)
- [TypeScript for JavaScript Programmers](https://www.typescriptlang.org/ko/docs/handbook/typescript-in-5-minutes.html)

## 1. REPL

- REPL(read-eval-print loop)
- 사용자의 입력을 읽고 명령어를 실행하고 사용자에게 결과를 반환해주며, 이 작업을 반복한다.

### ts-node 사용

```Bash
# REPL 실행
npx ts-node
```

<br />

## 2. TypeScript

### 타입지정

- 복잡한 오브젝트의 타입을 재사용하기 위해 타입을 정의할 수 있다.
  - [타입 정의하기 (Defining Types)](https://www.typescriptlang.org/ko/docs/handbook/typescript-in-5-minutes.html#%ED%83%80%EC%9E%85-%EC%A0%95%EC%9D%98%ED%95%98%EA%B8%B0-defining-types)
  - [타입 별칭과 인터페이스의 차이점](https://www.typescriptlang.org/ko/docs/handbook/2/everyday-types.html#%ED%83%80%EC%9E%85-%EB%B3%84%EC%B9%AD%EA%B3%BC-%EC%9D%B8%ED%84%B0%ED%8E%98%EC%9D%B4%EC%8A%A4%EC%9D%98-%EC%B0%A8%EC%9D%B4%EC%A0%90)

### [타입 추론](https://www.typescriptlang.org/ko/docs/handbook/typescript-in-5-minutes.html#%ED%83%80%EC%9E%85-%EC%B6%94%EB%A1%A0-types-by-inference)

- 타입을 모두 지정하지 않아도 알아서 추론해준다.

### [Union Type](https://www.typescriptlang.org/ko/docs/handbook/typescript-in-5-minutes.html#%EC%9C%A0%EB%8B%88%EC%96%B8-unions)

- 여러 타입 중 하나로 `boolean (true/false)` 를 생각할 수 있다.
- 매개변수를 제한하려 할 때 유용하다.

```TypeScript
type Category = 'food' | 'toy' | 'bag';

function fetchProducts({ category }: { category: Category }) {
  console.log(`Fetch ${category}`);
}
```

- 레거시 환경 / 코드 에서 사용 [React Types](https://github.com/facebook/react/blob/main/packages/shared/ReactTypes.js) 중 `ReactNode`가 대표적이다.

```TypeScript
export type ReactNode =
  | React$Element<any>
  | ReactPortal
  | ReactText
  | ReactFragment
  | ReactProvider<any>
  | ReactConsumer<any>;
```

### [Intersection Type](https://www.typescriptlang.org/docs/handbook/2/objects.html#intersection-types)

- [교집합](https://www.typescriptlang.org/ko/docs/handbook/typescript-in-5-minutes-func.html#%EA%B5%90%EC%A7%91%ED%95%A9)
- 타입을 확장하는 방법

  ```TypeScript
  type Human = {
    name: string;
    age: number;
  };

  type Creature = {
    hp: number;
    mp: number;
  };

  type Person = Human & Creature;

  let person: Person;

  person = { name: '홍길동', age: 13, hp: 256, mp: 16 };
  ```

### Optional Parameter

- [선택적 매개변수](https://www.typescriptlang.org/docs/handbook/2/functions.html#optional-parameters)
- 물음표(?) 를 사용하여 매개변수를 선택사항으로 표시한다.

```TypeScript
function greeting(name?: string): string {
  return `Hello, ${name || 'world'}`;
}

// 기본값을 잡아주는 것도 좋다.
function greeting(name: string = 'world'): string {
  return `Hello, ${name}`;
}
```

- 오브젝트일 때도 활용 가능하지만 아래처럼 사용할 경우 ts-node에선 해석이 불가능하기 때문에 한 줄로 붙여쓰거나 type 등으로 따로 잡아주면 가능하다.

```TypeScript
function greeting({ name, age }: {
  name: string;
  age?: number;  
}): string {
  return age ? `${name} (${age})` : name;
}

// 한줄
function greeting({ name, age }: { name: string; age?: number; }): string {
  return age ? `${name} (${age})` : name;
}

// type으로 분리
type Human = {
  name: string;
  age?: number;
};

function greeting({ name, age }: Human): string {
  return age ? `${name} (${age})` : name;
}

greeting()

greeting({ name: '홍길동' })

greeting({ name: '홍길동', age: 13 })
```
