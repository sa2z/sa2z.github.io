플랫폼 : Fast campus 
강의명 : 리눅스 실전정복 올인원 패키지 Online
강사 : 박수현

# 1 용어정리
  - 리눅스(Linux) : 리누스 토발즈(linus Torvalds)에 의해 개발된 운영체제
  - 운영체제 : 시스템하드웨어 관리 및 운영소프트웨어 실행을 위한 추상화 플랫폼 및 공통 시스템 서비스 제공하는 시스템소프트웨어
  - 시스템소프트웨어 : 응용 소프트웨어를 실행하기 위한 플랫폼제공, 하드웨어동작,접근하도록 설계된 컴퓨터 소프트웨어
  - 리눅스사용현황 : 일반PC는 Windows점유율이 크지만 서버,인프라,슈퍼컴퓨터,웹사이트 등은 대부분 리눅스 운영체제 사용
  - 개발,운영을 위해 리눅스는 필수
  - 안드로이드 - 리눅스커널 위 자바 등 가상화 운영체제
  - 정부기관,군,경,은행 등 안정성과 보안고려하여 오래전부터 꾸준히 사용량 증가중
  - 활용분야 : 서버,서비스,클라우드,커널,빅데이터,인공지능,임베디드 개발
  
# 2. 학습순서
  - 개요 : 설치 - 서비스활용(웹) - 배포판익히기 - GUI/CLI 활용 - 서비스 데모
  - 활용 : 명령어심화 - 스크립트 다루기 - 파일시스템 구조 - 멀티유저와 퍼미션 - 시스템명령어
  - 개발/운영 : 시스템모니터링 - 프로세스모니터링 - 네트워크 모니터링 - 장애분석대응 - 방화벽보안- 리눅스활용
  
# 3. 리눅스 기초 이론
  - Minix운영체제 표방, 리누스토발즈에 의해 개발된 운영체제
  - 초기 인텔CPU 구동 운영체제 -> 이후 오픈소스로 개발되어 타 CPU및 워크스테이션까지 이식(Porting)
  - 현재 라우터,자동제어시스템,셋톱박스,게임콘솔,스마트워치 등에도 사용됨
  - Unix: AT&T 사에 의해 1960년도 개발됨, BSC(무료,학교),SYS-V(유료,상용),POSIX 계열이 있음
  - Unix -> Minix -> Linux
  - GNU프로젝트(GNU is Not Unix_리차드스톨만) : 누구자 자유롭게 쓸수 있는 소프트웨어 라이센스 gcc,glibc,gnu-utils(make 등),gdb,emacs 
  - 오픈소스 프로젝트 : 오픈소스모델,개방협협업, 오픈소스라이센스 (아파치 재단)
    * 오픈소스 라이센스 : https://www.dlis.or.kr  / 라이센스 비교표 : https://olis.or.kr/license/compareGuide.do
    * Porting_기존시스템을 다른하드웨어시스템에서 동작하도록 변경하는것
    * 배포판계보 : http://futurist.se/gldt, https://futurist.se/gldt/wp-content/uploads/12.09/gldt1209.svg
  - 슬랙웨어(Slackware)계열 : SuSe 안정성, 패키지관리자rpm,zypper, 노벨(Novell)에 인수
  - 데비안(Debian) 계열 : Ubuntu,Mint,Lindows 패키지관리자 dpkg,apt,
  - 레드헷(Redhat) 계열 : RHEL,Fedora,CentOS,Mandrake 패키지관리자 rpm,yum, 서버운영체제강자, RHEL(유료)/CentOS(무료)
  - 리눅스배포판구성 : Linux 커널 + Desktop UI + Utilities
  - 배포판선택 : 상업/비상업, 기업/개인, 하드웨어벤더인증, 서버/데스크탑/임베디드/특수목적, 특정산업군,보안/안정/이식성, 
  
  - Desktop Environment
    - GNOME(GNU Network Object Model Environment) : 손쉬운사용, GNU계열, / 도구 : GTK+,Unity
    - KDE(K-Desktop Environment) : 다중플랫폼 호환(Linux,FreeBSD, Windows,Solaris,MAC 등) / 도구 : QT,Piasma
    - XFce(XForms Common Environment) : 2D lightweight(오래된 HW도 지원하기 위해 저사양사용가능한)
    - LXDE(Lightweight X11 Desktop Environment : Minimalistic Desktop Environment
  - 운영체제 : 시스템하드웨어 관리,응용소프트웨어 실행 -> 하드웨어 추상화 플랫폼,공통시스템서비스 제공하는 시스템소프트웨어
  - 커널 : 운영체제의 핵심프로그램, 시스템모든것을 통제 https://makelinux.github.io/kernel/map/ 
  
  - 가상환경 : virtualbox(오픈소스), vmware(개인무료), ms hyper-V(win pro이상), 웹터미널 cocalc / https://codepen.io/z-/pen/eJNgWO
  - 가상환경 네트워크 
    - NAT(가상머신 내부 네트워크에서 Host PC 외부네트워크 단방향 연결(Host내부네트워크와 통신불가)
    - 어댑터에 브리지 : 호스트 PC와 동등하게 외부 네트워크와 연결(IP할당 외부로부터 받음)
    - 내부네트워크 : Host 내부 네트워크와만 통신가능
    - 호스트전용 : Host와 내부 네트워크와만 통신가능(외부 네트워크와 단절)
    - 일반드라이버 : 거의 미사용(UDP 터널네트워크 등)
    - NAT 네트워크 : NAT+Host내부네트워크 통신가능
    - 연결되지않음 : 네트워크미사용
  - 원격접속 : putty
    - 피원격서버 : [원격설치] $ apt install openssh-server
                  [원격실행] $ sudo service sshd start
                  [원격확인] $ sudo service sshd status
                  [IP확인] $ ifconfig > NAT 외부에서 들어오지못함
                  [핑확인] $ ping {IP}
                  [라우터테이블] $ route print
                  - 포트포워딩 :호스트 내부네트워크의 포트로 접속
  # 우분투 GUI
    - Desktop, Server 버전
    - GNOME 메뉴바,좌측런처,검색기(고정)
    - chrome 설치파일 .deb 다운 -> 설치 $ dpkg -i google~.deb 
    - 문서 : OpenOffice(Apache), LibreOffice(Document Foundation)
    - software update -> UbuntuOS,기타,업데이트,드라이버 등 설치가능
    - 추가환경설정 도구설치 : $ apt install unity-tweak-tool gnome-tweak-tool tweaks // compiz fusion
    - 
