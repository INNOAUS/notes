# CentOS 7 에 Cisco VPN 연결을 위한 VPN 클라이언트 vpnc 설치하기
vpnc 패키지는 기본 리포지터리에 패키지가 없어 EPEL(Extra Packages for Enterprise Linux) 최신 패키지 목록을 설치해야 합니다.

## EPEL 최신 패키지 목록 설치하기
EPEL Site : https://fedoraproject.org/wiki/EPEL
```shell
# yum install https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
Loaded plugins: fastestmirror
epel-release-latest-7.noarch.rpm                                                                                               |  15 kB  00:00:00
Examining /var/tmp/yum-root-I01hVd/epel-release-latest-7.noarch.rpm: epel-release-7-11.noarch
Marking /var/tmp/yum-root-I01hVd/epel-release-latest-7.noarch.rpm to be installed
Resolving Dependencies
--> Running transaction check
---> Package epel-release.noarch 0:7-11 will be installed
--> Finished Dependency Resolution

Dependencies Resolved

======================================================================================================================================================
 Package                            Arch                         Version                    Repository                                           Size
======================================================================================================================================================
Installing:
 epel-release                       noarch                       7-11                       /epel-release-latest-7.noarch                        24 k

Transaction Summary
======================================================================================================================================================
Install  1 Package

Total size: 24 k
Installed size: 24 k
Is this ok [y/d/N]: y
Downloading packages:
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
  Installing : epel-release-7-11.noarch                                                                                                           1/1
  Verifying  : epel-release-7-11.noarch                                                                                                           1/1

Installed:
  epel-release.noarch 0:7-11

Complete!
```
## vpnc 패키지 검색하기
```shell
# yum search vpnc
Loaded plugins: fastestmirror
Loading mirror speeds from cached hostfile
 * base: mirror.kakao.com
 * epel: mirror.premi.st
 * extras: mirror.kakao.com
 * updates: mirror.kakao.com
====================================================================== N/S matched: vpnc =======================================================================
NetworkManager-vpnc.x86_64 : NetworkManager VPN plugin for vpnc
NetworkManager-vpnc-gnome.x86_64 : NetworkManager VPN plugin for vpnc - GNOME files
kde-plasma-networkmanagement-vpnc.x86_64 : Vpnc support for kde-plasma-networkmanagement-extras
vpnc-script.noarch : Routing setup script for vpnc and openconnect
vpnc.x86_64 : IPSec VPN client compatible with Cisco equipment
vpnc-consoleuser.x86_64 : Allows console user to run the VPN client directly

  Name and summary matches only, use "search all" for everything.
```
## vpnc 패키지 설치하기
```
# yum install -y vpnc
...
Resolving Dependencies
--> Running transaction check
---> Package vpnc.x86_64 0:0.5.3-22.svn457.el7 will be installed
--> Processing Dependency: libgnutls.so.28(GNUTLS_1_4)(64bit) for package: vpnc-0.5.3-22.svn457.el7.x86_64
--> Processing Dependency: vpnc-script for package: vpnc-0.5.3-22.svn457.el7.x86_64
--> Processing Dependency: libgnutls.so.28()(64bit) for package: vpnc-0.5.3-22.svn457.el7.x86_64
--> Running transaction check
---> Package gnutls.x86_64 0:3.3.29-8.el7 will be installed
--> Processing Dependency: trousers >= 0.3.11.2 for package: gnutls-3.3.29-8.el7.x86_64
--> Processing Dependency: libnettle.so.4()(64bit) for package: gnutls-3.3.29-8.el7.x86_64
--> Processing Dependency: libhogweed.so.2()(64bit) for package: gnutls-3.3.29-8.el7.x86_64
---> Package vpnc-script.noarch 0:0.5.3-22.svn457.el7 will be installed
--> Running transaction check
---> Package nettle.x86_64 0:2.7.1-8.el7 will be installed
---> Package trousers.x86_64 0:0.3.14-2.el7 will be installed
--> Finished Dependency Resolution

Dependencies Resolved

================================================================================================================================================================
 Package                                Arch                              Version                                         Repository                       Size
================================================================================================================================================================
Installing:
 vpnc                                   x86_64                            0.5.3-22.svn457.el7                             epel                             85 k
Installing for dependencies:
 gnutls                                 x86_64                            3.3.29-8.el7                                    base                            680 k
 nettle                                 x86_64                            2.7.1-8.el7                                     base                            327 k
 trousers                               x86_64                            0.3.14-2.el7                                    base                            289 k
 vpnc-script                            noarch                            0.5.3-22.svn457.el7                             epel                             14 k

Transaction Summary
================================================================================================================================================================
Install  1 Package (+4 Dependent packages)

Total download size: 1.4 M
Installed size: 3.7 M
Downloading packages:
(1/5): nettle-2.7.1-8.el7.x86_64.rpm                                                                                                     | 327 kB  00:00:00     
(2/5): trousers-0.3.14-2.el7.x86_64.rpm                                                                                                  | 289 kB  00:00:00     
(3/5): gnutls-3.3.29-8.el7.x86_64.rpm                                                                                                    | 680 kB  00:00:00     
warning: /var/cache/yum/x86_64/7/epel/packages/vpnc-0.5.3-22.svn457.el7.x86_64.rpm: Header V3 RSA/SHA256 Signature, key ID 352c64e5: NOKEY
Public key for vpnc-0.5.3-22.svn457.el7.x86_64.rpm is not installed
(4/5): vpnc-0.5.3-22.svn457.el7.x86_64.rpm                                                                                               |  85 kB  00:00:00     
(5/5): vpnc-script-0.5.3-22.svn457.el7.noarch.rpm                                                                                        |  14 kB  00:00:00     
----------------------------------------------------------------------------------------------------------------------------------------------------------------
Total                                                                                                                           2.4 MB/s | 1.4 MB  00:00:00     
Retrieving key from file:///etc/pki/rpm-gpg/RPM-GPG-KEY-EPEL-7
Importing GPG key 0x352C64E5:
 Userid     : "Fedora EPEL (7) <epel@fedoraproject.org>"
 Fingerprint: 91e9 7d7c 4a5e 96f1 7f3e 888f 6a2f aea2 352c 64e5
 Package    : epel-release-7-11.noarch (installed)
 From       : /etc/pki/rpm-gpg/RPM-GPG-KEY-EPEL-7
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
  Installing : trousers-0.3.14-2.el7.x86_64                                                                                                                 1/5 
  Installing : nettle-2.7.1-8.el7.x86_64                                                                                                                    2/5 
  Installing : gnutls-3.3.29-8.el7.x86_64                                                                                                                   3/5 
  Installing : vpnc-script-0.5.3-22.svn457.el7.noarch                                                                                                       4/5 
  Installing : vpnc-0.5.3-22.svn457.el7.x86_64                                                                                                              5/5 
  Verifying  : gnutls-3.3.29-8.el7.x86_64                                                                                                                   1/5 
  Verifying  : vpnc-script-0.5.3-22.svn457.el7.noarch                                                                                                       2/5 
  Verifying  : nettle-2.7.1-8.el7.x86_64                                                                                                                    3/5 
  Verifying  : trousers-0.3.14-2.el7.x86_64                                                                                                                 4/5 
  Verifying  : vpnc-0.5.3-22.svn457.el7.x86_64                                                                                                              5/5 

Installed:
  vpnc.x86_64 0:0.5.3-22.svn457.el7                                                                                                                             

Dependency Installed:
  gnutls.x86_64 0:3.3.29-8.el7        nettle.x86_64 0:2.7.1-8.el7        trousers.x86_64 0:0.3.14-2.el7        vpnc-script.noarch 0:0.5.3-22.svn457.el7       

Complete!


```

