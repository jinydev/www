---
layout: home
---
# WSL 마리아DB 설치

WSL 우분투 리눅스에서 마리아 DB를 설치해 봅니다.



## 설치

atp를 통하여 마리아DB를 설치할 수 있습니다.

```
sudo apt-get install mariadb-server
```

네트웍 상태에 따라서 설치하는데 약간의 시간이 소요될 수 있습니다.



## 설정

마리아DB를 정상적으로 설치한 후에는 몇개의 보안설정이 필요로 합니다. 보완설정은 루투계정의 암호, 외부 접근, 익명사용자 등을 설정합니다.

```
sudo mysql_secure_installation
```



## 상태확인

```
service mysql status
```



## 실행

```
sudo service mysql start
```







mysqld.sock



## 마리아DB 삭제

간혹 마리아DB 설치에 문제가 있어서 재설치를 해야할 경우가 발생될 수 있습니다. 다음은 우분투 리눅스에서 설치된 마리아DB를 삭제하는 방법입니다.

```
sudo apt-get purge mariadb-server

sudo apt-get purge mariadb-common

```

[주의] 기존에 사용된 DB가 있는 경우 반드시 백업한 후에 설치를 삭제해야 합니다.







## 미드나잇 커멘더(midnight commander)

리눅스용 파일관리자인 mc

```
sudo apt install mc
```



