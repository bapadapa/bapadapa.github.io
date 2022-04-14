---
layout: single
title: "GitBlog - Category"
categories: Gitblog
---

> ## GItblog 기본 구축
>
> [Minimal Mistakes Jekyll theme](https://github.com/mmistakes/minimal-mistakes) 를 **Fork**하여 제작
>
> > 1. [GitBlog-**기본환경**]({{site.url}}/GitBlog-기본환경)
> > 1. [GitBlog-**댓글**]({{site.url}}/GitBlog-댓글)
> > 1. [GitBlog-**방문자 분석** With **Google-Analytics**]({{site.url}}/GitBlog-Google-Analytics)
> > 1. [GitBlog-**카테고리**]({{site.url}}/GitBlog-Category)

> ## 에러 해결
>
> > 1. [GitBlog-포스팅실패]({{site.url}}/GitBlog-포스팅실패)

---

# 카테고리 생성하기

> ## `_config.yml` 의 주석 풀기
>
> ```yml
>  jekyll-archives:
>      enabled:
>       - categories
>        - tags
>       layouts:
>        category: archive-taxonomy
>        tag: archive-taxonomy
>      permalinks:
>        category: /categories/:name/
>        tag: /tags/:name/
> ```

> ## `_Pages` 및 `category-archive.md` 생성
>
> 1. Root 에 \_Pages 디렉토리생성
> 1. \_Pages안에 `category-archive.md` 파일 생성
> 1. category-archive.md 안에 아래 코드삽입
>
> ```yml
> ---
> title: "Category"
> layout: "categories"
> permalink: /categories/
> author_profile: true
> sidebar_main: true
> ---
> ```

> ## `_data`의 `navigation.yml`
>
> 페이지 상단에 띄울 `네비게이션바`이다.
> `Default 제거` 하고, 위에 만든 `Category`를 삽입하자.
>
> ```yml
> main:
>   - title: "Category"
>     url: /categories/
>   # 아래 부분 제거
>   - title: "Quick-Start Guide"
>     url: https://mmistakes.github.io/minimal-mistakes/docs/quick-start-guide/
> ```
>
> 상단에 여러 네비게이션 바를 생성하고 싶으면 위 과정을 반복하면 된다.

> ## Post에 Post Option 추가
>
> 다음과 같이 `categories: Category 명`를 추가해주면 된다
>
> ```yml
> ---
> layout: single
> title: "GitBlog - Category"
> categories: Gitblog
> ---
> ```