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

# client에서 server 에 접속 (root 계정은 비번설정 필요, 로컬호스트에서만 가능)
mysql -u my-user -p
```
