# db-helm

MySQL 등등 테스트용 DB설정은 미리 따로 좀 정리해두면 좋을 것 같다.

## MySQL

```sh
helm repo add bitnami https://charts.bitnami.com/bitnami

helm install my-mysql bitnami/mysql --version 11.1.2 -f mysql.yaml
helm upgrade my-mysql bitnami/mysql --version 11.1.2 -f mysql.yaml
```
