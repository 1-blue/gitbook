---
description: 로그인한 유저 엔드포인트
---

# /me

{% swagger method="get" path="/me" baseUrl="https://blegram.vercel.app/api" summary="로그인한 유저 정보 요청" expanded="true" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="cookie" required="true" name="bat" type="JWT" %}
엑세스 토큰을 갖는 쿠키 ( 10분 )
{% endswagger-parameter %}

{% swagger-parameter in="cookie" required="true" name="brt" type="JWT" %}
리프레쉬 토큰을 갖는 쿠키 ( 7일 )
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="유저 정보 응답 성공" %}
{% code lineNumbers="true" %}
```json
{
    "message": "\"apple\"님의 정보를 가져왔습니다.",
    "user": {
        "idx": 1,
        "id": "a",
        "name": "유저 - 1",
        "nickname": "apple",
        "email": "apple@naver.com",
        "phone": "01011111111",
        "birthday": "20010101",
        "introduction": "소개1\n🐳🐍🐊🦖🦈🐢\n😕🫤🙃🫠☹️🙁",
        "avatar": "development/photos/cat.jpg",
        "createdAt": "2023-05-26T04:09:33.489Z",
        "updatedAt": "2023-05-26T04:09:33.716Z"
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

{% swagger method="patch" path="/me" baseUrl="https://blegram.vercel.app/api" summary="로그인한 유저 정보 수정 요청" expanded="true" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="cookie" required="true" name="bat" type="JWT" %}
엑세스 토큰을 갖는 쿠키 ( 10분 )
{% endswagger-parameter %}

{% swagger-parameter in="cookie" required="true" name="brt" type="JWT" %}
리프레쉬 토큰을 갖는 쿠키 ( 7일 )
{% endswagger-parameter %}

{% swagger-parameter in="body" name="name" required="true" type="string" %}
수정할 이름
{% endswagger-parameter %}

{% swagger-parameter in="body" name="nickname" required="true" type="string" %}
수정할 별칭
{% endswagger-parameter %}

{% swagger-parameter in="body" name="email" required="true" type="string" %}
수정할 이메일
{% endswagger-parameter %}

{% swagger-parameter in="body" name="phone" required="true" type="string" %}
수정할 휴대폰 번호
{% endswagger-parameter %}

{% swagger-parameter in="body" name="introduction" required="true" type="string" %}
수정할 자기 소개
{% endswagger-parameter %}

{% swagger-parameter in="body" name="avatar" required="false" type="string" %}
수정할 아바타 이미지 URL
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="유저 정보 수정 성공" %}
{% code lineNumbers="true" %}
```json
{
    "message": "\"apple\"님의 데이터를 수정했습니다."
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

{% swagger-response status="409: Conflict" description="이메일 || 별칭 || 휴대폰 번호 중복" %}

{% endswagger-response %}

{% swagger-response status="500: Internal Server Error" description="서버측 문제 ( 코드상의 문제 )" %}
```json
{
    "message": "서버측 문제입니다.\n잠시후에 다시 시도해주세요!"
}
```
{% endswagger-response %}
{% endswagger %}
