# CentOS7에 PostgreSQL Multi-Master 데이터베이스 Postgresql-BDR 9.4 설치하기
다음은 2ndQuadrant사에서 만든 PostgreSQL Multi-Master 플러그인 bdr(Bidirectional Replication Plugin)을 설치방법을 정리한 것입니다.

## Postgres-BDR 을 소스코드 컴파일 하여 설치하기
소스코드를 컴파일하기 위해서 gcc 컴파일러를 설치해야 합니다. 여기서는 gcc 7을 사용할 것입니다.
자세한 내용은 ... 블로그를 참고하십시오.

### 준비사항
```shell
$ sudo yum -y install centos-release-scl
$ sudo yum -y install devtoolset-7
$ sudo yum -y install readline-devel bison-devel bison flex-devel flex zlib-devel
$ sudo yum -y install git
```

### Postgres-BDR-9.4 설치하기
최신 소스코드를 $HOME/2ndquadrant_bdr 폴더에 다운로드한 후 컴파일 합니다.
```shell
$ curl -s "https://raw.githubusercontent.com/2ndQuadrant/bdr/bdr-plugin/REL1_0_STABLE/scripts/bdr_quickstart.sh" | bash
```

### 설치 결과 확인하기
컴파일이 성공적으로 진행되었다면, $HOME/2ndquadrant_bdr 폴더에 
```shell
drwxrwxr-x.  6 user user    56 Mar  3 11:30 bdr
drwxrwxr-x.  7 user user  4096 Mar  3 11:28 bdr-pg-src
drwxrwxr-x. 11 user user  4096 Mar  3 11:32 bdr-plugin-src
-rw-rw-r--.  1 user user 16110 Mar  3 11:32 install.log
```
와 같이 bdr, bdr-pg-src, bdr-plugin-src 폴더가 생깁니다.
bdr 폴더는 컴파일된 결과로 이 폴더를 복사하여 사용하면 됩니다.
bdr-pg-src 폴더는 2ndQuadrant에서 Multi-master 환경 구성이 가능하도록 postgresql-9.4 를 변경한 코드가 저장된 곳이고, bdr-plugin-src 폴더는 관련된 plugin 소스코드가 저장된 곳입니다.

만약, 컴파일 시 오류가 발생하였다면 폴더 중 bdr 폴더가 생성되지 않습니다.

### 독립실행환경 구성하기
$HOME/2ndquadrant_bdr/bdr 폴더를 원하는 위치에 복사하여 구성합니다.
다음은 $HOME/dbroot 폴더를 가정하였습니다.
```shell
$ cp -R $HOME/2ndquadrant_bdr/bdr $HOME/dbroot
```

환경변수에 database 커멘드 실행을 위한 경로를 설정합니다.
```shell
$ echo "export PATH=$PATH:$HOME/dbroot/bin" | tee -a ~/.bash_profile
$ echo "export DBROOT=$HOME/dbroot" | tee -a ~/.bash_profile
```

설정된 환경변수 리로드합니다.
```shell
$ . $HOME/.bash_profile
```

버전을 확인합니다.
```shell
$ psql --version
psql (PostgreSQL) 9.4.13
```

#### 데이터베이스 초기화 하기
$HOME/dbroot/data 폴더에 새로운 데이터베이스를 초기화합니다.
```shell
$ initdb -D $DBROOT/data -A trust -U postgres
```

#### 데이터베이스 구동하기
```shell
$ pg_ctl -D /home/user/dbroot/data -l logfile start
server starting
```

#### 데이터베이스 중지하기
```shell
$ pg_ctl -D /home/user/dbroot/data stop
waiting for server to shut down.... done
server stopped
```

#### 데이터베이스 동작 확인하기
프로세스가 정상동작 확인하기 위하여 ps 커멘드를 이용하여 확인합니다.
```shell
$ ps -ef | grep postgres
user        829     1  0 11:58 pts/0    00:00:00 /home/user/dbroot/bin/postgres -D /home/leo/dbroot/data
user        831   829  0 11:58 ?        00:00:00 postgres: checkpointer process   
user        832   829  0 11:58 ?        00:00:00 postgres: writer process   
user        833   829  0 11:58 ?        00:00:00 postgres: wal writer process   
user        834   829  0 11:58 ?        00:00:00 postgres: autovacuum launcher process   
user        835   829  0 11:58 ?        00:00:00 postgres: stats collector process   
user        838  1225  0 11:59 pts/0    00:00:00 grep --color=auto postgres
```

#### 데이터베이스 접속 확인하기
```shell
$ psql -U postgres
psql (9.4.13)
Type "help" for help.

postgres=# \q
$
```


