# Frontend Coding Convention

> 아무튼 수정함
>
> 코딩 컨벤션이란?
>
> 개발자들끼리 읽고, 관리하기 쉬운 코드를 작성하기 위한 일종의 코딩 스타일 규약이다.
>
> 모든 개발자들은 각자 자신만의 스타일을 가지고 있지만 어느 정도의 강제성을 부여한 코딩 컨벤션을 통해
>
> 서비스의 품질을 위해 신경써야된다.

## 🕹️ 폴더 및 파일 구조

> `Next.js App Router`를 기반으로 사용

### 0️⃣ 사전 지식

1. [Private Folder](https://nextjs.org/docs/app/getting-started/project-structure#private-folders)
2. [Route Group](https://nextjs.org/docs/app/building-your-application/routing/route-groups#convention)

### 1️⃣ 공용 파일에 대한 구조

> `_apis`, `_components`, `_hooks`, `_types` 등 폴더명은 모두 `_`로 시작하고, 복수형으로 사용한다.`component`, `type`, `hook`, `api` 등 각 페이지에서 사용하는 파일은 `Private Folder`를 이용해서 만든다.\
> ~~만약 두 개 이상의 페이지에서 사용되는 파일이라면 두개의 페이지의 공통된 부모로 끌어올려서 사용한다.~~\
> `(2025.01.06)`두 개 이상의 페이지에서 사용되는 파일이라면 먼저 선언한 곳에서 `import` 하는 것을 원칙으로 한다.\
>

```txt
├── _apis
│   └── index.ts
├── _components
│   ├── HappyfolioCard.tsx
│   ├── HappyfolioDetailMainInfoTitle.tsx
│   ├── HappyfolioList.tsx
│   ├── HappyfolioLoadingCard.tsx
│   └── HappyfolioLoadingCardList.tsx
├── _types
│   └── index.ts
├── (list)
│   ├── _components
│   ├── _hooks
│   └── page.tsx
├── [id]
│   ├── _components
│   ├── _hooks
│   └── page.tsx
└── layout.tsx
```

### 2️⃣ 그룹 폴더 사용 예시

아래 폴더 구조에서 `(list)`를 사용하지 않으면 더 상위에 있는 폴더와 리스트 페이지에서만 사용하는 폴더가 겹치기 때문에 이런 상황에서는 그룹으로 묶어서 사용한다.

```txt
├── _apis
├── _components # 겹침
├── _types
├── (list)
│   ├── _components # 겹침
│   ├── _hooks
│   └── page.tsx
├── [id]
│   ├── _components
│   ├── _hooks
│   └── page.tsx
```

## 📖 네이밍 규칙

### 0️⃣ 변수

1. 변수명은 `camelCase`를 사용한다.
2. 복수형일 경우에는 복수의 의미를 사용한다.
3. 상태에 대한 변수를 선언할때 `is`, `has` 등을 활용하자.

```ts
// camelCase
const companyName = "openknowl";
// 단수 & 복수
const tag = "미니인턴";
const tags = ["채용형 미니인턴", "교육형 미니인턴"];
// 상태 변수
const isMyCompany = false;
const hasNumber = false;
```

### 1️⃣ 컴포넌트

1. 컴포넌트명은 `PascalCase`를 사용한다.\

2. 컴포넌트 `props`의 타입은 `interface`를 사용하고 `컴포넌트명` + `Props`를 사용한다.\


```tsx
interface CompanyProps {
  name: string;
}
const Company: React.FC<CompanyProps> = ({ name }) => {
  return (
    <section>
      <span>{name}</span>
    </section>
  );
};
export default Company;
```

### 2️⃣ 타입

1. 타입은 `PascalCase`를 사용한다.
2. 접미사로 `Type`을 사용한다.

* 사용 접미사 리스트
  1. `*Type`: 일반적인 타입인 경우
  2. `ArgsType`: 함수의 `arguments` 타입인 경우
  3. `ParamsType`: `params`의 타입인 경우 ( `/company/25` )
  4. `QueriesType`: `query`의 타입인 경우 ( `?q=apple` )
  5. `BodyType`: `body`의 타입인 경우
  6. `RequestType`: `API` 요청 타입
  7. `ResponseType`: `API` 응답 타입

### 3️⃣ className

1. 클래스 네임을 사용하는 경우 `kebab-case`를 사용한다.
2. 컴포넌트명을 접두사로 사용하는 것을 원칙으로 한다.

```tsx
import styled from 'styled-components';
const CompanyBlock = styled.section`
  .company-name {
    font-size: 20px;
    font-weight: bold;
  }
`;
interface CompanyProps {
  name: string;
}
const Company: React.FC<CompanyProps> = ({ name }) => {
  return (
    <ChampionBlock>
      <span className="company-name">{name}</span>
    </ChampionBlock>
  );
};
export default Company;
```

### 4️⃣ styled-components

1. 최상위 엘리먼트에 `styled-components`를 사용하고 접미사로 `Block`을 붙인다.
2. 최상위를 제외한 엘리먼트는 `className`으로 선택해서 스타일을 부여한다.\
   ( `className`은 컴포넌트명을 기반으로 작성한다. )
3. `className`은 해당 컴포넌트 이름을 `kebab-case`의 접두사로 사용한다.
4. 조건부 스타일이 필요한 경우에는 새로운 `component`를 만들어서 사용한다.
5. `className`에 조건문을 넣는것을 지양한다.

```tsx
import styled from 'styled-components';
const CompanyBlock = styled.section`
  // ...
`;
const CompanyInfo = styled.div<{hasMoney: boolean}>`
   // ...
`
const Company: React.FC<CompanyProps> = () => {
  return (
    <CompanyBlock>
      <span className="company-name">오픈놀</span>
      <CompanyInfo hasMoney />
    </CompanyBlock>
  );
};
export default Company;
```

## 📓 코드

### 0️⃣ if문

1. `if ~ else`나 중첩 `if`를 사용하기 보다는 가능하다면 `early return`을 사용하자.

```ts
type RoundCheckboxColorType = 'blue' | 'navy' | 'black';
// BAD
const getFontColor = (checked: boolean, color: RoundCheckboxColorType) => {
  if (checked) {
    if (color === 'blue') {
      return palette.blue_500;
    }
    if (color === 'black') {
      return palette.black;
    }
  }
  return palette.black;
};
// GOOD
const getFontColor = (checked: boolean, color: RoundCheckboxColorType) => {
  if (!checked) return palette.black;
  if (color === 'blue') return palette.blue_500;
  if (color === 'black') return palette.black;
  
  return palette.black;
};
```

한줄짜리 간단한 조건문이라면 블럭(`{}`)으로 감싸지 않고 바로 리턴해도 되지만, 두 줄 이상이면 블럭으로 감싸서 리턴하자.

```ts
// BAD
if (videoRef.current && videoRef.current.clientHeight > 0) return setSpeedControllerMaxHeight(videoRef.current.clientHeight - 60);
// GOOD
if (videoRef.current && videoRef.current.clientHeight > 0) {
  return setSpeedControllerMaxHeight(videoRef.current.clientHeight - 60);
}
// GOOD
if (isFirst) return;
if (isFirst) {
  return;
}
```

### 1️⃣ 배열과 객체 선언

배열과 객체를 선언하는 경우엔 생성자 함수가 아닌 리터럴로 선언한다.\


```ts
// BAD
const emptyArr = new Array(); // []
const arr = new Array(1, 2, 3, 4); // [1, 2, 3, 4]
const emptyObj = new Object(); // {}
const obj = new Object();
obj.first = 1;
console.log(obj); // {first: 1};
// GOOD
const emptyArr = [];
const arr = [1, 2, 3, 4];
const emptyObj = {};
const obj = { first: 1, };
```

### 2️⃣ 함수

1. 화살표함수를 최우선으로 사용한다.

```ts
// BAD
console.log(typeof foo); // "function"
function foo() {
  // ...
}
// GOOD
console.log(typeof foo); // Uncaught ReferenceError: foo is not defined
const foo = () => {
  // ...
};
```

### 3️⃣ 이벤트 핸들러

이벤트 핸들러의 접두사는 `on`으로 사용하고, 구체적인 행위에 대한 이름을 붙여준다.\


* ex) 버튼을 클릭하면 프로젝트가 수정되는 핸들러인 경우 `onClick` + `UpdateProject` ( 구체적인 행위 ) + `Button`\
  단, 핸들러 함수내에서 모든 로직을 처리하지 않고 하나의 행위는 하나의 함수로 구분해서 작성한다.\

* ex) `updateProject()`, `openToast()`, `loadingSpinner()`, `closeSpinner()`

