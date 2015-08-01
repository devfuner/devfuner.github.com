---
layout: post
title: "연속된 이미지로 영상 만들기 - 타임랩스 만들기"
category: blog
tags: [ffmpeg, timelapse]
---
<div align="center"><iframe width="560" height="315" src="https://www.youtube.com/embed/vsoCgW4CixA" frameborder="0" allowfullscreen></iframe></div>

개인적인 목적으로 내가 컴퓨터를 사용하는 동안 1분마다 스크린샷을 찍도록 스크립트를 돌리고 있다.
나중에 내가 뭘 했는지 볼 수도 있고 기록으로 남는다고 생각하니 뻘짓하는걸 조금은 줄일 수 있다.
그래도 볼건 다 본다 :)
이렇게 만들어진 연속된 이미지를 하나씩 보기는 힘들기도 하고 뭔가 좀 쓸만하게 활용할 생각을 하니 바로 타임랩스가 생각났다.
처음엔 FotoMagico라는 앱으로 해볼려다가 바로 포기했다.
생성되는 이미지가 내가 사용할 때만 생성된다고 해도 하루에 양이 꽤 된다.
1분에 한장이니까 하루에 1440장.
이중에 내가 12시간만 사용해도 720장이 생긴다.
한달이면? 어휴...
내가 사용하는게 맥북에어 기본 모델이기도 해서 메모리도 부족하기 때문에 감당이 안된다.
우선 한달정도 이미지는 모아졌고 테스트로 하루치의 타임랩스를 만들어 봤다.  
우선 400장 정도의 이미지가 있었고 그중에 추려서 테스트 영상을 만들었다.



ffmpeg는 brew로 기본설치 하였고 명령은 아래와 같다.
타임랩스를 만들 이미지의 이름이 숫자로 연속되어 있어야한다.
```
prompt> ffmpeg -r 6 -f image2 -start_number 001 -i sc_%03d.jpg -codec:v prores -profile:v 2 ../test.mov
```

####참조 자료
- https://www.youtube.com/watch?v=WDV15nm-KJE