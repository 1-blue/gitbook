---
description: 게시글에 좋아요 누른 사람들 엔드포인트
---

# /likers/post

{% swagger method="post" path="/likers/post" baseUrl="https://blegram.vercel.app/api" summary="특정 게시글에 좋아요 누른 사람들 요청" expanded="true" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="cookie" required="true" name="bat" type="JWT" %}
엑세스 토큰을 갖는 쿠키 ( 10분 )
{% endswagger-parameter %}

{% swagger-parameter in="cookie" required="true" name="brt" type="JWT" %}
리프레쉬 토큰을 갖는 쿠키 ( 7일 )
{% endswagger-parameter %}

{% swagger-parameter in="body" name="postIdx" type="number" required="true" %}
게시글의 식별자 ( idx )
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="좋아요 누른 사람들 요청 성공" %}
{% code lineNumbers="true" %}
```json
{
    "message": "게시글에 좋아요를 누른 유저들을 가져왔습니다.",
    "likers": [
        {
            "postLikerIdx": 1,
            "postLikedIdx": 35,
            "createdAt": "2023-05-29T05:50:07.149Z",
            "updatedAt": "2023-05-29T05:50:07.151Z",
            // 해당 게시글에 좋아요 누른 사람들 상세 정보
            "postLiker": {
                "idx": 1,
                "nickname": "apple",
                "avatar": "development/photos/cat.jpg",
                "name": "유저 - 1",
                "followers": []
            }
        }
        // ... 좋아요 누른 사람들
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

{% swagger-response status="404: Not Found" description="존재하지 않는 게시글에 요청" %}
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
