# @ohos.app.ability.appManager (appManager)

appManager模块提供App管理的能力，包括查询当前是否处于稳定性测试场景、查询是否为ram受限设备、获取应用程序的内存大小、获取有关运行进程的信息等。

> **说明：**
> 
> 本模块首批接口从API version 9 开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。

## 导入模块

```ts
import appManager from '@ohos.app.ability.appManager';
```

## appManager.isRunningInStabilityTest

static isRunningInStabilityTest(callback: AsyncCallback&lt;boolean&gt;): void

查询当前是否处于稳定性测试场景。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**参数：**

  | 参数名 | 类型 | 必填 | 说明 | 
  | -------- | -------- | -------- | -------- |
  | callback | AsyncCallback&lt;boolean&gt; | 是 |以回调方式返回接口运行结果及当前是否处于稳定性测试场景，可进行错误处理或其他自定义处理。true: 处于稳定性测试场景，false：处于非稳定性测试场景。  | 

**错误码**：

| 错误码ID | 错误信息 |
| ------- | -------- |
| 16000050 | Internal error. |

以上错误码详细介绍请参考[errcode-ability](../errorcodes/errorcode-ability.md)。

**示例：**

```ts
import appManager from '@ohos.app.ability.appManager';

appManager.isRunningInStabilityTest((err, flag) => {
    if (err) {
        console.error(`isRunningInStabilityTest fail, err: ${JSON.stringify(err)}`);
    } else {
        console.log(`The result of isRunningInStabilityTest is: ${JSON.stringify(flag)}`);
    }
});  
```


## appManager.isRunningInStabilityTest

static isRunningInStabilityTest(): Promise&lt;boolean&gt;

查询当前是否处于稳定性测试场景。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**返回值：**

  | 类型 | 说明 | 
  | -------- | -------- |
  | Promise&lt;boolean&gt; | 以Promise方式返回接口运行结果及当前是否处于稳定性测试场景，可进行错误处理或其他自定义处理。true: 处于稳定性测试场景，false：处于非稳定性测试场景。 | 

**错误码**：

| 错误码ID | 错误信息 |
| ------- | -------- |
| 16000050 | Internal error. |

以上错误码详细介绍请参考[errcode-ability](../errorcodes/errorcode-ability.md)。

**示例：**

```ts
import appManager from '@ohos.app.ability.appManager';

appManager.isRunningInStabilityTest().then((flag) => {
    console.log(`The result of isRunningInStabilityTest is: ${JSON.stringify(flag)}`);
}).catch((error) => {
    console.error(`error: ${JSON.stringify(error)}`);
});
```


## appManager.isRamConstrainedDevice

isRamConstrainedDevice(): Promise\<boolean>;

查询是否为ram受限设备。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**返回值：**

  | 类型 | 说明 | 
  | -------- | -------- |
  | Promise&lt;boolean&gt; | 以Promise方式返回接口运行结果及当前设备是否为ram受限设备，可进行错误处理或其他自定义处理。true：当前设备为ram受限设备，false：当前设备为非ram受限设备。 | 

**错误码**：

| 错误码ID | 错误信息 |
| ------- | -------- |
| 16000050 | Internal error. |

以上错误码详细介绍请参考[errcode-ability](../errorcodes/errorcode-ability.md)。

**示例：**

```ts
import appManager from '@ohos.app.ability.appManager';

appManager.isRamConstrainedDevice().then((data) => {
    console.log(`The result of isRamConstrainedDevice is: ${JSON.stringify(data)}`);
}).catch((error) => {
    console.error(`error: ${JSON.stringify(error)}`);
});
```

## appManager.isRamConstrainedDevice

isRamConstrainedDevice(callback: AsyncCallback\<boolean>): void;

查询是否为ram受限设备。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**参数：**

  | 参数名 | 类型 | 必填 | 说明 | 
  | -------- | -------- | -------- | -------- |
  | callback | AsyncCallback&lt;boolean&gt; | 是 |以回调方式返回接口运行结果及当前设备是否为ram受限设备，可进行错误处理或其他自定义处理。true：当前设备为ram受限设备，false：当前设备为非ram受限设备。  | 

**错误码**：

| 错误码ID | 错误信息 |
| ------- | -------- |
| 16000050 | Internal error. |

以上错误码详细介绍请参考[errcode-ability](../errorcodes/errorcode-ability.md)。

**示例：**

```ts
import appManager from '@ohos.app.ability.appManager';

appManager.isRamConstrainedDevice((err, data) => {
    if (err) {
        console.error(`isRamConstrainedDevice fail, err: ${JSON.stringify(err)}`);
    } else {
        console.log(`The result of isRamConstrainedDevice is: ${JSON.stringify(data)}`);
    }
});
```

## appManager.getAppMemorySize

getAppMemorySize(): Promise\<number>;

获取应用程序的内存大小。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**返回值：**

  | 类型 | 说明 | 
  | -------- | -------- |
  | Promise&lt;number&gt; | 以Promise方式返回接口运行结果及应用程序内存大小，可进行错误处理或其他自定义处理。 | 

**错误码**：

