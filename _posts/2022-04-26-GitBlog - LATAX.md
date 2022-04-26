---
layout: single
title: "GitBlog - LATAX 추가하기 ( 수식 사용하기 )"
categories: Gitblog
tag: [blog, git, init, LATAX, 수식]
---

---

{% capture my_index %}{%include_relative index/github_init_index.md %}{% endcapture %}
{{ my_index | markdownify }}

---

# LATAX 사용하기

## MathJax srcipt 가져오기

`_includes/head.html`안에 아래 코드 추가해주기

```html
<!-- MATHJAX -->
<script
  type="text/javascript"
  src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML"
></script>

<!-- 위에 것이 안 되면 아래 것을 추가 해보자!  본인은 아래 script가 성공함 -->
<!-- MATHJAX -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.2/MathJax.js?config=TeX-MML-AM_CHTML"></script>
```

끝

## 간단 문법

아래와 같이 **`$$`** 로 묶어 사용하면 된다. <br>

[라텍스 문법 위키](https://ko.wikipedia.org/wiki/%EC%9C%84%ED%82%A4%EB%B0%B1%EA%B3%BC:TeX_%EB%AC%B8%EB%B2%95) 에 들어가서 문법을 확인하고 사용해보자

```
$$ A^B  $$
```

$$ A^B $$
