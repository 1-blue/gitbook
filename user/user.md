---
description: 특정 유저 관련 엔드포인트
---

# /user

{% swagger method="post" path="" baseUrl="https://blegram.vercel.app/api/user" summary="특정 유저 정보 요청" expanded="true" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="body" name="nickname" type="String" required="true" %}
찾을 유저의 닉네임
{% endswagger-parameter %}

{% swagger-parameter in="cookie" required="false" name="bat" type="String" %}
엑세스 토큰을 갖는 쿠키 ( 10분 )
{% endswagger-parameter %}

{% swagger-parameter in="cookie" required="false" name="brt" type="String" %}
리프레쉬 토큰을 갖는 쿠키 ( 7일 )
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="특정 유저 정보 찾기 성공" %}
<pre class="language-json" data-line-numbers><code class="lang-json">// 로그인 성공 시 쿠키 전송 ( access, refresh )
{
  // 10분 ( blegram-access-token )
<strong>  Set-Cookie: bat=keyboardcat; Domain=blegram.vercel.app; Path=/; SameSite=Strict; Max-Age=3600000; HttpOnly; Secure;
</strong><strong>  // 7일 ( blegram-refresh-token )
</strong>  Set-Cookie: brt=keyboardcat; Domain=blegram.vercel.app; Path=/; SameSite=Strict; Max-Age=604800000; HttpOnly; Secure;
}
</code></pre>
{% endswagger-response %}

{% swagger-response status="404: Not Found" description="존재하지 않는 유저" %}

{% endswagger-response %}
{% endswagger %}