| 错误码ID | 错误信息 |
| ------- | -------- |
| 16000050 | Internal error. |

以上错误码详细介绍请参考[errcode-ability](../errorcodes/errorcode-ability.md)。

**示例：**

```ts
import appManager from '@ohos.app.ability.appManager';

appManager.getAppMemorySize().then((data) => {
    console.log(`The size of app memory is: ${JSON.stringify(data)}`);
}).catch((error) => {
    console.error(`error: ${JSON.stringify(error)}`);
});
```

## appManager.getAppMemorySize

getAppMemorySize(callback: AsyncCallback\<number>): void;

获取应用程序的内存大小。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**参数：**

  | 参数名 | 类型 | 必填 | 说明 | 
  | -------- | -------- | -------- | -------- |
  | callback | AsyncCallback&lt;number&gt; | 是 |以回调方式返回接口运行结果及应用程序内存大小，可进行错误处理或其他自定义处理。 | 

**错误码**：

| 错误码ID | 错误信息 |
| ------- | -------- |
| 16000050 | Internal error. |

以上错误码详细介绍请参考[errcode-ability](../errorcodes/errorcode-ability.md)。

**示例：**

```ts
import appManager from '@ohos.app.ability.appManager';

appManager.getAppMemorySize((err, data) => {
    if (err) {
        console.error(`getAppMemorySize fail, err: ${JSON.stringify(err)}`);
    } else {
        console.log(`The size of app memory is: ${JSON.stringify(data)}`);
    }
});
```

## appManager.getRunningProcessInformation

getRunningProcessInformation(): Promise\<Array\<ProcessInformation>>;

获取有关运行进程的信息。

**需要权限**：ohos.permission.GET_RUNNING_INFO

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| Promise\<Array\<[ProcessInformation](js-apis-inner-application-processInformation.md)>> | 以Promise方式返回接口运行结果及有关运行进程的信息，可进行错误处理或其他自定义处理。 |

**错误码**：

| 错误码ID | 错误信息 |
| ------- | -------- |
| 16000050 | Internal error. |

以上错误码详细介绍请参考[errcode-ability](../errorcodes/errorcode-ability.md)。

**示例：**

```ts
import appManager from '@ohos.app.ability.appManager';

appManager.getRunningProcessInformation().then((data) => {
    console.log(`The running process information is: ${JSON.stringify(data)}`);
}).catch((error) => {
    console.error(`error: ${JSON.stringify(error)}`);
});
```

## appManager.getRunningProcessInformation<sup>9+</sup>

getRunningProcessInformation(callback: AsyncCallback\<Array\<ProcessInformation>>): void;

获取有关运行进程的信息。

**需要权限**：ohos.permission.GET_RUNNING_INFO

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**参数：**

  | 参数名 | 类型 | 必填 | 说明 | 
  | -------- | -------- | -------- | -------- |
  | callback | AsyncCallback\<Array\<[ProcessInformation](js-apis-inner-application-processInformation.md)>>  | 是 |以回调方式返回接口运行结果及有关运行进程的信息，可进行错误处理或其他自定义处理。 | 

**错误码**：

| 错误码ID | 错误信息 |
| ------- | -------- |
| 16000050 | Internal error. |

以上错误码详细介绍请参考[errcode-ability](../errorcodes/errorcode-ability.md)。

**示例：**

```ts
import appManager from '@ohos.app.ability.appManager';

appManager.getRunningProcessInformation((err, data) => {
    if (err) {
        console.error(`getRunningProcessInformation fail, err: ${JSON.stringify(err)}`);
    } else {
        console.log(`The process running information is: ${JSON.stringify(data)}`);
    }
});
```

## appManager.isSharedBundleRunning<sup>10+</sup>

isSharedBundleRunning(bundleName: string, versionCode: number): Promise\<boolean>;

检查共享库是否正在使用。使用Promise异步回调。

**需要权限**：ohos.permission.GET_RUNNING_INFO

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**系统接口**：此接口为系统接口。

**参数**：

| 参数名        | 类型                                       | 必填   | 说明             |
| --------- | ---------------------------------------- | ---- | -------------- |
| bundleName    | string   | 是    | 表示要查询的共享库包名。 |
| versionCode   | number   | 是    | 表示要查询的共享库版本号。      |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| Promise\<boolean> | Promise对象。返回true表示共享库正在使用，返回false表示共享库不在使用。 |

**错误码**：

| 错误码ID | 错误信息 |
| ------- | -------- |
| 16000050 | Internal error. |

以上错误码详细介绍请参考[errcode-ability](../errorcodes/errorcode-ability.md)。

**示例：**

```ts
import appManager from '@ohos.app.ability.appManager';

const bundleName = "this is a bundleName";
const versionCode = 1;
appManager.isSharedBundleRunning(bundleName, versionCode).then((data) => {
    console.log(`The shared bundle running is: ${JSON.stringify(data)}`);
}).catch((error) => {
    console.error(`error: ${JSON.stringify(error)}`);
});
```

## appManager.isSharedBundleRunning<sup>10+</sup>

isSharedBundleRunning(bundleName: string, versionCode: number, callback: AsyncCallback\<boolean>): void;

