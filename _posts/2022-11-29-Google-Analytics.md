---
layout: post
title:  "About Google Analytics"
subtitle: "Google analytics란, 추가과정"
date:   2022-11-29 14:44:13 +0900
background: '/img/posts/05.jpg'
categories: jekyll update
comments: true
---

## Google analytics란 무엇인가

- 구글에서 무료로 제공하고 있는 웹분석 서비스
- 구글의 Urchin 인수 후 제공된 서비스이다.
- 구글의 빅쿼리와의 연동이 존재하는데, 이를 통해 무료 사용자들이 더 넓은 클라우드 제공 기능과 연동할 수 있게 하려는 구글의 노력을 엿볼 수 있다.


## Google analytics 추가 과정

1. [Google Anayltics](https://analytics.google.com/analytics/web/provision/?hl=ko&pli=1#/provision)에 접속해서 계정 설정
    - 계정 설정, 속성 설정, 비즈니스 정보를 차례대로 입력해준다.
2. 데이터 스트림 웹 항목에 본인 블로그 주소를 입력하여 스트림 추가 (측정항목은 마음대로 선택)
3. 블로그에 사용할 측정 ID 확인
    - 측정 ID형식은 다음과 같다.
        - G-XXXXXXXX 형식 ⇒ Google 애널리틱스 4 를 사용함
        - UA-XXXXXXXX-X 형식 ⇒ 유니버설 애널리틱스 를 사용함
4. _config.yml 파일에 아래 코드 추가
```markdown
analytics:
  provider: "google-gtag" 
            # false (default), "google", "google-universal", "google-gtag", "custom"
  google:
    tracking_id: "본인 ID"
    anonymize_ip: # true, false (default)
```
5. includes/head.html 파일에 아래 코드 추가
```html
  <!-- Google tag (gtag.js) -->
  <script async src="https://www.googletagmanager.com/gtag/js?id=본인 ID"></script>
  <script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());

  gtag('config', '본인 ID');
  </script>
```
6. Result
![result1](file:///home/jimin/result1.png)
![result2](file:///home/jimin/result2.png)