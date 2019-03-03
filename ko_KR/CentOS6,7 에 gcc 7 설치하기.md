# CentOS 6/7 에 gcc 7 설치하기
gcc 7 및 관련된 개발도구를 간단히 한꺼번에 설치하는 방법을 소개합니다.

## SoftwareCollections.org 프로젝트
SoftwareCollections.org 프로젝트는 레드헷(Red Hat Enterprise Linux), Fedora, CentOS, 그리고 Scientific Linux를 위한 Software Collections(SCLs)를 만드는 프로젝트 입니다.
https://www.softwarecollections.org

이 것은 패키지간의 영향없이 하나의 시스템에 다양한 버전을 설치하여 개발에 도움을 줍니다.

## Software Collection 패키지 설치하기
```shell
$ sudo yum -y install centos-release-scl
Loaded plugins: fastestmirror
Determining fastest mirrors
 * base: data.aonenetworks.kr
 * extras: data.aonenetworks.kr
 * updates: data.aonenetworks.kr
base                                                                                                                                                   | 3.6 kB  00:00:00     
extras                                                                                                                                                 | 3.4 kB  00:00:00     
updates                                                                                                                                                | 3.4 kB  00:00:00     
(1/4): base/7/x86_64/group_gz                                                                                                                          | 166 kB  00:00:00     
(2/4): extras/7/x86_64/primary_db                                                                                                                      | 180 kB  00:00:00     
(3/4): updates/7/x86_64/primary_db                                                                                                                     | 2.4 MB  00:00:00     
(4/4): base/7/x86_64/primary_db                                                                                                                        | 6.0 MB  00:00:01     
Resolving Dependencies
--> Running transaction check
---> Package centos-release-scl.noarch 0:2-2.el7.centos will be installed
--> Processing Dependency: centos-release-scl-rh for package: centos-release-scl-2-2.el7.centos.noarch
--> Running transaction check
---> Package centos-release-scl-rh.noarch 0:2-2.el7.centos will be installed
--> Finished Dependency Resolution

Dependencies Resolved

==============================================================================================================================================================================
 Package                                            Arch                                Version                                     Repository                           Size
==============================================================================================================================================================================
Installing:
 centos-release-scl                                 noarch                              2-2.el7.centos                              extras                               12 k
Installing for dependencies:
 centos-release-scl-rh                              noarch                              2-2.el7.centos                              extras                               12 k

Transaction Summary
==============================================================================================================================================================================
Install  1 Package (+1 Dependent package)

Total download size: 24 k
Installed size: 39 k
Is this ok [y/d/N]: y
Downloading packages:
(1/2): centos-release-scl-rh-2-2.el7.centos.noarch.rpm                                                                                                 |  12 kB  00:00:00     
(2/2): centos-release-scl-2-2.el7.centos.noarch.rpm                                                                                                    |  12 kB  00:00:00     
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
Total                                                                                                                                          60 kB/s |  24 kB  00:00:00     
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
  Installing : centos-release-scl-rh-2-2.el7.centos.noarch                                                                                                                1/2 
  Installing : centos-release-scl-2-2.el7.centos.noarch                                                                                                                   2/2 
  Verifying  : centos-release-scl-rh-2-2.el7.centos.noarch                                                                                                                1/2 
  Verifying  : centos-release-scl-2-2.el7.centos.noarch                                                                                                                   2/2 

Installed:
  centos-release-scl.noarch 0:2-2.el7.centos                                                                                                                                  

Dependency Installed:
  centos-release-scl-rh.noarch 0:2-2.el7.centos                                                                                                                               

Complete!
```

