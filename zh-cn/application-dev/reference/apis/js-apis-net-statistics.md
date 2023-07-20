# @ohos.net.statistics (流量管理)

流量管理模块，支持基于网卡/UID的实时流量统计和历史流量统计查询能力。

> **说明：**
> 本模块首批接口从API version 10开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。

## 导入模块

```js
import statistics from '@ohos.net.statistics'
```

## statistics.getIfaceRxBytes<sup>10+</sup>

getIfaceRxBytes(nic: string, callback: AsyncCallback\<number>): void;

获取指定网卡实时下行流量，使用callback方式作为异步方法。

**系统能力**：SystemCapability.Communication.NetManager.Core

**参数：**

| 参数名       | 类型                          | 必填 | 说明                                                         |
| ------------ | ----------------------------- | ---- | ------------------------------------------------------------ |
| nic | string | 是   | 指定查询的网卡名。                   |
| callback | AsyncCallback\<number>         | 是   | 回调函数。当成功获取网卡实时下行流量时，error为undefined，stats为获取到的网卡实时下行流量(单位:字节)；否则为错误对象|

**错误码：**

以下错误码的详细介绍参见[statistics错误码](../errorcodes/errorcode-net-statistics.md)。

| 错误码ID | 错误信息                        |
| ------- | -----------------------------  |
| 401     | Parameter error.             |
| 2100002 | Operation failed. Cannot connect to service.             |
| 2100003 | System internal error.         |
| 2103005 | Failed to read map.             |
| 2103011 | Failed to create map.             |
| 2103012 | Get iface name failed.         |


**示例：**

```js
  statistics.getIfaceRxBytes("wlan0", (error, stats) => {
    console.log(JSON.stringify(error))
    console.log(JSON.stringify(stats))
  })
```

## statistics.getIfaceRxBytes<sup>10+</sup>

getIfaceRxBytes(nic: string): Promise\<number>;

获取指定网卡实时下行流量，使用Promise方式作为异步方法。

**系统能力**：SystemCapability.Communication.NetManager.Core

**参数：**

| 参数名       | 类型                          | 必填 | 说明                                                         |
| ------------ | ----------------------------- | ---- | ------------------------------------------------------------ |
| nic | string | 是   | 指定查询的网卡名。                   |

**返回值：**
| 类型 | 说明 |
| -------- | -------- |
| Promise\<number> | 以Promise形式返回获取结果。返回网卡实时下行流量(单位:字节)。 |

**错误码：**

以下错误码的详细介绍参见[statistics错误码](../errorcodes/errorcode-net-statistics.md)。

| 错误码ID | 错误信息                        |
| ------- | -----------------------------  |
| 401     | Parameter error.             |
| 2100002 | Operation failed. Cannot connect to service.             |
| 2100003 | System internal error.         |
| 2103005 | Failed to read map.             |
| 2103011 | Failed to create map.             |
| 2103012 | Get iface name failed.         |

**示例：**

```js
  statistics.getIfaceRxBytes("wlan0").then(function (stats) {
    console.log(JSON.stringify(stats))
  })
```

## statistics.getIfaceTxBytes<sup>10+</sup>

getIfaceTxBytes(nic: string, callback: AsyncCallback\<number>): void;

获取指定网卡实时上行流量，使用callback方式作为异步方法。

**系统能力**：SystemCapability.Communication.NetManager.Core

**参数：**

| 参数名       | 类型                          | 必填 | 说明                                                         |
| ------------ | ----------------------------- | ---- | ------------------------------------------------------------ |
| nic | string | 是   | 指定查询的网卡名。                   |
| callback | AsyncCallback\<number>         | 是   | 回调函数。当成功获取网卡实时上行流量时，error为undefined，stats为获取到的网卡实时上行流量(单位:字节)；否则为错误对象|

**错误码：**

以下错误码的详细介绍参见[statistics错误码](../errorcodes/errorcode-net-statistics.md)。

| 错误码ID | 错误信息                        |
| ------- | -----------------------------  |
| 401     | Parameter error.             |
| 2100002 | Operation failed. Cannot connect to service.             |
| 2100003 | System internal error.         |
| 2103005 | Failed to read map.             |
| 2103011 | Failed to create map.             |
| 2103012 | Get iface name failed.         |

