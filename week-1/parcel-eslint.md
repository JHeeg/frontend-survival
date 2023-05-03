# 5. Parcel & ESLint

## [Parcel](https://parceljs.org/)

* Zero Configuration : 특별한 설정 없이 바로 사용 가능한 빌드 도구.

### parcel 설정

* `package.json` 파일에 source 속성 추가

```json
"source": "./index.html",
```

* [parcel-reporter-static-files-copy](https://github.com/elwin013/parcel-reporter-static-files-copy) 패키지 설치 후 `.parcelrc` 파일 작성.
* static 폴더의 파일을 정적 파일로 Serving 가능(assets)

```json
{
  "extends": ["@parcel/config-default"],
  "reporters":  ["...", "parcel-reporter-static-files-copy"]
}
```

* 빌드 및 정적 서버 실행
* [servor](https://github.com/lukejacksonn/servor)

```bash
npx parcel build
npx servor ./dist
```

\


## [ESLint](https://eslint.org/)

* [Lint](https://ko.wikipedia.org/wiki/%EB%A6%B0%ED%8A%B8\_\(%EC%86%8C%ED%94%84%ED%8A%B8%EC%9B%A8%EC%96%B4\)): 소스코드를 분석하고 프로그램 오류,버그 등을 표시하기 위한 도구
* [정적 분석 도구](https://ko.wikipedia.org/wiki/%EC%A0%95%EC%A0%81\_%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%A8\_%EB%B6%84%EC%84%9D): 실제 실행 없이 소스코드를 분석하는 것
* [Coding conventions](https://en.wikipedia.org/wiki/Coding\_conventions): 해당 언어로 작성된 프로그램에 대한 코딩 스타일, 방식 등에 대한 지침

### 장점

* 스타일 통일
* 잠재적 문제 발견
* 베스트 프랙티스 추천 -> 최신 트렌드를 학습하는데 활용

### [VS Code ESLint extension](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)

* `.vscode/settings.json` 파일을 추가하여 JS/TS 파일을 저장할 때마다 ESLint를 실행하고 문제점을 고치도록 설정하면 편리하다.

```json
{
    "editor.codeActionsOnSave": {
        "source.fixAll.eslint": true
    }
}
```
