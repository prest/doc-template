---
title: "查询语句"
date: 2017-08-30T19:06:04-03:00
weight: 12
menu: main
---

### 条件查询过滤Filter (WHERE)

```
GET /DATABASE/SCHEMA/TABLE?FIELD=$eq.VALUE
```

查询运算符：

| Name | 描述 |英文表述|
|----|----|-------------|
| $eq | 相等| Matches values that are equal to a specified value.|
| $gt | 大于|Matches values that are greater than a specified value.|
| $gte |大于等于| Matches values that are greater than or equal to a specified value.|
| $lt | 小于|Matches values that are less than a specified value.|
| $lte |小于等于| Matches values that are less than or equal to a specified value.|
| $ne | 不等于|Matches all values that are not equal to a specified value.|
| $in | 包含|Matches any of the values specified in an array.|
| $nin | 不包含|Matches none of the values specified in an array.|
| $null | 空值|Matches if field is null.|
| $notnull | 非空|Matches if field is not null.|
| $true | 为真|Matches if field is true.|
| $nottrue |不为真| Matches if field is not true.|
| $false |为伪| Matches if field is false.|
| $notfalse |不为伪| Matches if field is not false.|
| $like |整个字符串匹配| Matches always cover the entire string.|
| $ilike |同上，不区分大小写| Matches *case-insensitive* always cover the entire string.|


### 条件查询过滤Filter (WHERE) with JSONb field

```
http://127.0.0.1:8000/DATABASE/SCHEMA/TABLE?FIELD->>JSONFIELD:jsonb=VALUE (filter)
```

### 选择 Select - GET

```
http://127.0.0.1:8000/databases (显示所有数据库)
http://127.0.0.1:8000/databases?_count=* (数据库计数)
http://127.0.0.1:8000/databases?_renderer=xml (返回xml格式，默认json)
http://127.0.0.1:8000/schemas (查看所有模式)
http://127.0.0.1:8000/schemas?_count=* (模式计数)
http://127.0.0.1:8000/schemas?_renderer=xml (返回xml格式，默认json)
http://127.0.0.1:8000/tables (查看所有表)
http://127.0.0.1:8000/tables?_renderer=xml (返回xml格式，默认json)
http://127.0.0.1:8000/DATABASE/SCHEMA (查询指定数据库名称的模式名称下的所有表)
http://127.0.0.1:8000/DATABASE/SCHEMA?_renderer=xml (返回xml格式，默认json)
http://127.0.0.1:8000/DATABASE/SCHEMA/TABLE (查询某表，返回所有行)
http://127.0.0.1:8000/DATABASE/SCHEMA/TABLE?_select=column (查询某表，返回所有列)
http://127.0.0.1:8000/DATABASE/SCHEMA/TABLE?_select=column[array id] (查询某表，返回某列)

http://127.0.0.1:8000/DATABASE/SCHEMA/TABLE?_select=* (查询整表)
http://127.0.0.1:8000/DATABASE/SCHEMA/TABLE?_count=* (统计表中的行数)
http://127.0.0.1:8000/DATABASE/SCHEMA/TABLE?_count=column (统计表中的某列的数量)
http://127.0.0.1:8000/DATABASE/SCHEMA/TABLE?_page=2&_page_size=10 (分页查询)
http://127.0.0.1:8000/DATABASE/SCHEMA/TABLE?FIELD=VALUE (条件查询)
http://127.0.0.1:8000/DATABASE/SCHEMA/TABLE?_renderer=xml (返回xml格式，默认json)


视图查询操作
http://127.0.0.1:8000/DATABASE/SCHEMA/VIEW?_select=column (select statement by columns in VIEW)
http://127.0.0.1:8000/DATABASE/SCHEMA/VIEW?_select=* (select all from VIEW)
http://127.0.0.1:8000/DATABASE/SCHEMA/VIEW?_count=* (use count function)
http://127.0.0.1:8000/DATABASE/SCHEMA/VIEW?_count=column (use count function)
http://127.0.0.1:8000/DATABASE/SCHEMA/VIEW?_page=2&_page_size=10 (pagination, page_size 10 by default)
http://127.0.0.1:8000/DATABASE/SCHEMA/VIEW?FIELD=VALUE (filter)
http://127.0.0.1:8000/DATABASE/SCHEMA/VIEW?_renderer=xml (JSON by default)

```

