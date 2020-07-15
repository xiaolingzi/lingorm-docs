# Data Query

## Where Clause

Example：

``` python
db = ORM.db("test")
where = db.createWhere()
where.add_or(FirstTableEntity.id.EQ(38), FirstTableEntity.id.EQ(39))
where.add_and(FirstTableEntity.first_name.LIKE("name%"))
fmt.Println(where.sql) // 输出 (t0.id = :p1 OR t0.id = :p2) AND t0.first_name like :p3
```

With 'create_where', you can create a WHERE clause object. All supported methods are as follows:
add_or | Build 'or' query statements and return the where object
add_and | Build 'and' query statements and return the where object
get_or Build 'or' query statements and return the where string
get_and Build 'and' query statements and return the string
and_or | such as 'and (xx or xx)', return the where object
or_and | such as 'or (xx and xx)', return the where object

Another example:

``` python
db = ORM.db("test")
where = db.CreateWhere()
where.add_or(FirstTableEntity.id.eq(38), FirstTableEntity.id.eq(39))
where.add_and(FirstTableEntity.first_name.like("name%"), where.get_or(FirstTableEntity.second_name.eq("name"), FirstTableEntity.second_name.like("a%")))
fmt.Println(where.sql) // 输出 (t1.id = :p1 OR t1.id = :p2) AND t1.first_name like :p5 AND (t1.second_name = :p3 OR t1.second_name like :p4)
```

The available operators are as follows:

gt | Greater than. Example: table.ID.GT(39)
ge | Greater and equal than.
lt| Less than.
le | Less and equal than.
eq | Equal.
neq | Not Equal.
like
in
nin | Not in.

## Simple Query

Use the 'Table' function

``` python
db = ORM.db("test")
t = FirstTableEntity
result = db.table(t).select(t.first_name).where(
            t.first_name.like("query%")).order_by(t.id.desc()).find()

```

This 'Where' method can accept the instance created by 'create_where' as argument.
In addition to the 'Find' method. All the available functions are as follows:

``` python
first(self) // return the first row
find(self) // return all rows
find_page(self, page_index, page_size) //return page result
find_count(self) // return the number of rows
```

Other functions

``` python
db = ORM.db("test")
t = FirstTableEntity
where = self.db.create_where()
where.add_and(t.first_name.eq("query 1"), t.first_number.eq(1))
where.or_and(t.first_name.eq("query 2"), t.first_number.eq(2))
order_by = self.db.create_order_by().by(t.id.desc())

result = self.db.find(t, where, order_by)
```

Other functions available:

``` python
find(self, cls, where, order_by=None, top=0)
find_top(self, cls, limit, where, order_by=None)
first(self, cls, where, order_by=None)
find_page(self, cls, page_index, page_size, where, order_by=None)
find_count(self, cls, where)
```

## Query Builder

Query Builder support for multi-table joint queries. For example:

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

The type of 'find' function's return value is dict. If you want to map the result to a class, you can do it like this:

``` python
result = builder.find(TestEntity)
```
