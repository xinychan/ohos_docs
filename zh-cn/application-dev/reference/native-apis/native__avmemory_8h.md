# native_avmemory.h


## 概述

声明了AVMemory的函数接口。

**起始版本：**

9

**相关模块：**

[Core](_core.md)


## 汇总


### 函数

| 名称 | 描述 | 
| -------- | -------- |
| \*[OH_AVMemory_Create](_core.md#oh_avmemory_create) (int32_t size) | 创建OH_AVMemory实例的指针。 | 
| \*[OH_AVMemory_GetAddr](_core.md#oh_avmemory_getaddr) (struct OH_AVMemory \*mem) | 获取入参的内存虚拟地址。 | 
| [OH_AVMemory_GetSize](_core.md#oh_avmemory_getsize) (struct OH_AVMemory \*mem) | 获取入参的内存长度。 | 
| [OH_AVMemory_Destroy](_core.md#oh_avmemory_destroy) (struct OH_AVMemory \*mem) | 释放OH_AVMemory实例指针的资源。 | 
