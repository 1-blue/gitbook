---
description: 회원가입 관련 엔드포인트
---

# /signup

{% swagger method="post" path="" baseUrl="https://blegram.vercel.app/api/signup" summary="회원가입 요청" expanded="true" fullWidth="false" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="body" name="id" type="String" required="true" %}
유저의 아이디 ( 16자 이하 )
{% endswagger-parameter %}

{% swagger-parameter in="body" name="password" type="String" required="true" %}
유저의 비밀번호
{% endswagger-parameter %}

{% swagger-parameter in="body" name="name" type="String" required="true" %}
유저의 이름 ( 20자 이하 )
{% endswagger-parameter %}

{% swagger-parameter in="cookie" required="false" name="bat" type="String" %}
엑세스 토큰을 갖는 쿠키 ( 10분 )
{% endswagger-parameter %}

{% swagger-parameter in="cookie" required="false" name="brt" type="String" %}
리프레쉬 토큰을 갖는 쿠키 ( 7일 )
{% endswagger-parameter %}

{% swagger-parameter in="body" name="nickname" type="String" required="true" %}
유저의 별칭 ( 30자 이하 )
{% endswagger-parameter %}

{% swagger-parameter in="body" name="email" required="true" type="String" %}
유저의 이메일 ( 30자 이하 )
{% endswagger-parameter %}

{% swagger-parameter in="body" name="phone" required="true" type="String" %}
유저의 휴대폰 번호 ( 11자 )
{% endswagger-parameter %}

{% swagger-parameter in="body" name="birthday" required="true" type="String" %}
유저의 생일 ( 8자 )
{% endswagger-parameter %}

{% swagger-parameter in="body" name="introduction" required="true" type="String" %}
유저의 자기소개 ( 100자 이하 )
{% endswagger-parameter %}

{% swagger-parameter in="body" name="avatar" type="String" %}
아바타 이미지
{% endswagger-parameter %}

{% swagger-response status="201: Created" description="회원가입 성공" %}
<pre class="language-json" data-line-numbers><code class="lang-json">// 로그인 성공 시 쿠키 전송 ( access, refresh )
{
  // 10분 ( blegram-access-token )
<strong>  Set-Cookie: bat=keyboardcat; Domain=blegram.vercel.app; Path=/; SameSite=Strict; Max-Age=3600000; HttpOnly; Secure;
</strong><strong>  // 7일 ( blegram-refresh-token )
</strong>  Set-Cookie: brt=keyboardcat; Domain=blegram.vercel.app; Path=/; SameSite=Strict; Max-Age=604800000; HttpOnly; Secure;
}
</code></pre>
{% endswagger-response %}

{% swagger-response status="403: Forbidden" description="이미 로그인한 상태에 회원가입 요청" %}

{% endswagger-response %}

{% swagger-response status="409: Conflict" description="id || nickname || email || phone 중복" %}

{% endswagger-response %}
{% endswagger %}
