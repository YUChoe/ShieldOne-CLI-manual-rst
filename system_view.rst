system 명령 모드
===========================
* OS 수준(ifconfig. route, ip, dhcp?)의 명령어들의 모음

::

    shieldone@fw-test> system
    Entering System Configuration mode ...
    shieldone@fw-test/system>
      !       Comments
      exit    Go back to main menu
      ip      Show/Manipulate routing, devices, policy routing and tunnels
      reload  Reboot System
      show    Show OS related commands
      trace   Follow System log



.. index:: 리부팅, reboot

.. _reload:

reload
^^^^^^
* 장비를 reboot 시키는 명령어

.. warning::
    재부팅 되어 모든 모듈/서비스가 정상작동하는데 1분~3분이 소요됩니다. 네트워크를 사용 중인 경우에 대해 주의를 요합니다.

IP 관련 명령
^^^^^^^^^^^^^^^^^

ip addr
---------------------
* 이더넷 장치에 할당 된 모든 아이피 정보를 화면에 출력합니다.

::

    shieldone@fw-test/system> ip addr
    1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default
        link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
        inet 127.0.0.1/8 scope host lo
           valid_lft forever preferred_lft forever
        inet6 ::1/128 scope host
           valid_lft forever preferred_lft forever
    2: eth0: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc htb state DOWN group default qlen 1000
        link/ether 00:90:00:00:00:9a brd ff:ff:ff:ff:ff:ff
        inet 192.168.37.10/24 brd 192.168.37.255 scope global eth0
           valid_lft forever preferred_lft forever
        inet 192.168.231.10/24 brd 192.168.231.255 scope global eth0:0
           valid_lft forever preferred_lft forever
        inet6 fe80::290:fbff:fe0c:c69a/64 scope link
           valid_lft forever preferred_lft forever
    3: eth1: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc htb state UP group default qlen 1000
        link/ether 00:90:00:00:00:9b brd ff:ff:ff:ff:ff:ff
        inet 231.16.0.2/24 scope global eth1
           valid_lft forever preferred_lft forever
    4: gre0@NONE: <NOARP> mtu 1476 qdisc noop state DOWN group default
        link/gre 0.0.0.0 brd 0.0.0.0
    5: gretap0@NONE: <BROADCAST,MULTICAST> mtu 1462 qdisc noop state DOWN group default qlen 1000
        link/ether 00:00:00:00:00:00 brd ff:ff:ff:ff:ff:ff
    6: tunl0@NONE: <NOARP> mtu 1480 qdisc noop state DOWN group default
        link/ipip 0.0.0.0 brd 0.0.0.0
    55: bond0: <BROADCAST,MULTICAST,MASTER,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default
        link/ether 00:90:00:00:00:9c brd ff:ff:ff:ff:ff:ff
        inet6 fe80::290:fbff:fe0c:c69c/64 scope link
           valid_lft forever preferred_lft forever
    56: tun0: <POINTOPOINT,MULTICAST,NOARP,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UNKNOWN group default qlen 100
        link/none
        inet 10.8.0.1 peer 10.8.0.2/32 scope global tun0
           valid_lft forever preferred_lft forever
    57: ipsec0: <NOARP,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UNKNOWN group default qlen 10
        link/ether 00:90:00:00:00:9b brd ff:ff:ff:ff:ff:ff
        inet 231.16.0.2/32 scope global ipsec0
           valid_lft forever preferred_lft forever
        inet6 fe80::290:fbff:fe0c:c69b/64 scope link
           valid_lft forever preferred_lft forever
    59: ipsec1: <NOARP> mtu 0 qdisc noop state DOWN group default qlen 10
        link/void

* 장비의 Spec.과 설정에 따라 위의 내용을 다를 수 있습니다.

ip route show
---------------------
* routing 정보를 확인 합니다.
* 각 WAN 장치별로 할당 된 라우팅 정보도 같이 확인 할 수 있습니다.

.. index:: routing cache

ip route flush all
---------------------
* 장비에 설정되어 있는 routing cache 를 모두 삭제 합니다.

ip route flush cache {IP/PRE}
------------------------------
* 장비에 설정되어 있는 routing cache 중 선택한 네트워크에 대한 것을 삭제 합니다.

.. index:: gre

ip gre
---------------------
* GRE 설정 정보를 화면에 출력합니다.


.. index:: interface, ifconfig, ethtool, link, 링크

인터페이스 정보 열람 관련 명령
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. index:: ifconfig, ipconfig

show interface {name}
---------------------

.. index:: ethtool, 링크, link, auto-neg

show interface link {name}
--------------------------

.. index:: arp, service, LISTEN, cache

정보 열람 관련 명령
^^^^^^^^^^^^^^^^^^^

show arp
---------------------
* 시스템의 ARP 캐시 테이블을 화면에 출력 합니다.

::

    shieldone@fw-test/system> show arp
    Address                  HWtype  HWaddress           Flags Mask            Iface
    192.168.20.102           ether   e6:00:00:00:00:5c   C                     eth1
    192.168.20.253                   (incomplete)                              eth1
    192.168.20.251           ether   08:00:00:00:00:7a   C                     eth1
    192.168.210.11                   (incomplete)                              eth0
    192.168.37.2             ether   00:00:00:00:00:27   C                     eth0
    192.168.10.200                   (incomplete)                              eth0
    192.168.20.91            ether   06:00:00:00:00:54   C                     eth1
    192.168.20.202           ether   00:00:00:00:00:30   C                     eth1
    10.112.82.25             ether   e6:00:00:00:00:5c   C                     eth1

* --filter 옵션을 이용하여 필요한 내용만 선택하여 화면에 출력할 수 있습니다.

show route
---------------------
* 시스템의 Kernel IP routing table 을 화면에 출력 합니다.

::

    shieldone@fw-test/system> show route
    Kernel IP routing table
    Destination     Gateway         Genmask         Flags Metric Ref    Use Iface
    0.0.0.0         219.16.0.1      0.0.0.0         UG    0      0        0 eth1
    10.8.0.0        10.9.8.2        255.255.255.0   UG    0      0        0 tun0
    10.10.30.0      0.0.0.0         255.255.255.0   U     0      0        0 eth3
    10.20.0.6       0.0.0.0         255.255.255.255 UH    0      0        0 tun2
    172.31.0.0      0.0.0.0         255.255.255.0   U     0      0        0 eth2
    192.168.0.0     0.0.0.0         255.255.255.0   U     0      0        0 eth1
    255.255.255.255 0.0.0.0         255.255.255.255 UH    0      0        0 eth2
    255.255.255.255 0.0.0.0         255.255.255.255 UH    0      0        0 eth0

show route cache
---------------------

show listening-service
-----------------------

show sysload
---------------------
* 현재 CPU/메모리/스토리지 사용량 출력

::

    shieldone@fw-test/system> show sysload
    CPU: 1.6 / MEM: 90.2694 / STORAGE: 64%

show ipsec route
---------------------
show ipsec status
---------------------

System 로그 열람 관련 명령
^^^^^^^^^^^^^^^^^^^^^^^^^^

show log {filename}
---------------------
* system 로그 열람



System 로그 추적 관련 명령
^^^^^^^^^^^^^^^^^^^^^^^^^^

trace {filename}
----------------
* system 로그를 실시간 follow
