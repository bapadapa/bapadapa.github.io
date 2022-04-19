---
layout: single
title: "GitBlog - SearchEngine"
categories: Gitblog
tag: [blog, git, init]
---

---

{% capture my_index %}{%include_relative index/github_init_index.md %}{% endcapture %}
{{ my_index | markdownify }}

---

> 아래 작업들은 당연히 **로그인을 진행**하고 수행해야 한다

# Google 검색엔진 등록

1.  [Google Searcg Console](https://search.google.com/search-console/welcome?hl=ko&utm_source=wmx&utm_medium=deprecation-pane&utm_content=home)에 들어가서 URL 접두어에 본인 `블로그 주소 (Github URL)`를 기입한다
1.  계속하기를 누르면 소유권 확인 이라는 팝업창이 뜨는데, 거기서 *google~.html*파일을 다운로드 받아준다.
1.  해당 파일을 본인 디렉토리의 가장 밖으로 옮겨준다. (\_config.xml, LICENSE등과 동일한 위치)
1.  파일을 옮긴 후 Git Push를 해주고, 적용되길 기다린다.
    - Push 및 Debug가 완료되면, 소유권 팝업에서 확인을 눌러준다.
1.  이제 속성을 설정하기 위해 **속성으로 이동**을 눌러준다
1.  **Sitemaps**를 클릭하고, 새 사이트 맵 추가에 본인블로그 URL/sitemap.xml을 삽입하여 제출해준다
    > `E.g https://bapadapa.github.io/sitemap.xml
    >
    > `404 가아니라, 다른 페이지 `<url> ~~~~ </url>`과 같이 뜬다면 즐거운 마음으로 기다려보자
    >
    > > 개시가 즉각적으로 되지 않는다. 기다려보고, 나중에도 안 된다면 다시 시도해보면 된다. GoogleConsole에서 즉각적인 반영하지 않는다함.

# Naver 검색엔진 등록

1.  [NAVER Search Advisor](https://searchadvisor.naver.com/)에 들어가서 `웹마스터 도구`를 눌러준다
1.  Google과 동일하게 본인 블로그 URL을 삽입해준다.
    - https://bapadapa.github.io
1.  HTML 태그라고 적혀있는곳에서 Content="abcde~~" 값을 복사해서 \_config.xml에 삽입해 준다.

    ```yml
    # 약 75번.
    # SEO Related
    google_site_verification:
    bing_site_verification:
    naver_site_verification: "abcde~~"
    yandex_site_verification:
    baidu_site_verification:
    ```

1.  모두 삽입하였으면 Push 해준다.

1.  Push 및 Debug가 완료되면 **소유확인**을 눌러준다

1.  소유 확인이 완료되면 , `사이트 목록`에서 등록한 사이트를 클릭해준다.
1.  우측 요청 - 사이트맵 제출을 클릭하여 위 Google과 동일하게 stiemap.xml을 추가시켜준다.
1.  검증에 들어가서 웹 페이지 최적화를 실행시켜보면, 등록이 잘 되었는지 확인할 수 있다.