**示例：**

```js
  statistics.getIfaceTxBytes("wlan0", (error, stats) => {
    console.log(JSON.stringify(error))
    console.log(JSON.stringify(stats))
  })
```

## statistics.getIfaceTxBytes<sup>10+</sup>

getIfaceTxBytes(nic: string): Promise\<number>;

获取指定网卡实时上行流量，使用Promise方式作为异步方法。

**系统能力**：SystemCapability.Communication.NetManager.Core

**参数：**

| 参数名       | 类型                          | 必填 | 说明                                                         |
| ------------ | ----------------------------- | ---- | ------------------------------------------------------------ |
| nic | string | 是   | 指定查询的网卡名。                   |

**返回值：**
| 类型 | 说明 |
| -------- | -------- |
| Promise\<number> | 以Promise形式返回获取结果。返回网卡实时上行流量(单位:字节)。 |

**错误码：**

以下错误码的详细介绍参见[statistics错误码](../errorcodes/errorcode-net-statistics.md)。

| 错误码ID | 错误信息                        |
| ------- | -----------------------------  |
| 401     | Parameter error.             |
| 2100002 | Operation failed. Cannot connect to service.             |
| 2100003 | System internal error.         |
| 2103005 | Failed to read map.             |
| 2103011 | Failed to create map.             |
| 2103012 | Get iface name failed.         |

**示例：**

```js
  statistics.getIfaceTxBytes("wlan0").then(function (stats) {
    console.log(JSON.stringify(stats))
  })
```

## statistics.getCellularRxBytes<sup>10+</sup>

getCellularRxBytes(callback: AsyncCallback\<number>): void;

获取蜂窝实时下行流量，使用callback方式作为异步方法。

**系统能力**：SystemCapability.Communication.NetManager.Core

**参数：**

| 参数名       | 类型                          | 必填 | 说明                                                         |
| ------------ | ----------------------------- | ---- | ------------------------------------------------------------ |
| callback | AsyncCallback\<number>         | 是   | 回调函数。当成功获取蜂窝实时下行流量时，error为undefined，stats为获取到的蜂窝实时下行流量(单位:字节)；否则为错误对象|

**错误码：**

以下错误码的详细介绍参见[statistics错误码](../errorcodes/errorcode-net-statistics.md)。

| 错误码ID | 错误信息                        |
| ------- | -----------------------------  |
| 2100002 | Operation failed. Cannot connect to service.             |
| 2100003 | System internal error.         |
| 2103005 | Failed to read map.             |
| 2103011 | Failed to create map.             |
| 2103012 | Get iface name failed.         |

**示例：**

```js
  statistics.getCellularRxBytes((error, stats) => {
    console.log(JSON.stringify(error))
    console.log(JSON.stringify(stats))
  })
```

## statistics.getCellularRxBytes<sup>10+</sup>

getCellularRxBytes(): Promise\<number>;

获取蜂窝实时下行流量，使用Promise方式作为异步方法。

**系统能力**：SystemCapability.Communication.NetManager.Core

**返回值：**
| 类型 | 说明 |
| -------- | -------- |
| Promise\<number> | 以Promise形式返回获取结果。返回蜂窝实时下行流量(单位:字节)。 |

**错误码：**

以下错误码的详细介绍参见[statistics错误码](../errorcodes/errorcode-net-statistics.md)。

| 错误码ID | 错误信息                        |
| ------- | -----------------------------  |
| 2100002 | Operation failed. Cannot connect to service.             |
| 2100003 | System internal error.         |
| 2103005 | Failed to read map.             |
| 2103011 | Failed to create map.             |
| 2103012 | Get iface name failed.         |

**示例：**

```js
  statistics.getCellularRxBytes().then(function (stats) {
    console.log(JSON.stringify(stats))
  })
```

## statistics.getCellularTxBytes<sup>10+</sup>

getCellularTxBytes(callback: AsyncCallback\<number>): void;

获取蜂窝实时上行流量，使用callback方式作为异步方法。

**系统能力**：SystemCapability.Communication.NetManager.Core

