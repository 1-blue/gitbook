---
description: 댓글들 관련 엔드 포인트
---

# /comments

{% swagger method="get" path="" baseUrl="https://blegram.vercel.app/api/comments" summary="특정 게시글의 댓글들 요청" expanded="true" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="cookie" required="false" name="bat" type="JWT" %}
엑세스 토큰을 갖는 쿠키 ( 10분 )
{% endswagger-parameter %}

{% swagger-parameter in="cookie" required="false" name="brt" type="JWT" %}
리프레쉬 토큰을 갖는 쿠키 ( 7일 )
{% endswagger-parameter %}

{% swagger-parameter in="query" name="postIdx" type="string" required="true" %}
게시글의 식별자 ( idx )
{% endswagger-parameter %}

{% swagger-parameter in="query" name="take" type="number" required="true" %}
탐색할 개수
{% endswagger-parameter %}

{% swagger-parameter in="query" name="lastIdx" type="number" required="true" %}
탐색 시작 위치

( 이전에 검색한 유저의 식별자 ( idx ) )
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="댓글들 가져오기 성공" %}
{% code lineNumbers="true" %}
```json
{
    "message": "댓글들을 2개 가져왔습니다.",
    "comments": [
        {
            "idx": 3,
            "content": "댓글",
            "createdAt": "2023-05-29T04:38:50.729Z",
            "updatedAt": "2023-05-29T04:38:50.732Z",
            "userIdx": 1,
            "postIdx": 34,
            // 댓글 작성자
            "user": {
                "idx": 1,
                "avatar": "development/photos/cat.jpg",
                "nickname": "apple"
            },
            // 댓글에 좋아요 누른 사람들
            "commentLikers": [
                {
                    "commentLikerIdx": 1,
                    "commentLikedIdx": 3,
                    "createdAt": "2023-05-29T04:41:59.409Z",
                    "updatedAt": "2023-05-29T04:41:59.411Z"
                }
            ],
            // 댓글 좋아요 총 개수
            "_count": {
                "commentLikers": 1
            }
        },
        {
            "idx": 4,
            "content": "댓글추가",
            "createdAt": "2023-05-29T04:38:58.044Z",
            "updatedAt": "2023-05-29T04:38:58.047Z",
            "userIdx": 1,
            "postIdx": 34,
            "user": {
                "idx": 1,
                "avatar": "development/photos/cat.jpg",
                "nickname": "apple"
            },
            "commentLikers": [],
            "_count": {
                "commentLikers": 0
            }
        }
        // ... 댓글들
    ]
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

{% swagger-response status="404: Not Found" description="존재하지 않는 게시글의 댓글들 요청" %}
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
