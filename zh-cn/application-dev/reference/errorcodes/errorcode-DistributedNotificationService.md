# DistributedNotificationService错误码

> **说明：**
>
> 以下仅介绍本模块特有错误码，通用错误码请参考[通用错误码说明文档](errorcode-universal.md)。

## 1600001 内部错误

**错误信息**

Internal Error.

**错误描述**

当发生内存申请失败、多线程处理失败等异常时，系统会报此错误码。

**可能原因**

1. 内存申请失败、多线程处理失败等内核通用错误。

**处理步骤**

1. 确认系统内存是否足够。
2. 重启系统。

## 1600002 应用与通知子系统数据处理或交互错误

**错误信息**

IPC Error.

**错误描述**

当序列化与反序列化错误与通知子系统交互失败时，系统会报此错误码。

**可能原因**

1. 序列化、反序列化错误。
2. 与通知子系统交互失败。

**处理步骤**

1. 确认输入参数是否超长。
2. 确认输入参数是否合法。
3. 确认通知子系统是否已启动。

## 1600003 连接服务错误

**错误信息**

Failed to connect to service.

**错误描述**

当连接服务失败而导致通知子系统异常时，系统会报此错误码。

**可能原因**

1. 服务繁忙、或通知子系统异常。

**处理步骤**

1. 服务繁忙时，需要再次尝试。
2. 确认通知子系统是否正常启动。

## 1600004 通知使能未开启

**错误信息**

Notification is not enabled.

**错误描述**

当通知使能未开启或手动被用户关闭时，系统会报此错误码。

**可能原因**

1. 应用的通知使能是未开启状态或者被用户手动关闭。

**处理步骤**

1. 检查应用通知使能是否已开启。

## 1600005 通知渠道未开启

**错误信息**

Notification slot is not enabled.

**错误描述**

当通知渠道未开启时，系统会报此错误码。

**可能原因**

1. 通知渠道使能未开启。

**处理步骤**

1. 检查应用通知渠道使能是否已开启。

## 1600006 通知不允许删除

**错误信息**

Notification is not allowed to remove.

**错误描述**

删除通知时不具有相应的权限。

**可能原因**

1. 通知设置`isUnremovable`为`true`，只允许删除单条通知，而不允许删除全部通知。
2. 通知设置`isRemoveAllowed`为`false`，不允许删除通知。

**处理步骤**

1. 检查通知是否设置了`isUnremovable`为`true`。
2. 检查通知是否设置了`isRemoveAllowed`为`false`。

## 1600007 通知不存在

**错误信息**

The notification is not exist.

**错误描述**

当通知不存在时，系统会报此错误码。

**可能原因**

1. 通知已被删除。
2. 通知已被取消。

**处理步骤**

1. 检查当前通知是否存在。

## 1600008 用户不存在

**错误信息**

The user is not exist.

**错误描述**

当用户ID错误，或设备用户未激活时，系统会报此错误码。

**可能原因**

1. 用户ID输入错误。
2. 设备上没有激活的用户。

**处理步骤**

1. 检查指定id的用户是否已经存在。

## 1600009 每秒发送通知超过最大限制

**错误信息**

Over max number notifications per second.

**错误描述**

当每秒发送通知超过最大限制时，系统会报此错误码。

**可能原因**

1. 每秒发送通知超过数超过10条。

**处理步骤**

1. 降低通知发送频率。

## 1600010 分布式处理错误

**错误信息**

Distributed operation failed.

**错误描述**

当操作数据库太频繁导致数据库处理异常，系统会报此错误码。

**可能原因**

1. 数据库处理异常、操作太频繁。

**处理步骤**

1. 检查分布式数据运行是否正常。
2. 降低操作频率。

## 1600011 读取模板配置文件错误

**错误信息**

Read template config failed.

**错误描述**

当模板配置文件丢失或不支持当前版本模板时，系统会报此错误码。

**可能原因**

1. 模板配置文件丢失。
2. 当前版本不支持模板。

**处理步骤**

1. 检查系统`/system/etc/notification_template/external.json`文件是否存在。
2. 升级系统版本到3.2及以上。

## 17700001 包名不存在

**错误信息**

The specified bundle name was not found.

**错误描述**

当应用未安装或包名不正确时，系统会报此错误码。

**可能原因**

1. 包名不正确。
2. 应用未安装。

**处理步骤**

1. 检查应用是否存在。