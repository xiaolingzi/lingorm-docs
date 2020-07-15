# 原生SQL支持

示例：

``` python
sql = "select * from company where id =:id"
params = {}
params["id"] = 1
db = ORM.db("test")
result = db.nativeQuery().find(sql, params)
```

*需要注意的是，这里的参数化查询采用的命名参数的方式而不是问号。

所有支持的方法如下：

```python
execute(self, sql, param_dict) // 执行增、删、改时使用，分别返回影响条数
find(self, sql, param_dict, cls=None) // 查询列表时使用
find_page(self, sql, param_dict, page_index, page_size, cls=None) // 查询分页数据时使用
find_count(self, sql, param_dict) // 查询数量时使用
first(self, sql, param_dict, cls=None) // 返回符合条件的第一条
```
