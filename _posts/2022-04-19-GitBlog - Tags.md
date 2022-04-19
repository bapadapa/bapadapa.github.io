---
layout: single
title: "GitBlog - Tags"
categories: Gitblog
tag: [blog, git, init, 깃, 블로그]
---

---

{% capture my_index %}{%include_relative index/github_init_index.md %}{% endcapture %}
{{ my_index | markdownify }}

---

# Gitblog에 Tag를 추가하기

> ## \_pages 에 tag-archive.md 추가
>
> > ```yml
> > ---
> > title: "Tag"
> > layout: "tags"
> > permalink: /tags/
> > author_profile: true
> > sidebar_main: true
> > ---
> > ```
>
> ## \_data/navigation.yml 에 아래 값 추가
>
> > ```yml
> > - title: "Tag"
> >   url: /tags/
> > ```
>
> ## Post Option에 값 추가
>
> > ```yml
> > layout: single
> > title: "GitBlog - Tags"
> > categories: Gitblog
> > tag: [blog, git, init]
> > ```
> >
> > 만약 1개만 원한다면 배열이 아니라 1개만 작성하면 된다.
> > e.g `tag: blog`
