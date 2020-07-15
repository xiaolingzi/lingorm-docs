# 模型的定义

## 示例及说明

``` python
from lingorm.mapping import *


class FirstTableEntity(ORMEntity):
    __table__ = "first_table"
    __database__ = "test"
    id = Field(field_name="id", field_type="int",
               is_primary=True, is_generated=True)
    first_name = Field(field_name="first_name", field_type="string", length="45")
    first_number = Field(field_name="first_number", field_type="int")
    first_time = Field(field_name="first_time", field_type="datetime")

    def __init__(self, **kwargs):
        self.id = kwargs.get("id")
        self.first_name = kwargs.get("first_name")
        self.first_number = kwargs.get("first_number")
        self.first_time = kwargs.get("first_time")
```

如果上面代码所示，模型的代码包含四个部分

第一部分是包的导入那块，需要导入 from lingorm.mapping import * 包。然后类需要继承于其中的ORMEntity。

第二部分是表结构映射，其中的字段说明如下：
1）__table__ 是指对应的表名
2）__database__ 是指对应的数据库名
2）field_name 是对应的数据表中的字段名
2）field_type 表示数据类型
3）is_primary 表示该字段是否为主键，设置为true或者1则表示是，不设置或者设置其它值则表示否；
4）is_generated 表示该字段的值是否为自动生成，设置为true或者1则表示是，不设置或者设置其它值则表示否；

第三部分是类的初始化

## 模型的生成

为了避免错误和效率，建议最好还是通过生成工具去生成对应的模型。代码中了tools目录有一个生成模型的例子，大家可以按自己的需求进行相应的修改或者自己写一个。
