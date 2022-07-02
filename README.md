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
3. ansibleコンテナにログイン
```
docker exec -it ansible bash
```
4. ansible コンテナで以下コマンドを実行し、ssh・hosts 設定を行う
```
node=(node01 node02 node03)
for i in ${node[@]} ;
do 
scp -pr /root/.ssh/authorized_keys root@$i:/root/.ssh/authorized_keys ;
done &&\
for i in ${node[@]} ;
do
ssh $i "sed -i -e 's/PasswordAuthentication yes/PasswordAuthentication no/g' /etc/ssh/sshd_config" ;
done &&\
for i in ${node[@]} ;
do
ssh $i service sshd reload ;
done &&\
bash -c "ssh node01 tail -1 /etc/hosts ;\
ssh node02 tail -1 /etc/hosts ;\
ssh node03 tail -1 /etc/hosts" >> /etc/hosts &&\
for i in ${node[@]} ;
do
scp -pr /etc/hosts root@$i:/etc/hosts ;
done
```
5. ansible コンテナから node コンテナに対して疎通確認
```
ansible node -m ping
```
6. ansible コンテナから playbook を実行
```
ansible-playbook install.yaml
```