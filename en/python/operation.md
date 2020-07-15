# Data CUD

## Insert

### Insert Single row

``` python
db = ORM.db("test")
entity = FirstTableEntity()
entity.first_name = "my test"
entity.first_number = 1
entity.first_time = time.time()
id = db.insert(entity)
```

### Batch Insert

``` python
db = ORM.db("test")
entity_list = []
for i in range(0, 10):
    entity = FirstTableEntity()
    entity.first_name = "batch"+str(i)
    entity.first_number = i
    entity.first_time = '2020-01-01 00:00:01'
    entity_list.append(entity)
affected_rows = db.batch_insert(entity_list)
```

## Update

### Update Single row

``` python
affected_rows = db.update(entity)
```

### Batch Update

``` python
affected_rows = db.batch_update(entity_list)
```

### Update By

``` python
where = db.create_where().add_and(
    FirstTableEntity.first_name.like("query%"))
set_list = [FirstTableEntity.first_name.eq(
    "update by"), FirstTableEntity.first_number.eq(5)]
affected_rows = db.update_by(FirstTableEntity, set_list, where)
```

## Delete

### Delete Single row

``` python
affected_rows = db.delete(exist_entity)
```

### Delete By

``` python
where = db.create_where().add_and(
    FirstTableEntity.first_name.like("delete_by%"))
affected_rows = db.delete_by(FirstTableEntity, where)
```
