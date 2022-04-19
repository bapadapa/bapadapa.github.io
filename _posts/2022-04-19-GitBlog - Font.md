---
layout: single
title: "GitBlog - 폰트변경"
categories: Gitblog
tag: [blog, git, init, 깃, 블로그]
---

---

{% capture my_index %}{%include_relative index/github_init_index.md %}{% endcapture %}
{{ my_index | markdownify }}

---

# Font변경

> Font를 가져오는 방법은 여러가지가 있지만, Google에 있는 Font를 가져와서 사용

1. [구글폰트](https://fonts.google.com/) 이곳에 접속하여 원하는 폰트를 검색해본다

1. 원하는 폰트를 찾았으면 Selected Family에서 @import를 클릭하여 import문을 가져온다

   - E.g `@import url('https://fonts.googleapis.com/css2?family=Cute+Font&display=swap');`
   - 만약 보이지 않는다면 폰트 확인하는 것 옆에 `select this style`를 클릭해주면 나타남

1. \_sass/minimal-mistakes.scss에 값 추가

```scss
/*Google Font */
@import url("https://fonts.googleapis.com/css2?family=Cute+Font&display=swap");
```

1. \_sass/minimal-mistakes/\_variables.scss에 값추가
   `"Cute Font"` 를 선택했기 때문에 `"Cute Font"`를 추가해 준다

```scss
/* system typefaces */
$serif: Georgia, Times, serif !default;
$sans-serif: -apple-system, BlinkMacSystemFont, "Cute Font", "Roboto",
  "Segoe UI", "Helvetica Neue", "Lucida Grande", Arial, sans-serif !default;
$monospace: Monaco, Consolas, "Lucida Console", monospace !default;
```
