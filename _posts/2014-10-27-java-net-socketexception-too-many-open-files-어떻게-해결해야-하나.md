---
title: 'java.net.SocketException: Too many open files 어떻게 해결해야 하나'
layout: post
categories:
  - Linux
  - WEB
tags:
  - error
  - 'java.net.SocketException: Too many open files'
---
웹서버를 운영하는 과정에서 아래와 같은 에러 메세지를 만났다.  
사용자가 늘어나면서 동시 접속자가 일시적을 증가하는 경우에 이런 에러가 나오기 시작했다.

java.net.SocketException: Too many open files  
at java.net.PlainSocketImpl.socketAccept(Native Method)  
at java.net.PlainSocketImpl.socketAccept(Compiled Code)  
at java.net.PlainSocketImpl.accept(Compiled Code)  
at java.net.ServerSocket.implAccept(Compiled Code)  
at java.net.ServerSocket.accept(Compiled Code)  
at org.apache.tomcat.service.PoolTcpEndpoint.acceptSocket(Compiled Code)  
at org.apache.tomcat.service.TcpWorkerThread.run(Compiled Code)  
at org.apache.tomcat.util.ThreadPool$ControlRunnable.run(Compiled Code)  
at java.lang.Thread.run(Compiled Code)  
구글링 후 리눅스의 계정 설정값 때문이라는 사실을 알게 되었다.  
특정 계정으로 프로세스가 구동될 경우, O/S 설정값에 영향을 받는다는 사실을 처음 알게 되었다.  
해결방법은 다음과 같다.  
1. open files 최대 개수 확인

먼저 ulimit -a 으로 open files 개수를 확인한다. ulimit -aH는 hard limit, -aS는 sort limit를 확인.  
csh 쉘을 사용하면 limit 명령으로 살펴볼 수 있다.  
$ ulimit -a  
core file size (blocks, -c) 0  
data seg size (kbytes, -d) unlimited  
file size (blocks, -f) unlimited  
pending signals (-i) 1024  
max locked memory (kbytes, -l) 32  
max memory size (kbytes, -m) unlimited  
open files (-n) 1024  
pipe size (512 bytes, -p) 8  
POSIX message queues (bytes, -q) 819200  
stack size (kbytes, -s) 10240  
cpu time (seconds, -t) unlimited  
max user processes (-u) 69632  
virtual memory (kbytes, -v) unlimited  
file locks (-x) unlimited  
2. 프로세스별로 오픈된 파일 개수 확인

열린 파일

lsof 명령으로 확인할 수 있다. 지정한 프로세스가 몇개의 파일을 사용중인지를 확인할 때는 다음처럼 실행  
하면 알 수 있다.

lsof -p PID | wc -l

1234, 1236 PID 2개에 대해 살펴본다면 콤마(,)로 PID를 구분해서 적어주면 된다.  
$ lsof -p 1234,1236 |wc -l  
3. 파일개수 늘리기

리눅스환경을 기준으로 설명한다. truefeel 사용자의 open files개수를 4096(sort limit),  
6144(hard limit) 로 제한한다면 /etc/security/limits.conf에 다음 줄을 추가해주면 로긴시 적용된다.  
truefeel soft nofile 4096  
truefeel hard nofile 6144
