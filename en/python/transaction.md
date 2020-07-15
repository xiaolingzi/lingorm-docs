# Transaction

Here's an example:

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

It is important to note that the same transaction must be in the same db connection. The three methods are executed under an instance created by the ORM.db("test") .
