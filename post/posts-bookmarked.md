---
description: 특정 유저가 북마크한 게시글들 엔드포인트
---

# /posts/bookmarked

{% swagger method="get" path="/api/posts/bookmarked" baseUrl="https://blegram.vercel.app" summary="특정 유저가 북마크한 게시글들 요청" expanded="true" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="cookie" required="false" name="bat" type="JWT" %}
엑세스 토큰을 갖는 쿠키 ( 10분 )
{% endswagger-parameter %}

{% swagger-parameter in="cookie" required="false" name="brt" type="JWT" %}
리프레쉬 토큰을 갖는 쿠키 ( 7일 )
{% endswagger-parameter %}

{% swagger-parameter in="query" name="nickname" type="string" required="true" %}
유저 닉네임
{% endswagger-parameter %}

{% swagger-parameter in="query" type="number" name="take" required="true" %}
탐색할 개수
{% endswagger-parameter %}

{% swagger-parameter in="query" name="lastIdx" type="number" required="true" %}
탐색 시작 위치

( 이전에 검색한 유저의 식별자 ( idx ) )
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="특정 유저가 북마크한 게시글들 요청 성공" %}
{% code lineNumbers="true" %}
```json
{
    "message": "apple님의 게시글 2개를 가져왔습니다.",
    "posts": [
        {
            "idx": 35,
            "content": "#apple\n#blue",
            "photos": "development/photos/chick_1685338872447.jpg|development/photos/parrot_1685338872456.jpg|development/photos/rabbit_1685338872458.jpg",
            "createdAt": "2023-05-29T05:41:23.396Z",
            "updatedAt": "2023-05-29T05:41:23.398Z",
            "userIdx": 1,
            // 게시글 작성자 정보
            "user": {
                "idx": 1,
                "avatar": "development/photos/cat.jpg",
                "nickname": "apple",
                "followers": []
            },
            // 게시글에 좋아요 누른 사람들
            "postLikers": [
                {
                    "postLikerIdx": 1,
                    "postLikedIdx": 35,
                    "createdAt": "2023-05-29T05:50:07.149Z",
                    "updatedAt": "2023-05-29T05:50:07.151Z"
                }
            ],
            // 게시글에 북마크 누른 사람들
            "bookMarkers": [
                {
                    "bookmarkerIdx": 1,
                    "bookmarkedIdx": 35,
                    "createdAt": "2023-05-29T05:50:11.082Z",
                    "updatedAt": "2023-05-29T05:50:11.084Z"
                }
            ],
            // 게시글의 좋아요/댓글 총 개수
            "_count": {
                "comments": 0,
                "postLikers": 1
            }
        },
        {
            "idx": 2,
            "content": "테스트 게시글 1\n🐳🐍🐊🦖🦈🐢\n😕🫤🙃🫠☹️🙁",
            "photos": "development/photos/cat.jpg|development/photos/dog.jpg|development/photos/lion.jpg",
            "createdAt": "2023-05-26T04:09:33.800Z",
            "updatedAt": "2023-05-26T04:09:33.803Z",
            "userIdx": 1,
            "user": {
                "idx": 1,
                "avatar": "development/photos/cat.jpg",
                "nickname": "apple",
                "followers": []
            },
            "postLikers": [
                {
                    "postLikerIdx": 1,
                    "postLikedIdx": 2,
                    "createdAt": "2023-05-26T09:28:58.091Z",
                    "updatedAt": "2023-05-26T09:28:58.092Z"
                }
            ],
            "bookMarkers": [
                {
                    "bookmarkerIdx": 1,
                    "bookmarkedIdx": 2,
                    "createdAt": "2023-05-26T09:29:03.933Z",
                    "updatedAt": "2023-05-26T09:29:03.935Z"
                }
            ],
            "_count": {
                "comments": 0,
                "postLikers": 1
            }
        }
        // ... 게시글들
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
