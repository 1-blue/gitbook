---
description: 추천 검색어 요청
---

# /search/suggested

{% swagger method="get" path="/suggested" baseUrl="https://blegram.vercel.app/api/search" summary="추천 검색어 요청 ( 해시태그 || 유저 닉네임 )" expanded="true" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="cookie" required="false" name="bat" type="JWT" %}
엑세스 토큰을 갖는 쿠키 ( 10분 )
{% endswagger-parameter %}

{% swagger-parameter in="cookie" required="false" name="brt" type="JWT" %}
리프레쉬 토큰을 갖는 쿠키 ( 7일 )
{% endswagger-parameter %}

{% swagger-parameter in="query" name="query" type="string" required="true" %}
검색할 내용 ( 해시태그 || 닉네임 )
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="추천 검색어 찾기 성공" %}
{% code lineNumbers="true" %}
```json
{
    "message": "추천 해시태그 및 유저들을 가져왔습니다.",
    // 추천 해시태그들
    "hashtags": [
        {
            "content": "apple"
        }
    ],
    // 추천 유저들
    "users": [
        {
            "idx": 1,
            "name": "유저 - 1",
            "nickname": "apple",
            "avatar": "development/photos/cat.jpg"
        }
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
