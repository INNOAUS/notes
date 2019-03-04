# CentOS 7 에서 Cryptopp 라이브러리 빌드하기
다음은 https://github.com/weidai11/cryptopp 에 있는 소스코드를 이용하여 CentOS 7 에서 Crypto++ 라이브러리 빌드하는 방법을 정리한 것입니다.

## 준비사항
gcc, g++ 컴파일러가 설치되어 있어야 합니다. 'CentOS 6,7 에서 gcc 7 설치하기' 블로그를 참고하십시오.

## 최신 릴리스 버전 다운로드 하기
2019년 3월 4일 현재 최신버전은 8.1.0 으로 https://github.com/weidai11/cryptopp/archive/CRYPTOPP_8_1_0.tar.gz 를 다운로드 합니다.
```shell
$ wget https://github.com/weidai11/cryptopp/archive/CRYPTOPP_8_1_0.tar.gz
```

## 압축해제하기
```shell
$ tar xvfz CRYPTOPP_8_1_0.tar.gz
```

## 빌드하기
설치 폴더를 $HOME/devtools 로 하여 빌드합니다.
```shell
$ cd cryptopp-CRYPTOPP_8_1_0
$ make -j 8 install PREFIX=$HOME/devtools
```

위와 같이 실행하면 컴파일이 진행되고 결과는 $HOME/devtools 아래에 설치됩니다.  여기서 -j 8 은 병렬컴파일 옵션으로 8 은 코어수를 의미합니다.


