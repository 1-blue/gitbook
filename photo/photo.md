---
description: 단일 이미지 관련 엔드포인트
---

# 🌇 /photo

{% swagger method="post" path="/api/photo" baseUrl="https://blegram.vercel.app" summary="단일 이미지 생성 요청" expanded="true" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="body" name="name" type="string" required="true" %}
생성할 이미지 이름
{% endswagger-parameter %}

{% swagger-parameter in="cookie" required="true" name="bat" type="JWT" %}
엑세스 토큰을 갖는 쿠키 ( 10분 )
{% endswagger-parameter %}

{% swagger-parameter in="cookie" required="true" name="brt" type="JWT" %}
리프레쉬 토큰을 갖는 쿠키 ( 7일 )
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="서명된 URL 얻기 성공" %}
{% code lineNumbers="true" %}
```json
{
    "message": "presignedURL을 가져왔습니다.",
    "presignedURL": "https://blegram.s3.ap-northeast-2.amazonaws.com/development/photos/cat_1685331095345.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIARBZ7RTMVBCIZ4PEW%2F20230529%2Fap-northeast-2%2Fs3%2Faws4_request&X-Amz-Date=20230529T033135Z&X-Amz-Expires=20&X-Amz-Signature=40b56cf4417b75a88e03c7b4708d1cf9f08064783a24d7d101c830a49eec249d&X-Amz-SignedHeaders=host"
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
