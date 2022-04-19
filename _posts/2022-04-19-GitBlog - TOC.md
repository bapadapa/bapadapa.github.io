---
layout: single
title: "GitBlog - TOC"
categories: Gitblog
tag: [blog, git, init, 깃, 블로그]
---

---

{% capture my_index %}{%include_relative index/github_init_index.md %}{% endcapture %}
{{ my_index | markdownify }}

---

# TOC ( Table of Contents ) 목차 추가하기!

> ## option 에 toc: true 추가
>
> > ```yml
> > ---
> > layout: single
> > title: "GitBlog - TOC"
> > categories: Gitblog
> > tag: [blog, git, init]
> > toc: true
> > ---
> > ```
>
> ## \_config.yml에 추가
>
> Post마다 추가하기 귀찮으니 \_config.yml에 추가하자
>
> > ```yml
> > # Defaults
> > defaults:
> >   # _posts
> >   - scope:
> >       path: ""
> >       type: posts
> >     values:
> >       layout: single
> >       author_profile: true
> >       read_time: true
> >       comments: true
> >       share: true
> >       related: true
> >       show_date: true
> >       toc: true # _posts 매번 추가하기 귀찮으니 여기에 추가
> > ```
