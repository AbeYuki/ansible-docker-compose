# ansible-docker-compose
Test ansible with docker-compose


# 構築
1. build
```
docker-compose build --no-cache
```
2. docker-compose up
```
docker-compose up -d
```
3. ansible コンテナから node コンテナに対して疎通確認
```
ansible node -m ping
```
4. ansible コンテナから playbook を実行
```
ansible-playbook install.yaml
```