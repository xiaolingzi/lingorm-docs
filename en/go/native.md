# Native SQL

For example:

``` go
db := lingorm.DB("testdb1")
native := db.NativeQuery()
sql := "select * from company where id =:id"
params := make(map[string]interface{})
params["id"] = 1
var result []company.CompanyEntity
_, err := native.Find(sql, params, &result)

// or
// result, err := native.Find(sql, params)
```

*Note that you should use the named parameters in the sql instead of question marks.

All supported methods are as follows:

```go
Execute(sql string, params map[string]interface{}) (int, int, error) // execute the insert, update and delete sql， return the number of affected rows, the last inserted id and error.
Find(sql string, params map[string]interface{}, slicePtr ...interface{}) (interface{}, error) // return all rows
FindPage(pageIndex int, pageSize int, sql string, params map[string]interface{}, slicePtr ...interface{}) (common.PageResult, error) // return page result
FindCount(sql string, params map[string]interface{}) (int, error) // return the number of rows
First(sql string, params map[string]interface{}, structPtr ...interface{}) (interface{}, error) // return the first row
```
