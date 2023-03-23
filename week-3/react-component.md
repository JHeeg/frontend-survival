# React로 사고하기

[Thinking in React](https://react.dev/learn/thinking-in-react)

- “Step 1: Break the UI into a component hierarchy”
- “Step 2: Build a static version in React”

## 데이터

B/E에서 JSON 형태의 데이터를 돌려주는 API를 제공한다고 가정(대부분은 `REST API` 또는 `GraphQL`).

__REST API__

- fetch API -> GET, POST, PUT/PATCH, DELETE (CRUD)
- Resource 중심

__GraphQL__

- Graph 자료 구조
- Query에서 얻고자 하는 것을 스키마 처럼 지정해줌
- Query(Read), Mutation(Command: Create, Update, Delete), Subscription(Event)

F/E는 이 데이터를 사용자가 볼 수 있도록 UI를 구성한다. React는 선언형(HTML과 유사한 모양의 DSL을 사용)으로 UI를 구성해 두면 내부가 변경되었을 때 자동으로 업데이트가 된다.

### JSON

🔗 [관련 링크](https://ko.wikipedia.org/wiki/JSON)

- F/E와 B/E가 서로 데이터를 교환하기 위해 만든 데이터 포맷
- 속성-값, 배열, 시리얼화 가능한 값 등의 데이터 오브젝트를 전달하기 위해 string으로 표현된 개방형 표준 포맷.

__JSON(문자열) 변환 방법__

- `parse()`: JSON 문자열을 자바스크립트 객체로 변환

```javascript
const json = '{"result":true, "count":42}';
const obj = JSON.parse(json);

console.log(obj.count);
// Expected output: 42

console.log(obj.result);
// Expected output: true
```

- `stringify()`: 객체를 JSON 문자열 형태로 변환

```javascript
console.log(JSON.stringify({ x: 5, y: 6 }));
// Expected output: "{"x":5,"y":6}"

console.log(JSON.stringify([new Number(3), new String('false'), new Boolean(false)]));
// Expected output: "[3,"false",false]"

console.log(JSON.stringify({ x: [10, undefined, function(){}, Symbol('')] }));
// Expected output: "{"x":[10,null,null,null]}"

console.log(JSON.stringify(new Date(2006, 0, 2, 15, 4, 5)));
// Expected output: ""2006-01-02T15:04:05.000Z""
```

## 컴포넌트 계층 구조

🔗 [React Component](https://react.dev/learn/thinking-in-react#step-1-break-the-ui-into-a-component-hierarchy)

__React의 강력한 특징__

- “Component-Based”
- “Build encapsulated components that manage their own state, then __compose__ them to make __complex UIs__.”
- 단순하고 간단한 캡슐화 된 컴포넌트들을 모아서 복잡한 UI를 만들 수 있다.

__컴포넌트의 기준__

- SRP (단일 책임 원칙) : 관련된 부분만 수정할 수 있도록 단일화 된 기능으로 쪼개줘야 한다.
- CSS : 클래스 선택자를 이용해서 공통된 요소의 스타일을 지정하여 재활용
- Design's Layer: ***`스타일가이드와 비슷한 개념일까?`***
- Information Architecture (JSON Schema의 영향)

[Atomic Design](https://bradfrost.com/blog/post/atomic-web-design/): 계층형 구조에 대한 기준을 몇 가지 카테고리로 묶은 것

## Extract Function

> 📕 마틴 파울러 - '리팩토링'
>> [Extract Function](https://refactoring.com/catalog/extractFunction.html)<br />
>> [Inline Function](https://refactoring.com/catalog/inlineFunction.html)

- 길게 코드를 작성하고, 적절하게 자를 수 있는 부분이 보이면 '함수'로 추출하고 파일을 만들어서 분리한다.
(ex. ProductRow, ProductCategoryRow, ProductInCategory, ...)
- 처음부터 파일을 나눠서 작업하려하지 않고 한 파일에서 분리해 나가는 방식으로 작업하는 것이 좋다.

## Props

> [Passing Props to a Component](https://react.dev/learn/passing-props-to-a-component)<br />
> [Components와 Props](https://ko.reactjs.org/docs/components-and-props.html)

- React 컴포넌트는 props를 사용하여 서로 통신하는데, 개념적으로 Javascript 함수와 유사하다.
>`props` 라고 하는 임의의 입력을 받고, 화면에 어떻게 표시되는지 기술하는 React 엘리먼트를 반환하기 때문
- 컴포넌트의 자체 Props를 수정해서는 안된다.

### Props 전달 방법
1. 부모 컴포넌트에서 자식 컴포넌트로 전달
2. 이름을 지정해서 전달
3. 매개변수 바로 뒤에 기본값을 넣어서 전달
```typescript
function Test({ name, study = 'math' }) {
  // ...
}
```
4. 반복되는 내용을 스프레드 구문으로 전달
5. 태그를 중첩하여 자식에 요소에 전달