检查共享库是否正在使用。使用callback异步回调。

**需要权限**：ohos.permission.GET_RUNNING_INFO

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**系统接口**：此接口为系统接口。

**参数**：

| 参数名        | 类型                                       | 必填   | 说明             |
| --------- | ---------------------------------------- | ---- | -------------- |
| bundleName    | string   | 是    | 表示要查询的共享库包名。 |
| versionCode   | number   | 是    | 表示要查询的共享库版本号。      |
|AsyncCallback\<boolean>> | 回调函数。返回true表示共享库正在使用，返回false表示共享库不在使用。 |

**错误码**：

| 错误码ID | 错误信息 |
| ------- | -------- |
| 16000050 | Internal error. |

以上错误码详细介绍请参考[errcode-ability](../errorcodes/errorcode-ability.md)。

**示例：**

```ts
import appManager from '@ohos.app.ability.appManager';

const bundleName = "this is a bundleName";
const versionCode = 1;
appManager.isSharedBundleRunning(bundleName, versionCode, (err, data) => {
    if (err) {
        console.error(`err: ${JSON.stringify(err)}`);
    } else {
        console.log(`The shared bundle running is: ${JSON.stringify(data)}`);
    }
});
```

## appManager.on

on(type: 'applicationState', observer: ApplicationStateObserver): number;

注册全部应用程序的状态观测器。

**需要权限**：ohos.permission.RUNNING_STATE_OBSERVER

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**系统API**：该接口为系统接口，三方应用不支持调用。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| type | string | 是 | 调用接口类型，固定填'applicationState'字符串。 |
| observer | [ApplicationStateObserver](./js-apis-inner-application-applicationStateObserver.md) | 是 | 应用状态观测器，用于观测应用的生命周期变化。 |

**返回值：**

| 类型 | 说明 |
| --- | --- |
| number | 已注册观测器的数字代码，可用于off接口取消注册观测器。|

**错误码**：

| 错误码ID | 错误信息 |
| ------- | -------- |
| 16000050 | Internal error. |

以上错误码详细介绍请参考[errcode-ability](../errorcodes/errorcode-ability.md)。

**示例：**

```ts
import appManager from '@ohos.app.ability.appManager';

let applicationStateObserver = {
    onForegroundApplicationChanged(appStateData) {
        console.log(`[appManager] onForegroundApplicationChanged: ${JSON.stringify(appStateData)}`);
    },
    onAbilityStateChanged(abilityStateData) {
        console.log(`[appManager] onAbilityStateChanged: ${JSON.stringify(abilityStateData)}`);
    },
    onProcessCreated(processData) {
        console.log(`[appManager] onProcessCreated: ${JSON.stringify(processData)}`);
    },
    onProcessDied(processData) {
        console.log(`[appManager] onProcessDied: ${JSON.stringify(processData)}`);
    },
    onProcessStateChanged(processData) {
        console.log(`[appManager] onProcessStateChanged: ${JSON.stringify(processData)}`);
    }
};
try {
    const observerId = appManager.on('applicationState', applicationStateObserver);
    console.log(`[appManager] observerCode: ${observerId}`);
} catch (paramError) {
    console.error(`[appManager] error: ${paramError.code}, ${paramError.message} `);
}
```

## appManager.on

on(type: 'applicationState', observer: ApplicationStateObserver, bundleNameList: Array\<string>): number;

注册指定应用程序的状态观测器。

**需要权限**：ohos.permission.RUNNING_STATE_OBSERVER

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**系统API**：该接口为系统接口，三方应用不支持调用。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| type | string | 是 | 调用接口类型，固定填'applicationState'字符串。 |
| observer | [ApplicationStateObserver](./js-apis-inner-application-applicationStateObserver.md) | 是 | 应用状态观测器，用于观测应用的生命周期变化。 |
| bundleNameList | `Array<string>` | 是 | 表示需要注册监听的bundleName数组。最大值128。 |

**返回值：**

| 类型 | 说明 |
| --- | --- |
| number | 已注册观测器的数字代码，可用于off接口注销观测器。|

**错误码**：

| 错误码ID | 错误信息 |
| ------- | -------- |
| 16000050 | Internal error. |

以上错误码详细介绍请参考[errcode-ability](../errorcodes/errorcode-ability.md)。

**示例：**

```ts
import appManager from '@ohos.app.ability.appManager';

let applicationStateObserver = {
    onForegroundApplicationChanged(appStateData) {
        console.log(`[appManager] onForegroundApplicationChanged: ${JSON.stringify(appStateData)}`);
    },
    onAbilityStateChanged(abilityStateData) {
        console.log(`[appManager] onAbilityStateChanged: ${JSON.stringify(abilityStateData)}`);
    },
    onProcessCreated(processData) {
        console.log(`[appManager] onProcessCreated: ${JSON.stringify(processData)}`);
    },
    onProcessDied(processData) {
        console.log(`[appManager] onProcessDied: ${JSON.stringify(processData)}`);
    },
    onProcessStateChanged(processData) {
        console.log(`[appManager] onProcessStateChanged: ${JSON.stringify(processData)}`);
    }
};
let bundleNameList = ['bundleName1', 'bundleName2'];
try {
    const observerId = appManager.on('applicationState', applicationStateObserver, bundleNameList);
    console.log(`[appManager] observerCode: ${observerId}`);
} catch (paramError) {
    console.error(`[appManager] error: ${paramError.code}, ${paramError.message} `);
}
```

