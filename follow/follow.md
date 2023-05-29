---
description: 팔로우/언팔로우 관련 엔드포인트
---

# /follow

{% swagger method="post" path="" baseUrl="https://blegram.vercel.app/api/follow" summary="특정 유저에게 팔로우 요청" expanded="true" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="cookie" required="true" name="bat" type="JWT" %}
엑세스 토큰을 갖는 쿠키 ( 10분 )
{% endswagger-parameter %}

{% swagger-parameter in="cookie" required="true" name="brt" type="JWT" %}
리프레쉬 토큰을 갖는 쿠키 ( 7일 )
{% endswagger-parameter %}

{% swagger-parameter in="query" name="userIdx" type="string" required="true" %}
팔로우할 유저의 식별자 ( idx )
{% endswagger-parameter %}

{% swagger-response status="201: Created" description="팔로우 성공" %}
{% code lineNumbers="true" %}
```json
{
    "message": "특정 유저의 팔로워들을 가져왔습니다.",
    "followers": [
        {
            "idx": 1,
            "avatar": "development/photos/cat.jpg",
            "name": "유저 - 1",
            "nickname": "apple",
            // 해당 유저의 팔로워들
            "followers": [
                {
                    "followerIdx": 1,
                    "followingIdx": 3
                }
            ]
        }
        // ...
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

{% swagger-response status="404: Not Found" description="존재하지 않는 유저에게 팔로우 요청" %}
```json
{
    "message": "존재하지 않는 유저입니다."
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

{% swagger method="delete" path="" baseUrl="https://blegram.vercel.app/api/follow" summary="특정 유저에게 언팔로우 요청" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="cookie" required="true" name="bat" type="JWT" %}
엑세스 토큰을 갖는 쿠키 ( 10분 )
{% endswagger-parameter %}

{% swagger-parameter in="cookie" required="true" name="brt" type="JWT" %}
리프레쉬 토큰을 갖는 쿠키 ( 7일 )
{% endswagger-parameter %}

{% swagger-parameter in="query" name="userIdx" type="string" required="true" %}
언팔로우할 유저의 식별자 ( idx )
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="언팔로우 성공" %}
{% code lineNumbers="true" %}
```json
{
    "message": "특정 유저의 팔로워들을 가져왔습니다.",
    "followers": [
        {
            "idx": 1,
            "avatar": "development/photos/cat.jpg",
            "name": "유저 - 1",
            "nickname": "apple",
            // 해당 유저의 팔로워들
            "followers": [
                {
                    "followerIdx": 1,
                    "followingIdx": 3
                }
            ]
        }
        // ...
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

{% swagger-response status="404: Not Found" description="존재하지 않는 유저에게 언팔로우 요청" %}
```json
{
    "message": "존재하지 않는 유저입니다."
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