**参数：**

| 参数名       | 类型                          | 必填 | 说明                                                         |
| ------------ | ----------------------------- | ---- | ------------------------------------------------------------ |
| callback | AsyncCallback\<number>         | 是   | 回调函数。当成功获取蜂窝实时上行流量时，error为undefined，stats为获取到的蜂窝实时上行流量(单位:字节)；否则为错误对象|

**错误码：**

以下错误码的详细介绍参见[statistics错误码](../errorcodes/errorcode-net-statistics.md)。

| 错误码ID | 错误信息                        |
| ------- | -----------------------------  |
| 2100002 | Operation failed. Cannot connect to service.             |
| 2100003 | System internal error.         |
| 2103005 | Failed to read map.             |
| 2103011 | Failed to create map.             |
| 2103012 | Get iface name failed.         |

**示例：**

```js
  statistics.getCellularTxBytes((error, stats) => {
    console.log(JSON.stringify(error))
    console.log(JSON.stringify(stats))
  })
```

## statistics.getCellularTxBytes<sup>10+</sup>

getCellularTxBytes(): Promise\<number>;

获取蜂窝实时上行流量，使用Promise方式作为异步方法。

**系统能力**：SystemCapability.Communication.NetManager.Core

**返回值：**
| 类型 | 说明 |
| -------- | -------- |
| Promise\<number> | 以Promise形式返回获取结果。返回蜂窝实时上行流量(单位:字节)。 |

**错误码：**

以下错误码的详细介绍参见[statistics错误码](../errorcodes/errorcode-net-statistics.md)。

| 错误码ID | 错误信息                        |
| ------- | -----------------------------  |
| 2100002 | Operation failed. Cannot connect to service.             |
| 2100003 | System internal error.         |
| 2103005 | Failed to read map.             |
| 2103011 | Failed to create map.             |
| 2103012 | Get iface name failed.         |

**示例：**

```js
  statistics.getCellularTxBytes().then(function (stats) {
    console.log(JSON.stringify(stats))
  })
```

## statistics.getAllRxBytes<sup>10+</sup>

getAllRxBytes(callback: AsyncCallback\<number>): void;

获取所有网卡实时下行流量，使用callback方式作为异步方法。

**系统能力**：SystemCapability.Communication.NetManager.Core

**参数：**

| 参数名       | 类型                          | 必填 | 说明                                                         |
| ------------ | ----------------------------- | ---- | ------------------------------------------------------------ |
| callback | AsyncCallback\<number>         | 是   | 回调函数。当成功获取所有网卡实时下行流量，error为undefined，stats为获取到的所有网卡实时下行流量(单位:字节)；否则为错误对象|

**错误码：**

以下错误码的详细介绍参见[statistics错误码](../errorcodes/errorcode-net-statistics.md)。

| 错误码ID | 错误信息                        |
| ------- | -----------------------------  |
| 2100002 | Operation failed. Cannot connect to service.             |
| 2100003 | System internal error.         |
| 2103005 | Failed to read map.             |
| 2103011 | Failed to create map.             |

**示例：**

```js
  statistics.getAllRxBytes((error, stats) => {
    console.log(JSON.stringify(error))
    console.log(JSON.stringify(stats))
  })
```

## statistics.getAllRxBytes<sup>10+</sup>

getAllRxBytes(): Promise\<number>;

获取所有网卡实时下行流量，使用Promise方式作为异步方法。

**系统能力**：SystemCapability.Communication.NetManager.Core

**返回值：**
| 类型 | 说明 |
| -------- | -------- |
| Promise\<number> | 以Promise形式返回获取结果。返回所有网卡实时下行流量(单位:字节)。 |

**错误码：**

以下错误码的详细介绍参见[statistics错误码](../errorcodes/errorcode-net-statistics.md)。

| 错误码ID | 错误信息                        |
| ------- | -----------------------------  |
| 2100002 | Operation failed. Cannot connect to service.             |
| 2100003 | System internal error.         |
| 2103005 | Failed to read map.             |
| 2103011 | Failed to create map.             |

**示例：**

```js
  statistics.getCellularRxBytes().then(function (stats) {
    console.log(JSON.stringify(stats))
  })
```

