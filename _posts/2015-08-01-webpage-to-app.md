---
layout: post
title: "자주가는 웹사이트를 앱으로 만들기"
category: blog
tags: [automator, web, app]
---

자주가는 웹사이트가 있으면 어떻게 하시나요?
일반적으로 하는 방법은 즐겨찾기에 추가해놓고 브라우저를 실행시키고 즐겨찾기를 클릭하는 방법일텐데요.
웹페이지 자체를 앱처럼 실행 시킬 수 있는 방법도 있습니다.
Automator를 활용해서 자주가는 웹페이지를 앱으로 만들어 보겠습니다.

1. Automator 작업흐름 만들기
Automator를 실행하시고 작업흐름으로 생성해주세요.
작업흐름으로 하는 이유는 마지막에 설명드리겠습니다. ▼
![Automator](/images/posts/webpage-to-app/5864fcd2_001.png)  
Automator의 보관함 > 인터넷 > 지정된 URL 가져오기 ▼
![Automator](/images/posts/webpage-to-app/5864fcd2_002.png)
Automator의 보관함 > 인터넷 > 웹 사이트 팝업 ▼
![Automator](/images/posts/webpage-to-app/5864fcd2_003.png)
지정된 URL 가져오기에는 앱에서 실행될 웹페이지의 주소를 입력해주세요.
웹 사이트 팝업에서는 앱의 크기를 지정해줍니다.
간편하게 아이폰이나 아이패드의 크기로 하실 수도 있고 직접 지정하실 수도 있습니다.
오른쪽 위에 있는 실행을 눌러서 직접 실행 해보고 알맞은 크기를 지정하세요.
참고로 이 크기는 실행 될 때의 초기값일뿐이며 앱을 실행한 후에도 앱의 크기는 변경할 수 있습니다.
1단계는 우선 다 됐습니다.
이 상태로 적당한 곳에 저장을 해주세요. ▼
![Automator](/images/posts/webpage-to-app/5864fcd2_004.png)

2. Automator 작업흐름을 응용 프로그램(앱)으로
1단계에서 저장한 작업흐름을 그대로 응용 프로그램을 변환하도록 하겠습니다.
파일 > 다음으로 변환 을 실행해주세요. ▼
![Automator](/images/posts/webpage-to-app/5864fcd2_005.png)  
새로운 Automator가 생겼죠?
여기서 유형 선택을 응용 프로그램으로 선택해주세요. ▼
![Automator](/images/posts/webpage-to-app/5864fcd2_006.png)  
지정된 URL 가져오기를 오른쪽클릭해서 나오는 메뉴에서 입력 무시를 클릭합니다. ▼
![Automator](/images/posts/webpage-to-app/5864fcd2_007.png)  
이상태에서 응용 프로그램으로 저장만 해주시면 됩니다. ▼
![Automator](/images/posts/webpage-to-app/5864fcd2_008.png)  
 실행 해볼까요? ▼
 ![Automator](/images/posts/webpage-to-app/5864fcd2_009.png)

3. 응용 프로그램의 아이콘
아이콘 변경은 이미 잘 정리되어있는 [원님의 블로그](http://macnews.tistory.com)를 참고 하시면 되겠습니다.
제가 귀찮아서 그런거 아닙니다. :)
* http://macnews.tistory.com/2254 (이미지 출처) ▼
![아이콘 변경](/images/posts/webpage-to-app/5864fcd2_010.png)

4. Automator를 작업흐름으로 저장한 이유
Automator를 처음부터 응용프로그램으로 만들어도 상관은 없습니다.
하지만 뭔가 수정해야 할 꺼리가 생겼을때는 응용 프로그램은 수정이 불가능 하기 때문에
작업흐름으로 저장한 것입니다.
수정할 것이 있을때 작업흐름을 수정하고 다시 응용 프로그램으로 변환하면 되니까요.
유지보수의 측면에서 작업흐름으로 저장하는 것이 훨씬 더 유용하다고 할 수 있습니다.

5. 아이콘 변경과 관련한 참고할만한 [원님의 블로그](http://macnews.tistory.com) 글들
    - http://macnews.tistory.com/2010
    - http://macnews.tistory.com/2042
    - http://macnews.tistory.com/2777