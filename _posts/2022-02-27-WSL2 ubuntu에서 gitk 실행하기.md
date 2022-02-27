---
layout: post
title: WSL2 ubuntu에서 gitk 실행하기
date: 2022-02-27
categories: 개발환경
tags: [git, WSL]
---

WSL2를 통해 설치한 ubuntu환경에서 git은 동작하지만 `gitk`가 다음과 같은 오류 메세지를 출력하며 동작하지 않는 문제가 있다.

```shell
application-specific initialization failed: no display name and no $DISPLAY environment variable
Error in startup script: no display name and no $DISPLAY environment variable
    while executing
"load /usr/lib/x86_64-linux-gnu/libtk8.6.so Tk"
    ("package ifneeded Tk 8.6.10" script)
    invoked from within
"package require Tk"
    (file "/usr/bin/gitk" line 10)
```

좀 더 정확히 이야기 하면,  `windows terminal`, `power shell`에선 동작하는 것으로 보아  ubuntu 환경이라기 보단 `bash shell`에서 동작하지 않는 것으로 보인다. 실제로 `cmder` 를 통한  `bash shell`에서도 처리가 안된다.

이 오류를 해결하려면 `gitk` 명령어 위치를 윈도우에 설치된 `gitk`로 바꿔주면 된다. 먼저 `cmd`에 다음과 같은 명령어를 친다.

```
where gitk
```

그러면 경로가 하나 뜰텐데 본인은 다음처럼 나온다.

```
C:\Program Files\Git\cmd\gitk.exe
```

그리고 다시 `bash shell`환경에서 다음 명령어를 입력하여 alias를 `.bashrc`에 입력한다. 이때 경로가 위와 다르다면 경로만 바꿔주면 된다.

``` shell
echo -e 'alias gitk="/mnt/c/\\047Program Files\\047/Git/cmd/gitk.exe"' >> ~/.bashrc
```

참고로 `\047`은 작은 따옴표를 의미하고 이를 출력하기 위해 옵션 `-e`를 준 것이다.

마지막으로 `source`명령어로 ~/.bashrc를 다시 로드 한다.

```shell
source ~/.bashrc
```

그리고 `gik`를 입력하면 정상적으로 동작하는걸 확인할 수 있다.