## statistics.getAllTxBytes<sup>10+</sup>

getAllTxBytes(callback: AsyncCallback\<number>): void;

获取所有网卡实时上行流量，使用callback方式作为异步方法。

**系统能力**：SystemCapability.Communication.NetManager.Core

**参数：**

| 参数名       | 类型                          | 必填 | 说明                                                         |
| ------------ | ----------------------------- | ---- | ------------------------------------------------------------ |
| callback | AsyncCallback\<number>         | 是   | 回调函数。当成功获取所有网卡实时上行流量，error为undefined，stats为获取到的所有网卡实时上行流量(单位:字节)；否则为错误对象|

**错误码：**

以下错误码的详细介绍参见[statistics错误码](../errorcodes/errorcode-net-statistics.md)。

| 错误码ID | 错误信息                        |
| ------- | -----------------------------  |
| 2100002 | Operation failed. Cannot connect to service.             |
| 2100003 | System internal error.         |
| 2103005 | Failed to read map.             |
| 2103011 | Failed to create map.             |

**示例：**

```js
  statistics.getAllTxBytes((error, stats) => {
    console.log(JSON.stringify(error))
    console.log(JSON.stringify(stats))
  })
```

## statistics.getAllTxBytes<sup>10+</sup>

getAllTxBytes(): Promise\<number>;

获取所有网卡实时上行流量，使用Promise方式作为异步方法。

**系统能力**：SystemCapability.Communication.NetManager.Core

**返回值：**
| 类型 | 说明 |
| -------- | -------- |
| Promise\<number> | 以Promise形式返回获取结果。返回所有网卡实时上行流量(单位:字节)。 |

**错误码：**

以下错误码的详细介绍参见[statistics错误码](../errorcodes/errorcode-net-statistics.md)。

| 错误码ID | 错误信息                        |
| ------- | -----------------------------  |
| 2100002 | Operation failed. Cannot connect to service.             |
| 2100003 | System internal error.         |
| 2103005 | Failed to read map.             |
| 2103011 | Failed to create map.             |

**示例：**

```js
  statistics.getAllTxBytes().then(function (stats) {
    console.log(JSON.stringify(stats))
  })
```

## statistics.getUidRxBytes<sup>10+</sup>

getUidRxBytes(uid: number, callback: AsyncCallback\<number>): void;

获取指定应用实时下行流量，使用callback方式作为异步方法。

**系统能力**：SystemCapability.Communication.NetManager.Core

**参数：**

| 参数名       | 类型                          | 必填 | 说明                                                         |
| ------------ | ----------------------------- | ---- | ------------------------------------------------------------ |
| uid | number | 是   | 指定查询的应用uid。                   |
| callback | AsyncCallback\<number>         | 是   | 回调函数。当成功获取应用实时下行流量时，error为undefined，stats为获取到的应用实时下行流量(单位:字节)；否则为错误对象|

**错误码：**

以下错误码的详细介绍参见[statistics错误码](../errorcodes/errorcode-net-statistics.md)。

| 错误码ID | 错误信息                        |
| ------- | -----------------------------  |
| 401     | Parameter error.             |
| 2100002 | Operation failed. Cannot connect to service.             |
| 2100003 | System internal error.         |
| 2103005 | Failed to read map.             |
| 2103011 | Failed to create map.             |

**示例：**

```js
  statistics.getUidRxBytes(20010038, (error, stats) => {
    console.log(JSON.stringify(error))
    console.log(JSON.stringify(stats))
  })
```

## statistics.getUidRxBytes<sup>10+</sup>

getUidRxBytes(uid: number): Promise\<number>;

获取指定应用实时下行流量，使用Promise方式作为异步方法。

**系统能力**：SystemCapability.Communication.NetManager.Core

**参数：**

| 参数名       | 类型                          | 必填 | 说明                                                         |
| ------------ | ----------------------------- | ---- | ------------------------------------------------------------ |
| uid | number | 是   | 指定查询的应用uid。                   |

**返回值：**
| 类型 | 说明 |
| -------- | -------- |
| Promise\<number> | 以Promise形式返回获取结果。返回指定应用实时下行流量(单位:字节)。 |