## appManager.off

off(type: 'applicationState', observerId: number,  callback: AsyncCallback\<void>): void;

取消注册应用程序状态观测器。

**需要权限**：ohos.permission.RUNNING_STATE_OBSERVER

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**系统API**：该接口为系统接口，三方应用不支持调用。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| type | string | 是 | 调用接口类型，固定填'applicationState'字符串。 |
| observerId | number | 是 | 表示观测器的编号代码。 |
| callback | AsyncCallback\<void> | 是 | 以回调方式返回接口运行结果，可进行错误处理或其他自定义处理。 |

**错误码**：

| 错误码ID | 错误信息 |
| ------- | -------- |
| 16000050 | Internal error. |

以上错误码详细介绍请参考[errcode-ability](../errorcodes/errorcode-ability.md)。

**示例：**

```ts
import appManager from '@ohos.app.ability.appManager';

let observerId = 0;

// 1.注册应用状态监听器
let applicationStateObserver = {
    onForegroundApplicationChanged(appStateData) {
        console.log(`[appManager] onForegroundApplicationChanged: ${JSON.stringify(appStateData)}`);
    },
    onAbilityStateChanged(abilityStateData) {
        console.log(`[appManager] onAbilityStateChanged: ${JSON.stringify(abilityStateData)}`);
    },
    onProcessCreated(processData) {
        console.log(`[appManager] onProcessCreated: ${JSON.stringify(processData)}`);
    },
    onProcessDied(processData) {
        console.log(`[appManager] onProcessDied: ${JSON.stringify(processData)}`);
    },
    onProcessStateChanged(processData) {
        console.log(`[appManager] onProcessStateChanged: ${JSON.stringify(processData)}`);
    }
};
let bundleNameList = ['bundleName1', 'bundleName2'];
try {
    observerId = appManager.on('applicationState', applicationStateObserver, bundleNameList);
    console.log(`[appManager] observerCode: ${observerId}`);
} catch (paramError) {
    console.error(`[appManager] error: ${paramError.code}, ${paramError.message} `);
}

// 2.注销应用状态监听器
function unregisterApplicationStateObserverCallback(err) {
    if (err) {
        console.error(`unregisterApplicationStateObserverCallback fail, err: ${JSON.stringify(err)}`);
    } else {
        console.log('unregisterApplicationStateObserverCallback success.');
    }
}
try {
    appManager.off('applicationState', observerId, unregisterApplicationStateObserverCallback);
} catch (paramError) {
    console.error(`error: ${paramError.code}, ${paramError.message}`);
}
```

## appManager.off

off(type: 'applicationState', observerId: number): Promise\<void>;

取消注册应用程序状态观测器。

**需要权限**：ohos.permission.RUNNING_STATE_OBSERVER

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**系统API**：该接口为系统接口，三方应用不支持调用。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| type | string | 是 | 调用接口类型，固定填'applicationState'字符串。 |
| observerId | number | 是 | 表示观测器的编号代码。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| Promise\<void> | 以Promise方式返回接口运行结果，可进行错误处理或其他自定义处理。 |

**错误码**：

| 错误码ID | 错误信息 |
| ------- | -------- |
| 16000050 | Internal error. |

以上错误码详细介绍请参考[errcode-ability](../errorcodes/errorcode-ability.md)。

**示例：**

```ts
import appManager from '@ohos.app.ability.appManager';

let observerId = 0;

// 1.注册应用状态监听器
let applicationStateObserver = {
    onForegroundApplicationChanged(appStateData) {
        console.log(`[appManager] onForegroundApplicationChanged: ${JSON.stringify(appStateData)}`);
    },
    onAbilityStateChanged(abilityStateData) {
        console.log(`[appManager] onAbilityStateChanged: ${JSON.stringify(abilityStateData)}`);
    },
    onProcessCreated(processData) {
        console.log(`[appManager] onProcessCreated: ${JSON.stringify(processData)}`);
    },
    onProcessDied(processData) {
        console.log(`[appManager] onProcessDied: ${JSON.stringify(processData)}`);
    },
    onProcessStateChanged(processData) {
        console.log(`[appManager] onProcessStateChanged: ${JSON.stringify(processData)}`);
    }
};
let bundleNameList = ['bundleName1', 'bundleName2'];
try {
    observerId = appManager.on('applicationState', applicationStateObserver, bundleNameList);
    console.log(`[appManager] observerCode: ${observerId}`);
} catch (paramError) {
    console.error(`[appManager] error: ${paramError.code}, ${paramError.message} `);
}
    
// 2.注销应用状态监听器
try {
    appManager.off('applicationState', observerId).then((data) => {
        console.log(`unregisterApplicationStateObserver success, data: ${JSON.stringify(data)}`);
    }).catch((err) => {
        console.error(`unregisterApplicationStateObserver fail, err: ${JSON.stringify(err)}`);
    });
} catch (paramError) {
    console.error(`error: ${paramError.code}, ${paramError.message}`);
}
```

