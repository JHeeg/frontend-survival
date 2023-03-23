# React로 사고하기

[Thinking in React](https://react.dev/learn/thinking-in-react)

- “Step 3: Find the minimal but complete representation of UI state”
- “Step 4: Identify where your state should live”
- “Step 5: Add inverse data flow”

## React의 State

- '변경'을 다루기 위한 요소.
- 상태 변화가 있으면 해당 컴포넌트와 하위 컴포넌트를 리렌더링 한다.
- 만드는 것은 자유지만 일관성과 효율을 위해 DRY 원칙을 따르는 SSOT를 만든다.

> 💡 <br />
> [DRY (Don’t Repeat Yourself)](https://ko.wikipedia.org/wiki/중복배제)<br />
> [SSOT (Single Source of Truth)](https://ko.wikipedia.org/wiki/단일_진실_공급원)


### React State의 조건
1. 상태가 변경되지 않는 것은 state로 다룰 필요가 없다.
2. 부모 컴포넌트로부터 props를 통해 전달받은 것은 state가 아니다.
3. 다른 state나 props로 계산 가능하다면 state가 아니다.

상태가 많아질 수 있는데 TypeScript를 잘 쓰면 상태의 수를 줄여서 직접 관리하는 것이 줄어들고, 재사용할 떄 부담감이 줄어든다.


> 그렇다면 그 상태를 누가 관리해야 할까? 더 정확히는, 상태를 누가 소유해야 할까?
> - React에서는 해당 상태에 의존적인 컴포넌트를 모두 포함하는 최상위 컴포넌트가 상태를 소유해야 한다.
> - [“Lifting State Up”](https://ko.reactjs.org/docs/lifting-state-up.html)
> - [Sharing State Between Components](https://beta.reactjs.org/learn/sharing-state-between-components)