**错误码：**

以下错误码的详细介绍参见[statistics错误码](../errorcodes/errorcode-net-statistics.md)。

| 错误码ID | 错误信息                        |
| ------- | -----------------------------  |
| 401     | Parameter error.             |
| 2100002 | Operation failed. Cannot connect to service.             |
| 2100003 | System internal error.         |
| 2103005 | Failed to read map.             |
| 2103011 | Failed to create map.             |

**示例：**

```js
  statistics.getUidRxBytes(20010038).then(function (stats) {
    console.log(JSON.stringify(stats))
  })
```

## statistics.getUidTxBytes<sup>10+</sup>

getUidTxBytes(uid: number, callback: AsyncCallback\<number>): void;

获取指定应用实时上行流量，使用callback方式作为异步方法。

**系统能力**：SystemCapability.Communication.NetManager.Core

**参数：**

| 参数名       | 类型                          | 必填 | 说明                                                         |
| ------------ | ----------------------------- | ---- | ------------------------------------------------------------ |
| uid | number | 是   | 指定查询的应用uid。                   |
| callback | AsyncCallback\<number>         | 是   | 回调函数。当成功获取应用实时上行流量时，error为undefined，stats为获取到的应用实时上行流量(单位:字节)；否则为错误对象|

**错误码：**

以下错误码的详细介绍参见[statistics错误码](../errorcodes/errorcode-net-statistics.md)。

| 错误码ID | 错误信息                        |
| ------- | -----------------------------  |
| 401     | Parameter error.             |
| 2100002 | Operation failed. Cannot connect to service.             |
| 2100003 | System internal error.         |
| 2103005 | Failed to read map.             |
| 2103011 | Failed to create map.             |

**示例：**

```js
  statistics.getUidTxBytes(20010038, (error, stats) => {
    console.log(JSON.stringify(error))
    console.log(JSON.stringify(stats))
  })
```

## statistics.getUidTxBytes<sup>10+</sup>

getUidTxBytes(uid: number): Promise\<number>;

获取指定应用实时上行流量，使用Promise方式作为异步方法。

**系统能力**：SystemCapability.Communication.NetManager.Core

**参数：**

| 参数名       | 类型                          | 必填 | 说明                                                         |
| ------------ | ----------------------------- | ---- | ------------------------------------------------------------ |
| uid | number | 是   | 指定查询的应用uid。                   |

**返回值：**
| 类型 | 说明 |
| -------- | -------- |
| Promise\<number> | 以Promise形式返回获取结果。返回指定应用实时上行流量(单位:字节)。 |

**错误码：**

以下错误码的详细介绍参见[statistics错误码](../errorcodes/errorcode-net-statistics.md)。

| 错误码ID | 错误信息                        |
| ------- | -----------------------------  |
| 401     | Parameter error.             |
| 2100002 | Operation failed. Cannot connect to service.             |
| 2100003 | System internal error.         |
| 2103005 | Failed to read map.             |
| 2103011 | Failed to create map.             |

**示例：**

```js
  statistics.getUidTxBytes(20010038).then(function (stats) {
    console.log(JSON.stringify(stats))
  })
```

## statistics.on('netStatsChange')<sup>10+</sup>

on(type: 'netStatsChange', callback: Callback\<{ iface: string, uid?: number }>): void

订阅流量改变事件通知。

**系统接口**：此接口为系统接口。

**需要权限**：ohos.permission.GET_NETWORK_STATS

**系统能力**：SystemCapability.Communication.NetManager.Core

**参数：**

| 参数名   | 类型                                    | 必填 | 说明       |
| -------- | --------------------------------------- | ---- | ---------- |
| type     | string                             | 是   | 订阅事件，固定为'netStatsChange'。|
| callback | Callback\<{ iface: string, uid?: number }\> | 是   | 当流量有改变时触发回调函数。<br>iface：网卡名称。<br>uid：应用uid |

**错误码：**

以下错误码的详细介绍参见[statistics错误码](../errorcodes/errorcode-net-statistics.md)。

