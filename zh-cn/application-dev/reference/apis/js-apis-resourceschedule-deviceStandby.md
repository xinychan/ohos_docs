# @ohos.resourceschedule.deviceStandby（设备待机模块）
当设备长时间未被使用或通过按键，可以使设备进入待机模式。待机模式不影响应用使用，还可以延长电池续航时间。通过本模块接口，可查询设备或应用是否为待机模式，以及为应用申请或取消待机资源管控。

>  **说明**:
>   
> 本模块首批接口从API version 10开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。<br>

## 导入模块

```js
import deviceStandby from '@ohos.resourceschedule.deviceStandby';
```

## deviceStandby.getExemptedApps

getExemptedApps(resourceTypes: number, callback: AsyncCallback<Array&lt;ExemptedAppInfo&gt;>): void;

获取进入待机模式的应用名单，使用Callback异步回调。

**系统能力:** SystemCapability.ResourceSchedule.DeviceStandby

**需要权限:** ohos.permission.DEVICE_STANDBY_EXEMPTION

**系统API:** 此接口为系统接口。

**参数**：

| 参数名      | 类型                   | 必填   | 说明                             |
| -------- | -------------------- | ---- | ------------------------------ |
| [ResourceTypes](#resourcetype)|number | 是    | 资源类型。 |
| callback | AsyncCallback<Array&lt;[ExemptedAppInfo](#exemptedappinfo)&gt;> | 是    |豁免应用信息 。|

**错误码**：

以下错误码的详细介绍请参见[后台任务错误码](../errorcodes/errorcode-backgroundTaskMgr.md)。

| 错误码ID  | 错误信息             |
| ---- | --------------------- |
| 9800001 | Memory operation failed. |
| 9800002 | Parcel operation failed. |
| 9800003 | Inner transact failed. |
| 9800004 | System service operation failed. |
| 18700001 | Caller information verification failed. |

**示例**：

```js
try{
deviceStandby.getExemptedApps(resourceTypes, (err, res) => {
  if (err) {
    console.log('DEVICE_STANDBY getExemptedApps callback failed. code is: ' + err.code + ',message is: ' + err.message);
  } else {
    console.log('DEVICE_STANDBY getExemptedApps callback success.');
    for (let i = 0; i < res.length; i++) {
      console.log('DEVICE_STANDBY getExemptedApps callback result ' + JSON.stringify(res[i]));
    }
  }
});
} catch (error) {
console.log('DEVICE_STANDBY getExemptedApps throw error, code is: ' + error.code + ',message is: ' + error.message);
}
```

## deviceStandby.getExemptedApps

getExemptedApps(resourceTypes: number): Promise<Array&lt;ExemptedAppInfo&gt;>;

获取进入待机模式的应用名单，使用Promise异步回调。

**系统能力:** SystemCapability.ResourceSchedule.DeviceStandby

**需要权限:** ohos.permission.DEVICE_STANDBY_EXEMPTION

**系统API:** 此接口为系统接口。

**参数**：

| 参数名      | 类型                   | 必填   | 说明                             |
| -------- | -------------------- | ---- | ------------------------------ |
| [ResourceTypes](#resourcetype)|number | 是    |资源类型。|

**返回值**：

| 类型                    | 说明                                       |
| --------------------- | ---------------------------------------- |
| Promise<Array&lt;[ExemptedAppInfo](#exemptedappinfo)&gt;> | 豁免应用信息。 |

**错误码**：

以下错误码的详细介绍请参见[后台任务错误码](../errorcodes/errorcode-backgroundTaskMgr.md)。

| 错误码ID  | 错误信息             |
| ---- | --------------------- |
| 9800001 | Memory operation failed. |
| 9800002 | Parcel operation failed. |
| 9800003 | Inner transact failed. |
| 9800004 | System service operation failed. |
| 18700001 | Caller information verification failed. |

**示例**：

```js
try{
deviceStandby.getExemptedApps(resourceTypes).then( res => {
  console.log('DEVICE_STANDBY getExemptedApps promise success.');
  for (let i = 0; i < res.length; i++) {
    console.log('DEVICE_STANDBY getExemptedApps promise result ' + JSON.stringify(res[i]));
  }
}).catch( err => {
  console.log('DEVICE_STANDBY getExemptedApps promise failed. code is: ' + err.code + ',message is: ' + err.message);
});
} catch (error) {
console.log('DEVICE_STANDBY getExemptedApps throw error, code is: ' + error.code + ',message is: ' + error.message);
}
```

## deviceStandby.requestExemptionResource

requestExemptionResource(request: ResourceRequest): void;

应用订阅申请豁免，使应用临时不进入待机管控。

**系统能力:** SystemCapability.ResourceSchedule.DeviceStandby.Exemption

**需要权限:** ohos.permission.DEVICE_STANDBY_EXEMPTION

**系统API:** 此接口为系统接口。

**参数**：

| 参数名      | 类型                   | 必填   | 说明                             |
| -------- | -------------------- | ---- | ------------------------------ |
| request |[ResourceRequest](#resourcerequest)| 是    | 资源请求。 |

**错误码**：

以下错误码的详细介绍请参见[后台任务错误码](../errorcodes/errorcode-backgroundTaskMgr.md)。

| 错误码ID  | 错误信息             |
| ---- | --------------------- |
| 9800001 | Memory operation failed. |
| 9800002 | Parcel operation failed. |
| 9800003 | Inner transact failed. |
| 9800004 | System service operation failed. |
| 18700001 | Caller information verification failed. |

**示例**：

```js
let resRequest = {
  resourceTypes: 1,
  uid:10003,
  name:"com.example.app",
  duration:10,
  reason:"apply",
};
// 异步方法promise方式
try{
deviceStandby.requestExemptionResource(resRequest).then( () => {
  console.log('DEVICE_STANDBY requestExemptionResource promise succeeded.');
}).catch( err => {
  console.log('DEVICE_STANDBY requestExemptionResource promise failed. code is: ' + err.code + ',message is: ' + err.message);
});
} catch (error) {
console.log('DEVICE_STANDBY requestExemptionResource throw error, code is: ' + error.code + ',message is: ' + error.message);
}

// 异步方法callback方式
try{
deviceStandby.requestExemptionResource(resRequest, (err) => {
   if (err) {
      console.log('DEVICE_STANDBY requestExemptionResource callback failed. code is: ' + err.code + ',message is: ' + err.message);
  } else {
      console.log('DEVICE_STANDBY requestExemptionResource callback succeeded.');
  }
});
} catch (error) {
console.log('DEVICE_STANDBY requestExemptionResource throw error, code is: ' + error.code + ',message is: ' + error.message);
}
```

## deviceStandby.releaseExemptionResource

releaseExemptionResource(request: ResourceRequest): void;

取消应用订阅申请豁免。

**系统能力:** SystemCapability.ResourceSchedule.DeviceStandby.Exemption

**需要权限:** ohos.permission.DEVICE_STANDBY_EXEMPTION

**系统API:** 此接口为系统接口。

**参数**：

| 参数名      | 类型                   | 必填   | 说明                             |
| -------- | -------------------- | ---- | ------------------------------ |
| request |[ResourceRequest](#resourcerequest)| 是    | 资源请求 。|

**错误码**：

以下错误码的详细介绍请参见[后台任务错误码](../errorcodes/errorcode-backgroundTaskMgr.md)。

| 错误码ID  | 错误信息             |
| ---- | --------------------- |
| 9800001 | Memory operation failed. |
| 9800002 | Parcel operation failed. |
| 9800003 | Inner transact failed. |
| 9800004 | System service operation failed. |
| 18700001 | Caller information verification failed. |

**示例**：

```js
let resRequest = {
  resourceTypes: 1,
  uid:10003,
  name:"com.demo.app",
  duration:10,
  reason:"unapply",
};
// 异步方法promise方式
try{
deviceStandby.releaseExemptionResource(resRequest).then( () => {
  console.log('DEVICE_STANDBY releaseExemptionResource promise succeeded.');
}).catch( err => {
  console.log('DEVICE_STANDBY releaseExemptionResource promise failed. code is: ' + err.code + ',message is: ' + err.message);
});
} catch (error) {
console.log('DEVICE_STANDBY releaseExemptionResource throw error, code is: ' + error.code + ',message is: ' + error.message);
}

// 异步方法callback方式
try{
deviceStandby.releaseExemptionResource(resRequest, (err) => {
  if (err) {
    console.log('DEVICE_STANDBY releaseExemptionResource callback failed. code is: ' + err.code + ',message is: ' + err.message);
  } else {
    console.log('DEVICE_STANDBY releaseExemptionResource callback succeeded.');
  }
});
} catch (error) {
console.log('DEVICE_STANDBY releaseExemptionResource throw error, code is: ' + error.code + ',message is: ' + error.message);
}
```

## ResourceType

非待机应用资源枚举。

**需要权限:** ohos.permission.DEVICE_STANDBY_EXEMPTION

**系统API:** 此接口为系统接口。

|名称   |值   |说明|
| ------------ | ------------ |--------------|
|NETWORK    |1   |网络访问资源|
|RUNNING_LOCK    |2   |cpu-runninglock资源|
|TIMER     |4   | timer任务资源|
|WORK_SCHEDULER     |8   | work任务资源|
|AUTO_SYNC      |16   | 自动同步的资源 |
|PUSH     |32   | pushkit资源|
|FREEZE       |64   | 冻结应用资源|

## ExemptedAppInfo 

豁免应用信息，未进入待机管控的应用信息。

**需要权限:** ohos.permission.DEVICE_STANDBY_EXEMPTION

**系统API:** 此接口为系统接口。

|名称  |类型   | 必填   |说明   |
| ------------ | ------------ |------------ | ------------ |
|[resourceTypes](#resourcetype)   | number  | 是   |应用的资源类型   |
|name   |string   | 是   |  应用名  |
|duration   | number  | 是   | 豁免时长 |

## ResourceRequest

待机资源请求体。

**需要权限:** ohos.permission.DEVICE_STANDBY_EXEMPTION

**系统API:** 此接口为系统接口。

|名称   |类型   | 必填   |说明   |
| ------------ | ------------ |------------| ------------ |
|[resourceTypes](#resourcetype)   | number  | 是   |应用的资源类型   |
|uid   | number  | 是   |应用uid   |
|name   |string   | 是   | 应用名称  |
|duration   | number  | 是   | 豁免时长 |
|reason   |string   | 是   |  申请原因  |