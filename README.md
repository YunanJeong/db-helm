# db-helm

MySQL 등등 테스트용 DB설정은 미리 따로 좀 정리해두면 좋을 것 같다.

## MySQL

```sh
# 설치
helm repo add bitnami https://charts.bitnami.com/bitnami

helm install my-mysql bitnami/mysql --version 11.1.2 -f mysql.yaml
helm upgrade my-mysql bitnami/mysql --version 11.1.2 -f mysql.yaml

# MySQL client
sudo apt update
sudo apt install mysql-client

# client에서 server 에 접속
mysql -u my-user -p
```

## 접근 오류 해결

- 컨테이너 내부에서만 `localhost`로 접근 가능
- 컨테이너 외부, 로컬호스트에서 접근시 `localhost`대신 `127.0.0.1`을 사용
  - (localhost로 접근시 TCP가 아닌 소켓통신이 적용되는데, 로컬호스트에 소켓파일이 없기 때문)

```sh
$ mysql -u myuser -pmypass -h localhost -P 3306
mysql: [Warning] Using a password on the command line interface can be insecure.
ERROR 2002 (HY000): Can't connect to local MySQL server through socket '/var/run/mysqld/mysqld.sock' (2)

$ mysql -u myuser -pmypass -h 127.0.0.1 -P 3306
mysql>
```

## 늦게켜지는 이슈

- WSL에서 DB 초기화 과정이 오래 걸린다.
  - Probe 기능을 전부 꺼도, 접속가능해지기 까지 오래 걸림
  - 특히 아래 Upgrade 과정때문에 늦다.
  - 3~4분 소요 후 완료되면 접속가능
- EC2 환경 등 좀 더 plain한 환경에선 괜찮았음

```sh
# MySQL 로그
mysql 2024-10-31T02:25:46.950581Z 4 [System] [MY-013381] [Server] Server upgrade from '80400' to '80400' started.                                         
mysql 2024-10-31T02:28:00.623049Z 4 [System] [MY-013381] [Server] Server upgrade from '80400' to '80400' completed.
```
