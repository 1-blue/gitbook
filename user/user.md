---
description: 특정 유저 관련 엔드포인트
---

# 🙋 /user

{% swagger method="post" path="/api/user" baseUrl="https://blegram.vercel.app" summary="특정 유저 정보 요청" expanded="true" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="cookie" required="false" name="bat" type="JWT" %}
엑세스 토큰을 갖는 쿠키 ( 10분 )
{% endswagger-parameter %}

{% swagger-parameter in="cookie" required="false" name="brt" type="JWT" %}
리프레쉬 토큰을 갖는 쿠키 ( 7일 )
{% endswagger-parameter %}

{% swagger-parameter in="query" name="nickname" type="string" required="true" %}
찾을 유저의 닉네임
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="특정 유저 정보 찾기 성공" %}
{% code lineNumbers="true" %}
```json
{
    "message": "\"apple\"님의 정보를 가져왔습니다.",
    "user": {
        "idx": 1,
        "name": "이름",
        "nickname": "apple",
        "introduction": "소개1\n🐳🐍🐊🦖🦈🐢\n😕🫤🙃🫠☹️🙁",
        "avatar": "development/photos/dog_1685342473905.jpg",
        "_count": {
            "posts": 10,
            "followers": 1,
            "followings": 1
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

{% swagger-response status="404: Not Found" description="존재하지 않는 유저" %}

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
