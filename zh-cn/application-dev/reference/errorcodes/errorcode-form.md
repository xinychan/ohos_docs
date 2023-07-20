# 卡片错误码

> **说明：**
>
> 以下仅介绍本模块特有错误码，通用错误码请参考[通用错误码说明文档](errorcode-universal.md)。

## 16500001 内部错误

**错误信息**

Internal Error.

**错误描述**

Malloc等内核通用错误。

**可能原因**

当前内存不足。

**处理步骤**

内存不足，需要分析整个进程的内存占用情况，是否有内存泄露的情况。

## 16500050 进程间通信失败

**错误信息**

An IPC connection error happened.

**错误描述**

系统内为执行当前请求进行必要进程间通信时出错，系统会报此错误码。

**可能原因**

当调用接口传入的入参过大时，进程间通信对数据校验失败。

**处理步骤**

确认入参是否过长。

## 16500060 连接服务失败

**错误信息**

A service connection error happened, please try again later.

**错误描述**

系统内为执行当前请求连接必要服务完成请求时出错，系统会报此错误码。

**可能原因**

当前服务繁忙，或服务出现异常。

**处理步骤**

待服务重启后重试。

## 16500100 获取卡片配置信息失败

**错误信息**

Failed to obtain configuration information.

**错误描述**

系统内为执行当前请求获取卡片相关配置信息时出错，系统会报此错误码。

**可能原因**

卡片相关配置信息字段缺失或非法。

**处理步骤**

确认并验证卡片配置信息正确性。

## 16501000 内部错误

**错误信息**

A functional error occurred.

**错误描述**

系统内为执行当前请求时发生内部错误，系统会报此错误码。

## 16501001 卡片ID不存在

**错误信息**

The ID of the form to be operated does not exist.

**错误描述**

当请求所指定的卡片ID未找到或不存在时，系统会报此错误码。

**可能原因**

指定卡片ID不存在，或传入无效卡片ID。

**处理步骤**

检查卡片ID的有效性。

## 16501002 卡片数量达到上限

**错误信息**

The number of forms exceeds the upper bound.

**错误描述**

当卡片数量已达到上限时继续请求添加卡片，系统会报此错误码。

**可能原因**

当前卡片数量已达到上限，但仍继续请求添加卡片。

**处理步骤**

删除不必要卡片后再请求添加。

## 16501003 无法操作指定卡片

**错误信息**

The form can not be operated by the current application.

**错误描述**

当前应用无法对指定卡片进行操作时，系统会报此错误码。

**可能原因**

指定的卡片非当前应用所有。

**处理步骤**

1. 检查传入卡片ID所有权
2. 升级权限为SystemApp

## 16501004 指定的ability未安装

**错误信息**

The ability is not installed.

**错误描述**

当指定的ability未安装时，系统会报此错误码。

**可能原因**

指定的ability未安装。

**处理步骤**

检查传入的abilityName与bundleName是否有效。

## 16501005 连接卡片渲染服务失败

**错误信息**

Connect FormRenderService failed, please try again later.

**错误描述**

连接卡片渲染服务失败时，系统会报此错误码。

**可能原因**

服务繁忙。

**处理步骤**

服务繁忙，请稍后重试。