## 설치 확인
설치 후 버전 확인을 하여 설치여부를 확인합니다.
```shell
# vpnc --version
vpnc version 0.5.3
Copyright (C) 2002-2006 Geoffrey Keating, Maurice Massar, others
vpnc comes with NO WARRANTY, to the extent permitted by law.
You may redistribute copies of vpnc under the terms of the GNU General
Public License.  For more information about these matters, see the files
named COPYING.
Built with certificate support.

Supported DH-Groups: nopfs dh1 dh2 dh5
Supported Hash-Methods: md5 sha1
Supported Encryptions: null des 3des aes128 aes192 aes256
Supported Auth-Methods: psk psk+xauth hybrid(rsa)

```

## VPN 클라이언트 설정하기
기본 설정 파일을 활용하여 특정 VPN서버용 설정파일로 만들기위하여 복사하여 설정합니다.

```shell
# cp /etc/vpnc/default.conf /etc/vpnc/myvpnc.conf
# vi /etc/vpnc/myvpnc.conf
IPSec gateway my.vpn.gateway  # vpn 서버 주소 혹은 hostname
IPSec ID my.ipsec.id          # vpn group id
IPSec secret mysecret         # vpn group password
# your username goes here:
Xauth username userid               # user id
Xauth password passwd               # user password

```

## VPN 클라이언트 구동하기
```shell
# vpnc /etc/vpnc/myvpnc.conf
VPNC started in background (pid: 3581)...
```

## VPN 연결끊기
```shell
# vpnc-disconnect
```
