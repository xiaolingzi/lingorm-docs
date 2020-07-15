# Native SQL

For example:

``` python
sql = "select * from company where id =:id"
params = {}
params["id"] = 1
db = ORM.db("test")
result = db.nativeQuery().find(sql, params)
```

*Note that you should use the named parameters in the sql instead of question marks.

All supported methods are as follows:

```python
execute(self, sql, param_dict) // execute the insert, update and delete sql， return the number of affected rows
find(self, sql, param_dict, cls=None) // return all rows
find_page(self, sql, param_dict, page_index, page_size, cls=None) // return page result
find_count(self, sql, param_dict) // return the number of rows
first(self, sql, param_dict, cls=None) // return the first row
```
