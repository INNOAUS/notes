# CentOS 7 에 ICE(Internet Communications Engine) 설치하기
ICE는 ZeroC, Inc. (https://www.zeroc.com) 이 개발한 분산객체모델을 위한 프레임워크로 다양한 언어환경을 지원한다. 다음은 CentOS 7 에 Ice Framework를 설치하는 방법을 간단히 정리한 것이다.

## yum 리포지터리 구성하기
```shell
$ wget https://zeroc.com/download/Ice/3.7/el7/zeroc-ice3.7.repo
$ sudo cp zeroc-ice3.7.repo /etc/yum.repos.d/
```

## Ice 설치하기 (C++, Python, PHP 그리고 Ice 기반 서비스 설치)
```shell
$ sudo yum -y install ice-all-runtime ice-all-devel
```

## 설치 확인하기
slice2cpp 커멘드는 Slice 파일을 하여 C++ 코드로 생성하는 유틸리티로 설치여부를 확인한다.
```shell
$ slice2cpp
slice2cpp: error: no input file
Usage: slice2cpp [options] slice-files...
Options:
-h, --help               Show this message.
-v, --version            Display the Ice version.
-DNAME                   Define NAME as 1.
-DNAME=DEF               Define NAME as DEF.
-UNAME                   Remove any definition for NAME.
-IDIR                    Put DIR in the include file search path.
-E                       Print preprocessor output on stdout.
--output-dir DIR         Create files in the directory DIR.
-d, --debug              Print debug messages.
--depend                 Generate Makefile dependencies.
--depend-xml             Generate dependencies in XML format.
--depend-file FILE       Write dependencies to FILE instead of standard output.
--validate               Validate command line options.
--header-ext EXT         Use EXT instead of the default `h' extension.
--source-ext EXT         Use EXT instead of the default `cpp' extension.
--add-header HDR[,GUARD] Add #include for HDR (with guard GUARD) to generated source file.
--include-dir DIR        Use DIR as the header include directory in source files.
--impl-c++11             Generate sample implementations for C++11 mapping.
--impl-c++98             Generate sample implementations for C++98 mapping.
--checksum               Generate checksums for Slice definitions.
--dll-export SYMBOL      Use SYMBOL for DLL exports
                         deprecated: use instead [["cpp:dll-export:SYMBOL"]] metadata.
--ice                    Allow reserved Ice prefix in Slice identifiers
                         deprecated: use instead [["ice-prefix"]] metadata.
--underscore             Allow underscores in Slice identifiers
                         deprecated: use instead [["underscore"]] metadata.

```

## 설치 버전 확인하기
```shell
$ slice2cpp --version
3.7.2
```
