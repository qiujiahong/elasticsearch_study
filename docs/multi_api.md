# 批量获取文档


```BASH
# 批量查询
GET /_mget
{
  "docs": [
      {
       "_index":"lib",
       "_type": "user",
       "_id": 1
      },
      {
       "_index":"lib",
       "_type": "user",
       "_id": 2
      },
      {
       "_index":"lib",
       "_type": "user",
       "_id": 3
      }
    ]
}

# 批量查询具体字段
GET /_mget
{
  "docs": [
      {
       "_index":"lib",
       "_type": "user",
       "_id": 1,
       "_source": "interests"
      },
      {
       "_index":"lib",
       "_type": "user",
       "_id": 2,
       "_source": ["age","interests"]
      }
    ]
}

# 批量查询简化,url上写索引和类型
GET /lib/user/_mget
{
  "docs": [
      {
       "_id": 1,
       "_source": "interests"
      },
      {
       "_id": 2,
       "_source": ["age","interests"]
      },
      {
       "_id": 3
      }
    ]
}

# 批量查询最简化
GET /lib/user/_mget
{
  "ids": ["1","2"]
}
```