## appManager.getForegroundApplications

getForegroundApplications(callback: AsyncCallback\<Array\<AppStateData>>): void;

获取当前所有前台应用的信息。该应用信息由[AppStateData](js-apis-inner-application-appStateData.md)定义。

**需要权限**：ohos.permission.GET_RUNNING_INFO

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**系统API**：该接口为系统接口，三方应用不支持调用。

**错误码**：

| 错误码ID | 错误信息 |
| ------- | -------- |
| 16000050 | Internal error. |

以上错误码详细介绍请参考[errcode-ability](../errorcodes/errorcode-ability.md)。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| callback | AsyncCallback\<Array\<[AppStateData](js-apis-inner-application-appStateData.md)>> | 是 | 以回调方式方式返回接口运行结果及应用状态数据数组，可进行错误处理或其他自定义处理。 |

**示例：**

```ts
import appManager from '@ohos.app.ability.appManager';

function getForegroundApplicationsCallback(err, data) {
    if (err) {
        console.error(`getForegroundApplicationsCallback fail, err: ${JSON.stringify(err)}`);
    } else {
        console.log(`getForegroundApplicationsCallback success, data: ${JSON.stringify(data)}`);
    }
}
try {
    appManager.getForegroundApplications(getForegroundApplicationsCallback);
} catch (paramError) {
    console.error(`error: ${paramError.code}, ${paramError.message}`);
}
```

## appManager.getForegroundApplications

getForegroundApplications(): Promise\<Array\<AppStateData>>;

获取当前所有前台应用的信息。该应用信息由[AppStateData](js-apis-inner-application-appStateData.md)定义。

**需要权限**：ohos.permission.GET_RUNNING_INFO

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**系统API**：该接口为系统接口，三方应用不支持调用。

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| Promise\<Array\<[AppStateData](js-apis-inner-application-appStateData.md)>> | 返回前台进程应用程序的数组。 |

**错误码**：

| 错误码ID | 错误信息 |
| ------- | -------- |
| 16000050 | Internal error. |

以上错误码详细介绍请参考[errcode-ability](../errorcodes/errorcode-ability.md)。

**示例：**

```ts
import appManager from '@ohos.app.ability.appManager';

appManager.getForegroundApplications().then((data) => {
    console.log(`getForegroundApplications success, data: ${JSON.stringify(data)}`);
}).catch((err) => {
    console.error(`getForegroundApplications fail, err: ${JSON.stringify(err)}`);
});
```

## appManager.killProcessWithAccount

killProcessWithAccount(bundleName: string, accountId: number): Promise\<void\>

切断account进程（Promise形式）。

> **说明：** 
>
> 当accountId为当前用户时，不需要校验ohos.permission.INTERACT_ACROSS_LOCAL_ACCOUNTS权限。