### 新增 Insert - POST

```
http://127.0.0.1:8000/DATABASE/SCHEMA/TABLE
```

JSON DATA:
```
{
    "FIELD1": "string value",
    "FIELD2": 1234567890
}
```

### 更新 Update - PATCH/PUT

使用查询字符作为过滤器(WHERE), 例如:

```
http://127.0.0.1:8000/DATABASE/SCHEMA/TABLE?FIELD1=xyz
```

JSON DATA:
```
{
    "FIELD1": "string value",
    "FIELD2": 1234567890,
    "ARRAYFIELD": ["value 1","value 2"]
}
```
### 删除 Delete - DELETE

使用查询字符作为过滤器(WHERE), 例如:

```
http://127.0.0.1:8000/DATABASE/SCHEMA/TABLE?FIELD1=xyz
```

## 连接 JOIN

```
/DATABASE/SCHEMA/Table?_join=Type:Table2:Table.field:Operator:Table2.field
```
参数:

1. Type (INNER, LEFT, RIGHT, OUTER)
1. Table2
1. Table.field
1. Operator ($eq, $lt, $gt, $lte, $gte)
1. Table2.field

使用查询字符连接表, 例如:

```
/DATABASE/SCHEMA/friends?_join=inner:users:friends.userid:$eq:users.id
```
## 查询运算符：

| Name | 描述 |英文表述|
|----|----|-------------|
| $eq | 相等| Matches values that are equal to a specified value.|
| $gt | 大于|Matches values that are greater than a specified value.|
| $gte |大于等于| Matches values that are greater than or equal to a specified value.|
| $lt | 小于|Matches values that are less than a specified value.|
| $lte |小于等于| Matches values that are less than or equal to a specified value.|
| $ne | 不等于|Matches all values that are not equal to a specified value.|
| $in | 包含|Matches any of the values specified in an array.|
| $nin | 不包含|Matches none of the values specified in an array.|



## 去重DISTINCT 

要在查询中使用 *DISTINCT* 子句, 需要附加 `_distinct=true`.

Examples:
```
    GET /DATABASE/SCHEMA/TABLE/?_distinct=true
```

## 排序
在查询中使用 *ORDER BY* 您必须在 *GET* 请求中传入带有fieldname（s）的属性`_order`作为值。 对于 *倒序 DESC* 命令，请使用前缀`-`。 对于 *multiple* 多重排序，字段用逗号分隔。



示例:

### 正序
    GET /DATABASE/SCHEMA/TABLE/?_order=fieldname

### 倒序
    GET /DATABASE/SCHEMA/TABLE/?_order=-fieldname

### 多重排序
    GET /DATABASE/SCHEMA/TABLE/?_order=fieldname01,-fieldname02,fieldname03

## 分组

支持以下方法：

| name | Use in request |中文|
| ------- | ------------- |------ |
| SUM | sum:field |求和|
| AVG | avg:field |求平均|
| MAX | max:field |求最大|
| MIN | min:field |求最小|
| MEDIAN | median:field |求中值|
| STDDEV | stddev:field |求标准差|
| VARIANCE | variance:field |求方差|

### 示例:
	GET /DATABASE/SCHEMA/TABLE/?_select=fieldname00,fieldname01&_groupby=fieldname01

#### 分组方法
	GET /DATABASE/SCHEMA/TABLE/?_select=fieldname00,sum:fieldname01&_groupby=fieldname01

#### 支持Having 
要在**Group By** 使用 Having ，使用以下语法:

	_groupby=fieldname->>having:GROUPFUNC:FIELDNAME:CONDITION:VALUE-CONDITION

示例:

	GET /DATABASE/SCHEMA/TABLE/?_select=fieldname00,sum:fieldname01&_groupby=fieldname01->>having:sum:fieldname01:$gt:500
