---
description: 프론트엔드의 코딩 컨벤션
cover: >-
  https://images.unsplash.com/photo-1667372393086-9d4001d51cf1?crop=entropy&cs=srgb&fm=jpg&ixid=M3wxOTcwMjR8MHwxfHNlYXJjaHwyfHxiYWNrZW5kfGVufDB8fHx8MTczNjkyODk5Nnww&ixlib=rb-4.0.3&q=85
coverY: 0
---

# 📤 프론트엔드

### API 작성 규칙

{% hint style="info" %}
자세한 코드 예시는 [GitHub](https://github.com/1-blue/story-dict/tree/master/apps/fe/src/apis)[ 참고](https://github.com/1-blue/story-dict/tree/master/apps/fe/src/apis)
{% endhint %}

#### 요청 타입

1. 외부에서 사용하지 않더라도 <mark style="color:blue;">`export`</mark>를 한다.
2. 당연한 내용이라도 <mark style="color:blue;">`TSDoc`</mark>으로 설명을 작성한다.
3. 타입명은 <mark style="color:blue;">`I or T`</mark> + <mark style="color:blue;">`HTTP Method`</mark> + <mark style="color:blue;">`행위`</mark> + <mark style="color:blue;">`APIRequest`</mark> 형태로 만든다.
4. 전달 방식에 따라서 <mark style="color:blue;">`body`</mark>, <mark style="color:blue;">`params`</mark>, <mark style="color:blue;">`queries`</mark>로 나눠서 받는다.

```typescript
/** 게시글 수정 요청 타입 */
export interface IPatchPostAPIRequest {
  params: { postId: Post["id"] };
  body: Partial<ICreatePostAPIRequest["body"]>;
}
```

#### 응답 타입

1. 외부에서 사용하지 않더라도 <mark style="color:blue;">`export`</mark>를 한다.
2. 당연한 내용이라도 <mark style="color:blue;">`TSDoc`</mark>으로 설명을 작성한다.
3. 타입명은 <mark style="color:blue;">`I or T`</mark> + <mark style="color:blue;">`HTTP Method`</mark> + <mark style="color:blue;">`행위`</mark> + <mark style="color:blue;">`APIResponse`</mark> 형태로 만든다

```typescript
/** 게시글 수정 응답 타입 */
export interface IPatchPostAPIResponse extends IAPIResponse<Post> {}
```

#### 함수명

1. 당연한 내용이라도 <mark style="color:blue;">`TSDoc`</mark>으로 설명을 작성한다.
2. 함수명은 <mark style="color:blue;">`HTTP Method`</mark> + <mark style="color:blue;">`행위`</mark> + <mark style="color:blue;">`API`</mark> 형태로 만든다

#### 그룹화

<mark style="color:blue;">`endpoint`</mark>, <mark style="color:blue;">`key`</mark>, <mark style="color:blue;">`fn`</mark>으로 분리된 객체로 만들어서 사용

```tsx
/** 게시글 수정 요청 타입 */
export interface IPatchPostAPIRequest {
  params: { postId: Post["id"] };
  body: Partial<ICreatePostAPIRequest["body"]>;
}
/** 게시글 수정 응답 타입 */
export interface IPatchPostAPIResponse extends IAPIResponse<Post> {}
/** 게시글 수정 함수 */
export const patchPostAPI = async ({
  body,
  params,
}: IPatchPostAPIRequest): Promise<IPatchPostAPIResponse> => {
  return fetchInstance(postApis.patch.endPoint({ params }), {
    method: "PATCH",
    body: JSON.stringify(body),
  })
    .then(fetchInstanceHandleResponse)
    .catch(fetchInstanceHandleError);
};

export const postApis = {
  patch: {
    endPoint: ({ params }: Pick<IPatchPostAPIRequest, "params">) =>
      SERVER_URL + `/apis/v1/posts/${params.postId}`,
    key: ({ params }: Pick<IPatchPostAPIRequest, "params">) => [
      "patch",
      "posts",
      params.postId,
    ],
    fn: patchPostAPI,
  },
};

// 최종적으로 api들 하나의 객체로 묶기
export const apis = {
  posts: {
    ...postApis,
  },
};

// 직접 사용
api.posts.patch.fn();

// tanstack-query 사용
const {} = useQuery({
  queryKey: api.posts.getAll.key(),
  queryFn: api.posts.getAll.fn(),
});
```

### API 관련 커스텀 훅 작성 규칙

<mark style="color:blue;">`GET`</mark> 요청을 제외한 <mark style="color:blue;">`API`</mark>관련 <mark style="color:blue;">`mutate`</mark>를 하나로 묶어서 관리\
성공과 실패의 경우는 훅에서 처리 ( 특수한 경우가 아니라면 컴포넌트 내부에서 처리하지 않음 )

```typescript
import { useRouter } from "next/navigation";
import { useMutation, useQueryClient } from "@tanstack/react-query";
import {
  apis,
  ICheckUniqueTitleAPIRequest,
  ICheckUniqueTitleAPIResponse,
  ICreatePostAPIRequest,
  ICreatePostAPIResponse,
  IDeletePostAPIRequest,
  IDeletePostAPIResponse,
  IPatchPostAPIRequest,
  IPatchPostAPIResponse,
} from "#fe/apis";
import { routes } from "#fe/constants";
import { revalidateTagForServer } from "#fe/actions/revalidateForServer";

const usePostMutations = () => {
  const router = useRouter();
  const queryClient = useQueryClient();

  const { mutateAsync: createPostMutateAsync } = useMutation<
    ICreatePostAPIResponse,
    Error,
    ICreatePostAPIRequest
  >({
    mutationFn: ({ body }) => apis.posts.create.fn({ body }),
    onSuccess: () => {
      queryClient.invalidateQueries({
        queryKey: apis.posts.getAll.key(),
      });

      revalidateTagForServer(apis.posts.getAll.key());

      router.replace(routes.post.url);
    },
  });
  const { mutateAsync: patchPostMutateAsync } = useMutation<
    IPatchPostAPIResponse,
    Error,
    IPatchPostAPIRequest
  >({
    mutationFn: ({ body, params }) => apis.posts.patch.fn({ body, params }),
    onSuccess: () => {
      queryClient.invalidateQueries({
        queryKey: apis.posts.getAll.key(),
      });

      revalidateTagForServer(apis.posts.getAll.key());

      router.replace(routes.post.url);
    },
  });
  const { mutateAsync: deletePostMutateAsync } = useMutation<
    IDeletePostAPIResponse,
    Error,
    IDeletePostAPIRequest
  >({
    mutationFn: ({ params }) => apis.posts.delete.fn({ params }),
    onSuccess: () => {
      queryClient.invalidateQueries({
        queryKey: apis.posts.getAll.key(),
      });

      router.replace(routes.post.url);
    },
  });
  const { mutateAsync: checkUniqueTitleMutateAsync } = useMutation<
    ICheckUniqueTitleAPIResponse,
    Error,
    ICheckUniqueTitleAPIRequest
  >({
    mutationFn: ({ body }) => apis.posts.checkUniqueTitle.fn({ body }),
  });

  return {
    createPostMutateAsync,
    patchPostMutateAsync,
    deletePostMutateAsync,
    checkUniqueTitleMutateAsync,
  };
};

export default usePostMutations;
```

