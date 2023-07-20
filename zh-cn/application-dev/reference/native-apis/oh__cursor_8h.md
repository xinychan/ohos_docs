# oh_cursor.h


## 概述

提供通过查询数据库生成的数据库结果集的访问方法。

结果集是指用户调用关系型数据库查询接口之后返回的结果集合，提供了多种灵活的数据访问方式，以便用户获取各项数据。

**起始版本：**

10

**相关模块：**

[RDB](_r_d_b.md)


## 汇总


### 结构体

| 名称 | 描述 |
| -------- | -------- |
| [OH_Cursor](_o_h___cursor.md) | 表示结果集。 |


### 类型定义

| 名称 | 描述 |
| -------- | -------- |
| [OH_Cursor](_r_d_b.md#oh_cursor) | 表示结果集。 |


### 枚举

| 名称 | 描述 |
| -------- | -------- |
| [OH_ColumnType](_r_d_b.md#oh_columntype)&nbsp;{<br/>TYPE_NULL&nbsp;=&nbsp;0,&nbsp;TYPE_INT64,&nbsp;TYPE_REAL,&nbsp;TYPE_TEXT,<br/>TYPE_BLOB<br/>} | 数据库字段类型. |
