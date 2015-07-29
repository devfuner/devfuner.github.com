---
layout: post
title: 알프레드로 쉘 실행하기
category: blog
tags: [bash, Alfred, workflow]
---

[쉘스크립트를 앱으로 래핑하기](http://devfuner.github.io/blog/2015/07/28/packaged-bash/) 이 방법보다는 알프레드의 파워팩을 가지고 있다면 이 방법이 가장 깔끔하다.

아래와 같은 bash 스크립트가 있다면  
```bash
#!/bin/bash -v
cd /당신의/경로를/입력/하세요
git pull
git add . -A
git commit -m "auto commit"
git push origin master
```

아래 이미지의 방법으로 간단하게 단축키로 실행할 수 있다.

![알프레드설정](/images/posts/alfred-hotkey/e01edbfc_001.png)
![알프레드설정](/images/posts/alfred-hotkey/e01edbfc_002.png)  
![알프레드설정](/images/posts/alfred-hotkey/e01edbfc_003.png)  
![알프레드설정](/images/posts/alfred-hotkey/e01edbfc_004.png)  
![알프레드설정](/images/posts/alfred-hotkey/e01edbfc_005.png)  
