기본 명령 모드
===========================

전체 모드에서 사용 할 수 있는 명령
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
?
---
* '?' 명령은 입력할 수 있는 명령어 목록이나 사용할 수 있는 매개변수 정보를 보여줍니다.
* 화면에 문자가 표시되지 않습니다.
::

  shieldone@fw-test> (?)
    !              Comments
    admin          Admin mode
    configuration  Backup/Restore Configuration
    diagnosis      Network Diagnosis mode
    logout         Logout of the current ShieldOne CLI Session
    show           Show System relative information
    system         System Configuration mode

  shieldone@fw-test> show(?)
    info     Show ShieldOne Information
    license  Show License

Tab(탭)
--------
* 명령어 입력 중에 Tab(탭) 키를 누르면 명령어를 자동 완성합니다.
* 만약, 여러개의 명령어가 있는 경우 사용할 수 있는 명령어의 목록을 보여 줍니다.
* 화면에 문자가 표시되지 않습니다.
::

  shieldone@fw-test> s(Tab)
  show   system

.. index:: exit, logout
exit / logout
-------------
* exit : 현재 진입 한 명령어 모드를 종료하고 상위 모드로 이동하는 명령어 입니다.
* logout : 콘솔에서 로그아웃하는 명령어입니다.

각각 모드 진입 명령
^^^^^^^^^^^^^^^^^^^

admin
------
* ShieldOne 에 관련 된 명령어 admin 모드로 진입 합니다.
* :doc:`admin_view`


system
--------
* 시스템에 관련 된 명령어 system 모드로 진입 합니다.
* :doc:`system_view`

.. index:: 트러블슈팅
diagnosis
---------
* 트러블 슈팅에 관련 된 명령어 diagnosis 모드로 진입 합니다.
* :doc:`diagnosis_view`


정보 열람 관련 명령
^^^^^^^^^^^^^^^^^^^

.. index:: serial, 장비시리얼, spm버전, shieldone버전

.. _serial:

show info
---------
* 장비의 시리얼, spm버전, shieldone 버전 표시
::

    shieldone@fw-test> show info
    serial      : ffb0f3c3
    spm         : spm version 4
    shieldone   : ShieldOne UTM-265

============= =============================================================
항목          설명
============= =============================================================
serial        10자리 hex(16진수)로 표시 되는 장비의 시리얼은 제조사(플러스아이)와 협업할때 기준이 되는 정보 입니다.
spm           ShieldOne Package Manager 프로그램으로 현재 설치 된 버전을 표시 합니다. 참조 :ref:`package-manager`.
shieldone     라이선스에 명시 된 장비의 Spec. 을 표시 합니다.
============= =============================================================

.. index:: license, 라이선스
show license
------------
* 현재 라이선스 키를 화면에 표시 합니다.
::

    shieldone@fw-test> show license
    U0g8Zy00bl5EcD5KfmVK41B1K000eVnxzSlplfnk0K000041hHRD85NmElMiluM01K0400X1BQJXJlSXZoOGdpfHBh4mth100001FeRUN0WFJUaH14ckpO1U00bXBFUHEleldM43s00145Y2pWUyF4J00QUW14YkxhIS04dHJ3OUhzKitg0081SyFC4DhNUj00TFh0QjJgL4t100lxQXtuVTJuWWQ+PlVZZV800200ZCspTFZGazAqSi00ej00MVYqO1YxRWAyI1U2R2wlS0olVEBSWX5VZTxRPm1MNSFJY24qezA0aEAjUF98VyFOSUM9REBKRDNrdTh8eHklY0BVaGt4RHR2fDFQQUcyQX4qTDJlJHV8R0pzNG4tKWU0cyU7NSsmXjRfamM7O2YoZG98I0FOOy1lP3kpKXspdnt2K1VGWE9MZig/KXFqMUx8JkZxIVhzRSFmdlRrU1NtfnRLIXQ7QjJ7Z2UyTzVlPkxlVn1yQ2tld3NEYHt3ektLQFJFdk9XY0hZI1gpKE5ucEwlSmI/RWZpWDxHdTglSUxWSWUzc3Y8JEdwSTZTI048KlNnY3NKUWdMWVZqZzRfXnc7fF54SjliVUIoX1kpdnteTihPKFFiOS10bUVvdk12YH0j
* 위와 예제와 같이 장비에 설정되어 있는 라이선스 키를 raw dump 결과를 보여 줍니다.

.. index:: configuration, backup, restore, 설정백업, 설정복구, zmodem, 설정업로드, 설정다운로드, upload, download
configuration 관련 명령
^^^^^^^^^^^^^^^^^^^^^^^
* ShieldOne 설정을 백업/복구/다운로드/업로드 하는 명령어 입니다.
* zmodem 을 사용하고, sz/rz 파일들에 대한 설정이 필요 합니다.

.. _configuration-list:

configuration list
------------------
* 백업된 설정 목록 표시
::

    shieldone@fw-test> configuration list
    shieldone7.backup.1473233011.tar.bz2
    shieldone7.backup.1473233012.tar.bz2
    shieldone7.backup.1474878776.tar.bz2
* 위와 예제와 같이 백업한 파일의 목록이 시간 순으로 출력 됩니다.

configuration delete {name}
---------------------------
* 백업 된 설정 파일 중 하나 선택 삭제하는 명령어 입니다.
* :ref:`configuration-list` 목록에 있는 파일 이름을 입력하여 삭제 합니다.

configuration backup
--------------------
* 현재 장비의 설정을 백업하는 명령어 입니다.
* 백업이 완료되면 파일명이 화면에 출력 됩니다.

configuration apply {name}
--------------------------
* 백업 된 설정 파일을 선택해서 그 당시의 설정으로 장비를 복원하는 명령어 입니다.
* 복원 이후에는 장비가 정확히 작동하도록 :ref:`reload` 명령으로 재부팅하는 것을 권장 합니다.

configuration download {name}
-----------------------------
* 백업된 설정 파일을 선택해서 zmodem으로 다운로드

configuration upload
--------------------
* PC에 저장 된 설정 파일을 zmodem으로 업로드