```tsx
const Openknowl: React.FC = () => {
  const updateProject = async () => {
    // ...
  };
  const openToast = () => {
    // ...
  };
  const onClickUpdateProjectButton = async () => {
    try {
      loadingSpinner();
      await updateProject();
    } catch (error) {
      sendErrorToSentry(error);
      openToast();
    } 
  };
  return (
      <button onClick={onClickUpdateProjectButton}>update project</button>
  );
};
export default Openknowl;
```

단, 한줄짜리 간단한 핸들러라면 인라인으로 작성한다.\


```tsx
import { useState } from 'react';
import styled from 'styled-components';
const StyledOpenknowlBlock = styled.section``;
const Openknowl: React.FC = () => {
  const [toggle, setToggle] = useState(false);
  return (
    <StyledOpenknowlBlock>
      <button onClick={() => setToggle(prev => !prev)}>click me : {toggle}</button>
    </StyledOpenknowlBlock>
  );
};
export default Openknowl;
```

### 4️⃣ Api 함수

1. 접미사로 `Api`를 사용한다.
2. `get` 메소드의 경우 `ApiKey`를 정의해서 사용한다. (`swr`, `axios`, `fetch` 에서 사용되는 `end-point`를 공용으로 관리하기 위함)
3. `RequestType` 과 `ResponseType`을 정의해서 사용한다.
4. `fetch`함수의 경우 사전에 정의된 `fetchWrapper`를 사용한다.

