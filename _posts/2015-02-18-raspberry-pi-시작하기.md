---
published: true
layout: post
categories:
  - Raspberry Pi
tags:
  - 라즈베리 파이
  - 라즈비안
  - NOOBS
---

###1. 라즈베리 파이(Raspberry Pi)란?

[라즈베리 파이][1]는 영국 BBC의 라즈베리 파이 재단에서 만든 초소형, 초저가 PC이다. 교육용으로 개발되었으며 2012년 3월에 출시된 이후 2013년 11월 기준으로 200만대 이상이 팔렸다. 좀 더 자세한 설명은 [위키백과][2]를 참조하자.

###2. 운영체제 설치

`라즈베리 파이` 역시 컴퓨터이고 운영체제를 필요로 한다. 라즈베리파이를 위해 배포되고 있는 운영체제는 `RASPBIAN`, `SNAPPY UBUNTU CORE`, `OPENELEC`,`RASPBMC`,`PIDORA`,`RISC OS` 등이 있다. 여기에서는 가장 일반적인 `RASPBIAN(라즈비안)`을 설치해 본다.


**준비물**

운영체제를 설치하기 위해서는 다음과 같은 것들이 필요하다.

- 최소 `Class 4` `4GB` 이상의 SD 카드
- 비디오를 연결하기 위한 HDMI-HDMI 케이블(디지털 TV) 또는 HDMI-DVI 케이블(LCD 모니터) 또는 RCA 케이블(구형 아날로그 TV)
- USB 키보드와 마우스
- 유선 랜을 사용하고자 한다면 이더넷 케이블
- 마이크로 USB 전원 어댑터 (보통의 스마트폰의 전원 어댑터)


#####1) 4GB 이상의 `SD 카드`를 컴퓨터에 삽입한다 

#####2) `SD 카드`를 포맷한다.
 
#####3) [라즈베리파이 홈페이지 다운로드 페이지][3]에서 `NOOBS` 파일을 다운로드한다.

#####4) 다운로드 받은 파일의 압축을 푼다. 

#####5) 압축이 풀린 파일들을 `SD 카드`로 복사한다. 

#####6) `SD 카드`를 `라즈베리 파이` 보드에 넣고 전원을 연결한다.

#####7) `NOOBS`로 부팅하면 나타나는 설치할 수 있는 OS 목록에서 `라즈비안`을 선택하고 설치한다.
    
    
    
 [1]: http://www.raspberrypi.org/
 [2]: http://ko.wikipedia.org/wiki/%EB%9D%BC%EC%A6%88%EB%B2%A0%EB%A6%AC_%ED%8C%8C%EC%9D%B4
 [3]: http://www.raspberrypi.org/downloads/