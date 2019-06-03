---
title: "批量操作"
date: 2018-05-14T12:00:00-03:00
weight: 13
menu: main
---

## 批量插入 Batch Insert - POST

您可以使用批处理一次插入多行

```
http://127.0.0.1:8000/batch/DATABASE/SCHEMA/TABLE

```

JSON 数据:

```
[
    {"FIELD1": "string value", "FIELD2": 1234567890},
    {"FIELD1": "other string value", "FIELD2":1234567891},
]
```

默认的insert方法使用多个元组值，例如`insert into table values（“value”，123），（“other”，456）`。 返回插入的行。
您可以使用带有值`copy`的`Prest-Batch-Method`头来更改此行为。 它对大量插入很有用，但返回为空。
