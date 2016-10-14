ShieldOne 접속하기
===========================

.. index:: 시리얼콘솔, USB2COM, RJ45, COM, Putty
시리얼 콘솔 연결
^^^^^^^^^^^^^^^^
.. sidebar:: 참고

    콘솔 포트 규격 RJ45 규격을 따릅니다. 한글 입출력이 필요할 때 언어 인코딩은 UTF-8을 사용합니다.
네트워크를 사용하지 않고 시리얼통신을 통해 CLI를 사용합니다. 연결할 컴퓨터에 COM5, COM6 등의 장치와 Putty 같은 터미널 클라이언트 그리고 파일전송을 위해 rz, sz 프로그램이 필요합니다.

1. ShieldOne 장비와 같이 제공되는 시리얼 케이블을 사용하여 콘솔로 사용할 컴퓨터와 장비를 연결합니다.
2. 터미널 클라이언트를 실행하고, 연결에 필요한 값을 입력합니다. (115200N81)
3. ShieldOne 로그인 프롬프트가 나오면 로그인합니다.

.. index:: Putty, SSH, 접속포트
SSH 연결
^^^^^^^^
.. sidebar:: 접근제어 설정

    관리(management) 아이피에 대해 ACCEPT 설정이 되어 있어야 합니다.
Putty 등의 터미널 클라이언트를 통해 장비의 IP 주소에 접속하여 로그인 합니다. (기본 접속 포트 TCP 22)

* 로그인 하면 다음과 같은 화면을 볼 수 있습니다.

::

    _________.__    .__       .__       .___________
   /   _____/|  |__ |__| ____ |  |    __| _/\_____  \   ____   ____
   \_____  \ |  |  \|  |/ __ \|  |   / __ |  /   |   \ /    \_/ __ \
   /        \|   Y  \  \  ___/|  |__/ /_/ | /    |    \   |  \  ___/
  /_______  /|___|  /__|\___  >____/\____ | \_______  /___|  /\___  >
          \/      \/        \/           \/         \/     \/     \/

  !          Comments
  admin      Admin mode
  diagnosis  Network Diagnosis mode
  logout     Logout of the current ShieldOne CLI Session
  show       Show System relative information
  system     System Configuration mode

  * Please set charaterset of your terminal UTF-8 for CJK charators

  Welcome [shieldone] it is [Wed Sep 7 11:51:26 KST 2016]
  shieldone@fw-test>