| 错误码ID | 错误信息                                      |
| ------- | -------------------------------------------- |
| 201     | Permission denied.             |
| 202     | Non-system applications use system APIs.             |
| 401     | Parameter error.         |
| 2100002 | Operation failed. Cannot connect to service.             |
| 2100003 | System internal error.             |

**示例：**

```js
 statistics.on('netStatsChange', (data) => {
  console.log('on netStatsChange' + JSON.stringify(data));
});
```

## statistics.off('netStatsChange')<sup>10+</sup>

off(type: 'netStatsChange', callback?: Callback\<{ iface: string, uid?: number }>): void;

取消订阅流量改变事件通知。

**系统接口**：此接口为系统接口。

**需要权限**：ohos.permission.GET_NETWORK_STATS

**系统能力**：SystemCapability.Communication.NetManager.Core

**参数：**

| 参数名   | 类型                                    | 必填 | 说明       |
| -------- | --------------------------------------- | ---- | ---------- |
| type   | string | 是   | 注销订阅事件，固定为'netStatsChange'。 |
| callback | Callback\<{ iface: string, uid?: number }\> | 否   | 当流量有改变时触发回调函数。<br>iface：网卡名称。<br>uid：应用uid |

**错误码：**

以下错误码的详细介绍参见[statistics错误码](../errorcodes/errorcode-net-statistics.md)。

| 错误码ID | 错误信息                                      |
| ------- | -------------------------------------------- |
| 201     | Permission denied.             |
| 202     | Non-system applications use system APIs.             |
| 401     | Parameter error.         |
| 2100002 | Operation failed. Cannot connect to service.             |
| 2100003 | System internal error.             |

**示例：**

```js
let callback = data => {
    console.log("on netStatsChange, data:" + JSON.stringify(data));
}
statistics.on('netStatsChange', callback);
// 可以指定传入on中的callback取消一个订阅，也可以不指定callback清空所有订阅。
statistics.off('netStatsChange', callback);
statistics.off('netStatsChange');
```

## statistics.getTrafficStatsByIface<sup>10+</sup>

getTrafficStatsByIface(ifaceInfo: IfaceInfo, callback: AsyncCallback\<NetStatsInfo>): void;

获取指定网卡历史流量信息，使用callback方式作为异步方法。

**系统接口**：此接口为系统接口。

**需要权限**：ohos.permission.GET_NETWORK_STATS

**系统能力**：SystemCapability.Communication.NetManager.Core

**参数：**

