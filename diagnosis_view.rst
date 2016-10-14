diagnosis 명령 모드
===========================
* 네트워크, 시스템 트러블슈팅에 필요한 명령어들의 모음입니다.
::

    shieldone@fw-test>diagnosis
    Entering Network Diagnosis mode ...
    shieldone@fw-test/diagnosis>
     !           Comments
     exit        Go back to main menu
     iptraf      Realtime IP Network Monitoring Software
     packetdump  Dump Traffic on a network
     ping        Send Ping messages to network hosts
     show        Show Diagnostic information
     sping       Send Source Ping messages to network hosts
     ssh         SSH to the destination host
     telnet      Telnet to the destination host (port)
     top         Dynamic real-time view of a running system
     traceroute  Traceroute to the destination host
     vmstat      Report virtual memory statistics


네트워크 조사용 명령어
^^^^^^^^^^^^^^^^^^^^^^
.. index:: ping, icmp, 핑
ping {parameter}
----------------
* 목적지로 핑(icmp-request 패킷)을 보내서 응답이 돌아오는 시간과 ttl을 측정합니다.
* 일반적인 Windows/Linux/Unix에서 사용하는 ping 명령어와 동일합니다.
* "(겹따옴표=double quote) 기호를 이용해서 다양한 파라매터를 사용 할 수 있습니다.
::

    shieldone@fw-test/diagnosis> ping "-i 0.2 192.168.80.1"
    PING 192.168.80.1 (192.168.80.1) 56(84) bytes of data.
    64 bytes from 192.168.80.1: icmp_seq=1 ttl=64 time=1.48 ms
    64 bytes from 192.168.80.1: icmp_seq=2 ttl=64 time=1.32 ms
    64 bytes from 192.168.80.1: icmp_seq=3 ttl=64 time=0.578 ms
    64 bytes from 192.168.80.1: icmp_seq=4 ttl=64 time=0.605 ms
    64 bytes from 192.168.80.1: icmp_seq=5 ttl=64 time=0.611 ms
    64 bytes from 192.168.80.1: icmp_seq=6 ttl=64 time=0.623 ms
    ^C
    --- 192.168.80.1 ping statistics ---
    6 packets transmitted, 6 received, 0% packet loss, time 1008ms
    rtt min/avg/max/mdev = 0.578/0.870/1.484/0.380 ms

.. index:: source ping, 소스핑
sping {src} {dst}
-----------------
* 장비의 매니지먼트 아이피가 아닌 다른 아이피를 사용해서 ping 을 하는 명령어 입니다.

.. index:: traceroute
traceroute {parameter}
----------------------
* 네트워크 상의 다른 시스템에 패킷을 보낼 때 거치는 시스템의 IP 주소, 걸린 시간, hop수를 보여줍니다.
* 일반적인 Linux/Unix에서 사용하는 traceroute 명령어와 동일합니다.
* "(겹따옴표=double quote) 기호를 이용해서 다양한 파라매터를 사용 할 수 있습니다.

.. index:: 패킷덤프, tcpdump, wireshark, pcap
packatdump {parameter}
----------------------
* 네트워크 패킷을 캡쳐하여 분석하는 명령어 입니다.
* 일반적인 Linux/Unix에서 사용하는 tcpdump 명령어와 동일합니다.
* "(겹따옴표=double quote) 기호를 이용해서 다양한 파라매터를 사용 할 수 있습니다.

iptraf
------
* iptraf - An IP Network Statistics Utility
* iptraf 프로그램을 실행 하여 네트워크 패킷을 실시간으로 분석하는 명령어 입니다.

.. warning::
    기본으로는 설치되지 않으며, 운영자가 필요 할 때 별도로 설치 해야 합니다. :ref:`package-manager` 참조

.. index:: telnet, ssh
원격 접속용 명령어
^^^^^^^^^^^^^^^^^^

telnet {parameter}
------------------
* telnet 프로토콜을 이용해 원격 호스트에 연결합니다.
* 일반적인 Windows/Linux/Unix에서 사용하는 telnet 명령어와 동일합니다.
* "(겹따옴표=double quote) 기호를 이용해서 다양한 파라매터를 사용 할 수 있습니다.
.. warning::
     telnet은 사용자의 패스워드가 노출될 수 있으므로 안전하지 않습니다. 연결할 대상 호스트와 통신 구간이 신뢰할 수 있는 경우에만 사용하십시오.


ssh {parameter}
---------------
* SSH 프로토콜을 이용해 원격 호스트에 연결합니다.
* 일반적인 Windows/Linux/Unix에서 사용하는 telnet 명령어와 동일합니다.
* "(겹따옴표=double quote) 기호를 이용해서 다양한 파라매터를 사용 할 수 있습니다.

장비 상태 확인 명령어
^^^^^^^^^^^^^^^^^^^^^^^

.. index:: bridge, Trunking ports, VLAN
show brctl
----------
* ShieldOne 장비에 구성 된 브리지 인터페이스 정보를 보여줍니다.
::

    shieldone@fw-test/diagnosis> show brctl
    bridge name     bridge id               STP enabled     interfaces
    br0             8000.0024546212cb       yes             eth1
                                                            eth2
.. index:: process, ps
show process
-------------
* 실행 중인 데몬과 프로세스들의 상태를 확인하는 명령어 입니다.
* 일반적인 Linux/Unix에서 사용하는 ps 명령어와 동일합니다.

.. index:: 부하, load
vmstat
------
* 장비의 CPU, 메모리 등의 사용량을 5초 간격으로 통계를 내어 보여 줍니다.
* 일반적인 Linux/Unix에서 사용하는 vmstat 명령어와 동일합니다.
* 가장 첫 줄은 계산을 시작하기 위한 baseline 이므로 무시합니다.
::

    shieldone@fw-test/diagnosis> vmstat
    procs -----------memory---------- ---swap-- -----io---- -system-- ------cpu-----
     r  b   swpd   free   buff  cache   si   so    bi    bo   in   cs us sy id wa st
     0  0      0 102860  21696 239184    0    0     0     0    0    0  1  1 98  0  0
     0  0      0 102604  21696 239216    0    0     0     0  255   44  0  1 99  0  0


.. index:: process, cpu
top
-----
* 장비에서 실행중인 프로세스 정보를 실시간으로 보여주는 명령어 입니다.
* 일반적인 Linux/Unix에서 사용하는 top 명령어와 동일합니다.
