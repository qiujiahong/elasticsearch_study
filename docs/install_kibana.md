# 安装kibana

kibana是针对elasticsearch的一个开源的分析及可视化平台，使用Kibana可以查询、查看并存储在es索引的数据，并进行交互操作，使用kibana能执行高级的数据分析，并能以图表和地图的方式查看数据。


## 安装kibana

```bash
# 安装java 如果该主机上已经安装则跳过
# 下载kibana
wget https://artifacts.elastic.co/downloads/kibana/kibana-6.8.1-linux-x86_64.tar.gz
tar -xzvf kibana-6.8.1-linux-x86_64.tar.gz -C /opt/
cd /opt/kibana-6.8.1-linux-x86_64 
```


* vim config/kibana.yml

```bash
# 修改Host服务地址，IP为服务的局域网IP
server.host: “192.168.30.11”
# 修改elasticsearch的url地址
# elasticsearch.url: "http://192.168.30.11:9200" # old
elasticsearch.hosts: ["http://192.168.30.11:9200"]
```

* 开启5601端口

```
systemctl start firewalld.service
firewall-cmd --premanent --zone=public --add-port=5601/tcp
firewall-cmd --reload
```

* 启动kibana

```bash
cd /opt/kibana-6.8.1-linux-x86_64 
./bin/kibana
# nohup ./bin/kibana &
# 访问 http://192.168.30.11:5601
```