| 参数名       | 类型                          | 必填 | 说明                                                         |
| ------------ | ----------------------------- | ---- | ------------------------------------------------------------ |
| ifaceInfo | [IfaceInfo](#ifaceinfo10) | 是   | 指定查询的网卡信息，参见[IfaceInfo](#ifaceinfo10)。                   |
| callback | AsyncCallback\<[NetStatsInfo](#netstatsinfo10)>         | 是   | 回调函数。成功时statsInfo返回包含网卡历史流量信息，error为undefined，否则为错误对象|

**错误码：**

以下错误码的详细介绍参见[statistics错误码](../errorcodes/errorcode-net-statistics.md)。

| 错误码ID | 错误信息                        |
| ------- | -----------------------------  |
| 201     | Permission denied.             |
| 202     | Non-system applications use system APIs.             |
| 401     | Parameter error.         |
| 2100001 | Invalid parameter value.         |
| 2100002 | Operation failed. Cannot connect to service.             |
| 2100003 | System internal error.             |
| 2103017 | Read data from database failed.             |

**示例：**

```js
  let ifaceInfo = {
    iface: "wlan0",
    startTime: 1685948465,
    endTime: 16859485670
  }

  statistics.getTrafficStatsByIface(ifaceInfo), (error, statsInfo) => {
    console.log(JSON.stringify(error))
    console.log("getTrafficStatsByIface bytes of received = " + JSON.stringify(statsInfo.rxBytes));
    console.log("getTrafficStatsByIface bytes of sent = " + JSON.stringify(statsInfo.txBytes));
    console.log("getTrafficStatsByIface packets of received = " + JSON.stringify(statsInfo.rxPackets));
    console.log("getTrafficStatsByIface packets of sent = " + JSON.stringify(statsInfo.txPackets));
  });
```

## statistics.getTrafficStatsByIface<sup>10+</sup>

getTrafficStatsByIface(ifaceInfo: IfaceInfo): Promise\<NetStatsInfo>;

获取指定网卡历史流量信息，使用Promise方式作为异步方法。

**系统接口**：此接口为系统接口。

**需要权限**：ohos.permission.GET_NETWORK_STATS

**系统能力**：SystemCapability.Communication.NetManager.Core

| 参数名       | 类型                          | 必填 | 说明                                                         |
| ------------ | ----------------------------- | ---- | ------------------------------------------------------------ |
| ifaceInfo | [IfaceInfo](#ifaceinfo10) | 是   | 指定查询的网卡信息，参见[IfaceInfo](#ifaceinfo10)。                   |

**返回值：**
| 类型 | 说明 |
| -------- | -------- |
| Promise\<[NetStatsInfo](#netstatsinfo10)> | 以Promise形式返回获取结果,返回网卡历史流量信息。 |

**错误码：**

以下错误码的详细介绍参见[statistics错误码](../errorcodes/errorcode-net-statistics.md)。

| 错误码ID | 错误信息                        |
| ------- | -----------------------------  |
| 201     | Permission denied.             |
| 202     | Non-system applications use system APIs.             |
| 401     | Parameter error.         |
| 2100001 | Invalid parameter value.         |
| 2100002 | Operation failed. Cannot connect to service.             |
| 2100003 | System internal error.             |
| 2103017 | Read data from database failed.             |

**示例：**

```js
  let ifaceInfo = {
    iface: "wlan0",
    startTime: 1685948465,
    endTime: 16859485670
  }

  statistics.getTrafficStatsByIface().then(function (statsInfo) {
    console.log("getTrafficStatsByIface bytes of received = " + JSON.stringify(statsInfo.rxBytes));
    console.log("getTrafficStatsByIface bytes of sent = " + JSON.stringify(statsInfo.txBytes));
    console.log("getTrafficStatsByIface packets of received = " + JSON.stringify(statsInfo.rxPackets));
    console.log("getTrafficStatsByIface packets of sent = " + JSON.stringify(statsInfo.txPackets));
  })
```

## statistics.getTrafficStatsByUid<sup>10+</sup>

getTrafficStatsByUid(uidInfo: UidInfo, callback: AsyncCallback\<NetStatsInfo>): void;

获取指定应用历史流量信息，使用callback方式作为异步方法。

**系统接口**：此接口为系统接口。

**需要权限**：ohos.permission.GET_NETWORK_STATS

**系统能力**：SystemCapability.Communication.NetManager.Core

**参数：**

| 参数名       | 类型                          | 必填 | 说明                                                         |
| ------------ | ----------------------------- | ---- | ------------------------------------------------------------ |
| uidInfo | [UidInfo](#uidinfo10) | 是   | 指定查询的应用信息，参见[UidInfo](#uidinfo10)。                   |
| callback | AsyncCallback\<[NetStatsInfo](#netstatsinfo10)>         | 是   | 回调函数。成功时statsInfo返回包含应用历史流量信息，error为undefined，否则为错误对象|

**错误码：**

以下错误码的详细介绍参见[statistics错误码](../errorcodes/errorcode-net-statistics.md)。

| 错误码ID | 错误信息                        |
| ------- | -----------------------------  |
| 201     | Permission denied.             |
| 202     | Non-system applications use system APIs.             |
| 401     | Parameter error.         |
| 2100001 | Invalid parameter value.         |
| 2100002 | Operation failed. Cannot connect to service.             |
| 2100003 | System internal error.             |
| 2103017 | Read data from database failed.             |

**示例：**

```js
  let uidInfo = {
    ifaceInfo: {
      iface: "wlan0",
      startTime: 1685948465,
      endTime: 16859485670
    },
    uid: 20010037
  }

  statistics.getTrafficStatsByUid(uidInfo), (error, statsInfo) => {
    console.log(JSON.stringify(error))
    console.log("getTrafficStatsByUid bytes of received = " + JSON.stringify(statsInfo.rxBytes));
    console.log("getTrafficStatsByUid bytes of sent = " + JSON.stringify(statsInfo.txBytes));
    console.log("getTrafficStatsByUid packets of received = " + JSON.stringify(statsInfo.rxPackets));
    console.log("getTrafficStatsByUid packets of sent = " + JSON.stringify(statsInfo.txPackets));
  });
```

## statistics.getTrafficStatsByUid<sup>10+</sup>

getTrafficStatsByUid(uidInfo: UidInfo): Promise\<NetStatsInfo>;

获取指定应用历史流量信息，使用Promise方式作为异步方法。

**系统接口**：此接口为系统接口。

**需要权限**：ohos.permission.GET_NETWORK_STATS

**系统能力**：SystemCapability.Communication.NetManager.Core

**参数：**

| 参数名       | 类型                          | 必填 | 说明                                                         |
| ------------ | ----------------------------- | ---- | ------------------------------------------------------------ |
| uidInfo | [UidInfo](#uidinfo10) | 是   | 指定查询的应用信息，参见[UidInfo](#uidinfo10)。                   |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| Promise\<[NetStatsInfo](#netstatsinfo10)> | 以Promise形式返回获取结果,返回应用历史流量信息。 |

**错误码：**

以下错误码的详细介绍参见[statistics错误码](../errorcodes/errorcode-net-statistics.md)。

| 错误码ID | 错误信息                        |
| ------- | -----------------------------  |
| 201     | Permission denied.             |
| 202     | Non-system applications use system APIs.             |
| 401     | Parameter error.         |
| 2100001 | Invalid parameter value.         |
| 2100002 | Operation failed. Cannot connect to service.             |
| 2100003 | System internal error.             |
| 2103017 | Read data from database failed.             |

**示例：**

```js
  let uidInfo = {
    ifaceInfo: {
      iface: "wlan0",
      startTime: 1685948465,
      endTime: 16859485670
    },
    uid: 20010037
  }

  statistics.getTrafficStatsByUid(uidInfo).then(function (statsInfo) {
    console.log("getTrafficStatsByUid bytes of received = " + JSON.stringify(statsInfo.rxBytes));
    console.log("getTrafficStatsByUid bytes of sent = " + JSON.stringify(statsInfo.txBytes));
    console.log("getTrafficStatsByUid packets of received = " + JSON.stringify(statsInfo.rxPackets));
    console.log("getTrafficStatsByUid packets of sent = " + JSON.stringify(statsInfo.txPackets));
  })
```

## IfaceInfo<sup>10+</sup>

查询网卡历史流量参数信息。

**系统接口**：此接口为系统接口。

**系统能力**：SystemCapability.Communication.NetManager.Core

| 名称                  | 类型                                | 必填 | 说明                     |
| --------------------- | ---------------------------------- | --- | ------------------------ |
| iface     | string    |  是 |  查询的网卡名。|
| startTime | number    |  是 |  查询的开始时间(时间戳;单位：秒)。   |
| endTime   | number    |  是 |  查询的结束时间(时间戳;单位：秒)。   |

## UidInfo<sup>10+</sup>

查询应用历史流量参数信息。

**系统接口**：此接口为系统接口。

**系统能力**：SystemCapability.Communication.NetManager.Core

| 名称                  | 类型                                | 必填 | 说明                     |
| --------------------- | ---------------------------------- | --- | ------------------------ |
| ifaceInfo   | IfaceInfo\<[IfaceInfo](#ifaceinfo10)> |  是 |  需查询的网卡和时间参数信息|
| uid         | number           |  是 |  需查询的应用uid|

## NetStatsInfo<sup>10+</sup>

获取的历史流量信息。

**系统接口**：此接口为系统接口。

**系统能力**：SystemCapability.Communication.NetManager.Core

| 名称                  | 类型                                | 必填 | 说明                     |
| --------------------- | ---------------------------------- | --- | ------------------------ |
| rxBytes   | number |  是 |  流量下行数据(单位:字节)|
| txBytes   | number |  是 |  流量上行数据(单位:字节)|
| rxPackets | number |  是 |  流量下行包个数|
| txPackets | number |  是 |  流量上行包个数|