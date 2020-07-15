# 事务的使用

示例如下：

```python
db = ORM.db("test")
db.begin()
entity = FirstTableEntity()
entity.first_name = "my name"
entity.first_number = 1
entity.first_time = '2020-01-01 00:00:01'
id = db.insert(entity)
db.commit()
// db.rollback()
```

需要注意的是，同一个事务必须在同一个ORM.db("test")创建的实例下执行以上三个方法。
