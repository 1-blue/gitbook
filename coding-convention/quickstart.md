---
icon: bullseye-arrow
description: 프론드엔드와 백엔드 모두 TypeScript를 사용하는 경우를 예시로 한다.
cover: >-
  https://images.unsplash.com/photo-1628258334105-2a0b3d6efee1?crop=entropy&cs=srgb&fm=jpg&ixid=M3wxOTcwMjR8MHwxfHNlYXJjaHwxfHxjb2Rpbmd8ZW58MHx8fHwxNzM2OTA4ODk3fDA&ixlib=rb-4.0.3&q=85
coverY: 0
---

# ⚖️ 공용

{% hint style="success" %}
공용으로 사용할 수 있는 것들은 반드시 하나의 근본만을 참고

1. 타입의 경우 `Prisma`에서 만든 모델 타입에 `TypeScript Utility`를 이용해서 만듦
2. [`routes`](https://github.com/1-blue/story-dict/blob/master/apps/fe/src/constants/routes.ts)에서 모든 경로에 대해 정의해두고 다른곳에서 재사용 ( [`navbar`](https://github.com/1-blue/story-dict/blob/master/apps/fe/src/constants/navRoutes.ts), [`sitemap`](https://github.com/1-blue/story-dict/blob/master/apps/fe/src/app/sitemap.ts) 등 )
{% endhint %}



## 공통 규칙

### 0️⃣ 절대경로는 #을 사용

절대경로는 <mark style="color:blue;">`#`</mark>을 사용한다.\
<mark style="color:blue;">`@`</mark>를 사용하면 특정 라이브러리와 겹쳐서 헷갈리는 경우가 발생하기 때문이다.

### 1️⃣ 절대경로 사용

같은 <mark style="color:blue;">**`depth`**</mark>도 원한다면 절대경로 사용가능

```tsx
import {
  ConflictException,
  Injectable,
  NotFoundException,
  UnauthorizedException,
} from "@nestjs/common";
import { Prisma } from "@sd/db";

import { compareValue, encryptionValue } from "#be/utils";
import { PrismaService } from "#be/apis/v0/prisma/prisma.service";
import { FindByUserIdDto } from "#be/apis/v1/users/dto/find-by-user-id.dto";
import { CreateUserDto } from "#be/apis/v1/users/dto/create-user.dto";
import { UpdateUserDto } from "#be/apis/v1/users/dto/update-user.dto";
```

### 2️⃣ import 순서

1. 외부 라이브러리
2. 내부 패키지
3. 절대경로
4. 상대경로

```tsx
import type { Metadata, NextPage } from "next";
import { cache } from "react";
import { dehydrate, HydrationBoundary } from "@tanstack/react-query";

import { apis } from "#fe/apis";
import { getQueryClient } from "#fe/libs/getQueryClient";
import { getSharedMetadata } from "#fe/libs/sharedMetadata";

import PostDetail from "#fe/app/post/[title]/_components/PostDetail";
```

### 3️⃣ 모델 타입와 유틸리티를 활용하기

<pre class="language-tsx"><code class="lang-tsx">// ❌ Bad
Interface IPost {
  id: string;
}

import type { Post } from "@sd/db";
// ⭕️ Good
Interface IPost {
  id: Post["id"]
}
// ⭕️ Good
<strong>Interface IPost extends Pick&#x3C;Post, "id"> {}
</strong></code></pre>

### 4️⃣ 타입 접두사

직접 만드는 타입은 접두사로 <mark style="color:blue;">`I`</mark>나 <mark style="color:blue;">`T`</mark>를 붙인다.\
컴포넌트명과 타입명이 겹치는 상황을 미연에 방지하기 위함

```tsx
import type { Comment, User } from "@sd/db";

// ❌ Bad
Interface CommentWithUser extends Comment {
  user: User
}
// ⭕️ Good
Interface ICommentWithUser extends Comment {
  user: User
}

// ❌ Bad ( Reaction이라는 컴포넌트명과 겹치는 경우가 발생할 수 있음 )
type Reaction = "GOOD" | "BAD" | "FIRE" | "SEE";
// ⭕️ Good
type TReaction = "GOOD" | "BAD" | "FIRE" | "SEE";
```

