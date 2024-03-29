# External Store

## 관심사의 분리 (Separation of Concerns)

🔗 [참고1](https://ko.wikipedia.org/wiki/%EA%B4%80%EC%8B%AC%EC%82%AC_%EB%B6%84%EB%A6%AC)

🔗 [참고2](https://velog.io/@seanlion/soc1)

관심사란 컴퓨터 프로그램 코드에 영향을 미치는 정보의 집합으로, 하나의 시스템은 작은 부품(정보)이 모여서 만들어진다.

관심사는 코드 최적화가 필요한 하드웨어의 세세한 부분만큼 포괄적이거나, 시작할 클래스의 이름처럼 구체적일 수 있다.

흔히 사용되는 **Layered Architecture**에선 `사용자에게 가까운 것`과 `사용자에게서 먼 것`으로 구분한다. 가장 가까운 건 UI를 다루는 부분, 그 다음엔 Business Logic을 다루는 부분, 그 너머에는 데이터에 접근하고 저장하는 부분으로 나눌 수 있게 된다. 각 부분은 하나의 역할, 하나의 관심사로 격리됨으로써 `복잡도`를 낮추게 된다.

`Input → Process → Output`이란 3단계로 코드를 적절히 구분만 해도 코드를 이해하고 유지보수하는데 크게 도움이 된다. 하나의 Output은 다시 사용자에게 Input을 요청하게 되고, 일반적인 프로그램은 다음과 같이 계속 순환하는 구조가 된다.

✍🏻 일반적인 프로그램의 순환구조

1. Input: 프로그램 시작
2. Process: 프로그램 초기화
3. Output: 사용자에게 초기 UI 보여주기
4. Input: 사용자의 입력
5. Process: 사용자의 입력에 따라 처리
6. Output: 처리 결과 보여주기
7. Input: 사용자의 또 다른 입력
8. …반복…

널리 알려진 MVC로 매핑하면 다음과 같다.

- Model → Process
- View → Output
- Controller → Input

## Flux Architecture

🔗 [Flux란?](https://haruair.github.io/flux/docs/overview.html)

Facebook에서 MVC의 대안으로 내세운 아키텍처.

2-way binding을 썼을 때 생길 수 있는 Model-View의 복잡한 관계(전통적인 MVC에선 이런 상황을 지양한다)를 겨냥해 명확히 “**unidirectional data flow**”를 강조한다.

1. Action → 이벤트/메시지 같은 객체.
2. Dispatcher → (여러) Store로 Action을 전달. 메시지 브로커와 유사하다.
3. Store (여러 개) → 받은 Action에 따라 상태를 변경. 상태 변경을 알림.
4. View → Store의 변화를 모니터링하여 상태를 반영.

🔗 [Redux Ovefrview & Concept](https://ko.redux.js.org/tutorials/essentials/part-1-overview-concepts/)

Redux는 단일 Store를 사용함으로써 좀 더 단순한 그림을 제안한다.

![Redux](https://ko.redux.js.org/assets/images/one-way-data-flow-04fe46332c1ccb3497ecb04b94e55b97.png)

1. Action
2. Store → dispatch를 통해 Action을 받고, 사용자가 정의한 reducer를 통해 State를 변경한다.
3. View → State를 반영.

Action을 어떻게 표현하느냐가 사용성에 큰 차이를 만들지만 상태를 UI에 반영하는 방법은 모두 동일하다.

3단계 프로세스와 매핑하면 다음과 같다.

- Input → Action + dispatch
- Process → reducer
- Output → View(React)

## External Store (useReducer, useCallback)

🔗 [ForceUpdate와 같은 것이 있습니까?](https://ko.reactjs.org/docs/hooks-faq.html#is-there-something-like-forceupdate)

- `useState`와 `useReducer Hook`은 다음 값이 이전 값과 같으면 업데이트에서 제외된다. State를 변경하고 setState를 호출해도 다시 렌더링 되지 않는다.
- 일반적으로 React에서 로컬 state를 변경해서는 안되지만, 도피 수단으로 증가하는 카운터를 사용하여 `state가 변경되지 않은 경우에도 강제로 다시 렌더링 할 수 있다.`

```tsx
// 가능한 피해주면 좋은 패턴
const [ignored, forceUpdate] = useReducer(x => x + 1, 0);

function handleClick() {
  forceUpdate();
}
```

```tsx
const [, setState] = useState({});
const forceUpdate = () => setState({});
```

- 커스텀 Hook 사용

```tsx
function useForceUpdate() {
  [, setState] = useState({});
  return useCallback(() => setState({}), []);
}
```

이러한 방식을 잘 활용하면 React가 UI를 담당하고, 순수한 TypeScript(또는 JavaScript)가 비즈니스 로직을 담당하는, `관심사의 분리(Separation of Concerns)`를 명확히 할 수 있다. 자주 바뀌는 UI 요소에 대한 테스트 대신, 오래 유지되는(바뀌면 치명적인) 비즈니스 로직에 대한 테스트 코드를 작성해 유지보수에 도움이 되는 테스트 코드를 치밀하게 작성할 수 있다.
