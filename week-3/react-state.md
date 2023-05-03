# 2. React State

[Thinking in React](https://react.dev/learn/thinking-in-react)

* “Step 3: Find the minimal but complete representation of UI state”
* “Step 4: Identify where your state should live”
* “Step 5: Add inverse data flow”

## React State란?

* '변경'을 다루기 위한 요소. **(Re-rendering)**
* 상태 변화가 있으면 해당 컴포넌트와 하위 컴포넌트를 리렌더링 한다.
* 만드는 것은 자유지만 일관성과 효율을 위해 DRY 원칙을 따르는 SSOT를 만든다.

> 💡\
>
>
> #### [DRY (Don't Repeat Yourself)](https://ko.wikipedia.org/wiki/%EC%A4%91%EB%B3%B5%EB%B0%B0%EC%A0%9C)
>
> 중복 배제 _`“소스 코드에서 동일한 코드가 반복이 된다는 것은 잠재적인 버그의 위협을 증가시킨다”`_
>
> #### [SSOT (Single Source of Truth)](https://ko.wikipedia.org/wiki/%EB%8B%A8%EC%9D%BC\_%EC%A7%84%EC%8B%A4\_%EA%B3%B5%EA%B8%89%EC%9B%90)
>
> 데이터를 하나의 공간에 저장하는 것.

### React State의 조건

1. 상태가 변경되지 않는 것은 state로 다룰 필요가 없다.
2. 부모 컴포넌트로부터 props를 통해 전달받은 것은 state가 아니다.
3. 다른 state나 props로 계산 가능하다면 state가 아니다.

상태가 많아질 수 있는데 TypeScript를 _`잘`_ 쓰면 상태의 수를 줄여서 직접 관리하는 것이 줄어들고, 재사용할 때 부담감이 줄어든다.

> React에서는 해당 상태에 의존적인 컴포넌트를 모두 포함하는 `최상위 컴포넌트`가 상태를 소유해야 한다.
>
> * [“Lifting State Up”](https://ko.reactjs.org/docs/lifting-state-up.html)
> * [Sharing State Between Components](https://beta.reactjs.org/learn/sharing-state-between-components)

### Lifting State Up

React 코드를 작성하는 가장 일반적인 작업 중 하나 두 구성 요소의 상태가 동시에 변경되야 한다면 각각의 컴포넌트에서 상태를 제거하고 가장 가까운 공통의 부모에서 props로 전달한다.

## Inverse Data Flow

하위 컴포넌트의 props로 함수를 전달 (=`콜백함수`)
