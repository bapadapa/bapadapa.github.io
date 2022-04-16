---
layout: single
title: "GitBlog - Tags"
categories: Gitblog
---

{% assign  cateLen = page.categories | downcase | size | minus: 4%}
{% assign  category = page.categories | downcase |  slice: 2 , cateLen %}

{{site.url}}/{{category}}

---

@[테스트](/_index/github_init_index.md)

<div>
    {%include_relative indexs/github_init_index.md %} 
    
</div>

> ## GItblog 기본 구축
>
> [Minimal Mistakes Jekyll theme](https://github.com/mmistakes/minimal-mistakes) 를 **Fork**하여 제작
>
> > 1. [GitBlog-**기본환경**]({{site.url}}/gitblog/GitBlog-기본환경)
> > 1. [GitBlog-**댓글**]({{site.url}}/gitblog/GitBlog-댓글)
> > 1. [GitBlog-**방문자 분석** With **Google-Analytics**]({{site.url}}/gitblog/GitBlog-Google-Analytics)
> > 1. [GitBlog-**카테고리**]({{site.url}}/gitblog/GitBlog-Category)

> ## 에러 해결
>
> > 1. [GitBlog-포스팅실패]({{site.url}}/gitblog/GitBlog-포스팅실패)

---

테스트중
