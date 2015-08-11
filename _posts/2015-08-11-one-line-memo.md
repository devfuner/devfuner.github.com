---
layout: post
title: "빠르게 한줄 메모하기"
category: blog
tags: [Alfred, python, workflow, app]
---

어떤 작업을 하다가 순간적으로 드는 생각을 빨리 메모해야 하는 경우가 자주 있지 않나요?
이럴 때 어떻게 하시나요?

1. 메모 앱  
2. (UI가 뜨길 기다렸다가) 새로운 노트를 생성한다.  
3. 메모를 작성한다.  
4. 메모 앱을 닫는다.  

가장 일반적인 경우가 저렇지 않을까 생각합니다.
위의 방법으로 메모를 입력하기까지 각 단계별로 딜레이가 조금씩 생기죠.
그래서 순간 드는 생각을 까먹을 때도 있구요.
딜레이를 없앨 수 있고 입력도 빠르게 할 수 있으면 좋겠는데요.
알프레드와 스크립트 언어만 있으면 가능합니다.

시작합니다.
알프레드를 이용한 한줄 메모를 빠르게 하기입니다.
작업 흐름은 이렇습니다.

1. 알프레드 실행  
2. 한줄 메모  
3. 엔터(끝)  

다 아시듯이 알프레드는 UI가 굉장히 빠르게 뜹니다.
딜레이가 거의 없으니 메모를 빠르게 입력 할 수 있습니다.
그리고 엔터만 치면 메모 작성 완료!
어떤 작업을 하고 있던 상관없이 바로 메모를 입력한 후 원래 하고 있던 작업으로 돌아올 수 있습니다.

우선 워크플로를 만들어 보겠습니다.
Alfred의 설정창을 여시고 워크플로 탭을 선택하세요.
새로운 Blank Workflow를 생성하시고 아래의 이미지를 따라하세요.

![one-line-memo-001](/images/posts/one-line-memo/119f0b72_001.png)
![one-line-memo-002](/images/posts/one-line-memo/119f0b72_002.png)
![one-line-memo-003](/images/posts/one-line-memo/119f0b72_003.png)
![one-line-memo-004](/images/posts/one-line-memo/119f0b72_004.png)
![one-line-memo-005](/images/posts/one-line-memo/119f0b72_005.png)
![one-line-memo-006](/images/posts/one-line-memo/119f0b72_006.png)

워크플로에서 사용하는 키워드(여기서는 ol)는 사용하기 편하신걸로 바꾸시면 됩니다.
이제 파이썬 스크립트를 복사해서 'Run Script'에 붙여넣기 해주세요.

    ```python
    #!/usr/bin/env python
    # -*- coding: utf-8 -*-

    from datetime import datetime
    import unicodedata
    import sys
    reload(sys)
    sys.setdefaultencoding("utf-8")


    def get_date_format(dformat="%Y-%m-%d"):  # "%Y-%m-%d_%H-%M-%S"
        d = datetime.now()
        return d.strftime(dformat)

    base_path = '/Users/devfuner/Dropbox/Public/dailymemo/'
    file_dailymemo = base_path + get_date_format() + '.txt'

    q = u'{query}'
    q2 = unicodedata.normalize('NFC', q)
    q3 = q2.encode('utf-8')

    text = q3

    with open(file_dailymemo, 'a') as f:
        f.write('[%s] - %s\n' % (get_date_format("%H:%M:%S"), text))

    그리고 base_path에 새로운 파일이 생길경로를 지정해주세요.  

        base_path = '/Users/devfuner/Dropbox/Public/dailymemo/'
    ```

마지막 '/'까지 꼭 넣어주세요.  
이제 테스트를 해보세요.  
오늘 날짜로 새로운 TXT파일이 생기고 입력한 메모에 입력한 시간이 붙어서 입력됩니다.
![one-line-memo-007](/images/posts/one-line-memo/119f0b72_007.png)
![one-line-memo-008](/images/posts/one-line-memo/119f0b72_008.png)