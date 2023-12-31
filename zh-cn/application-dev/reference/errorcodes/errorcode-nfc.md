# NFC错误码

> **说明：**
>
> 以下仅介绍本模块特有错误码，通用错误码请参考[通用错误码说明文档](errorcode-universal.md)。

## 3100101

**错误信息**

NFC state is abnormal in service.

**错误描述**

NFC服务内部执行NFC打开或关闭异常。

**可能原因**

1. 和NFC服务建立通信异常。
2. NFC芯片通信异常。

**处理步骤**

1. 重新执行打开或关闭NFC。
2. 重新执行打开或关闭NFC，或重启设备尝试。

## 3100201

**错误信息**

Tag running state is abnormal in service.

**错误描述**

NFC服务执行Tag业务逻辑遇到错误。

**可能原因**
1. Tag参数值和实际调用函数要求不匹配。
2. Tag操作时，NFC状态是关闭的。
3. Tag操作前，已经处在断开状态。
4. Tag芯片返回错误状态或响应超时。
5. 和NFC服务没有建立绑定关系，无法调用接口。

**处理步骤**
1. 检查NFC参数是否和所调用接口匹配。
2. 打开设备NFC。
3. 先调用连接，再执行读写操作。
4. 重新触碰读取卡片。
5. 退出应用后，重新读取卡片。

## 3200101

**错误信息**

Connected NFC tag running state is abnormal in service.

**错误描述**

执行有源NFC Tag业务逻辑遇到错误。

**可能原因**
1. 有源NFC Tag参数值和实际调用函数要求不匹配。
2. 有源NFC Tag芯片返回错误状态或响应超时。

**处理步骤**
1. 检查有源NFC Tag参数是否和所调用接口匹配。
2. 重新触碰读取卡片。
