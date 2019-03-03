# Linux 에서 암호입력없이 'sudo' 커멘드 실행하기
## 'superman' 이라는 계정을 가정하여 설명

sudo 커멘드 실행과 관련된 설정 파일은 /etc/sudoers 파일이고, 'superman' 계정에 대해 암호업력 없도록 설정하기 위하여 이 파일에 설정을 한다.

## /etc/sudoers 파일 수정하기
```
# vi /etc/sudoers
```

### 관리자 권한으로 구동하는 모든 커멘드에 대해 적용하려면
파일의 끝에 
```
%superman ALL=(ALL) NOPASSWD: ALL
```
를 추가한다.

### 특정 커멘드(/bin/kill, /bin/rm)에 대해 적용하려면
```
%superman ALL=(ALL) NOPASSWD: /bin/kill, /bin/rm
```

를 추가하고 저장한다.

