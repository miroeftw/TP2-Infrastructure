## Configuration de ISP1
```console
enable
conf t
hostname ISP1
aaa new-model
aaa authentication login default local
aaa authentication enable default enable
username nrenlab secret nsrc-PW
enable secret nsrc-EN
service password-encryption
line vty 0 4
transport preferred none
line console 0
transport preferred none
no logging console
logging buffered 8192 debugging
no ip domain-lookup
ipv6 unicast-routing
ipv6 cef
no ip source-route
no ipv6 source-route
!
interface Loopback0
ip address 100.121.0.1 255.255.255.255
ipv6 address 2001:18::1/128
!
interface FastEthernet0/0
description Workshop Backbone
ip address 10.10.0.235 255.255.255.0
no ip directed-broadcast
no ip redirects
no ip proxy-arp
no shutdown
!
interface GigabitEthernet1/0
description Link to IXP
ip address 100.127.1.1 255.255.255.0
no ip directed-broadcast
no ip redirects
no ip proxy-arp
ipv6 address 2001:DB8:FFFF:1::1/64
ipv6 nd prefix default no-advertise
ipv6 nd ra suppress all
no shutdown
!
! Link to Group 1
interface GigabitEthernet3/0
description P2P Link to B12
ip address 100.121.1.1 255.255.255.252
no ip directed-broadcast
no ip redirects
no ip proxy-arp
ipv6 address 2001:18:0:10::/127
ipv6 nd prefix default no-advertise
ipv6 nd ra suppress all
no shutdown
!
! Link to Group 2
interface GigabitEthernet4/0
description P2P Link to B22
ip address 100.121.1.5 255.255.255.252
no ip directed-broadcast
no ip redirects
no ip proxy-arp
ipv6 address 2001:18:0:11::/127
ipv6 nd prefix default no-advertise
ipv6 nd ra suppress all
no shutdown
!
! Link to Group 3
interface GigabitEthernet5/0
description P2P Link to B32
ip address 100.121.1.9 255.255.255.252
no ip directed-broadcast
no ip redirects
no ip proxy-arp
ipv6 address 2001:18:0:12::/127
ipv6 nd prefix default no-advertise
ipv6 nd ra suppress all
no shutdown
!
! Routes to Group 1
ip route 100.68.1.0 255.255.255.0 100.121.1.2
ipv6 route 2001:db8:1::/48 2001:18:0:10::1
!
! Routes to Group 2
ip route 100.68.2.0 255.255.255.0 100.121.1.6
ipv6 route 2001:db8:2::/48 2001:18:0:11::1
!
! Routes to Group 3
ip route 100.68.3.0 255.255.255.0 100.121.1.10
ipv6 route 2001:db8:3::/48 2001:18:0:12::1
!
! Routes to Group 4
ip route 100.68.4.0 255.255.255.0 100.127.1.2
ipv6 route 2001:db8:4::/48 2001:DB8:FFFF:1::2
!
! Routes to Group 5
ip route 100.68.5.0 255.255.255.0 100.127.1.2
ipv6 route 2001:db8:5::/48 2001:DB8:FFFF:1::2
!
! Routes to Group 6
ip route 100.68.6.0 255.255.255.0 100.127.1.2
ipv6 route 2001:db8:6::/48 2001:DB8:FFFF:1::2
!
! Routes to ISP2 address space
ip route 100.122.0.0 255.255.0.0 100.127.1.2
ipv6 route 2001:19::/32 2001:DB8:FFFF:1::2
!
! Pull-up routes for address blocks of ISP1
ip route 100.121.0.0 255.255.0.0 null0
ipv6 route 2001:18::/32 null0
!
```