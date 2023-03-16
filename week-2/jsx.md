# JSX

## "XML-like syntax extension to ECMAScript"

- React를 다룰 때 가장 기본이 되는 기술
- Javascript를 확장한 문법
- HTML이 아님.

### React에 JSX를 꼭 사용해야 하나요?

- No.

### React에 ES6(+)를 꼭 사용해야 하나요?

- No.

JSX는 XML처럼 작성된 부분을 React.createElement을 쓰는 JavaScript 코드로 변환한다.
중간중간 중괄호를 써서 JavaScript 코드를 그대로 쓸 수 있고,  JavaScript 코드와 1:1로 매칭된다.

#### Babel

- 변환기 중 가장 유명
- <https://babeljs.io/repl>
  - "Presets"에서 "react" 체크 또는 "Plugin"에서 "@babel/plugin-transform-react-jsx"를 설치해야 JSX를 test해볼 수 있다.
- JSX 파일에 /*@jsx aaa*/ 주석을 추가하면 React.createElement 대신 aaa 를 쓰게 된다.
- 최근에는 Babel이 아닌 다른 도구도 많이 사용

##### Babel 사용 예시

##### ex 1

```javascript
// JSX 
  <p>Hello, world</p>

// 변환 된 javascript 코드
  React.createElement("p", null, "Hello, world!");
  // React.createElement(함수(컴포넌트명)orHTML태그, 속성, "내용");
```

##### ex 2

```javascript
// JSX 
  <Greeting name="world" />

// 변환 된 javascript 코드
  React.createElement(Greeting, { name: "world", age={13}, addr={{ 'key': 'value' }} });
```

##### ex 3

```javascript
// JSX 
  <Button type="submit" onClick="() => console.log('Clicked'))">Send</Button>

// 변환 된 javascript 코드
  React.createElement(Button, { type: "submit" }, "Send");
```

Button 처럼 컴포넌트명을 그대로 넣으면 따옴표 없이 함수로 들어가고,
button 으로 html 기본 태그를 넣으면 "button"로 들어간다.

##### ex 4

```javascript
// JSX 
  <div className="test">
    <p>Hello, world!</p>
    <Button type="submit">Send</Button>
  </div>

// 변환 된 javascript 코드
  React.createElement(
    "div",
    { className: "test" },
    React.createElement("p", null, "Hello, world!"),
    React.createElement(Button, { type: "submit" }, "Send")
  );
```

Fragment

- <></>
- <React.Fragment></React.Fragent>
- <div></div> 로 대체 가능

##### ex 5

```javascript
// JSX
  <> 
    <p>
      {"Count: "}{count * 2}{"!"}  
    </p>
    <Button type="submit" onClick={() => setCount(count + 1)}>Increase</Button>
  </>

// 변환 된 javascript 코드  
  React.createElement(
    "div",
    null,
    React.createElement("p", null, "Count: ", count, "!"),
    React.createElement("button", { type: "button", onClick: () => setCount(count + 1) }, "Increase")
  );

// React.createElement (
//   "객체",
//   속성,
//   자녀(객체, 속성, 내용)
// )
```

- JSX는 React에 있는 createElement를 사용하도록 코드를 바꿔주는 것

### React Element

- JSX 대신 React.createElement를 써서 React Element 트리를 갱신하는데 쓸 수 있다.
- JSX Runtimedms _jsx 함수를, Preact는 h() 함수를 직접 지원한다.

- JSX 없이 사용하는 React

  - <https://ko.reactjs.org/docs/react-without-jsx.html>
  - React에서 JSX는 필수가 아니다.
  - 빌드 환경에서 컴파일 설정을 하는게 아닌 javascript로 직접 구현하려할 때 편리하다.
  - JSX로 할 수 있는 모든 것을 순수 JavaScript로도 할 수 있다.

- createElement

  - <https://beta.reactjs.org/reference/react/createElement>
  - React element를 만들어낸다.

### VDOM(Virtual DOM)

🔗 [공식문서](https://ko.reactjs.org/docs/faq-internals.html)

- UI의 이상적 혹은 `가상`의 표현을 메모리에 저장하고 ReactDOM과 같은 라이브러리에 의해 “실제” `DOM과 동기화하는 프로그래밍 개념`으로, 기존 DOM Tree와 비교 후에 업데이트가 필요한 부분만 DOM Tree에 업데이트 해준다. (💡[재조정](https://ko.reactjs.org/docs/reconciliation.html))
- `React는 선언적 API를 제공`하기 때문에 갱신이 될 때마다 매번 무엇이 바뀌었는지를 걱정할 필요 없다.

### VDOM을 쓰는 이유

`유지보수`가 가능한 애플리케이션을 만드는걸 도와주고, 충분히 빠른 속도 때문에 사용한다.

#### DOM과 Virtual DOM의 차이

- DOM에는 Fragment가 없다.
- vuejs에서는 비슷하게 template을 사용하기도 한다.

### React StrictMode

- StrictMode는 APP 내의 문제를 알아내기 위한 도구로, 요소들에 대한 부가적인 검사와 경고를 활성화해준다.

작업 중 어디에서든지 Strict mode를 적용할 수 있다.

```tsx
root.render((
  <React.StrictMode>
    <App />
  </React.StrictMode>
))
```

### React Developer Tools

🔗 [참고](https://github.com/facebook/react/tree/main/packages/react-devtools-extensions)

- 브라우저의 확장 소스 코드
- StrictMode 를 사용하지 않으면 경고
- React 구성요소를 트리구조로 보여준다.

### 성능최적화

🔗 [공식문서](https://ko.reactjs.org/docs/optimizing-performance.html)
