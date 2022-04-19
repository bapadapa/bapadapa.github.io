---
layout: single
title: "GitBlog - Google Analytics"
categories: Gitblog
tag: [blog, git, init, 깃, 블로그]
---

---

{% capture my_index %}{%include_relative index/github_init_index.md %}{% endcapture %}
{{ my_index | markdownify }}

---

# 방문자 분석하기!

## 기본 애널리틱스 생성하기

1. [Google Analytics](https://analytics.google.com) 에 들어간다
1. 로그인 후 `측정시작` ( 생성하기 )을 누른다
1. 계정이름, 속성 이름등 원하는 값들을 삽입하고 만들어 주면 된다

## 애널리틱스 설정하기

1. 생성된 페이지에서 플랫폼을 웹을 선택해 준다.
1. `웹사이트 URL : 본인 블로그 URL` 및 `스트림 이름 : 별칭` 을 설정 후 `스트림 만들기 클릭`
1. `웹 스트림 세부정보`에 보여지는 `측정 ID`를 잘 저장해준다.

## 적용시키기

```yml
# _config.yml
# 약 90번째줄
# Analytics
analytics:
  provider: "google-gtag"
  google:
    tracking_id: "측정 ID"
    anonymize_ip: false
```

---

위와 같이 진행하면, 애널리틱스의 보고서에서 저장되는 것을 잘 확인할 수 있다.
