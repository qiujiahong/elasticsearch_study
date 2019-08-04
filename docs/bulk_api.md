# 批量操作



```bash
# 批量添加，索引和类型在URL内

POST /libs/books/_bulk
{ "index": {"_id":1}}
{ "title": "java","price":55}
{ "index": {"_id":2}}
{ "title": "php","price":20}
{ "index": {"_id":2}}
{ "title": "ruby","price":44}
# 批量添加,索引和类型在数据内
POST _bulk
{ "index" : { "_index" : "libs", "_type" : "books", "_id" : "1" } }
{ "title" : "java","price":55 }
{ "index" : { "_index" : "libs", "_type" : "books", "_id" : "2" } }
{ "title" : "php","price":200 }

# 验证
GET /libs/books/_mget
{
  "ids": ["1","2","3","4"]
}

# 一次有读写更新创建
POST /libs/books/_bulk
{ "delete": {"_index":"libs","_type":"books","_id":1}}
{ "create": {"_index":"libs1","_type":"students","_id":2}}
{ "name": "张三","age":20}
{ "index": {"_id":4}}
{ "title": "ruby","price":44}
{ "update": {"_index":"libs1","_type":"students","_id":2}}
{ "doc": {"age":25}}
```