**需要权限**：ohos.permission.INTERACT_ACROSS_LOCAL_ACCOUNTS, ohos.permission.CLEAN_BACKGROUND_PROCESSES

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**系统API**: 此接口为系统接口，三方应用不支持调用。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| bundleName | string | 是 | 应用Bundle名称。 |
| accountId | number | 是 | 系统帐号的帐号ID，详情参考[getCreatedOsAccountsCount](js-apis-osAccount.md#getosaccountlocalidfromprocess)。 |

**错误码**：

| 错误码ID | 错误信息 |
| ------- | -------- |
| 16000050 | Internal error. |

以上错误码详细介绍请参考[errcode-ability](../errorcodes/errorcode-ability.md)。

**示例：**

```ts
import appManager from '@ohos.app.ability.appManager';

let bundleName = 'bundleName';
let accountId = 0;
try {
    appManager.killProcessWithAccount(bundleName, accountId).then(() => {
        console.log('killProcessWithAccount success');
    }).catch((err) => {
        console.error(`killProcessWithAccount fail, err: ${JSON.stringify(err)}`);
    });
} catch (paramError) {
    console.error(`error: ${paramError.code}, ${paramError.message}`);
}
```


## appManager.killProcessWithAccount

killProcessWithAccount(bundleName: string, accountId: number, callback: AsyncCallback\<void\>): void

切断account进程（callback形式）。

> **说明：** 
>
> 当accountId为当前用户时，不需要校验ohos.permission.INTERACT_ACROSS_LOCAL_ACCOUNTS权限。

**需要权限**：ohos.permission.INTERACT_ACROSS_LOCAL_ACCOUNTS, ohos.permission.CLEAN_BACKGROUND_PROCESSES

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**系统API**: 此接口为系统接口，三方应用不支持调用。

**参数：**

  | 参数名 | 类型 | 必填 | 说明 | 
  | -------- | -------- | -------- | -------- |
  | bundleName | string | 是 | 应用Bundle名称。 | 
  | accountId | number | 是 | 系统帐号的帐号ID，详情参考[getCreatedOsAccountsCount](js-apis-osAccount.md#getosaccountlocalidfromprocess)。 | 
  | callback | AsyncCallback\<void\> | 是 | 以回调方式返回接口运行结果，可进行错误处理或其他自定义处理。 | 

**错误码**：

| 错误码ID | 错误信息 |
| ------- | -------- |
| 16000050 | Internal error. |

以上错误码详细介绍请参考[errcode-ability](../errorcodes/errorcode-ability.md)。

**示例：**

```ts
import appManager from '@ohos.app.ability.appManager';

let bundleName = 'bundleName';
let accountId = 0;
function killProcessWithAccountCallback(err, data) {
    if (err) {
        console.error(`killProcessWithAccountCallback fail, err: ${JSON.stringify(err)}`);
    } else {
        console.log('killProcessWithAccountCallback success.');
    }
}
appManager.killProcessWithAccount(bundleName, accountId, killProcessWithAccountCallback);
```

## appManager.killProcessesByBundleName

killProcessesByBundleName(bundleName: string, callback: AsyncCallback\<void>);

通过Bundle名称终止进程。

**需要权限**：ohos.permission.CLEAN_BACKGROUND_PROCESSES

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**系统API**：该接口为系统接口，三方应用不支持调用。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| bundleName | string | 是 | 表示Bundle名称。 |
| callback | AsyncCallback\<void> | 是 | 以回调方式返回接口运行结果，可进行错误处理或其他自定义处理。 |

**错误码**：

| 错误码ID | 错误信息 |
| ------- | -------- |
| 16000050 | Internal error. |

以上错误码详细介绍请参考[errcode-ability](../errorcodes/errorcode-ability.md)。

**示例：**

```ts
import appManager from '@ohos.app.ability.appManager';

let bundleName = 'bundleName';
function killProcessesByBundleNameCallback(err, data) {
    if (err) {
        console.error(`killProcessesByBundleNameCallback fail, err: ${JSON.stringify(err)}`);
    } else {
        console.log('killProcessesByBundleNameCallback success.');
    }
}
try {
    appManager.killProcessesByBundleName(bundleName, killProcessesByBundleNameCallback);
} catch (paramError) {
    console.error(`error: ${paramError.code}, ${paramError.message}`);
}
```

## appManager.killProcessesByBundleName

killProcessesByBundleName(bundleName: string): Promise\<void>;

通过Bundle名称终止进程。

**需要权限**：ohos.permission.CLEAN_BACKGROUND_PROCESSES

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**系统API**：该接口为系统接口，三方应用不支持调用。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| bundleName | string | 是 | 表示Bundle名称。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| Promise\<void> | 返回执行结果。 |

**错误码**：

| 错误码ID | 错误信息 |
| ------- | -------- |
| 16000050 | Internal error. |

以上错误码详细介绍请参考[errcode-ability](../errorcodes/errorcode-ability.md)。

**示例：**

```ts
import appManager from '@ohos.app.ability.appManager';

let bundleName = 'bundleName';
try {
    appManager.killProcessesByBundleName(bundleName).then((data) => {
        console.log('killProcessesByBundleName success.');
    }).catch((err) => {
        console.error(`killProcessesByBundleName fail, err: ${JSON.stringify(err)}`);
    });
} catch (paramError) {
    console.error(`error: ${paramError.code}, ${paramError.message}`);
}
```

## appManager.clearUpApplicationData

clearUpApplicationData(bundleName: string, callback: AsyncCallback\<void>);

通过Bundle名称清除应用数据。

**需要权限**：ohos.permission.CLEAN_APPLICATION_DATA

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**系统API**：该接口为系统接口，三方应用不支持调用。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| bundleName | string | 是 | 表示Bundle名称。 |
| callback | AsyncCallback\<void> | 是 | 以回调方式返回接口运行结果，可进行错误处理或其他自定义处理。 |

**错误码**：

| 错误码ID | 错误信息 |
| ------- | -------- |
| 16000050 | Internal error. |

以上错误码详细介绍请参考[errcode-ability](../errorcodes/errorcode-ability.md)。

**示例：**

```ts
import appManager from '@ohos.app.ability.appManager';

let bundleName = 'bundleName';
function clearUpApplicationDataCallback(err, data) {
    if (err) {
        console.error(`clearUpApplicationDataCallback fail, err: ${JSON.stringify(err)}`);
    } else {
        console.log('clearUpApplicationDataCallback success.');
    }
}
try {
    appManager.clearUpApplicationData(bundleName, clearUpApplicationDataCallback);
} catch (paramError) {
    console.error(`error: ${paramError.code}, ${paramError.message}`);
}
```

## appManager.clearUpApplicationData

clearUpApplicationData(bundleName: string): Promise\<void>;

通过Bundle名称清除应用数据。

**需要权限**：ohos.permission.CLEAN_APPLICATION_DATA

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**系统API**：该接口为系统接口，三方应用不支持调用。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| bundleName | string | 是 | 表示Bundle名称。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| Promise\<void> | 以Promise方式返回接口运行结果，可进行错误处理或其他自定义处理。 |

**错误码**：

| 错误码ID | 错误信息 |
| ------- | -------- |
| 16000050 | Internal error. |

以上错误码详细介绍请参考[errcode-ability](../errorcodes/errorcode-ability.md)。

**示例：**

```ts
import appManager from '@ohos.app.ability.appManager';

let bundleName = 'bundleName';
try {
    appManager.clearUpApplicationData(bundleName).then((data) => {
        console.log('clearUpApplicationData success.');
    }).catch((err) => {
        console.error(`clearUpApplicationData fail, err: ${JSON.stringify(err)}`);
    });
} catch (paramError) {
    console.error(`error: ${paramError.code}, ${paramError.message}`);
}
```

## appManager.getProcessMemoryByPid<sup>10+</sup>

getProcessMemoryByPid(pid: number, callback: AsyncCallback\<number>): void;

通过pid查询对应进程占用的内存大小。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**系统API**：此接口为系统接口。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| pid | number | 是 | 表示进程id，详情参考[getRunningProcessInfoByBundleName](js-apis-app-ability-appManager.md#appmanagergetrunningprocessinfobybundlename10)。 |
| callback | AsyncCallback\<number> | 是 | 以回调方式返回接口运行结果及进程占用的内存大小（单位KB），可进行错误处理或其他自定义处理。 |

**错误码**：

以下错误码详细介绍请参考[errcode-ability](../errorcodes/errorcode-ability.md)。

| 错误码ID | 错误信息 |
| ------- | -------- |
| 16000050 | Internal error. |

**示例：**

```ts
import appManager from '@ohos.app.ability.appManager';

let pid = 0;
function getProcessMemoryByPidCallback(err, data) {
    if (err) {
        console.error(`getProcessMemoryByPidCallback fail, err: ${JSON.stringify(err)}`);
    } else {
        console.log('getProcessMemoryByPidCallback success.');
    }
}
try {
    appManager.getProcessMemoryByPid(pid, getProcessMemoryByPidCallback);
} catch (paramError) {
    console.error(`error: ${paramError.code}, ${paramError.message}`);
}
```

## appManager.getProcessMemoryByPid<sup>10+</sup>

getProcessMemoryByPid(pid: number): Promise\<number>;

通过pid查询对应进程占用的内存大小。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**系统API**：此接口为系统接口。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| pid | number | 是 | 表示进程id，详情参考[getRunningProcessInfoByBundleName](js-apis-app-ability-appManager.md#appmanagergetrunningprocessinfobybundlename10)。  |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| Promise\<number> | 以Promise方式返回接口运行结果及进程占用的内存大小（单位KB），可进行错误处理或其他自定义处理。 |

**错误码**：

以下错误码详细介绍请参考[errcode-ability](../errorcodes/errorcode-ability.md)。

| 错误码ID | 错误信息 |
| ------- | -------- |
| 16000050 | Internal error. |

**示例：**

```ts
import appManager from '@ohos.app.ability.appManager';

let pid = 0;
try {
    appManager.getProcessMemoryByPid(pid).then((data) => {
        console.log('getProcessMemoryByPid success.');
    }).catch((err) => {
        console.error(`getProcessMemoryByPid fail, err: ${JSON.stringify(err)}`);
    });
} catch (paramError) {
    console.error(`error: ${paramError.code}, ${paramError.message}`);
}
```

## appManager.getRunningProcessInfoByBundleName<sup>10+</sup>

getRunningProcessInfoByBundleName(bundleName: string, callback: AsyncCallback\<Array\<ProcessInformation>>): void;

通过bundleName获取有关运行进程的信息。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**系统API**：此接口为系统接口。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| bundleName | string | 是 | 表示Bundle名称。 |
| callback | AsyncCallback\<Array\<[ProcessInformation](js-apis-inner-application-processInformation.md)>> | 是 | 以回调方式返回接口运行结果及有关运行进程的信息，可进行错误处理或其他自定义处理。 |

**错误码**：

以下错误码详细介绍请参考[errcode-ability](../errorcodes/errorcode-ability.md)。

| 错误码ID | 错误信息 |
| ------- | -------- |
| 16000050 | Internal error. |

**示例：**

```ts
import appManager from '@ohos.app.ability.appManager';

let bundleName = "bundleName";
function getRunningProcessInfoByBundleNameCallback(err, data) {
    if (err) {
        console.error(`getRunningProcessInfoByBundleNameCallback fail, err: ${JSON.stringify(err)}`);
    } else {
        console.log('getRunningProcessInfoByBundleNameCallback success.');
    }
}
try {
    appManager.getRunningProcessInfoByBundleName(bundleName, getRunningProcessInfoByBundleNameCallback);
} catch (paramError) {
    console.error(`error: ${paramError.code}, ${paramError.message}`);
}
```

## appManager.getRunningProcessInfoByBundleName<sup>10+</sup>

getRunningProcessInfoByBundleName(bundleName: string): Promise\<Array\<ProcessInformation>>;

通过bundleName获取有关运行进程的信息。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**系统API**：此接口为系统接口。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| bundleName | string | 是 | 表示Bundle名称。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| Promise\<Array\<[ProcessInformation](js-apis-inner-application-processInformation.md)>> | 以Promise方式返回接口运行结果及有关运行进程的信息，可进行错误处理或其他自定义处理。 |

**错误码**：

以下错误码详细介绍请参考[errcode-ability](../errorcodes/errorcode-ability.md)。

| 错误码ID | 错误信息 |
| ------- | -------- |
| 16000050 | Internal error. |

**示例：**

```ts
import appManager from '@ohos.app.ability.appManager';

let bundleName = "bundleName";
try {
    appManager.getRunningProcessInfoByBundleName(bundleName).then((data) => {
        console.log('getRunningProcessInfoByBundleName success.');
    }).catch((err) => {
        console.error(`getRunningProcessInfoByBundleName fail, err: ${JSON.stringify(err)}`);
    });
} catch (paramError) {
    console.error(`error: ${paramError.code}, ${paramError.message}`);
}
```

## appManager.getRunningProcessInfoByBundleName<sup>10+</sup>

getRunningProcessInfoByBundleName(bundleName: string, userId: number, callback: AsyncCallback\<Array\<ProcessInformation>>): void;

通过bundleName和userId获取有关运行进程的信息。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**系统API**：此接口为系统接口。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| bundleName | string | 是 | 表示Bundle名称。 |
| userId | number | 是 | 表示用户Id。 |
| callback | AsyncCallback\<Array\<[ProcessInformation](js-apis-inner-application-processInformation.md)>> | 是 | 以回调方式返回接口运行结果及有关运行进程的信息，可进行错误处理或其他自定义处理。 |

**错误码**：

以下错误码详细介绍请参考[errcode-ability](../errorcodes/errorcode-ability.md)。

| 错误码ID | 错误信息 |
| ------- | -------- |
| 16000050 | Internal error. |

**示例：**

```ts
import appManager from '@ohos.app.ability.appManager';

let bundleName = "bundleName";
let userId = 0;
function getRunningProcessInfoByBundleNameCallback(err, data) {
    if (err) {
        console.error(`getRunningProcessInfoByBundleNameCallback fail, err: ${JSON.stringify(err)}`);
    } else {
        console.log('getRunningProcessInfoByBundleNameCallback success.');
    }
}
try {
    appManager.getRunningProcessInfoByBundleName(bundleName, userId, getRunningProcessInfoByBundleNameCallback);
} catch (paramError) {
    console.error(`error: ${paramError.code}, ${paramError.message}`);
}
```

## appManager.getRunningProcessInfoByBundleName<sup>10+</sup>

getRunningProcessInfoByBundleName(bundleName: string, userId: number): Promise\<Array\<ProcessInformation>>;

通过bundleName和userId获取有关运行进程的信息。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**系统API**：此接口为系统接口。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| bundleName | string | 是 | 表示Bundle名称。 |
| userId | number | 是 | 表示用户Id。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| Promise\<Array\<[ProcessInformation](js-apis-inner-application-processInformation.md)>> | 以Promise方式返回接口运行结果及有关运行进程的信息，可进行错误处理或其他自定义处理。 |

**错误码**：

以下错误码详细介绍请参考[errcode-ability](../errorcodes/errorcode-ability.md)。

| 错误码ID | 错误信息 |
| ------- | -------- |
| 16000050 | Internal error. |

**示例：**

```ts
import appManager from '@ohos.app.ability.appManager';

let bundleName = "bundleName";
let userId = 0;
try {
    appManager.getRunningProcessInfoByBundleName(bundleName, userId).then((data) => {
        console.log('getRunningProcessInfoByBundleName success.');
    }).catch((err) => {
        console.error(`getRunningProcessInfoByBundleName fail, err: ${JSON.stringify(err)}`);
    });
} catch (paramError) {
    console.error(`error: ${paramError.code}, ${paramError.message}`);
}
```

## ApplicationState

应用状态，该类型为枚举，可配合[AbilityStateData](js-apis-inner-application-appStateData.md)返回相应的应用状态。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**系统API**: 此接口为系统接口，三方应用不支持调用。

| 名称                 | 值  | 说明                               |
| -------------------- | --- | --------------------------------- |
| STATE_CREATE    | 1   |   当应用在创建中的时候处于的状态。         |
| STATE_FOREGROUND          | 2   |      当应用切换到前台的时候处于的状态。            |
| STATE_ACTIVE  | 3   |         当应用在获焦的时候处于的状态。     |
| STATE_BACKGROUND        | 4   |       当应用处于后台不可见时处于的状态。           |
| STATE_DESTROY        | 5   |           当应用在销毁的时候处于的状态。       |

## ProcessState

进程状态，该类型为枚举，可配合[ProcessData](js-apis-inner-application-processData.md)返回相应的进程状态。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**系统API**: 此接口为系统接口，三方应用不支持调用。

| 名称                 | 值  | 说明                               |
| -------------------- | --- | --------------------------------- |
| STATE_CREATE    | 1   |      当进程在创建中的时候处于的状态。       |
| STATE_FOREGROUND          | 2   |            当进程切换到前台的时候处于的状态。      |
| STATE_ACTIVE  | 3   |          当进程在获焦的时候处于的状态。   |
| STATE_BACKGROUND        | 4   |       当进程处于后台不可见时处于的状态。           |
| STATE_DESTROY        | 5   |         当进程在销毁的时候处于的状态。         |
