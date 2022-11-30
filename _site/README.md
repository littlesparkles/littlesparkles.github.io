# **개인 Git Blog 과제**

[![screenshot](/img/screenshot.png)](https://littlesparkles.github.io/)
**사진을 클릭하면 블로그 페이지로 넘어갑니다!**

## 체점 조건
- [x] 마감: 2022-11-30-23:59 (모든 채점은 원격저장소의 마감일자 전 commit 버전을 기준으로 진행)
- [x] 본인의 git주소와 만들었던 git blog 주소를 제출 (blog 결과 확인 가능한 git주소 제출. 채점시 확인이 불가한 경우, 미제출 처리 예정)

- 필수 과제 (80%)
  - [x] Remote Repository의 README.md 자신의 프로젝트를 Build한 과정을 기술 (50%)
  - [x] <username>.github.io를 접속했을 때 블로그가 정상적으로 동작 (10%)
    - CSS 깨짐, 404 Error 등이 발생 X
  - [x] 특강에 다뤄졌던 내용 Topic 중 배운 내용에 관해 Post 작성 (10%)
    - 주제 : Git & Github, Jekyll, Markdown 등
  - [x] 기본 테마 이외의 목적에 맞는 테마 적용 (10%)
    - Jekyll의 기본 테마 minima 이외의 테마를 적용
    - 템플릿의 dummy 정보가 아닌, 본인이 만든 사이트의 기능에 필요한 정보 O (navbar, profile text 등)
- 선택 과제 (20%)
  - [x] Post에 댓글 기능 추가 (10%)
    - 위 필수과제에 있는 Post에서 댓글 기능을 추가
  - [x] 수업시간에 다루어지지 않은 기능(Google Analytics, Jekyll-admin 등)을 추가하고 이를 추가하는 과정을 Post로 작성 (5%)
  - [x] 사이트에 favicon 추가 (5%)

## Build

### 1단계 Github page 시작하기

1. **Repository 생성**
- Github에서 <username>.github.io 이름의 Repo 생성

2. **Local-Remote Repository 연동**
- Remote Repository의 주소를 복사
- `git clone <repo_name> <path>`로 clone
- `git commit -m "<commit msg>"`로 커밋 남기기
- `git branch -M main`으로 현재 branch의 이름을 main으로 변경
- `git status`로 현재 상태 확인 후 `git add`로 변경파일 추가
- `git push origin main`으로 main에 로컬 변경사항 push
  - push를 할 때 비밀번호처럼 사용 할 개인 token 생성

### 2단계 테마 추가

1. **Jekyll 시작하기**
- [우분투에서의 Jekyll](https://jekyllrb-ko.github.io/docs/installation/ubuntu/)
  - Jekyll을 설치하기 전, 필요한 모든 의존요소를 가지고 있는지 확인하고 젬 설치 디렉토리를 설정
- Jekyll과 Bundler 설치
  - `gem install jekyll bundler`
- Jekyll이 잘 설치되어있는지 확인
  - `jekyll -v`
- 현재 디렉토리(.)에 Jekyll을 설치
  - `jekyll new . --force`
- Jekyll 시작
  - `(bundle exec) jekyll serve` 실행 후, localhost:4000 접속


2. **테마 적용**
- [다음](http://jekyllthemes.org/)과 [다음](https://jekyllthemes.io/free)에서 원하는 테마 선택
- 선택한 테마를 fork
  - username.github.io 이름의 Repository 생성


3. **내용 수정**
- **confing.yml** 파일에서 블로그 이름, 프로필 사진 등 수정

```
title: Jimin's Blog
email: happyjmpark@gmail.com
description: >- # this means to ignore newlines until "baseurl:"
  You cannot be happy everyday, but there are happy things everyday!
baseurl: "" # the subpath of your site, e.g. /blog
url: "" # the base hostname & protocol for your site, e.g. http://example.com
instagram_username: Gminii__
github_username:  littlesparkles
```

- **_posts** 폴더에서 블로그 포스팅
  - YYYY-MM-DD-TITLE.md 형태로 새로운 문서를 생성
  - 다음 형식으로 post 문서를 시작

  ```
  ---
  layout: post
  title:  "제목"
  subtitle: "간략한설명"
  date:   업로드 날짜 및 시간
  background: '사진'
  categories: jekyll update
  —
  ```

  - markdown 형식으로 post파일 만들기


4. **댓글 기능 추가**

- [Disqus홈페이지](https://disqus.com/) 가입
- "I want to install Disqus on my site" 선택
- 사이트 정보 입력 - **Website Name** 기억해두기 
- Platform 중 Jekyll 선택
- Install Instruction을 읽어본 후 **Configure**를 눌러 다음을 진행
- **Website URL**에 블로그 주소 입력 후 Next 이동
- Comment 정책 체크 후, Complete Setup을 눌러 설정 마무리
- **_config.yml**에 다음과 같은 key-value 추가

```
# Custom vars
comment:
  provider: "disqus"
  disqus:
    shortname:  "littlesparkles"
    shortname1: "Git"
    shortname2: "Github"
    shortname3: "Jekyll"
    shortname4: "Markdown"
    shortname5: "Google-Analytics"
```

- **_layout/post.html**에 Universal Code 적용 (PAGE_URL과 PAGE_IDENTIFIER은 나의 정보에 맞게 수정)
```
{% if page.comments %}
<h2>Comments</h2>
<div id="disqus_thread"></div>
<script>
    /**
    *  RECOMMENDED CONFIGURATION VARIABLES: EDIT AND UNCOMMENT THE SECTION BELOW TO INSERT DYNAMIC VALUES FROM YOUR PLATFORM OR CMS.
    *  LEARN WHY DEFINING THESE VARIABLES IS IMPORTANT: https://disqus.com/admin/universalcode/#configuration-variables    */
    let PAGE_URL = "{{site.url}}{{page.url}}"
    let PAGE_IDENTIFIER = "{{page.url}}"
    var disqus_config = function () {
    this.page.url = PAGE_URL;  // Replace PAGE_URL with your page's canonical URL variable
    this.page.identifier = PAGE_IDENTIFIER; // Replace PAGE_IDENTIFIER with your page's unique identifier variable
    };
    (function() { // DON'T EDIT BELOW THIS LINE
    var d = document, s = d.createElement('script');
    s.src = 'https://littlesparkles.disqus.com/embed.js';
    s.setAttribute('data-timestamp', +new Date());
    (d.head || d.body).appendChild(s);
    })();
</script>
<noscript>Please enable JavaScript to view the <a href="https://disqus.com/?ref_noscript">comments powered by Disqus.</a></noscript>
{% endif %}
```

5. Favicon 추가
- [favicon generator](https://realfavicongenerator.net/)에 접속해서 원하는 사진 넣기
- 다운로드를 받고 압축 폴더를 받기
- 현재 디렉토리의 assets 폴더 내의 favicon.ico라는 폴더를 만들고 여기에 압축 풀기
- 다운로드 하고 난 사이트 가장 하단에서 **Generate your Favicons and HTML code** 버튼 누르기
- _includes/head.html 파일에 아래 코드 추가
  - 파일 이름 앞에 **/assets/logo.ico** 추가하기

```
<link rel="apple-touch-icon" sizes="180x180" href="/assets/favicon.ico/apple-touch-icon.png">
<link rel="icon" type="image/png" sizes="32x32" href="/assets/favicon.ico/favicon-32x32.png">
<link rel="icon" type="image/png" sizes="16x16" href="/assets/favicon.ico/favicon-16x16.png">
<link rel="manifest" href="/assets/favicon.ico/site.webmanifest">
<link rel="mask-icon" href="/assets/favicon.ico/safari-pinned-tab.svg" color="#5bbad5">
<meta name="msapplication-TileColor" content="#da532c">
<meta name="theme-color" content="#ffffff">
```

6. Google analytics
- **Google-Analytics 기능 추가 포스팅은 블로그 내에 있음**

## Copyright and License

Copyright 2013-2021 Start Bootstrap LLC. Code released under the [MIT](https://github.com/StartBootstrap/startbootstrap-clean-blog-jekyll/blob/master/LICENSE) license.
