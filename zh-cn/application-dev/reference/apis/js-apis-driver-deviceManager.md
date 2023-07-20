# @ohos.driver.deviceManager (外设管理)

本模块主要提供管理外部设备的相关功能，包括查询设备列表、绑定设备和解除绑定设备。

>  **说明：**
> 
> 本模块首批接口从API version 10开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。

## 导入模块

```js
import deviceManager from "@ohos.driver.deviceManager";
```

## deviceManager.queryDevices

queryDevices(busType?: number): Array&lt;Readonly&lt;Device&gt;&gt;

获取接入主设备的外部设备列表。如果没有设备接入，那么将会返回一个空的列表。

**系统能力：**  SystemCapability.Driver.ExternalDevice

**参数：**

| 参数名  | 类型   | 必填 | 说明                                 |
| ------- | ------ | ---- | ------------------------------------ |
| busType | number | 否   | 设备总线类型，不填则查找所有类型设备 |

**返回值：**

| 类型                                           | 说明           |
| ---------------------------------------------- | -------------- |
| Array&lt;Readonly&lt;[Device](#device)&gt;&gt; | 设备信息列表。 |

**错误码：**

| 错误码ID | 错误信息                                 |
| -------- | ---------------------------------------- |
| 401      | The parameter check failed.              |
| 22900001 | ExternalDeviceManager service exception. |

**示例：**

```js
try {
  let devices = deviceManager.queryDevices(deviceManager.BusType.USB);
  for (let item of devices) {
    console.info('Device id is ${item.deviceId}')
  }
} catch (error) {
  console.error('Failed to query device. Code is ${error.code}, message is ${error.message}');
}
```

## deviceManager.bindDevice

bindDevice(deviceId: number, onDisconnect: AsyncCallback&lt;number&gt;,
  callback: AsyncCallback&lt;{deviceId: number, remote: rpc.IRemoteObject}&gt;): void;

根据queryDevices()返回的设备信息绑定设备。

需要调用[deviceManager.queryDevices](#devicemanagerquerydevices)获取设备信息以及device。

**系统能力：**  SystemCapability.Driver.ExternalDevice

**参数：**

| 参数名       | 类型                                                                                                 | 必填 | 说明                                   |
| ------------ | ---------------------------------------------------------------------------------------------------- | ---- | -------------------------------------- |
| deviceId     | number                                                                                               | 是   | 设备ID，通过queryDevices获得           |
| onDisconnect | AsyncCallback&lt;number&gt;                                                                          | 是   | 绑定设备断开的回调                     |
| callback     | AsyncCallback&lt;{deviceId: number, remote: [rpc.IRemoteObject](./js-apis-rpc.md#iremoteobject)}&gt; | 是   | 绑定设备的回调，返回绑定设备的通信对象 |

**错误码：**

| 错误码ID | 错误信息                                 |
| -------- | ---------------------------------------- |
| 401      | The parameter check failed.              |
| 22900001 | ExternalDeviceManager service exception. |

**示例：**

```js
try {
  deviceManager.bindDevice(device.deviceId, (error, data) => {
    console.error('Device is disconnected');
  }, (error, data) => {
    if (error) {
      console.error('bindDevice async fail. Code is ${error.code}, message is ${error.message}');
      return;
    }
    console.info('bindDevice success');
  });
} catch (error) {
  console.error('bindDevice fail. Code is ${error.code}, message is ${error.message}');
}
```

## deviceManager.bindDevice

bindDevice(deviceId: number, onDisconnect: AsyncCallback&lt;number&gt;): Promise&lt;{deviceId: number,
  remote: rpc.IRemoteObject}&gt;;

根据queryDevices()返回的设备信息绑定设备。

需要调用[deviceManager.queryDevices](#devicemanagerquerydevices)获取设备信息以及device。

**系统能力：**  SystemCapability.Driver.ExternalDevice

**参数：**

| 参数名       | 类型                        | 必填 | 说明                         |
| ------------ | --------------------------- | ---- | ---------------------------- |
| deviceId     | number                      | 是   | 设备ID，通过queryDevices获得 |
| onDisconnect | AsyncCallback&lt;number&gt; | 是   | 绑定设备断开的回调           |

**返回值：** 

| 类型                                                                                           | 说明                                         |
| ---------------------------------------------------------------------------------------------- | -------------------------------------------- |
| Promise&lt;{deviceId: number, remote: [rpc.IRemoteObject](./js-apis-rpc.md#iremoteobject)}&gt; | Promise对象，返回设备ID和IRemoteObject对象。 |

**错误码：**

| 错误码ID | 错误信息                                 |
| -------- | ---------------------------------------- |
| 401      | The parameter check failed.              |
| 22900001 | ExternalDeviceManager service exception. |

**示例：**

```js
try {
  deviceManager.bindDevice(matchDevice.deviceId, (error, data) => {
    console.error('Device is disconnected');
  }).then(data => {
    console.info('bindDevice success');
  }, error => {
    console.error('bindDevice async fail. Code is ${error.code}, message is ${error.message}');
  });
} catch (error) {
  console.error('bindDevice fail. Code is ${error.code}, message is ${error.message}');
}
```

## deviceManager.unbindDevice

unbindDevice(deviceId: number, callback: AsyncCallback&lt;number&gt;): void

解除设备绑定。

**系统能力：**  SystemCapability.Driver.ExternalDevice

**参数：**

| 参数名   | 类型                        | 必填 | 说明                           |
| -------- | --------------------------- | ---- | ------------------------------ |
| deviceId | number                      | 是   | 设备ID，通过queryDevices获得。 |
| callback | AsyncCallback&lt;number&gt; | 是   | 解绑完成的回调。               |

**错误码：**

| 错误码ID | 错误信息                                 |
| -------- | ---------------------------------------- |
| 401      | The parameter check failed.              |
| 22900001 | ExternalDeviceManager service exception. |

**示例：**

```js
try {
  deviceManager.unbindDevice(matchDevice.deviceId, (error, data) => {
  if (error) {
    console.error('unbindDevice async fail. Code is ${error.code}, message is ${error.message}');
    return;
  }
  console.info('unbindDevice success');
  });
} catch (error) {
  console.error('unbindDevice fail. Code is ${error.code}, message is ${error.message}');
}
```
## deviceManager.unbindDevice

unbindDevice(deviceId: number): Promise&lt;number&gt;

解除设备绑定。

**系统能力：**  SystemCapability.Driver.ExternalDevice

**参数：**

| 参数名   | 类型   | 必填 | 说明                           |
| -------- | ------ | ---- | ------------------------------ |
| deviceId | number | 是   | 设备ID，通过queryDevices获得。 |

**错误码：**

| 错误码ID | 错误信息                                 |
| -------- | ---------------------------------------- |
| 401      | The parameter check failed.              |
| 22900001 | ExternalDeviceManager service exception. |

**返回值：** 

| 类型                  | 说明                      |
| --------------------- | ------------------------- |
| Promise&lt;number&gt; | Promise对象，返回设备ID。 |

**示例：**

```js
try {
  deviceManager.unbindDevice(matchDevice.deviceId).then(data => {
    console.info('unbindDevice success');
  }, error => {
    console.error('unbindDevice async fail. Code is ${error.code}, message is ${error.message}');
  });
} catch (error) {
  console.error('unbindDevice fail. Code is ${error.code}, message is ${error.message}');
}
```

## Device

外设信息。

**系统能力：** SystemCapability.Driver.ExternalDevice

| 名称        | 类型                | 必填 | 说明       |
| ----------- | ------------------- | ---- | ---------- |
| busType     | [BusType](#bustype) | 是   | 总线类型。 |
| deviceId    | number              | 是   | 设备ID。   |
| description | string              | 是   | 设备描述。 |

## USBDevice

USB设备信息。

**系统能力：** SystemCapability.Driver.ExternalDevice

| 名称      | 类型   | 必填 | 说明                |
| --------- | ------ | ---- | ------------------- |
| vendorId  | number | 是   | USB设备Vendor ID。  |
| productId | number | 是   | USB设备Product ID。 |

## BusType

设备总线类型。

**系统能力：** SystemCapability.Driver.ExternalDevice

| 名称 | 值  | 说明          |
| ---- | --- | ------------- |
| USB  | 1   | USB总线类型。 |