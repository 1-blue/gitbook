---
description: 커밋과 브랜치 컨벤션에 대해 작성한 문서
icon: github
cover: >-
  https://images.unsplash.com/photo-1630514969818-94aefc42ec47?crop=entropy&cs=srgb&fm=jpg&ixid=M3wxOTcwMjR8MHwxfHNlYXJjaHwzfHxnaXRodWJ8ZW58MHx8fHwxNzQyMDkyMDg2fDA&ixlib=rb-4.0.3&q=85
coverY: 274
layout:
  cover:
    visible: true
    size: full
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# 깃 컨벤션

## 📕 커밋 컨벤션

<pre><code>접두사:[domain] 내용
<strong>ex) feat:[/home] 썸네일 미리보기 모달 구현
</strong><strong>
</strong><strong># 전체에 영향이 간다면 [all], 도메인이 여러개면 ,로 구분
</strong></code></pre>

### 0️⃣ 접두사

* feat: 기능 구현
* hotfix: 급한 버그 수정
* bugfix: 버그 수정
* refactor: 이미 작성한 코드 수정
* chore: 간단한 코드 수정 ( .eslintrc 등 )
* docs: 문서 수정 ( README.md 등 )

## 📗 브랜치 컨벤션

1. 실서버 브랜치: master
2. 테스트 서버 브랜치: development
3. 기능 브랜치: feat/고유번호-기능\_내용
4. 코드 수정 브랜치: refactor/고유번호-수정\_내용
5. 버그 수정 브랜치: hotfix/고유번호-버그\_내용

### 0️⃣ 접두사

* feat: 기능 구현
* hotfix: 급한 버그 수정
* bugfix: 버그 수정
* refactor: 이미 작성한 코드 수정
* chore: 간단한 코드 수정
* docs: 문서 수정

### 1️⃣ 고유 번호

발급된 티켓의 번호 ( ex) TSK-1 )
