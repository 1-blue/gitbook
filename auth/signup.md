---
description: 회원가입 관련 엔드포인트
---

# 📝 /signup

{% swagger method="post" path="/api/signup" baseUrl="https://blegram.vercel.app" summary="회원가입 요청" expanded="true" fullWidth="false" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="body" name="id" type="string" required="true" %}
유저의 아이디 ( 16자 이하 )
{% endswagger-parameter %}

{% swagger-parameter in="body" name="password" type="string" required="true" %}
유저의 비밀번호
{% endswagger-parameter %}

{% swagger-parameter in="body" name="name" type="string" required="true" %}
유저의 이름 ( 20자 이하 )
{% endswagger-parameter %}

{% swagger-parameter in="cookie" required="false" name="bat" type="JWT" %}
엑세스 토큰을 갖는 쿠키 ( 10분 )
{% endswagger-parameter %}

{% swagger-parameter in="cookie" required="false" name="brt" type="JWT" %}
리프레쉬 토큰을 갖는 쿠키 ( 7일 )
{% endswagger-parameter %}

{% swagger-parameter in="body" name="nickname" type="string" required="true" %}
유저의 별칭 ( 30자 이하 )
{% endswagger-parameter %}

{% swagger-parameter in="body" name="email" required="true" type="string" %}
유저의 이메일 ( 30자 이하 )
{% endswagger-parameter %}

{% swagger-parameter in="body" name="phone" required="true" type="string" %}
유저의 휴대폰 번호 ( 11자 )
{% endswagger-parameter %}

{% swagger-parameter in="body" name="birthday" required="true" type="string" %}
유저의 생일 ( 8자 )
{% endswagger-parameter %}

{% swagger-parameter in="body" name="introduction" required="true" type="string" %}
유저의 자기소개 ( 100자 이하 )
{% endswagger-parameter %}

{% swagger-parameter in="body" name="avatar" type="string" %}
아바타 이미지
{% endswagger-parameter %}

{% swagger-response status="201: Created" description="회원가입 성공" %}
{% code lineNumbers="true" %}
```json
{
    "message": "회원가입을 성공했습니다.\n로그인페이지로 이동됩니다."
}
```
{% endcode %}
{% endswagger-response %}

{% swagger-response status="302: Found" description="인증 토큰 만료 ( 잘못된, 만료된 )" %}

{% endswagger-response %}

{% swagger-response status="403: Forbidden" description="이미 로그인한 상태에 회원가입 요청" %}
```json
{
    "message": "로그인을 하지 않은 경우에만 회원가입이 가능합니다."
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

{% swagger-response status="409: Conflict" description="id || nickname || email || phone 중복" %}
```json
{
    "message": "아이디가 이미 존재합니다." // 아이디, 별칭, 이메일, 휴대폰 번호
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
