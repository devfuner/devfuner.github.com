---
layout: post
title: "쉘스크립트를 앱으로 래핑하기"
category: blog
tags: [bash, applescript]
---

이 위키를 만들면서 불편한 점은 수정한 것이 생길때마다 터미널에서 커밋을 해줘야한다는 것이다.  
그나마 쉘스크립트로 커밋은 한번에 할 수 있다.  

###### 파일이름: sync.sh
```bash
#!/bin/bash -v
git pull
git add . -A
git commit -m "auto commit"
git push origin master
```

###### sync파일의 속성 변경
>prompt> chmod +rx sync.sh  

###### 실행하는법
>prompt> ./sync.sh  


![나의 실행 화면](/images/posts/packaged-bash/f2f1c71c_001.jpg)  
커밋을 한 직후라서 커밋할 내용이 없다.  


이렇게 쉘스크립트를 사용해서 간편하게 할 수는 있다지만 수정사항이 생길때마다 실행중인 앱(wiki 작성중인)에서 터미널로 포커스를 옮겨야 하고 터미널에 쉘스크립트 실행명령을 타이핑해야한다.  
얼마나 귀찮아!!!  
여기까지는 이분의 블로그를 참조했다. 덕분에 감사합니다. ^^  

[빠르고 가벼운 개인용 마크다운 위키 - 비트버킷과 골룸을 활용](http://nolboo.github.io/blog/2013/12/17/markdown-wiki-bitbucket-gollum/)

<hr>
더 간단하게 할 수 있는 방법을 찾아보다가 애플스크립트로 래핑을 해주면 맥에서 응용프로그램처럼 사용할 수 있다는걸 알았다.  
이제 터미널에서 쉘스크립트 실행하는 것보다 간편하게 하는 방법을 알아보자.  
sync를 해주는 응용프로그램을 만들고 그것만 더블클릭하면 sync가 되도록 할것이다.  
우선 *스크립트 편집기*를 실행해서 아래의 애플스크립트를 붙여넣는다.  

###### 파일이름: wiki sync.app
```applescript
tell application "Terminal"
    -- 터미널을 실행하고 쉘스크립트를 실행한 후 12초 후에 터미널 종료
    activate
    delay 2
    set currentTab to do script ("cd /이곳에/당신의/위키/경로를/적는다/wiki")
    delay 2
    do script ("./sync.sh") in currentTab
    delay 12
    quit
end tell
```

![애플스크립트](/images/posts/packaged-bash/f2f1c71c_002.jpg)  
![애플스크립트](/images/posts/packaged-bash/f2f1c71c_003.jpg)  

이 스크립트를 붙여넣고 저장할때 응용프로그램으로 선택하고 저장하면 끝난다.  
그럼 스크립트의 내용부터 한번 보자.  
중요한것은 경로와 실행파일이름이다.  
이것만 자신의 경로와 이름에 맞게 수정해주면 된다.  
저장하고 실행하면 자동으로 터미널이 실행되고 쉘스크립트를 실행한 후 대략 16초의 시간이 지나면 터미널이 자동으로 닫힌다.  
이 애플스크립트를 이용해서 오토메이터로 '서비스'를 만들면 단축키를 지정해서 사용할 수 있다.  

주의할 점은!  
애플스크립트에서 딜레이시간을 짧게 주면 sync중인 작업때문에 터미널을 닫을거냐고 물어본다.  
수정한게 많아서 sync가 오래 걸릴 경우 참고해야 한다.  

애플스크립트 잘 아시는분은 터미널에서 뭔가를 실행중인지 체크하는 명령어 좀 알려주세요~  