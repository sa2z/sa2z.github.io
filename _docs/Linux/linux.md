# Linux 목차
  - 역사,개요,정의
  - 명령어, 문법,인자,용도
  - 동장방식, 세부기술
  - 스크립팅, 실전예시
  - ref : 패스트캠퍼스 올인원패키지-리눅스실전정복 박현수, https://www.fastcampus.co.kr/courses/202555/clips/
  
# Linux란?
  - Linus Torvalds 에 의해 개발된 운영체제
  - 운영체제 : 하드웨어 관리, 응용소프트웨어 실행을 위한 하드웨어 추상화 플랫폼과 공통 시스템 서비스제공하는 시스템 소프트웨어
  - 시스템 소프트웨어 : 응용 소프트웨어 실행을 위한 플랫폼을 제공하고, HW동작,접근할 수 있도록 설계된 컴퓨터 소프트웨어
  - 슈퍼컴퓨터,웹사이트,서버,클라우드인프라의 대부분이 리눅스 운영체제사용
  - Unix : AT&T 개발 운영체제, 기업용 운영체제 BSD_무료/시스템V_유료 계열
  - GNU(GNU is Not Unix) 프로젝트 : "누구나 자유롭게 실행,복사,수정,배포 할 수 있고 누구도 그런 권리를 제한하면 안된다."
    - gcc, glibc, gnu-utils(make 등), gdb, emacs
  - 오픈소스 프로젝트 : 상업적용도도 자유롭게 사용 - apach 재단(의무,책임 확인)
  - 배포판 : http://futurist.se/gldt/
    - slackware(SuSE 사용리눅스배포판 안정성확보)- 노벨(Novell에인수)
    - debian(ubuntu) - 상업적시장에서 경쟁가능한 비상업적 배포판
    - Redhat(RHEL,Fedora,CentOS) - 기술지원가능 유료(RHEL) 무료(CentOS) , IBM인수
    - 구성 : 리눅스커널 + GUI + 패키지관리자 + 응용소프트웨어
  - GUI
    - GNOME(GNU Network Object Model Environment) : GNU후원, 쉬운사용 - 개발도구 GTK+,Unity (https://www.gnome.org/gnome-3/)
    - KDE(K-Desktop Environment) : 기능과 확장성 - 개발도구 Qt,Plasma (https://kde.org/plasma-desktop)
    - XFce(XForms Common Environment) : 2D lightweight(오래된 HW지원을 위해 저사양에서도 사용가능하도록)
    - LXDE(Lightweight X11 Desktop Environment) : minimalistic Desktop Environment
  - 운영체제 : 시스템HW관리, 운영소프트웨어 실행을 위한 시스템 소프트웨어(입출력,메모리관리,프로세스관리)
  - 커널(Kernel) : 운영체제의 핵심프로그램, 시스템 모든것 통제 - 마이크로커널,단일형커널 (https//kernel.org/,git.kernel.org)
  - 배포버전 :Major.Minor.Patch - Trusty(14.xx)-Xenial(16.xx)-Bionix(18.xx)-Eoan(19.xx) 홀수-최신기능(플래그쉽) 짝수-안정성, LTS(5년간 보안지원)  
  - 미러사이트(중계다운) : https://kr.archive.ubuntu.com/ubuntu , https://mirror.kakao.com/ubuntu-release/xenial
  - 가상환경(Virtual


# 계정작업
  ```
  # 계정생성
    $ sudo adduser {user_name}
  
  # 그룹에 추가
    $ sudo usermod -aG {group} {user_name}
  
  # 경로권한 변경 (xxx user/group/other , x = rwx(2) )
    $ sudo chmod -R xxx {path}
  
  # 경로소유권 변경
    $ sudo chown -R {group}:{user} {path}
    
  # 계정설정확인(비밀번호 변경시기,비밀번호 만기일 등)
    $ sudo chage -l {user_name}
    
  # 비밀번호 변경
    $ su - {user} // user 터미널진입
    $ passwd
    
  - ref : http://www.incodom.kr/Linux/%EA%B8%B0%EB%B3%B8%EB%AA%85%EB%A0%B9%EC%96%B4/chmod
  ```
  
# Samba
  
  - 설치
    ```
    $ apt-get install samba
    $ apt-get install 
    ```
  
  - 설정
  ```
  # Samba 용 계정생성
    $ sudo adduser {user_name}
  # Samba 사용 등록
    $ sudo smbpasswd -a {user_name}
 
  # 경로등록
    $ sudo nano /etc/samba/smb.conf
      >>> 맨아래 경로정보 작성
        [path_name]
        comment = poc image directory
        path = /home/test/data # server dir
        valid users = {samba_user}
        writeable = yes
        read only = no
        guest ok = yes
        create mode = 0777
        directory mask = 0777
        browsable = yes
        public = no
  ```
  - 재시작
  ```
  $ sudo service smbd restart
  ```
  
  
  
