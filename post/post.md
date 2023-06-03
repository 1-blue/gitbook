---
description: 특정 유저 관련 엔드포인트
---

# 📘 /post

{% swagger method="get" path="/api/post" baseUrl="https://blegram.vercel.app" summary="게시글 가져오기 요청" expanded="true" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="cookie" required="false" name="bat" type="JWT" %}
엑세스 토큰을 갖는 쿠키 ( 10분 )
{% endswagger-parameter %}

{% swagger-parameter in="cookie" required="false" name="brt" type="JWT" %}
리프레쉬 토큰을 갖는 쿠키 ( 7일 )
{% endswagger-parameter %}

{% swagger-parameter in="query" name="postIdx" type="number" required="true" %}
가져올 게시글의 식별자
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="게시글 가져오기 성공" %}
{% code lineNumbers="true" %}
```json
{
    "message": "특정 게시글을 가져왔습니다.",
    "post": {
        "idx": 35,
        "content": "#apple\n#blue",
        "photos": "development/photos/chick_1685338872447.jpg|development/photos/parrot_1685338872456.jpg|development/photos/rabbit_1685338872458.jpg",
        "createdAt": "2023-05-29T05:41:23.396Z",
        "updatedAt": "2023-05-29T05:41:23.398Z",
        "userIdx": 1,
        "user": {
            "idx": 1,
            "avatar": "development/photos/dog_1685342473905.jpg",
            "nickname": "apple",
            "followers": []
        },
        "postLikers": [
            {
                "postLikerIdx": 1,
                "postLikedIdx": 35,
                "createdAt": "2023-06-01T06:10:02.785Z",
                "updatedAt": "2023-06-01T06:10:02.787Z"
            }
        ],
        "bookMarkers": [
            {
                "bookmarkedIdx": 35,
                "bookmarkerIdx": 1,
                "createdAt": "2023-06-02T10:31:57.540Z",
                "updatedAt": "2023-06-02T10:31:57.540Z"
            }
        ],
        "_count": {
            "comments": 3,
            "postLikers": 1
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

{% swagger-response status="404: Not Found" description="존재하지 않는 게시글" %}
```json
{
    "message": "존재하지 않는 게시글입니다."
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

{% swagger method="post" path="/api/post" baseUrl="https://blegram.vercel.app" summary="게시글 생성 요청" expanded="true" %}
{% swagger-description %}
content에서 해시태그 추출해서 해시태그 생성 및 등록
{% endswagger-description %}

{% swagger-parameter in="body" name="content" type="string" required="true" %}
생성할 게시글 내용
{% endswagger-parameter %}

{% swagger-parameter in="body" name="photoPaths" type="string[]" required="true" %}
게시글 이미지들
{% endswagger-parameter %}

{% swagger-parameter in="cookie" required="true" name="bat" type="JWT" %}
엑세스 토큰을 갖는 쿠키 ( 10분 )
{% endswagger-parameter %}

{% swagger-parameter in="cookie" required="true" name="brt" type="JWT" %}
리프레쉬 토큰을 갖는 쿠키 ( 7일 )
{% endswagger-parameter %}

{% swagger-response status="201: Created" description="게시글 생성 성공" %}
{% code lineNumbers="true" %}
```json
{
    "message": "게시글을 업로드했습니다.\n메인 페이지로 이동됩니다.",
    "createdPost": {
        "idx": 34,
        "content": "#고양이\n테스트",
        "photos": "development/photos/cat_1685331095345.jpg|development/photos/cat2_1685331095354.jpg|development/photos/cat3_1685331095355.jpg",
        "createdAt": "2023-05-29T03:31:44.568Z",
        "updatedAt": "2023-05-29T03:31:44.571Z",
        "userIdx": 1,
        // 게시글 작성자 정보
        "user": {
            "idx": 1,
            "avatar": "development/photos/cat.jpg",
            "nickname": "apple",
            "followers": []
        },
        // 게시글에 좋아요를 누른 사람들
        "postLikers": [],
        // 게시글에 북마크를 누른 사람들
        "bookMarkers": [],
        // 게시글의 댓글/좋아요 총개수
        "_count": {
            "comments": 0,
            "postLikers": 0
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

{% swagger method="delete" path="/api/post" baseUrl="https://blegram.vercel.app" summary="게시글 삭제 요청" expanded="true" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="cookie" required="true" name="bat" type="JWT" %}
엑세스 토큰을 갖는 쿠키 ( 10분 )
{% endswagger-parameter %}

{% swagger-parameter in="cookie" required="true" name="brt" type="JWT" %}
리프레쉬 토큰을 갖는 쿠키 ( 7일 )
{% endswagger-parameter %}

{% swagger-parameter in="query" name="idx" type="string" required="true" %}
삭제할 게시글 식별자
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="게시글 제거 성공" %}
{% code lineNumbers="true" %}
```json
{
    "message": "게시글을 삭제했습니다."
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
