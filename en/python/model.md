# Model

## Examples and Instructions

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

As shown in the code above.

First, you have to import the mapping packages, it is "from lingorm.mapping import *". And then the class extends ORMEntity.

Second, define a class that map to a database table. Like the 'FirstTableEntity' above.
1）__table__ | table name
2）__database__ | database name
3）field_name | column name
4）field_type | data type
5）is_primary | It indicates whether the field is a primary key, True or 1 means yes, and no setting or setting another value means No.
6）is_generated | It indicates whether the field is self-added, true or 1 means yes, and no setting or setting another value means No.

1）json. It is the property name after json serialization, It's mainly up to the serialization plug-ins used.
2）column. It is the name of the table fields.
3）primary_key. It indicates whether the field is a primary key, true or 1 means yes, and no setting or setting another value means No.
4）auto_increment. It indicates whether the field is self-added, true or 1 means yes, and no setting or setting another value means No.

At last, Define a struct type for table and a 'Table' function which return a table instance. You may be confused about this. As for most orm frameworks, define the second part is enough. But it does improve our efficiency. For example:

## Model Generation

It is highly recommended to use code generation tools to generate code for the model. There is an example in the tools diretory, and you can change it to meet your needs.
