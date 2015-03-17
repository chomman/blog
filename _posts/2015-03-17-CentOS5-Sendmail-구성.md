---
published: true
layout: post
---

##1. Sendmail 패키지 설치

    {% raw %}
	yum install -y sendmail sendmail-cf
    {% endraw %}

##2. Sendmail 설정

### sendmail.cf 변경

sendmail.cf 파일에서 원격연결 설정을 수정한다. 주석처리 또는 삭제
550 5.1.1 User unknown 에러가 나는 원인이 되기 때문

    {% raw %}
    vi /etc/mail/sendmail.cf
    {% endraw %} 
    {% raw %}
    O DaemonPortOptions=Port=smtp,Addr=127.0.0.1, Name=MTA
    {% endraw %}   
    ↓
    {% raw %}
    \\#O DaemonPortOptions=Port=smtp,Addr=127.0.0.1, Name=MTA
    {% endraw %}

### sendmail.mc 변경

    {% raw %}
    vi /etc/mail/sendmail.mc
    {% endraw %}    
    {% raw %}
    DAEMON_OPTIONS(`Port=smtp,Addr=127.0.0.1, Name=MTA')
    {% endraw %}    
    ↓
    {% raw %}
    dnl DAEMON_OPTIONS(`Port=smtp,Addr=127.0.0.1, Name=MTA')
    {% endraw %}

발송 시 인증을 이용한 메일 발송으로 변경
  
    {% raw %}
    dnl TRUST_AUTH_MECH(`EXTERNAL DIGEST-MD5 CRAM-MD5 LOGIN PLAIN’)dnl
    dnl define(`confAUTH_MECHANISMS’, `EXTERNAL GSSAPI DIGEST-MD5 CRAM-MD5 ...
    {% endraw %}
    ↓
    {% raw %}
    TRUST_AUTH_MECH(`EXTERNAL DIGEST-MD5 CRAM-MD5 LOGIN PLAIN’)dnl
    define(`confAUTH_MECHANISMS’, `EXTERNAL GSSAPI DIGEST-MD5 CRAM-MD5 ...
    {% endraw %}

외부에서 25번 포트 접속 허용
    
    {% raw %}
    DAEMON_OPTIONS(`Port=smtp, Addr=127.0.0.1, Name=MTA’)dnl
    {% endraw %}
    ↓
    {% raw %}
    DAEMON_OPTIONS(`Port=smtp, Name=MTA’)dnl
    {% endraw %}

발송 호스트명 지정

    {% raw %}
    LOCAL_DOMAIN(`localhost.localdomain’)dnl
    {% endraw %}
    ↓
    {% raw %}
    LOCAL_DOMAIN(`실제 발송 도메인’)dnl
    {% endraw %}

Sendmail 버전 숨기기

    {% raw %}
    \#define(`confSMTP_LOGIN_MSG’, `$j Sendmail; $b’)dnl
    {% endraw %}   
    ↓
    {% raw %}
    define(`confSMTP_LOGIN_MSG’ )dnl
    {% endraw %}

설정 컴파일

    {% raw %}
    m4 sendmail.mc > sendmail.cf
    {% endraw %}

##3. Sendmail 서비스 활성화 및 시작

    {% raw %}
    chkconfig sendmail on
    chkconfig saslauthd on
    /etc/init.d/sendmail start
    /etc/init.d/ saslauthd start
    [root@localhost /]# netstat -antp
    Active Internet connections (servers and established)
    Proto Recv-Q Send-Q Local Address Foreign Address State PID/Program name
    tcp 0 0 0.0.0.0:25 0.0.0.0:* LISTEN 19466/sendmail
    {% endraw %}

##4. 접속 테스트

    {% raw %}
    telnet localhost 25
    mail from:발신계정
    rcpt to:수신계정
    data
    send test
    .
    quit
    {% endraw %}