# 1. 개발 환경 세팅 ⚙️

## Node.js 기반으로 한 JavaScript 개발 환경 세팅

<br />

- [Node.js](https://nodejs.org/ko/) 설치
  - 무조건 최신 버전을 사용하지 않아도 된다. (LTS 사용)
  - 최신버전 확인 `node -v`
  - fnm(Fast Node Manager)을 이용해서 Node.js 설치하면 관리하기 쉽고 nvm보다 빠르다.

```Bash
# Homebrew로 fnm 설치
brew install fnm

# fnm을 이용해 LTS 버전의 nodejs 설치
fnm install --lts
fnm use lts-lastet
fnm default $(fnm current)
```

<br /><br />

## TypeScript + React + Jest + Parcel 개발 환경 세팅

<br />

### 1. 작업폴더 준비

```Bash
mkdir test
cd test

# IDE 실행 (vscode)
code .
```

### 2. npm 패키지 준비

```Bash
npm init -y
```

### 3. `.gitignore` 파일작성해서 불필요한 파일까지 commit 하는 일을 방지할 수 있다
  
- [github/gitignore](https://github.com/github/gitignore)에서 기본으로 제공하는 것 사
- [gitignore.io](https://www.toptal.com/developers/gitignore) 에서 생성해주는 템플릿 사용
- 직접 필요한 것만 추가해서 사용

~~~Bash
touch .gitignore

# vi .gitignore
# node_modules/
# dist
~~~

### 4. typescript 설정, typescript 컴파일러

```Bash
npm i -D typescript
npx tsc --init
```

- 프로그램에서 실제로 사용할 것은 dependencies
- 도구로서 설치되는 것은 devDependencies (-D) 배포할 때 도구는 배포에서 제외시켜서 파일의 크기를 줄일 수 있다.

### 4-1 `tsconfig.js` 파일의 jsx 속성 변경

"jsx" 속성을 "jsx": "react-jsx" 로 변경하고 주석 해제

### 5. ESLint 설정

```Bash
npm i -D eslint
npx eslint --init
```

- `.gitignore`와 같이 `.eslintignore` 도 똑같이 작성
- `.eslintrc.js`도 필요에 맞게 수정 `jest: true` 미리 설정

### 6. 리액트 설치

```Bash
npm i react react-dom

# 타입스크립트 관련 도구 설치
npm i -D @types/react @types/react-dom
```

### 7. 테스팅도구 설치 (jest)

```Bash
npm i -D jest @types/jest @swc/core @swc/jest \
    jest-environment-jsdom \
    @testing-library/react @testing-library/jest-dom
```

`jest.config.js` 파일을 작성하고 테스트에서 SWC를 사용

```Bash
module.exports = {
  testEnvironment: 'jsdom',
  setupFilesAfterEnv: [
    '@testing-library/jest-dom/extend-expect',
  ],
  transform: {
    '^.+\\.(t|j)sx?$': ['@swc/jest', {
      jsc: {
        parser: {
          syntax: 'typescript',
          jsx: true,
          decorators: true,
        },
        transform: {
          react: {
            runtime: 'automatic',
          },
        },
      },
    }],
  },
  testPathIgnorePatterns: [
    '<rootDir>/node_modules/',
    '<rootDir>/dist/',
  ],
};
```

### 8. parcel 설치

- 웹 애플리케이션 번들러
- 웹서버를 띄울 수 있다.

```Bash
npm i -D parcel
```

### 9. `package.json` 파일의 scripts를 용도에 맞게 수정하여 사용

```json
"source": "index.html",
"scripts": {
    "start": "parcel --port 8080",
    "build": "parcel build",
    "check": "tsc --noEmit",
    "lint": "eslint --fix --ext .js,.jsx,.ts,.tsx .",
    "test": "jest",
    "coverage": "jest --coverage --coverage-reporters html",
    "watch:test": "jest --watchAll"
  },
```

- source : 웹 서버를 실행했을 때 열릴 파일, node는 `"main": "index.js"` 로 초기 세팅되어 있다.
