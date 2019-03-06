# CentOS 7 에서 사용자 서비스 업데이트 하는 방법
동작중인 사용자 서비스를 다운타임을 최소로 하여 업데이트 하는 방법을 간단히 소개합니다.

## 가정
1. 서비스는 이미 등록되어 동작 중입니다.
2. 서비스 실행파일 명은 'a_process' 입니다.
3. 서비스 실행파일 동작에 필요한 shared object 파일 명을 'a_lib.so' 입니다.
4. 서비스 명은 'a_process.service' 입니다.

## 업데이트 시나리오
a_lib.so 파일이 수정되어 이 파일을 교체합니다.

## 스크립트 작성
업데이트를 위하여 간단한 스크립트를 다음과 같이 작성합니다.
```shell
$ vi update_service.sh

#!/bin/sh

sudo service a_process.service stop
sudo cp a_lib.so {대상폴더}/a_lib.so
sudo systemctl daemon-reload
sudo service a_process.service start

```

위에서 작성한 update_service.sh 에 실행모드를 설정합니다.
```shell
$ chmod +x update_service.sh
```

서비스 업데이트를 위해서는 관리자 권한이 필요하고 sudo 명령을 사용합니다.

동작중인 서비스를 중지합니다.
```shell
sudo service a_process.service stop
```

shared object 를 복사합니다.
```shell
sudo cp a_lib.so {대상폴더}/a_lib.so
```

서비스가 수정되면 서비스 컨트롤러는 업데이트된 것을 reload 해야 합니다.
```shell
sudo systemctl daemon-reload
```

서비스를 시작합니다.
```shell
sudo service a_process.service start
```

