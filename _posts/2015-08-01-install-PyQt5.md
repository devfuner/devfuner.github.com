---
layout: post
title: "OS X(10.10.4) PyQt5 설치하기"
category: blog
tags: [OS_X, PyQt5, python]
---

파이썬으로 GUI 한번 해봅시다.  
[[bash파일 다운로드]](/download/install_pyqt5.sh)

```bash
#!/bin/bash -v
# 참조 사이트 
# https://gist.github.com/guillaumevincent/10983814
# https://forum.qt.io/topic/42698/qt5-3-could-not-resolve-sdk-path-for-macosx10-8/3

wget http://www.riverbankcomputing.com/static/Downloads/sip4/sip-4.16.9.tar.gz
wget http://www.riverbankcomputing.com/static/Downloads/PyQt5/PyQt-gpl-5.5.tar.gz

tar zxvf PyQt-gpl-5.5.tar.gz
tar zxvf sip-4.16.9.tar.gz

cd sip-4.16.9
python configure.py -d /Users/devfuner/.pyenv/versions/pyqt5/lib/python3.4/site-packages --arch x86_64
make
sudo make install
sudo make clean

# Download Link 
# http://download.qt.io/archive/qt/5.2/5.2.1/qt-opensource-mac-x64-clang-5.2.1.dmg
# install qt-opensource-mac-x64-clang-5.2.1.dmg

####
# You may try

# Open with a text editor
#   Qt5.3 /5.3 /clang_64 /mkspecs /qdevice.pri

# change
#   !host_build:QMAKE_MAC_SDK = macosx10.8

#   to

#   !host_build:QMAKE_MAC_SDK = macosx10.9

# restart your Qt
####
cd PyQt-gpl-5.5
python configure.py --verbose -d /Users/devfuner/.pyenv/versions/pyqt5/lib/python3.4/site-packages --qmake /Users/devfuner/Qt5.2.1/5.2.1/clang_64/bin/qmake
make
sudo make install
sudo make clean
```