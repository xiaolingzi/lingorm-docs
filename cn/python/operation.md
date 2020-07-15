# 数据的增删改

## 插入

### 单条插入

``` python
db = ORM.db("test")
entity = FirstTableEntity()
entity.first_name = "my test"
entity.first_number = 1
entity.first_time = time.time()
id = db.insert(entity)
```

### 批量插入

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

## 更新

### 单条更新

``` python
affected_rows = db.update(entity)
```

### 批量更新

``` python
affected_rows = db.batch_update(entity_list)
```

### 条件更新

``` python
where = db.create_where().add_and(
    FirstTableEntity.first_name.like("query%"))
set_list = [FirstTableEntity.first_name.eq(
    "update by"), FirstTableEntity.first_number.eq(5)]
affected_rows = db.update_by(FirstTableEntity, set_list, where)
```

## 删除

### 单条删除

``` python
affected_rows = db.delete(exist_entity)
```

### 条件删除

``` python
where = db.create_where().add_and(
    FirstTableEntity.first_name.like("delete_by%"))
affected_rows = db.delete_by(FirstTableEntity, where)
```
