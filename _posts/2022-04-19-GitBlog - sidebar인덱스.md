---
layout: single
title: "GitBlog - Sidebar에 Index추가"
categories: Gitblog
tag: [blog, git, init, 깃, 블로그]
---

---

{% capture my_index %}{%include_relative index/github_init_index.md %}{% endcapture %}
{{ my_index | markdownify }}

---

# SideBar 인덱스 추가

1. \_data/navigation.yml에 아래코드 추가
   > 만약 여러개를 원한다면, -title를 여러개 붙여놔 주면 된다.

```yml
docs:
  - title: "Index"
    children:
      - title: "Category"
        url: /categories/
      - title: "Tag"
        url: /tags/
```

1. post시 아래 코드를 Option에 추가
   > docs는 `navigation`에서 설정한 값이다.

```md
    sidebar:
      nav: "docs"
```

1. 하지만 매번 추가하기 귀찮으니 \_config.yml에 추가해주자.

```yml
# Defaults
defaults:
  # _posts
  - scope:
      path: ""
      type: posts
    values:
      layout: single
      toc: true
      author_profile: true
      read_time: true
      comments: true
      share: true
      related: true
      show_date: true
      sidebar:
        nav: "docs"
```
