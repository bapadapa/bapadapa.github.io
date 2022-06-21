---
layout: single
title: "Linux - Shebang Line "
categories: Linux
tag: [Linux, Command, shebang]
---

# Shebang Line? ( #! ? )

Shell script에서 최상단에 적어두는 명령줄이다.

간단하게 말하자면 `윈도우의 확장자`라고 보면 된다.

사실 윈도우에서 .exe , .mp4 등 여러 확장자가 있지만, 사실 윈도우 내에서 자동으로 해당 파일이 무엇인지 맵핑을 시켜준 것이다.

그러한 것을 리눅스에서는 자동으로 해주지 않기 때문에 Shebang Line을 이용하여 명시를 해 준다고 생각하면 편하다. - 리눅스에서는 확장자가 구분에는 좋지만, 맵핑이 되지는 않는다.

- e.g `python a.c`처럼 a.c C언어로 구현된 파일을 실행을 시켜도 python을 이용하여 실행이 된다.

```shell
#!/usr/bin/python
Script
```

`#!/usr/bin/python` 를 가장 상단에 명시하면, /usr/bin/python를 이용하여 아래 Script 를 실행하겠다는 의미다.

위와같은 방식으로 할 수 있지만, env를 이용하여 보다 편리하게 사용할 수 있다.

```shell
#!/usr/bin/env python
Script
```

`#!/usr/bin/env python`를 명시하면 env(환경변수)기준으로 python을 찾아서 Script를 실행해준다.

이때 환경변수 기준으로 실행하기 때문에 환경변수 설정을 잘 하고 수행해야 된다.

# 결론

1. 윈도우에 확장자가 있다면, 리눅스에는 Shebang Line이 있다!
2. shebang Line에 Python을 넣었으면 Python 코드를, Bash를 넣었으면 Bash코드를 작성하자!
