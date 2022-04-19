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

# Google 검색엔진 등록

1. [Google Searcg Console](https://search.google.com/search-console/welcome?hl=ko&utm_source=wmx&utm_medium=deprecation-pane&utm_content=home)에 들어가서 URL 접두어에 본인 `블로그 주소 (Github URL)`를 기입한다
1. 계속하기를 누르면 소유권 확인 이라는 팝업창이 뜨는데, 거기서 *google~.html*파일을 다운로드 받아준다.
1. 해당 파일을 본인 디렉토리의 가장 밖으로 옮겨준다. (\_config.xml, LICENSE등과 동일한 위치)
