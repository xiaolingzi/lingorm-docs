# 数据查询

## 查询条件构建

我们先来看一个示例：

``` python
db = ORM.db("test")
where = db.createWhere()
where.add_or(FirstTableEntity.id.EQ(38), FirstTableEntity.id.EQ(39))
where.add_and(FirstTableEntity.first_name.LIKE("name%"))
fmt.Println(where.sql) // 输出 (t0.id = :p1 OR t0.id = :p2) AND t0.first_name like :p3
```

通过create_where方法可以构建一个where对象，where对象支持的所有方法如下：
add_or 构建数据库中对应的or条件，并返回对象本身
add_and 构建数据库中对应的and条件，并返回对象本身
get_or 构建or条件，并返回条件的字符串结果
get_and 构建and条件，并返回条件的字符串结果
and_or 构建类似 and (xx or xx)，并返回对象本身
or_and 构建类似 or (xx and xx)，并返回对象本身

另外一个例子如下：

``` python
db = ORM.db("test")
where = db.CreateWhere()
where.add_or(FirstTableEntity.id.eq(38), FirstTableEntity.id.eq(39))
where.add_and(FirstTableEntity.first_name.like("name%"), where.get_or(FirstTableEntity.second_name.eq("name"), FirstTableEntity.second_name.like("a%")))
fmt.Println(where.sql) // 输出 (t1.id = :p1 OR t1.id = :p2) AND t1.first_name like :p5 AND (t1.second_name = :p3 OR t1.second_name like :p4)
```

条件中比较运算符有如下：
gt 大于。比如 FirstTableEntity.id.gt(39)
ge 大于等于
lt 小于
le 小于等于
eq 等于
neq 不等于
like 模糊匹配
in 对应sql中的in
nin 对应sql中的not in

## 简单查询

1）通过Table方法进行链式调用

``` python
db = ORM.db("test")
t = FirstTableEntity
result = db.table(t).select(t.first_name).where(
            t.first_name.like("query%")).order_by(t.id.desc()).find()

```

其中where方法可以还可以接收create_where创建的where对象以支持复杂的查询条件。find方法返回的是一个列表，已经映射到模型中。
除了Find方法之外，还有以下几个方法：

``` python
first(self) // 返回符合条件的第一条数据
find(self) // 返回符合条件的数据列表
find_page(self, page_index, page_size) //返回分页数据
find_count(self) // 返回数量
```

2）直接查询

``` python
db = ORM.db("test")
t = FirstTableEntity
where = self.db.create_where()
where.add_and(t.first_name.eq("query 1"), t.first_number.eq(1))
where.or_and(t.first_name.eq("query 2"), t.first_number.eq(2))
order_by = self.db.create_order_by().by(t.id.desc())

result = self.db.find(t, where, order_by)
```

类似的也有以下几个方法

``` python
find(self, cls, where, order_by=None, top=0)
find_top(self, cls, limit, where, order_by=None)
first(self, cls, where, order_by=None)
find_page(self, cls, page_index, page_size, where, order_by=None)
find_count(self, cls, where)
```

## 复杂查询

复杂查询支持多表联合查询。示例：

``` python
db = ORM.db("test")
f = FirstTableEntity
s = SencondTableEntity
where = self.db.create_where()
where.add_and(f.first_name.eq("query 1"), f.first_number.eq(1))
where.or_and(f.first_name.eq("query 2"), f.first_number.eq(2))
builder = self.db.query_builder()
builder = builder.select(f.first_name, s.second_name).from_table(f).left_join(
    s, f.first_number.eq(s.second_number)).where(where).order_by(f.id.desc())

result = builder.find()
```

其中find方法默认返回的是字典类型，如果需要映射到类，则将定义的类传递给find方法，比如

``` python
result = builder.find(TestEntity)
```