## devtoolset-7 소프트웨어 컬렉션을 이용하여 gcc 7 을 설치하기
```shell
$ sudo yum install devtoolset-7
Loaded plugins: fastestmirror
Loading mirror speeds from cached hostfile
 * base: data.aonenetworks.kr
 * extras: data.aonenetworks.kr
 * updates: data.aonenetworks.kr
centos-sclo-rh                                                                                                                                         | 3.0 kB  00:00:00     
centos-sclo-sclo                                                                                                                                       | 2.9 kB  00:00:00     
(1/2): centos-sclo-sclo/x86_64/primary_db                                                                                                              | 264 kB  00:00:02     
(2/2): centos-sclo-rh/x86_64/primary_db                                                                                                                | 3.7 MB  00:00:04     
Resolving Dependencies
--> Running transaction check
---> Package devtoolset-7.x86_64 0:7.1-4.el7 will be installed
--> Processing Dependency: devtoolset-7-toolchain for package: devtoolset-7-7.1-4.el7.x86_64
--> Processing Dependency: devtoolset-7-runtime for package: devtoolset-7-7.1-4.el7.x86_64
--> Processing Dependency: devtoolset-7-perftools for package: devtoolset-7-7.1-4.el7.x86_64
--> Running transaction check

...



Installed:
  devtoolset-7.x86_64 0:7.1-4.el7                                                                                                                                             

Dependency Installed:
  audit-libs-python.x86_64 0:2.8.4-4.el7                    avahi-libs.x86_64 0:0.6.31-19.el7                     boost-date-time.x86_64 0:1.53.0-27.el7                     
  boost-system.x86_64 0:1.53.0-27.el7                       boost-thread.x86_64 0:1.53.0-27.el7                   checkpolicy.x86_64 0:2.5-8.el7                             
  cpp.x86_64 0:4.8.5-36.el7                                 devtoolset-7-binutils.x86_64 0:2.28-11.el7            devtoolset-7-dwz.x86_64 0:0.12-1.1.el7                     
  devtoolset-7-dyninst.x86_64 0:9.3.2-3.el7                 devtoolset-7-elfutils.x86_64 0:0.170-5.el7            devtoolset-7-elfutils-libelf.x86_64 0:0.170-5.el7          
  devtoolset-7-elfutils-libs.x86_64 0:0.170-5.el7           devtoolset-7-gcc.x86_64 0:7.3.1-5.15.el7              devtoolset-7-gcc-c++.x86_64 0:7.3.1-5.15.el7               
  devtoolset-7-gcc-gfortran.x86_64 0:7.3.1-5.15.el7         devtoolset-7-gdb.x86_64 0:8.0.1-36.el7                devtoolset-7-libquadmath-devel.x86_64 0:7.3.1-5.15.el7     
  devtoolset-7-libstdc++-devel.x86_64 0:7.3.1-5.15.el7      devtoolset-7-ltrace.x86_64 0:0.7.91-2.el7             devtoolset-7-make.x86_64 1:4.2.1-3.el7                     
  devtoolset-7-memstomp.x86_64 0:0.1.5-5.1.el7              devtoolset-7-oprofile.x86_64 0:1.2.0-2.el7.1          devtoolset-7-perftools.x86_64 0:7.1-4.el7                  
  devtoolset-7-runtime.x86_64 0:7.1-4.el7                   devtoolset-7-strace.x86_64 0:4.17-7.el7               devtoolset-7-systemtap.x86_64 0:3.1-4s.el7                 
  devtoolset-7-systemtap-client.x86_64 0:3.1-4s.el7         devtoolset-7-systemtap-devel.x86_64 0:3.1-4s.el7      devtoolset-7-systemtap-runtime.x86_64 0:3.1-4s.el7         
  devtoolset-7-toolchain.x86_64 0:7.1-4.el7                 devtoolset-7-valgrind.x86_64 1:3.13.0-11.el7          efivar-libs.x86_64 0:36-11.el7_6.1                         
  gcc.x86_64 0:4.8.5-36.el7                                 glibc-devel.x86_64 0:2.17-260.el7_6.3                 glibc-headers.x86_64 0:2.17-260.el7_6.3                    
  kernel-debug-devel.x86_64 0:3.10.0-957.5.1.el7            kernel-headers.x86_64 0:3.10.0-957.5.1.el7            libcgroup.x86_64 0:0.41-20.el7                             
  libgfortran4.x86_64 0:8.2.1-1.3.1.el7_5                   libmpc.x86_64 0:1.0.1-3.el7                           libquadmath.x86_64 0:4.8.5-36.el7                          
  libsemanage-python.x86_64 0:2.5-14.el7                    mokutil.x86_64 0:15-2.el7.centos                      mpfr.x86_64 0:3.1.1-4.el7                                  
  perl.x86_64 4:5.16.3-294.el7_6                            perl-Carp.noarch 0:1.26-244.el7                       perl-Encode.x86_64 0:2.51-7.el7                            
  perl-Exporter.noarch 0:5.68-3.el7                         perl-File-Path.noarch 0:2.09-2.el7                    perl-File-Temp.noarch 0:0.23.01-3.el7                      
  perl-Filter.x86_64 0:1.49-3.el7                           perl-Getopt-Long.noarch 0:2.40-3.el7                  perl-HTTP-Tiny.noarch 0:0.033-3.el7                        
  perl-PathTools.x86_64 0:3.40-5.el7                        perl-Pod-Escapes.noarch 1:1.04-294.el7_6              perl-Pod-Perldoc.noarch 0:3.20-4.el7                       
  perl-Pod-Simple.noarch 1:3.28-4.el7                       perl-Pod-Usage.noarch 0:1.63-3.el7                    perl-Scalar-List-Utils.x86_64 0:1.27-248.el7               
  perl-Socket.x86_64 0:2.010-4.el7                          perl-Storable.x86_64 0:2.45-3.el7                     perl-Text-ParseWords.noarch 0:3.29-4.el7                   
  perl-Time-HiRes.x86_64 4:1.9725-3.el7                     perl-Time-Local.noarch 0:1.2300-2.el7                 perl-constant.noarch 0:1.27-2.el7                          
  perl-libs.x86_64 4:5.16.3-294.el7_6                       perl-macros.x86_64 4:5.16.3-294.el7_6                 perl-parent.noarch 1:0.225-244.el7                         
  perl-podlators.noarch 0:2.5.1-3.el7                       perl-threads.x86_64 0:1.87-4.el7                      perl-threads-shared.x86_64 0:1.43-6.el7                    
  policycoreutils-python.x86_64 0:2.5-29.el7_6.1            python-IPy.noarch 0:0.75-6.el7                        scl-utils.x86_64 0:20130529-19.el7                         
  setools-libs.x86_64 0:3.3.8-4.el7                         unzip.x86_64 0:6.0-19.el7                             zip.x86_64 0:3.0-11.el7                                    

Dependency Updated:
  audit.x86_64 0:2.8.4-4.el7                    audit-libs.x86_64 0:2.8.4-4.el7        glibc.x86_64 0:2.17-260.el7_6.3         glibc-common.x86_64 0:2.17-260.el7_6.3        
  libgcc.x86_64 0:4.8.5-36.el7                  libgomp.x86_64 0:4.8.5-36.el7          libselinux.x86_64 0:2.5-14.1.el7        libselinux-python.x86_64 0:2.5-14.1.el7       
  libselinux-utils.x86_64 0:2.5-14.1.el7        libsemanage.x86_64 0:2.5-14.el7        libsepol.x86_64 0:2.5-10.el7            policycoreutils.x86_64 0:2.5-29.el7_6.1       

Complete!


```

## gcc 혹은 g++ 환경설정하기
```shell
$ scl enable devtoolset-7 bash
```
이 명령은 devtoolset-7에 포함된 도구를 사용할 수 있는 환경을 즉석으로 구성하여 쉘을 구동시킵니다.  만약, 로그인 할 때 마다 적용되기 위해서는 ~/.bash_profile 에 다음과 같이 추가합니다.

```shell
. /opt/rh/devtoolset-7/enable
```

## gcc 와 g++ 버전 확인하기
```shell
$ gcc --version
gcc (GCC) 7.3.1 20180303 (Red Hat 7.3.1-5)
Copyright (C) 2017 Free Software Foundation, Inc.
This is free software; see the source for copying conditions.  There is NO
warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.

$ g++ --version
g++ (GCC) 7.3.1 20180303 (Red Hat 7.3.1-5)
Copyright (C) 2017 Free Software Foundation, Inc.
This is free software; see the source for copying conditions.  There is NO
warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.
```