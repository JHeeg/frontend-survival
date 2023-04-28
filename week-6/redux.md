# 3. Redux 따라하기

## Redux란?

📎 [Redux 공식 문서](https://redux.js.org/)

* 자바스크립트 상태관리 라이브러리
* 일관성 있게 동작하고 서로 다른 환경(클라이언트, 서버, 네이티브)에서 실행되며, 테스트하기 쉬운 애플리케이션을 만들 수 있도록 도와준다.
* 최상의 개발자 경험을 제공하기 위한 타임 트래블 디버거를 결합한 라이브 코드 편집 등의 기능을 제공한다.
* vuejs, react와 함께 사용할 수 있다.

### 기본 세가지 원칙

1. 동일한 데이터는 <mark style="background-color:orange;">Store</mark>라는 하나의 공간에서 가져온다.
2. <mark style="background-color:orange;">Action</mark> 이라는 객체를 통해 상태를 변경할 수 있다.
3. 순수 함수로만 변경이 가능하다.

#### ✔️ Store (스토어)

상태가 관리되는 하나의 공간

* 컴포넌트와는 별개로 스토어라는 공간에 어플리케이션의 필요한 상태를 담아둔다.
* 컴포넌트에서 상태 정보가 필요할 때 스토어에 접근한다.

#### ✔️ Action (액션)

어플리케이션에서 스토어에 전달할 데이터로, 자바스크립트 객체 형식으로 되어있다.

#### ✔️ Reducer (리듀서)

* Action -> Reducer -> Store
* 액션을 리듀서에 전달 후 리듀서가 확인 후 스토어의 상태를 업데이트 한다.
* 액션을 리듀서에 전달하기 위해서는 dispatch() 메서드를 사용한다.

## Redux의 장점

* 상태를 예측 가능
* 유지보수 편리
* 디버깅에 유리
* 테스트를 붙이기에 용의





<details>

<summary>🙇‍♀️ 도움이 된 사이트</summary>

* [https://hanamon.kr/redux%EB%9E%80-%EB%A6%AC%EB%8D%95%EC%8A%A4-%EC%83%81%ED%83%9C-%EA%B4%80%EB%A6%AC-%EB%9D%BC%EC%9D%B4%EB%B8%8C%EB%9F%AC%EB%A6%AC/](https://hanamon.kr/redux%EB%9E%80-%EB%A6%AC%EB%8D%95%EC%8A%A4-%EC%83%81%ED%83%9C-%EA%B4%80%EB%A6%AC-%EB%9D%BC%EC%9D%B4%EB%B8%8C%EB%9F%AC%EB%A6%AC/)

<!---->

* [https://redux.js.org/tutorials/essentials/part-1-overview-concepts](https://redux.js.org/tutorials/essentials/part-1-overview-concepts)

</details>
