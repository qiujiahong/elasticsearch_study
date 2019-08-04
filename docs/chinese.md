# 安装中文分词器


## 安装

* 下载中文分词器 https://github.com/medcl/elasticsearch-analysis-ik

* 离线安装
  * download pre-build package from here: https://github.com/medcl/elasticsearch-analysis-ik/releases
  * create plugin folder cd your-es-root/plugins/ && mkdir ik
  * unzip plugin to folder your-es-root/plugins/ik

* 在线安装
```
./bin/elasticsearch-plugin install https://github.com/medcl/elasticsearch-analysis-ik/releases/download/v6.8.1/elasticsearch-analysis-ik-6.8.1.zip
```

* 重启elasticsearch

```bash 
ps -ef | grep elastic| grep -v grep | awk '{print $2}' | xargs -r kill -9
./bin/elasticsearch -d
```



## 安装后测试

* 创建索引

```bash
curl -XPUT http://192.168.30.11:9200/index
# curl -XDELETE http://192.168.30.11:9200/index

curl -XGET http://192.168.30.11:9200/index

```

* 创建map 

```bash 
# curl -XDELETE http://192.168.30.11:9200/index/_mapping
# curl -XGET http://192.168.30.11:9200/index/_mapping
curl -XPOST http://192.168.30.11:9200/index/_mapping -H 'Content-Type:application/json' -d'
{
        "properties": {
            "content": {
                "type": "text",
                "analyzer": "ik_max_word",
                "search_analyzer": "ik_smart"
            }
        }

}'
```
