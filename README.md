#### elasticsearch:8.7.0 实体服务器 docker-compose 部署集群，集成中文分词插件

#### 拉取本仓库配置
#### Pull the warehouse configuration
````
ssh 192.168.1.2
git clone git@github.com:anjingjingan/elasticsearch-cluster-docker-compose.git

ssh 192.168.1.3
git clone git@github.com:anjingjingan/elasticsearch-cluster-docker-compose.git

ssh 192.168.1.4
git clone git@github.com:anjingjingan/elasticsearch-cluster-docker-compose.git
````
#### 生成本地集群证书（注意 req.cnf IP.1，IP.2，IP.2 填写实际服务器IP）
#### Generate a local cluster certificate (note that req.cnf IP.1, IP.2, IP.2 fill in the actual server IP)
````
openssl req -x509 -nodes -days 100000 -newkey rsa:2048 -keyout ./elasticsearch/certs/elasticsearch_key.pem -out ./elasticsearch/certs/elasticsearch_cert.pem -config req.cnf -sha256
````

#### 复制证书到其他集群服务器
#### Copy the certificate to other cluster servers
````
scp -r ./elasticsearch/certs root@192.168.1.3:/path/elasticsearch/
scp -r ./elasticsearch/certs root@192.168.1.4:/path/elasticsearch/
````

#### 启动集群
#### Start the cluster
````
docker-compose up -d
````

#### 修改 kibana 默认密码
#### Modify kibana default password
````
curl -XPOST -u elastic:password 'http://localhost:9200/_security/user/kibana/_password' -H 'Content-Type: application/json' -d '{ "password" : "password" }'
````


