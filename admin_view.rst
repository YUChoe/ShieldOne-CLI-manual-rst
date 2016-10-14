admin 명령 모드
===========================
* shieldone 의 각각 기능(방화벽, IPS, SSLVPN, IPSecVPN, etm 등)에 대한 명령 모드 입니다.
::

    shieldone@fw-test> admin
    Entering ShieldOne Admin mode ...
    shieldone@fw-test/admin>
      !                Comments
      etm              ETM command
      exit             Go back to main menu
      factory-default  Initialize the ShieldOne Configuration as Factory Default
      package-manager  ShieldOne Package Manager related commands
      shieldone        ShieldOne command
      show             Show ShieldOne related commands
      trace            Follow ShieldOne log

.. index:: 공장초기화
factory-default
^^^^^^^^^^^^^^^
* 장비를 공장 초기화 모드로 돌리는 명령입니다.
* 현재 설정 된 모든 값을 초기화 하고 데이터를 삭제 합니다.

.. warning::

    이 명령어는 시스템의 모든 환경 설정 데이터 뿐만 아니라 할당 된 라이선스까지 삭제하여 공장 초기 출하 상태가 됩니다. 이 명령을 실행하면 모든 데이터가 손실되므로 주의하십시오.

.. index:: spm, package manager, ShieldOne패키지
.. _package-manager:

package-manager 관련 명령
^^^^^^^^^^^^^^^^^^^^^^^^^

package-manager package list
----------------------------
::

    shieldone@fw-test/admin> package-manager package list
     firewall                20160523     lastest
     shieldone-hb            unknown      20160523
     package-manager         20160828     lastest
     ips                     20160523     lastest
     domain-filter           20160810     lastest
     vpn                     20160406     lastest
     conf-logrotate          20160704    20160110
* 위의 예시와 같이 현재 설치 된 ShieldOne패키지의 목록과 버전(날짜)의 목록을 출력합니다.
* 최신 버전인 경우 lastest 로 표시 됩니다.

.. index:: UTF-8, 인코딩, encoding, codec
package-manager package show {name}
----------------------------
* 선택한 이름의 패키지에 대한 정보를 출력합니다.
::

    shieldone@fw-test/admin> package-manager package show firewall

    Package name: firewall

    * 20151028:
            Released: firewall 정책 설정
    * 20160406:
            Fixed:
    * 20160523:
            Fixed: 방화벽 정책 설정에 SSL P2P 선택 가능

    Dependency packages:
            None

    Lastest: (20160523)
* firewall 을 입력 한 경우 위의 예시와 같은 화면이 출력 됩니다.
* 한글로 된 정보를 보려면 인코딩 설정이 UTF-8 로 되어 있어야 합니다.

.. index:: 라이선스, 업데이트, update, license
package-manager package update
----------------------------
* 패키지 정보를 최신으로 업데이트 합니다.
.. warning::
    * 인터넷에 연결이 되어 있어야 합니다.
    * 라이선스가 유효한 경우에만 작동 합니다.

.. index:: 업그레이드, upgrade
package-manager package upgrade {name}
----------------------------
* 선택 한 이름의 패키지를 업그레이드 합니다.

.. index:: install, 인스톨
package-manager package install {name}
----------------------------
* 선택 한 이름의 패키지를 신규 인스톨 합니다.

.. index:: 라이선스 입력
package-manager license set {license}
----------------------------
* 제조사(플러스아이)에서 전달받은 라이선스 키의 내용을 입력하여 장비에 적용합니다.
* 입력 후 자동으로 유효성을 검증하여 결과를 화면에 출력 합니다.

.. index:: 라이선스 검증
package-manager license verify
----------------------------
* 현재 입력 된 라이선스의 유효성을 검증합니다.
::

    shieldone@fw-test/admin> package-manager license verify
    ok
* 정상인 경우 위의 예시와 같이 ok 가 화면에 출력 됩니다.

shieldone 관련 명령
^^^^^^^^^^^^^^^^^^^
* 각 모듈의 상태를 확인 할 수 있고, start/stop 명령으로 제어 할 수 있습니다.

shieldone status
----------------
::

    shieldone@fw-test/admin> shieldone status
    ETM Engine              : Stop
    Inspector Engine        : Stop
    Spool Engine            : Stop
    IPS Log Engine          : Stop
    SSL VPN Engine          : Running
    IPSec VPN Engine        : Running

shieldone start
----------------
* 중단 된 shieldone 모듈을 시작 합니다.

shieldone stop
----------------
* shieldone 모듈의 작동을 중단 합니다.


.. index:: etm, tsm
etm 관련 명령
^^^^^^^^^^^^^
* ETM(Enterprise Traffic Monitoring System) 의 상태를 확인 할 수 있고, start/stop 명령으로 제어할 수 있습니다.

