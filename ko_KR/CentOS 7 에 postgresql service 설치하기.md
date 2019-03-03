# CentOS 7 에 Postgresql Service 설정하기
다음은 소스코드를 이용하여 빌드하였거나 복사한 데이터베이스를 서비스로 동작하기 위한 방법을 정리한 것이다.

## 서비스 스크립트 작성
```shell
$ vi postgresql.service

# Systemd service definition for postgresql-bdr94
# 
# It's not recommended to modify this file in-place, because it will be
# overwritten during package upgrades.  If you want to customize, the
# best way is to create a file "/etc/systemd/system/postgresql-9.4.service",
# containing
#   .include /lib/systemd/system/postgresql-9.4.service
#   ...make your changes here...
# For more info about custom unit files, see
# http://fedoraproject.org/wiki/Systemd#How_do_I_customize_a_unit_file.2F_add_a_custom_unit_file.3F

# Note: changing PGDATA will typically require adjusting SELinux
# configuration as well.

# Note: do not use a PGDATA pathname containing spaces, or you will
# break postgresql-setup.
[Unit]
Description=PostgreSQL 9.4 database server with BDR
After=syslog.target
After=network.target

[Service]
Type=forking

User={서비스 소유자}
Group={서비스 그룹}

# Note: avoid inserting whitespace in these Environment= lines, or you may
# break postgresql-setup.

# Location of database directory
Environment=PGDATA={데이터베이스 데이터 폴더}

# Where to send early-startup messages from the server (before the logging
# options of postgresql.conf take effect)
# This is normally controlled by the global default set by systemd
# StandardOutput=syslog

# Disable OOM kill on the postmaster
OOMScoreAdjust=-1000

ExecStart={데이터베이스 커멘드 폴더}/pg_ctl start -D "${PGDATA}" -s -w -t 300
ExecStop={데이터베이스 커멘드 폴더}/pg_ctl stop -D "${PGDATA}" -s -m fast
ExecReload={데이터베이스 커멘드 폴더}/pg_ctl reload -D "${PGDATA}" -s

# Give a reasonable amount of time for the server to start up/shut down
TimeoutSec=300

[Install]
WantedBy=multi-user.target
```

위 postgresql.service 스크립트의 {서비스 소유자}, {서비스 그룹}, {데이터베이스 데이터 폴더}, {데이터베이스 커맨드 폴더} 에 값을 자신의 환경으로 수정한다.
1. {서비스 소유자} 는 서비스 구동시 프로세스 소유자를 의미한다.
2. {서비스 그룹} 은 소유자가 속한 그룹을 위미한다. 일반적으로 소유자와 동일하게 지정한다.
3. {데이터베이스 데이터 폴더} 는 initdb 를 이용하여 초기화한 데이터베이스 데이터 폴더를 의미한다.
4. {데이터베이스 커맨드 폴더} 는 initdb, createdb 등 관련 커멘드가 위치한 곳을 의미한다.

다음은 서비스 소유자 계정이 user, 그룹이 user라고 가정하고, 데이터베이스 커멘드는 /home/user/dbroot/bin, 데이터 폴더는 /home/user/dbroot/data 라고 가정하였을 때의 스크립트 이다.
```shell

# Systemd service definition for postgresql-bdr94
# 
# It's not recommended to modify this file in-place, because it will be
# overwritten during package upgrades.  If you want to customize, the
# best way is to create a file "/etc/systemd/system/postgresql-9.4.service",
# containing
#   .include /lib/systemd/system/postgresql-9.4.service
#   ...make your changes here...
# For more info about custom unit files, see
# http://fedoraproject.org/wiki/Systemd#How_do_I_customize_a_unit_file.2F_add_a_custom_unit_file.3F

# Note: changing PGDATA will typically require adjusting SELinux
# configuration as well.

# Note: do not use a PGDATA pathname containing spaces, or you will
# break postgresql-setup.
[Unit]
Description=PostgreSQL 9.4 database server with BDR
After=syslog.target
After=network.target

[Service]
Type=forking

User=user
Group=user

# Note: avoid inserting whitespace in these Environment= lines, or you may
# break postgresql-setup.

# Location of database directory
Environment=PGDATA=/home/user/dbroot/data

# Where to send early-startup messages from the server (before the logging
# options of postgresql.conf take effect)
# This is normally controlled by the global default set by systemd
# StandardOutput=syslog

# Disable OOM kill on the postmaster
OOMScoreAdjust=-1000

ExecStart=/home/user/dbroot/bin/pg_ctl start -D "${PGDATA}" -s -w -t 300
ExecStop=/home/user/dbroot/bin/pg_ctl stop -D "${PGDATA}" -s -m fast
ExecReload=/home/user/dbroot/bin/pg_ctl reload -D "${PGDATA}" -s

# Give a reasonable amount of time for the server to start up/shut down
TimeoutSec=300

[Install]
WantedBy=multi-user.target

```

## 서비스 설정하기
CentOS 7 에서 서비스 스크립트 위치는 /usr/lib/systemd/system 이다. 위 스크립트 파일명이 postgresql.service 라고 하면 이 파일을 /usr/lib/systemd/system 에 생성, 복사 혹은 symbolic link로 지정한다.

다음은 symbolic link로 지정하는 방법이다.
```shell
$ sudo ln -s /home/user/dbroot/postgresql.service /usr/lib/systemd/system/postgresql.service
```

### 서비스 활성화 하기
```shell
$ sudo systemctl enable postgresql.service
Created symlink from /etc/systemd/system/multi-user.target.wants/postgresql.service to /home/user/dbroot/postgresql.service.
Created symlink from /etc/systemd/system/postgresql.service to /home/leo/dbroot/postgresql.service.
```

### 서비스 구동하기
```shell
$ sudo systemctl start postgresql.service
$ ps -ef | grep postgres
user      11661     1  0 13:02 ?        00:00:00 /home/user/dbroot/bin/postgres -D /home/user/dbroot/data
user      11663 11661  0 13:02 ?        00:00:00 postgres: checkpointer process   
user      11664 11661  0 13:02 ?        00:00:00 postgres: writer process   
user      11665 11661  0 13:02 ?        00:00:00 postgres: wal writer process   
user      11666 11661  0 13:02 ?        00:00:00 postgres: autovacuum launcher process   
user      11667 11661  0 13:02 ?        00:00:00 postgres: stats collector process   
user      11671  1225  0 13:02 pts/0    00:00:00 grep --color=auto postgres
```

### 서비스 중지하기
```shell
$ sudo systemctl stop postgresql.service
```

### 데이터베이스 연결하기
```shell
$ psql -U postgres
psql (9.4.13)
Type "help" for help.

postgres=# 
```
