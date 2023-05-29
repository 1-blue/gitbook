---
description: 댓글 관련 엔드 포인트
---

# /comment

{% swagger method="post" path="" baseUrl="https://blegram.vercel.app/api/comment" summary="특정 게시글에 댓글 생성 요청" expanded="true" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="cookie" required="true" name="bat" type="JWT" %}
엑세스 토큰을 갖는 쿠키 ( 10분 )
{% endswagger-parameter %}

{% swagger-parameter in="cookie" required="true" name="brt" type="JWT" %}
리프레쉬 토큰을 갖는 쿠키 ( 7일 )
{% endswagger-parameter %}

{% swagger-parameter in="query" name="postIdx" type="string" required="true" %}
게시글의 식별자 ( idx )
{% endswagger-parameter %}

{% swagger-parameter in="query" name="content" type="string" required="true" %}
댓글 내용
{% endswagger-parameter %}

{% swagger-response status="201: Created" description="댓글 생성 성공" %}
{% code lineNumbers="true" %}
```json
{
    "message": "댓글을 업로드했습니다.",
    "createdComment": {
        "idx": 5,
        "content": "댓글생성",
        "createdAt": "2023-05-29T04:47:50.625Z",
        "updatedAt": "2023-05-29T04:47:50.626Z",
        "userIdx": 1,
        "postIdx": 34,
        // 댓글 작성자
        "user": {
            "idx": 1,
            "avatar": "development/photos/cat.jpg",
            "nickname": "apple"
        },
        // 댓글에 좋아요 누른 사람들
        "commentLikers": [],
        // 댓글에 좋아요 총 개수
        "_count": {
            "commentLikers": 0
        }
    }
}
```
{% endcode %}
{% endswagger-response %}

{% swagger-response status="302: Found" description="인증 토큰 만료 ( 재발급 )" %}

{% endswagger-response %}

{% swagger-response status="401: Unauthorized" description="유효하지 않은 토큰 ( 잘못된, 만료된 )" %}
```json
{
    "message": "로그인후에 접근해주세요!"
}
```
{% endswagger-response %}

{% swagger-response status="404: Not Found" description="존재하지 않는 게시글의 댓글 생성 요청" %}
```json
{
    "message": "존재하지 않는 게시글입니다."
}
```
{% endswagger-response %}

{% swagger-response status="405: Method Not Allowed" description="접근할 수 없는 메서드" %}
```json
{
    "message": "가능한 요청이 아닙니다.\n확인후에 다시 시도해주세요!"
}
```
{% endswagger-response %}

{% swagger-response status="500: Internal Server Error" description="서버측 문제 ( 코드상의 문제 )" %}
```json
{
    "message": "서버측 문제입니다.\n잠시후에 다시 시도해주세요!"
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger method="patch" path="" baseUrl="https://blegram.vercel.app/api/comment" summary="특정 게시글의 댓글 수정 요청" expanded="true" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="cookie" required="true" name="bat" type="JWT" %}
엑세스 토큰을 갖는 쿠키 ( 10분 )
{% endswagger-parameter %}

{% swagger-parameter in="cookie" required="true" name="brt" type="JWT" %}
리프레쉬 토큰을 갖는 쿠키 ( 7일 )
{% endswagger-parameter %}

{% swagger-parameter in="query" name="commentIdx" type="string" required="true" %}
댓글의식별자 ( idx )
{% endswagger-parameter %}

{% swagger-parameter in="query" name="content" type="string" required="true" %}
수정할댓글 내용
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="댓글 수정 성공" %}
{% code lineNumbers="true" %}
```json
{
    "message": "댓글을 수정했습니다."
}
```
{% endcode %}
{% endswagger-response %}

{% swagger-response status="302: Found" description="인증 토큰 만료 ( 재발급 )" %}

{% endswagger-response %}

{% swagger-response status="401: Unauthorized" description="유효하지 않은 토큰 ( 잘못된, 만료된 )" %}
```json
{
    "message": "로그인후에 접근해주세요!"
}
```
{% endswagger-response %}

{% swagger-response status="404: Not Found" description="존재하지 않는 댓글 수정 요청" %}
```json
{
    "message": "존재하지 않는 게시글입니다."
}
```
{% endswagger-response %}

{% swagger-response status="405: Method Not Allowed" description="접근할 수 없는 메서드" %}
```json
{
    "message": "가능한 요청이 아닙니다.\n확인후에 다시 시도해주세요!"
}
```
{% endswagger-response %}

{% swagger-response status="500: Internal Server Error" description="서버측 문제 ( 코드상의 문제 )" %}
```json
{
    "message": "서버측 문제입니다.\n잠시후에 다시 시도해주세요!"
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger method="delete" path="" baseUrl="https://blegram.vercel.app/api/comment" summary="특정 게시글의 댓글 제거 요청" expanded="true" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="cookie" required="true" name="bat" type="JWT" %}
엑세스 토큰을 갖는 쿠키 ( 10분 )
{% endswagger-parameter %}

{% swagger-parameter in="cookie" required="true" name="brt" type="JWT" %}
리프레쉬 토큰을 갖는 쿠키 ( 7일 )
{% endswagger-parameter %}

{% swagger-parameter in="query" name="commentIdx" type="string" required="true" %}
댓글의식별자 ( idx )
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="댓글 제거 성공" %}
{% code lineNumbers="true" %}
```json
{
    "message": "댓글을 수정했습니다."
}
```
{% endcode %}
{% endswagger-response %}

{% swagger-response status="302: Found" description="인증 토큰 만료 ( 재발급 )" %}

{% endswagger-response %}

{% swagger-response status="401: Unauthorized" description="유효하지 않은 토큰 ( 잘못된, 만료된 )" %}
```json
{
    "message": "로그인후에 접근해주세요!"
}
```
{% endswagger-response %}

{% swagger-response status="404: Not Found" description="존재하지 않는 댓글 제거 요청" %}
```json
{
    "message": "존재하지 않는 댓글입니다."
}
```
{% endswagger-response %}

{% swagger-response status="405: Method Not Allowed" description="접근할 수 없는 메서드" %}
```json
{
    "message": "가능한 요청이 아닙니다.\n확인후에 다시 시도해주세요!"
}
```
{% endswagger-response %}

{% swagger-response status="500: Internal Server Error" description="서버측 문제 ( 코드상의 문제 )" %}
```json
{
    "message": "서버측 문제입니다.\n잠시후에 다시 시도해주세요!"
}
```
{% endswagger-response %}
{% endswagger %}
