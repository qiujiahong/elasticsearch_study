# elastic search安装

## 准备工作

* 安装好的centos 7 操作系统；
* 下载jdk1.8
* [下载elasticsearch 6](https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-6.8.1.tar.gz) 


## 操作步骤

### 安装jdk 

* 解压java包

```bash
tar -xzvf jdk-8u211-linux-x64.tar.gz -C /opt/
```

* 编辑/etc/profile，添加入下几行

```bash
JAVA_HOME=/opt/jdk1.8.0_211/
PATH=$JAVA_HOME/bin:$PATH
export JAVA_HOME PATH
```

* 使java环境变量生效,执行命令检查JAVA是否安装完成   
```
source /etc/profile
java -version
```


## 安装elastic search 

* 安装 

```bash
# 解压包
tar -xzvf elasticsearch-6.8.1.tar.gz -C /opt/
# 为es 添加用户和用户组
groupadd esgroup
useradd esuser -g esgroup -p 123456
chown -R esuser:esgroup /opt/elasticsearch-6.8.1
su esuser
cd /opt/elasticsearch-6.8.1/bin
# 后台启动
#  ./elasticsearch -d  
#  前台启动
./elasticsearch
# 检验是否启动成功
curl http://127.0.0.1:9200
```

* 修改可以远程访问

```bash
# vim config/elasticsearch.yml  修改文件
network.host: 192.168.30.11
# 末尾添加
http.cors.enabled: true
http.cors.allow-origin: '*'
#  http.cors.allow-origin: /http?:\/\/192.168.10.139(:[0-9]+)?/
```

* 配置系统参数，设置用户打开最大文件数   vim /etc/security/limits.conf 文件末尾追加  
```
esuser soft nofile 65536
esuser hard nofile 65536
esuser soft nproc 4096
esuser hard nproc 4096
```
*  vim /etc/security/limits.d/20-nproc.conf，添加行 

```
esuser     soft    nproc     4096
```

* vim /etc/sysctl.conf,末尾添加

```
vm.max_map_count=655360
```

* 执行命令，生效前面设置参数,重启虚拟机： 
```bash
sysctl -p 
systemctl stop firewalld
```

* 开启9200端口 

```
systemctl start firewalld.service
firewall-cmd --premanent --zone=public --add-port=9200/tcp
firewall-cmd --reload
```


* 再次启动es  

```bash
su esuser
cd /opt/elasticsearch-6.8.1/bin
# 后台启动
 ./elasticsearch -d  
#  前台启动
# ./elasticsearch
# 检验是否启动成功,在网络通畅的另外一台主机上执行如下命令,也可以打开浏览器访问
curl http://192.168.30.11:9200
```


>  验证完能够正常启动之后，可以使用后台启动。