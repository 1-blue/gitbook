---
description: 로그인한 유저 프로필 이미지 수정 엔드포인트
---

# 🙍 /me/photo

{% swagger method="patch" path="/api/me/photo" baseUrl="https://blegram.vercel.app" summary="로그인한 유저 프로필 이미지 수정 요청" expanded="true" %}
{% swagger-description %}
기존 프로필 이미지는 제거하지 않고 다른 폴더에 저장함
{% endswagger-description %}

{% swagger-parameter in="cookie" required="true" name="bat" type="JWT" %}
엑세스 토큰을 갖는 쿠키 ( 10분 )
{% endswagger-parameter %}

{% swagger-parameter in="cookie" required="true" name="brt" type="JWT" %}
리프레쉬 토큰을 갖는 쿠키 ( 7일 )
{% endswagger-parameter %}

{% swagger-parameter in="body" name="avatarPath" type="string" required="true" %}
수정될 아바타 이미지 URL
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="유저 정보 수정 성공" %}
{% code lineNumbers="true" %}
```json
{
    "message": "프로필 이미지를 업로드했습니다."
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