etm status
----------
* etm 라이선스가 등록되지 않았거나 기한이 지난 경우 다음과 같은 내용이 출력 됩니다.
::

    shieldone@fw-test/admin> etm status
    < TMS Version 1.0.3 >
    License Key File Verifying Fail
* 라이선스가 유효한 경우 아래와 같은 내용이 출력 됩니다.
::

    shieldone@fw-test/admin> etm status
    < TMS Version 1.0.3 >
    License Key File Verifying Success
    License Correct
    License is Available
    Expire Date : 2017-01-31
    License type : All of both
    Running Mode : Disk Mode(All)
    [Monitor Modules]
      LAN1 : Stoped!
      LAN2 : Stoped!
      Internal_DMZ : Stoped!
    [Service Modules]
      tms_distributor : Stoped!
      tms_statistics : Stoped!
      tms_csmodule : Stoped!
      tms_updater : Stoped!
* 위의 내용은 2017년 1월 31일까지 유효하며, 모니터 설정은 LAN1, LAN2, Internal_DMZ로 되어 있지만 현재 중단(stoped) 상태이고, 각 데몬의 상태는 중단(stoped) 상태임을 보여 줍니다.

etm start
----------
* 중단 상태인 ETM을 시작 합니다.

etm stop
----------
* 작동 중인 ETM을 중단 시킵니다.


정보 열람 관련 명령
^^^^^^^^^^^^^^^^^^^

.. index:: uptime, date, serial, 장비시리얼, 맥주소, mac
show sysinfo
------------
* uptime, date, 장비시리얼, 관리맥주소 를 출력
::

    shieldone@fw-test/admin> show sysinfo
    uptime      : 11:43:59 up 239 days,  1:21,  0 users,  load average: 0.00, 0.03, 0.05
    system clock: Wed Sep 7 11:43:59 KST 2016
    serial      : ffb0f3c3
    mac address : 00:90:00:00:00:9a

============= =============================================================
항목          설명
============= =============================================================
uptime        현재 시간, 장비가 재부팅 없이 작동 한 시간, 부하량입니다.
system clock  장비에 설정 된 현재 날짜와 시간입니다.
serial        :ref:`serial` 참조
============= =============================================================

.. index:: 방화벽정책
show firewall-policy
------------------
* 현재 장비에 설정 된 방화벽 정책을 화면에 출력 합니다.
* --filter 옵션을 이용하여 필요한 내용만 선택하여 화면에 출력할 수 있습니다.

.. index:: NAT
show nat-policy
------------------
* 현재 장비에 설정 된 NAT 정책을 화면에 출력 합니다.
* --filter 옵션을 이용하여 필요한 내용만 선택하여 화면에 출력할 수 있습니다.

.. index:: 객체
show object list
------------------
* 현재 장비에 설정 된 IP 객체의 목록을 출력 합니다.
::

    shieldone@fw-test/admin> show object list
    사무실네트워크
    Test
    공장
    전화망
    인터넷차단
    Root_전산실
    병원내부사설네트워크
* --filter 옵션을 이용하여 필요한 내용만 선택하여 화면에 출력할 수 있습니다.

.. index:: routing, 소스라우팅, 정책라우팅
show policy-route
------------------
* 정책라우팅, 소스라우팅 관련 정보를 화면에 출력합니다.

.. index:: vrrp, HA
show vrrp
------------------

.. index:: ospf, routing
show ospf
------------------

.. index:: rip, routing
show rip
------------------

.. _shieldone-log:

ShieldOne 로그 열람 관련 명령
^^^^^^^^^^^^^^^^^^^

show log {logfile}
------------------
* shieldone 에서 생성되는 로그를 선택하여 전체를 열람하는 명령문입니다.

============= =============================================================
로그종류      설명
============= =============================================================
shieldone     ShieldOne 내부 기능 또는 GUI 를 통해 작동되는 기능에 대한 로그
access        GUI 접속에 대한 로그
firewall      방화벽 정책에 의해 발생 된 로그
sslvpn        SSL VPN(P2P, Remote)에 의해 발생 된 로그
ipsecvpn      IPSecVPN에 의해 발생 된 로그
============= =============================================================

* --filter 옵션을 이용하여 필요한 내용만 선택하여 화면에 출력할 수 있습니다.

.. warning::
    로그 파일 전체를 보여주므로 파일 크기가 큰 경우 주의해서 사용해야 합니다.
    실시간으로 입력되는 로그를 볼 수 있는 :ref:`admin-trace` 와 구분하여 사용되어야 합니다.

.. _admin-trace:

ShieldOne 로그 추적 관련 명령
^^^^^^^^^^^^^^^^^^^

trace {filename}
----------------
* shieldone 로그를 실시간 follow 하는 명령어입니다.
* --filter 옵션을 이용하여 필요한 내용만 선택하여 화면에 출력할 수 있습니다.
* 로그 종류는 :ref:`shieldone-log` 참조
