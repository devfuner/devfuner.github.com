---
layout: post
title: "동영상에서 이미지 추출하기"
category: blog
tags: [ffmpeg, image, python]
---
어느날 형이 외장하드를 주면서 블랙박스 영상인데 시간 날때 확인 좀 해달라는거였다.
어젯밤에 누가 아주 살짝 스치고 지나간것 같은데 이벤트영상에는 없더라는 것이었다.
우선 영상을 보기로 했는데.... 이런 30G나 되는 영상을 나보고 다 어떻게 보라는거냐....
30초짜리 영상이 760여개는 되었던거 같은데.
단순히 계산해도 6시간 반동안 보고 있어야 한다.
아냐 이건 못해. 사람이 할 짓이 아니지.
어쩐다? 어쩌지?

그래서 ffmpeg로 우선 영상을 이미지로 추출하기로 했다.
난 허접해서 영상분석같은건 할줄 모른다.

ffmpeg 명령어
    ffmpeg -i video-filename.mp4 -r 1 -t 30 image-filename-%2d.jpeg

옵션의 자세한 내용은 나도 잘 모른다.
이렇게 하는걸 검색해서 찾아고 이래 저래 따라 했을 뿐이다.
[FFmpeg 라이브러리 : 코덱과 영상 변환을 중심으로](http://www.hanbit.co.kr/ebook/look.html?isbn=9788968487729) 최근에 이런 책도 나왔던데 한번 보고 싶다.

간단히 소개하자면 1초에 1프레임을 추출하는데 30초까지만 작동한다는 명령이다.
나의 경우 영상이 딱 30초짜리기 때문에 이걸로 충분하다.
오케이 그럼 영상에서 이미지 추출하는 방법은 해결. 근데 이거 영상 파일이 760개 라고 하지 않았나?
일일이 하나씩 친다면 일일이 영상 보는거랑 별다르지 않은 고생을 해야한다.
이럴때 우리는 우리의 노예. 컴퓨터에게 이런 일을 시켜야 한다.
파이썬으로 간단하게 반복문을 사용해서 명령어를 반복 실행 시킨다.
(이것만 해도 시간이 오래 걸린다. 그럼 쓰레드나 프로세스를 여러개 띄우는 방식으로 조금 더 빠르게 작업을 마칠 수 있다.)

작업중.....

자! 760 X 30 = 22800개의 이미지가 만들어 졌다.
이제 이걸 일일이 확인하자.
잉? 아니지? ㅋ
일일이 볼거 였으면 그냥 영상 보고 말았지.

뛰어난 우리의 개발자님들은 이럴때를 대비해서인지 벌써 여러가지 소스를 공개해주셨다.
[이상욱님의 비슷한 이미지 검색(Python)](http://yisangwook.tumblr.com/post/83365685690/detecting-duplicate-images-using-python)
이것을 활용하면 우리는 편안히 커피한잔 마시며 다른일 하면 된다.

```python
#!/usr/bin/env python
# -*- coding: utf-8 -*-
from PIL import Image
import glob
from shutil import copy


def dhash(image, hash_size=8):
    # Grayscale and shrink the image in one step.
    image = image.convert('L').resize(
        (hash_size + 1, hash_size),
        Image.ANTIALIAS,
    )

    pixels = list(image.getdata())

    # Compare adjacent pixels.
    difference = []
    for row in range(hash_size):
        for col in range(hash_size):
            pixel_left = image.getpixel((col, row))
            pixel_right = image.getpixel((col + 1, row))
            difference.append(pixel_left > pixel_right)

    # Convert the binary array to a hexadecimal string.
    decimal_value = 0
    hex_string = []
    for index, value in enumerate(difference):
        if value:
            decimal_value += 2**(index % 8)
        if (index % 8) == 7:
            hex_string.append(hex(decimal_value)[2:].rjust(2, '0'))
            decimal_value = 0

    return ''.join(hex_string)


def img_diff(orig, modif, hash_size):
    # hash_size로 이미지의 정확도를 조절합니다.
    # 높을수록 비교 정확도가 올라가고 낮을수록 비교 정확도가 내려갑니다.

    # crop은 이미지를 자르는 명령이다.
    # 이미지를 자른 이유는 빨간색 LED가 계속 깜빡거리며 나오기 때문에 그 부분을 제외시키려고 잘랐다.
    # 이미지를 비교할때만 자르는 것이고 원본은 그대로 있다.
    o = Image.open(orig).crop((0, 0, 1920, 800))
    m = Image.open(modif).crop((0, 0, 1920, 800))
    if dhash(o, hash_size) != dhash(m, hash_size):
        print("Difference Image {0} / {1}".format(orig, modif))
        # 첫번째 이미지와 두번째 이미지가 다르다면 첫번째 이미지를 event디렉토리로 복사합니다.
        copy(orig, "event/") # event 디렉토리는 이미 만들어져 있어야 합니다.


# 이미지 파일이 위치한 곳에서 스크립트를 실행해야 합니다.
if __name__ == '__main__':
    file_list = glob.glob('*')

    for idx, f in enumerate(file_list):
        try:
            img_diff(f, file_list[idx+1], 4)
        except IndexError as e:
            print(e)
```

이 스크립트를 실행하면 이미지가 다를 경우 event디렉토리로 복사해준다.
그럼 우리는 복사된 이미지를 보고 해당 시간의 영상만 확인하면 된다.

예시 이미지 01
![블랙박스 영상 이미지](/images/posts/image-diff/e22c1219_001.jpeg)
예시 이미지 02
![블랙박스 영상 이미지](/images/posts/image-diff/e22c1219_002.jpeg)

궁금하신 부분은 얼마든지 댓글로 남겨주세요.