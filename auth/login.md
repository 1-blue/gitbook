---
description: 로그인 관련 엔드포인트
---

# 🔓 /login

{% swagger method="post" path="/api/login" baseUrl="https://blegram.vercel.app" summary="로그인 요청" expanded="true" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="body" name="id" type="string" required="true" %}
로그인할 유저의 아이디
{% endswagger-parameter %}

{% swagger-parameter in="body" name="password" type="string" required="true" %}
로그인할 유저의 비밀번호
{% endswagger-parameter %}

{% swagger-parameter in="cookie" required="false" name="bat" type="JWT" %}
엑세스 토큰을 갖는 쿠키 ( 10분 )
{% endswagger-parameter %}

{% swagger-parameter in="cookie" required="false" name="brt" type="JWT" %}
리프레쉬 토큰을 갖는 쿠키 ( 7일 )
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="로그인 성공" %}
<pre class="language-json" data-line-numbers><code class="lang-json">// 로그인 성공 시 쿠키 전송 ( access, refresh )
{
  // 10분 ( blegram-access-token )
<strong>  Set-Cookie: bat=keyboardcat; Domain=blegram.vercel.app; Path=/; SameSite=Strict; Max-Age=3600000; HttpOnly; Secure;
</strong><strong>  // 7일 ( blegram-refresh-token )
</strong>  Set-Cookie: brt=keyboardcat; Domain=blegram.vercel.app; Path=/; SameSite=Strict; Max-Age=604800000; HttpOnly; Secure;
}
</code></pre>
{% endswagger-response %}

{% swagger-response status="401: Unauthorized" description="id, password에 일치하는 유저가 없는 경우" %}
```json
{
    "message": "존재하는 유저가 없습니다." // 비밀번호가 일치하지 않습니다.
}
```
{% endswagger-response %}

{% swagger-response status="403: Forbidden" description="이미 로그인한 상태에 로그인 요청" %}
```json
{
    "message": "로그인을 하지 않은 경우에만 로그인이 가능합니다."
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
