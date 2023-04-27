# 2. TSyringe

## [TSyringe](https://github.com/microsoft/tsyringe)

Lightweight dependency injection container for JavaScript/TypeScript

* TypeScript용 DI도구(IoC Container)로 External Store를 관리하는데 활용
* React 컴포넌트 입장에서는 '전역' 처럼 여겨지고, [<mark style="background-color:green;">"Prop Drilling"</mark>](https://react.dev/learn/passing-data-deeply-with-context#the-problem-with-passing-props) 문제를 해결할 수 있는 방법 중 하나이다.

## [의존성주입(DI)](https://ko.wikipedia.org/wiki/%EC%9D%98%EC%A1%B4%EC%84%B1\_%EC%A3%BC%EC%9E%85)

의존성 주입은 객체의 생성과 사용의 관심을 분리하는 것이다. 즉, 가독성과 코드 재 사용성을 높여 준다.

👍🏻 장점

* 클라이언트의 구성 가능성을 유연하게 해준다.
* 시스템의 구성 세부 사항을 외부의 구성 파일에서 사용하여, 리컴파일 없이 시스템을 재 구성할 수 있다.
* 코드의 동작에서 어떠한 변경도 요구하지 않기 때문에 리팩터링으로써 레거시 코드에도 적용할 수 있다.
* 클라이언트는 사용해야하는 모든 구체적인 구현에 대한 지식을 제거할 수 있다.

## reflect-metadata

📎 Github : [reflect-metadata](https://github.com/rbuckton/reflect-metadata)



## 싱글톤 패턴 (Singleton pattern)

'하나'의 인스턴스만 생성하여 사용하는 디자인 패턴 (**똑같은 인스턴스를 여러개 만들지 않고 기존의 인스턴스를 활용**)\


#### Why?

객체를 생성할 때마다 메모리 영역을 할당받아야 하지만, 한 번의 new를 통해 객체를 생성하면 메모리 낭비를 방지할 수 있다. 싱글톤으로 구현한 인스턴스는 '전역' 이므로, 다른 클래스의 인스턴스들이 데이터를 공유하는 것이 가능한 장점도 있다.

####

### 의존성 설치

```bash
npm i tsyringe reflect-metadata
```

src/main.tsx, src/setupTests.ts 파일에서 reflect-metadata import.

```typescript
import 'reflect-metadata'
```

싱글톤으로 관리할 CounterStore class 준비

```typescript
import { singleton } from 'tsyringe';

@singleton()
class CounterStore {
    // ...
}
```

싱글톤 CounterStore 객체 사용

```typescript
import { container } from from 'tsyringe';

const counterStore = container.resolve(CounterStore);
```

테스트에서 TSyringe에서 관리하는 객체 초기화

```typescript
container.clearInstances();
```