```ts
export const getEventsApiKey = (queries: EventQueries) => makeUrlQueries('/api/v3/events', queries);
export const getEventsApi = (queries: EventQueries) =>
  axios.get<EventResponseType>(getEventsApiKey(queries));
export const fetchEventsApi = async (queries: EventQueries) =>
  await fetchWrapper<EventResponseType>(getEventsApiKey(queries));
```

### 4️⃣ 에러핸들링 (try - catch)

1. 에러핸들링은 마지막 컴포넌트에서 처리하는 것을 원칙으로 하며, 이전 단계에서는 `throw error`를 사용해 에러를 반환시킨다.
2. 사전에 정의된 에러핸들링 함수(`sendErrorToSentry`) 를 사용해 에러를 처리한다.
3. `catch`문에 `error`인자는 `"error"` 로 통일한다.

```ts
// useParticipants.tsx (hook)
const updateParticipants = async () => {
  try {
    const response = await updateEventParticipantsAPI(id, participations);
    return response.data;
  } catch (error) {
    throw error;
  }
};
```

```ts
// Participant.tsx (view)
const Participant: React.FC = () => {
  const onClickButton = () => {
    try {
      updateParticipants();
    } catch (error) {
      sendErrorToSentry(error);
    }
  };
  return <button onClick={onClickButton}>클릭</button>;
};
```

## 🪄 Prettier & Eslint

### 0️⃣ Eslint

```js
// .eslintrc.cjs
module.exports = {
  extends: ['turbo', 'next/core-web-vitals', 'plugin:prettier/recommended'],
  plugins: ['unused-imports'], //* 사용하지 않는 import 체크,
  settings: {
    react: {
      version: 'detect',
    },
  },
  rules: {
    'react/no-unescaped-entities': 'off',
    '@next/next/no-img-element': 'off' /* <img>태그 사용 가능*/,
    'react-hooks/rules-of-hooks': 'error',
    'react-hooks/exhaustive-deps': 'off' /* react hook dependencies 자율성을 줌*/,
    '@next/next/no-html-link-for-pages': 'off' /* <a>태그 사용가능*/,
    'unused-imports/no-unused-imports': 'error',
    'react/display-name': 'off',
    'no-empty-function': 'off',
  },
  overrides: [
    {
      files: ['**/*.ts', '**/*.tsx'],
      plugins: ['@typescript-eslint'],
      extends: ['plugin:@typescript-eslint/recommended'],
      parser: '@typescript-eslint/parser',
      rules: {
        /*
        const _a = 'unused, with underscore, no warning'
        const b = 'unused, no underscore, warning'
        */
        '@typescript-eslint/no-explicit-any': 'off',
        'no-unused-vars': 'off',
        '@typescript-eslint/no-empty-function': ['off'],
        '@typescript-eslint/no-non-null-assertion': 'off',
        '@typescript-eslint/no-unused-vars': [
          'error',
          {
            argsIgnorePattern: '^_',
            varsIgnorePattern: '^_',
            caughtErrorsIgnorePattern: '^_',
            ignoreRestSiblings: true,
          },
        ],
        '@typescript-eslint/no-empty-interface': 'off',
        /** RequestType<Params = {}, Queries = {}, Body = {}>에서 error 발생 */
        '@typescript-eslint/ban-types': 'off',
      },
    },
  ],
};
```

### 1️⃣ Prettier

```json
// .prettierrc
{
  "singleQuote": true,
  "semi": true,
  "useTabs": false,
  "tabWidth": 2,
  "trailingComma": "all",
  "printWidth": 100,
  "arrowParens": "avoid"
}
```

> 아직 미완성이고 추가로 정리할 예정입니다 :)
