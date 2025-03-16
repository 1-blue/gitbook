---
description: 타입을 정의하는 규칙에 대해 작성한 문서
cover: >-
  https://images.unsplash.com/photo-1699885960867-56d5f5262d38?crop=entropy&cs=srgb&fm=jpg&ixid=M3wxOTcwMjR8MHwxfHNlYXJjaHwxfHx0eXBlc2NyaXB0fGVufDB8fHx8MTc0MjA5MzY2NXww&ixlib=rb-4.0.3&q=85
coverY: 0
layout:
  cover:
    visible: true
    size: full
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# 🩻 타입 컨벤션

```typescript
/**
 * + 책 유형
 *   1. `thriller`: 스릴러
 *   2. `mystery`: 추리소설
 *   3. `romance`: 로맨스 소설
 *   4. `horror`: 공포 소설
 *   5. `fantasy`: 판타지 소설
 */
export type TBookType = 'thriller' | 'mystery' | 'romance' | 'horror' | 'fantasy';

/** 책의 스키마 타입 */
export interface IBook {
  /** 식별자 */
  id: number;
  /** 제목 */
  title: string;
  /** 작가 */
  author: string;
  /** 책 유형 */
  type: TBookType;
}
```

## 🎈 접두사

컴포넌트와 이름이 충돌날 수 있기 때문에 <mark style="color:blue;">`I`</mark>나 <mark style="color:blue;">`T`</mark>를 접두사로 사용한다.

```typescript
export type TBookType = "";
export interface IBook {}
```

## 📖 TSDoc

> <mark style="color:blue;">`TSDoc`</mark>으로 작성해두면 사용하는 곳에서 마우스를 올리면 주석이 나타납니다.

<mark style="color:blue;">`TSDoc`</mark>을 반드시 작성한다.

지금 예시는 너무 간단하고 직관적이라 설명이 없어도 이해할 수 있지만, 실제로 사용하다보면 영단어 하나로 설명하기 힘든 값이거나 개발을 진행한 당자사를 제외하고 이해하기 힘든 값일 수 있기 때문에 모든 타입에는 <mark style="color:blue;">`TSDoc`</mark>을 사용한다.

굳이 타입에 <mark style="color:blue;">`TSDoc`</mark>을 작성하는 이유는 타입에 작성해두면 타입을 사용하는 변수에도 적용되기 때문에 한 번 제대로 작성해두면 이후에 사용할때와 유지보수 혹은 타인이 수정할때 보기좋은 문서가 된다.

특히 <mark style="color:blue;">`enum`</mark>형태는 반드시 작성해두는게 좋다.\
미래의 본인도 이 값들이 어떤 역할인지 모르는 경우가 많다.

```typescript
/**
 * + 책 유형
 *   1. `thriller`: 스릴러
 *   2. `mystery`: 추리소설
 *   3. `romance`: 로맨스 소설
 *   4. `horror`: 공포 소설
 *   5. `fantasy`: 판타지 소설
 */
export type TBookType = 'thriller' | 'mystery' | 'romance' | 'horror' | 'fantasy';
```

## 📦 API 타입

> 만약 원본 타입이 존재하는 경우 유틸리티 함수를 활용하고, 원본 타입이 없다면 길어져도 하나씩 직접 작성한다.\
> ( 원본 타입이란 DB의 모델, 스키마에 대한 타입 )

API 타입은 따로 타입만을 관리하기 위한 파일로 분리하지 않고 API 요청 함수 바로 위에 사용한다.

```typescript
// ============================== 게시글 수정 ==============================
/** 게시글 수정 요청 타입 */
export interface IPatchBookAPIRequest {
  params: { bookId: IBook["id"] };
  body: Partial<IBook>;
  queries: {
    page: number;
    limit: number;
  };
}
/** 게시글 수정 응답 타입 */
export interface IPatchBookAPIResponse extends IBook {}
/** 게시글 수정 함수 */
export const patchBookAPI = async ({
  body,
  params,
  queries,
}: IPatchBookAPIRequest): Promise<IPatchBookAPIResponse> => {
  return fetchInstance(`/apis/v1/books/${params.bookId}`, {
    method: "PATCH",
    body: JSON.stringify(body),
  })
    .then(fetchInstanceHandleResponse)
    .catch(fetchInstanceHandleError);
};
```

### 0️⃣ 요청 타입

예외 없이 <mark style="color:blue;">`body`</mark>, <mark style="color:blue;">`params`</mark>, <mark style="color:blue;">`queries`</mark>로 구분해서 값을 받는다.\
그리고 접미사로 반드시 <mark style="color:blue;">`APIRequest`</mark>를 사용한다.

```typescript
/** 게시글 수정 요청 타입 */
export interface IPatchBookAPIRequest {
  params: { bookId: IBook["id"] };
  body: Partial<IBook>;
  queries: {
    page: number;
    limit: number;
  };
}
```

### 1️⃣ 응답 타입

접미사로 반드시 <mark style="color:blue;">`APIResponse`</mark>를 사용한다.

```typescript
/** 게시글 수정 응답 타입 */
export interface IPatchBookAPIResponse extends IBook {}
```

## 🗂️ 타입 정의 위치

개인적으로 타입은 사용하는곳 바로 위에 작성하는게 좋은 것 같다.\
과거에는 <mark style="color:blue;">`/apis/book.ts`</mark>, <mark style="color:blue;">`/types/book.ts`</mark> 이런식으로 분리해서 관리했는데 규모가 조금이라도 커지면 각각의 위치를 찾는게 더 힘들어지는 경험을 했다.\
그래서 공용으로 사용하는 타입이 아니라면 코드가 길어지더라도 사용하는곳 바로 위에 사용하는게 좋다고 생각한다. &#x20;
