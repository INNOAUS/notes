# CentOS 7 에서 ACE 라이브러리 빌드하기
다음은 https://github.com/DOCGroup/ACE_TAO 에 있는 소스코드를 이용하여 CentOS 7 에서 ACE 라이브러리 빌드하는 방법을 정리한 것입니다.

## 준비사항
gcc, g++ 컴파일러가 설치되어 있어야 합니다. 'CentOS 6,7 에서 gcc 7 설치하기' 블로그를 참고하십시오.

## 최신 릴리스 버전 다운로드 하기
2019년 3월 4일 현재 최신버전은 6.5.4 로 https://github.com/DOCGroup/ACE_TAO/releases/download/ACE%2BTAO-6_5_4/ACE-6.5.4.tar.gz 를 다운로드 합니다.
```shell
$ wget https://github.com/DOCGroup/ACE_TAO/releases/download/ACE%2BTAO-6_5_4/ACE-6.5.4.tar.gz
```

## 압축해제하기
```shell
$ tar xvfz ACE-5.6.4.tar.gz
```

## 컴파일 환경 설정하기
ACE 라이브러리 컴파일을 위해서 환경변수 ACE_ROOT를 설정해야 합니다. 이 때 ACE_ROOT 환경변수는 ACE_wrappers 폴더 경로를 의미합니다.
```shell
$ cd ACE_wrappers
$ export ACE_ROOT=$PWD
```

또한 리눅스버전의 config.h 파일을 ACE_wrappers/ace 에 생성합니다. 여기서는 간단히 symbolic link를 사용하여 생성합니다.
```shell
$ cd ACE_wrappers/ace
$ ln -s config-linux.h config.h
$ cd ..
```

그리고, 컴파일러 옵션을 설정하기위하여 ACE_wrappers/include/makeinclude/platform_macros.GNU 파일을 다음과 같이 생성합니다.
```shell
$ vi ACE_wrappers/include/makeinclude/platform_macros.GNU
include $(ACE_ROOT)/include/makeinclude/platform_linux.GNU
INSTALL_PREFIX=$(HOME)/devtools
CPPFLAGS=-fPIC
```

## 동적라이브러리 빌드하기
```shell
$ cd ACE_wrappers
$ make -j 8 install
```
위와 같이 실행하면 컴파일이 진행되고 결과는 $HOME/devtools 아래에 설치됩니다.  여기서 -j 8 은 병렬컴파일 옵션으로 8 은 코어수를 의미합니다.

## 정적라이브러리 빌드하기
```shell
$ cd ACE_wrappers
$ make -j 8 install static_libs_only=1
```

