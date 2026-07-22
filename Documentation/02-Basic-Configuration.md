Current configuration : 3209 bytes
!
! Last configuration change at 23:22:57 UTC Wed Jul 22 2026
!
version 15.6
service timestamps debug datetime msec
service timestamps log datetime msec
service password-encryption
!
hostname EDGE-R1
!
boot-start-marker
boot-end-marker
!
!
enable secret 5 $1$zMGg$7WfUzGsWvN8u.IljxPSen/
!
no aaa new-model
ethernet lmi ce
!
!
!
mmi polling-interval 60
no mmi auto-configure
no mmi pvc
mmi snmp-timeout 180
!
!
!
!
!
!
!
!
!
!
!
no ip domain lookup
ip domain name enterprise.lab
ip cef
no ipv6 cef
!
multilink bundle-name authenticated
!
!
!
!
username admin privilege 15 secret 5 $1$9HSp$LukdS7bKk4iQpXNpvF0r2/
!
redundancy
!
!
!
!
!
!
!
!
!
!
!
!
!
!
!
interface GigabitEthernet0/0
 no ip address
 shutdown
 duplex auto
 speed auto
 media-type rj45
!
interface GigabitEthernet0/1
 no ip address
 shutdown
 duplex auto
 speed auto
 media-type rj45
!
interface GigabitEthernet0/2
 no ip address
 shutdown
 duplex auto
 speed auto
 media-type rj45
!
interface GigabitEthernet0/3
 no ip address
 shutdown
 duplex auto
 speed auto
 media-type rj45
!
ip forward-protocol nd
!
!
no ip http server
no ip http secure-server
ip ssh version 2
!
!
!
!
control-plane
!
banner exec ^C
**************************************************************************
* IOSv is strictly limited to use for evaluation, demonstration and IOS  *
* education. IOSv is provided as-is and is not supported by Cisco's      *
* Technical Advisory Center. Any use or disclosure, in whole or in part, *
* of the IOSv Software or Documentation to any third party for any       *
* purposes is expressly prohibited except as otherwise authorized by     *
* Cisco in writing.                                                      *
**************************************************************************^C
banner incoming ^C
**************************************************************************
* IOSv is strictly limited to use for evaluation, demonstration and IOS  *
* education. IOSv is provided as-is and is not supported by Cisco's      *
* Technical Advisory Center. Any use or disclosure, in whole or in part, *
* of the IOSv Software or Documentation to any third party for any       *
* purposes is expressly prohibited except as otherwise authorized by     *
* Cisco in writing.                                                      *
**************************************************************************^C
banner login ^C
**************************************************************************
* IOSv is strictly limited to use for evaluation, demonstration and IOS  *
* education. IOSv is provided as-is and is not supported by Cisco's      *
* Technical Advisory Center. Any use or disclosure, in whole or in part, *
* of the IOSv Software or Documentation to any third party for any       *
* purposes is expressly prohibited except as otherwise authorized by     *
* Cisco in writing.                                                      *
**************************************************************************^C
banner motd ^C
Authorized Access Only!
^C
!
line con 0
 password 7 1125180737405B5E52
 logging synchronous
 login
line aux 0
line vty 0 4
 login local
 transport input ssh
!
no scheduler allocate
!
end
