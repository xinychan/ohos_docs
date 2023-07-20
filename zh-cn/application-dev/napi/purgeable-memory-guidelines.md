# 内存管理purgeable内存开发指导

## 场景介绍

开发者可以通过本指导了解在OpenHarmony应用中，如何使用Native purgeablememory接口操作purgeable内存。功能包括purgeable内存申请、释放。


针对Purgeable memory，常见的开发场景如下：

* 通过`Purgeablmemory`提供的`NAPI`接口申请PurgeableMemory对象，并将数据内容写入PurgeableMemory对象。
* 使用完毕后释放

## 接口说明

| 接口名 | 描述 | 
| -------- | -------- |
| OH_PurgeableMemory \*OH_PurgeableMemory_Create(size_t size, OH_PurgeableMemory_ModifyFunc func, void \*funcPara) | 创建Purgeable memory对象，每次调用都会产生一个新的Purgeable memory对象。 | 
| bool OH_PurgeableMemory_Destroy(OH_PurgeableMemory \*purgObj) | 对Purgeable memory对象进行析构操作。 | 
| bool OH_PurgeableMemory_BeginRead(OH_PurgeableMemory \*purgObj) | 对purgeable对象进行读访问。 | 
| void OH_PurgeableMemory_EndRead(OH_PurgeableMemory \*purgObj) | 读操作结束，将Purgeable对象的引用计数减1，当引用计数为0的时候， 该Purgeable memory对象可以被系统回收。 | 
|bool OH_PurgeableMemory_BeginWrite(OH_PurgeableMemory \*purgObj) | 对purgeable对象进行写访问。|
|void OH_PurgeableMemory_EndWrite(OH_PurgeableMemory \*purgObj)|写操作结束，将Purgeable对象的引用计数减1，当引用计数为0的时候，该Purgeable memory对象可以被系统回收。|
|void \*OH_PurgeableMemory_GetContent(OH_PurgeableMemory \*purgObj)|获取PurgeableMemory对象内存数据。|
|size_t OH_PurgeableMemory_ContentSize(OH_PurgeableMemory \*purgObj)|获取PurgeableMemory对象内存数据大小。|
|bool OH_PurgeableMemory_AppendModify(OH_PurgeableMemory \*purgObj, OH_PurgeableMemory_ModifyFunc func, void \*funcPara)|添加PurgeableMemory对象的修改方法。|


## Purgeable应用开发步骤

以下步骤描述了在**OpenHarmony**中如何使用`PurgeableMemory`提供的`NAPI`接口，申请Purgeable Memory对象，并将内容写入Purgeable对象后，对相应对象进行读写访问。

1. 声明purgeable 对象创建规则
    ```c++
    // 声明构建函数的参数
    struct ParaData{
        int start;
        int end;
    };

    // 声明一个使用ModifyFunc
    bool FactorialFunc(void* data, size_t size, void* param){
        bool ret = true;
        ParaData *pdata = (ParaData*) param;
        int* oriData = (int*)data;
        int i = pdata->start;
        while(i<pdata->end){
            *oriData *= i;
        }
        return ret;
    }

    // 声明修改purgeable对象扩展函数的参数
    struct AppendParaData{
        int newPara;
    };

    // 声明修改purgeable对象的扩展函数
    bool AddFunc(void* data, size_t size, void* param){
        bool ret = true;
        int *oriDatap = (int*) data;
        AppendParaData* apData = (AppendParaData*)param;
        *oriDatap += apData->newPara;
        return ret;
    }
    ```
2. 创建Purgeable对象
    ```c++
    // 声明一个4MB的purgeable对象大小
    #define DATASIZE (4 * 1024 * 1024)

    // 声明创建函数的参数
    struct ParaData pdata = {1,2};

    // 创建一个Purgeable对象
    OH_PurgeableMemory* pPurgmem = OH_PurgeableMemory_Create(DATASIZE, FactorialFunc, &pdata);
    ```

3. 读访问Purgeable 对象
    ```c++
    //业务定义对象类型
    class ReqObj;

    // 读取对象
    OH_PurgeableMemory_BeginRead(pPurgmem);

    // 获取purgeable对象大小
    size_t size = OH_PurgeableMemory_ContentSize(pPurgmem);

    // 获取purgeable对象内容
    ReqObj* pReqObj = (ReqObj*) OH_PurgeableMemory_GetContent(pPurgmem);

    // 读取purgeable对象结束
    OH_PurgeableMemory_EndRead(pPurgmem);
    ```

4. 写访问Purgeable对象
    ```c++
     //业务定义对象类型
    class ReqObj;

    // 修改Purgeable对象
    OH_PurgeableMemory_BeginWrite(pPurgmem);

    // 获取purgeable对象数据
    ReqObj* pReqObj = (ReqObj*) OH_PurgeableMemory_GetContent(pPurgmem);

    // 声明扩展创建函数的参数
    struct AppendParaData apdata = {1};

    // 更新purgeable 对象重建规则
    OH_PurgeableMemory_AppendModify(pPurgmem, AddFunc, &apdata);

    // 修改purgeable对象结束
    OH_PurgeableMemory_EndWrite(pPurgmem);
    ```

5. 销毁Purgeable对象
    ```c++
    // 销毁对象
    OH_PurgeableMemory_Destroy(pPurgmem);
    ```