---
title: 🔨 라즈베리파이에 사용한 SD카드 맥북에서 읽기
author: bokyung
date: 2024-03-20 00:00:00 +0800
toc: true
pin: false
published: true
categories: [Blogging, Etc]
tags: [RaspberryPi, extFS]
image: https://github.com/bokyung39/intro-me/assets/72790694/51ca1bda-08b1-4939-a975-36c4bd0ffd1e
---

#### **문제 상황**

라즈베리파이에 사용했던 sd카드의 내용을 노트북으로 보고싶어서 맥북에 sd카드 연결하면 되겠지~ 라고 아주 간단하게 생각했는데... <br>
연결해봤더니 파일탐색기엔 **boot**라는 오로지 라즈베리파이를 부팅할때만 필요한 파일들만 보이고 정작 내가 원하는 내용들은 볼 수 없었음ㅎㅎ!!<br>
<img width="597" alt="스크린샷 2024-03-20 오후 2 54 49" src="https://github.com/bokyung39/intro-me/assets/72790694/bb435cf3-8c28-4e5e-ac12-f3bbc441bf23">{: .normal}

난 저 리눅스 부분을 보고싶은데.. ㅠㅡㅠ<br>

가장 간단한 방법은 그냥 노트북으로 사용하던 라즈베리파이에 접속해서 사용하면 되겠지만<br>
그럴 수 있었다면 내가 이렇게 삽질을 하지 않았겠지 ^^<br>
내 라즈베리파이는 본가에 있다구....<br>
나에게 주어진 건 맥북과 sd카드뿐...<br>

찾아보니 <br>

라즈베리 파이의 SD 카드에는 일반적으로 **"boot"** 파티션과 **"root"** 파티션으로 두 가지 파티션이 있다고 한다<br>

> #### Boot 파티션

- boot 파티션은 라즈베리 파이가 부팅할 때 필요한 모든 부트로더 파일과 설정 파일이 포함되어 있는 곳.
- 이 파티션에는 주로 Raspberry Pi용 운영 체제 이미지가 포함되는데, 이 이미지는 보통 FAT32 형식으로 포맷되어 있음
- 부팅에 필요한 커널 파일, 부트로더 파일 및 config.txt와 같은 설정 파일이 포함되어 있음
  <br>

> #### Root 파티션

- root 파티션은 실제 운영 체제 파일 시스템이 있는 곳.
- 이 파티션에는 보통 리눅스 파일 시스템(예: ext4)이 사용됨
- 이 파티션에는 운영 체제의 모든 파일 및 디렉토리가 포함되어 있으며, 라즈베리 파이에서 실행되는 모든 소프트웨어 및 데이터도 여기에 저장됨
  <br>

그러니까... 내가 원하는 파일들은 전부 다 ext4로 되어있는 Root 파티션에 있다는 것<br>

#### 그런데

macOS는 일반적으로 FAT, exFAT과 같은 파일 시스템만을 자동으로 인식하고, ext2, ext3, ext4와 같은 리눅스 파일 시스템은 기본적으로 인식하지 못한댄다...<br>
그래서 파일탐색기에 boot만 표시되는거였다..<br>

![IMG_1389](https://github.com/bokyung39/intro-me/assets/72790694/9c7e58ab-f9c7-44fc-9477-f1d7d94a1f00){: width="50%" height="50%" .normal}

#### 그래서 !!!

root 파티션의 내용을 읽으려면 어떻게 해야하느냐?<br>
하루종일 삽질하고 드디어 성공한 방법 대 공 개<br>

리눅스 파일 시스템을 읽고 쓸 수 있도록 도와주는 소프트웨어를 설치해야함<br>

설치해보자.<br>

### 1. Paragon Software의 extFS for Mac 설치하기

Paragon Software라는 곳에서 ext 형태의 파일 시스템을 읽고 쓸 수 있도록 도와주는 소프트웨어를 설치할 수 있다. 참고로 10일동안 무료로 사용가능 <br>
[https://www.paragon-software.com/ko/home/extfs-mac/](https://www.paragon-software.com/ko/home/extfs-mac/) 설치 ㄱㄱ

### 2. 시스템 확장 프로그램 활성화하기

설치하고 하라는대로 따라가다 보면 환경설정에서 시스템 확장 프로그램을 활성화하라고 시킴<br>
근데 또 활성화 시키려고 하면 <br>
**"시스템 확장 프로그램을 활성화하려면 복구 환경에서 보안 설정을 수정해야 합니다"** 라는 메시지가 뜨면서 시스템을 종료해서 뭐 어쩌구 하라고 하는데 그 방법은<br>
[https://change-words.tistory.com/entry/mac-security-option](https://change-words.tistory.com/entry/mac-security-option) <br>
이 분의 글을 보고 따라했다 !

![image](https://github.com/bokyung39/intro-me/assets/72790694/a23d7469-f069-4f19-a990-3fcc1511a3fd){:width="70%" height="70%" .normal}

그랬더니 extFS 볼륨 부분에 rootfs가 !!!<br>
설레는 마음을 안고 파일 탐색기를 열어보았더니<br>
<img width="367" alt="스크린샷 2024-03-20 오후 2 57 09" src="https://github.com/bokyung39/intro-me/assets/72790694/187c157f-3741-41ce-b720-ecee28c0ef7e">{: width="50%" height="50%" .normal}

이 전엔 없었던 rootfs가 생겼다. <br>
내가 원하던 파일들이 보인다. <br>

![IMG_7458](https://github.com/bokyung39/intro-me/assets/72790694/ef656a40-c8c9-4656-8464-af894e992952){: .normal}
