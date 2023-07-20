# UIAbilityContext

UIAbilityContext是[UIAbility](js-apis-app-ability-uiAbility.md)的上下文环境，继承自[Context](js-apis-inner-application-context.md)，提供UIAbility的相关配置信息以及操作UIAbility和ServiceExtensionAbility的方法，如启动UIAbility，停止当前UIAbilityContext所属的UIAbility，启动、停止、连接、断开连接ServiceExtensionAbility等。

> **说明：**
>
>  - 本模块首批接口从API version 9开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。
>  - 本模块接口仅可在Stage模型下使用。

## 导入模块

```ts
import common from '@ohos.app.ability.common';
```

## 属性

**系统能力**：以下各项对应的系统能力均为SystemCapability.Ability.AbilityRuntime.Core

| 名称 | 类型 | 可读 | 可写 | 说明 |
| -------- | -------- | -------- | -------- | -------- |
| abilityInfo | [AbilityInfo](js-apis-bundleManager-abilityInfo.md) | 是 | 否 | UIAbility的相关信息。 |
| currentHapModuleInfo | [HapModuleInfo](js-apis-bundleManager-hapModuleInfo.md) | 是 | 否 | 当前HAP的信息。 |
| config | [Configuration](js-apis-app-ability-configuration.md) | 是 | 否 | 与UIAbility相关的配置信息，如语言、颜色模式等。 |

> **关于示例代码的说明：**
>
> 在本文档的示例中，通过`this.context`来获取`UIAbilityContext`，其中`this`代表继承自`UIAbility`的`UIAbility`实例。如需要在页面中使用`UIAbilityContext`提供的能力，请参见[获取UIAbility的上下文信息](../../application-models/uiability-usage.md#获取uiability的上下文信息)。

## UIAbilityContext.startAbility

startAbility(want: Want, callback: AsyncCallback&lt;void&gt;): void;

启动Ability（callback形式）。

使用规则：
 - 调用方应用位于后台时，使用该接口启动Ability需申请`ohos.permission.START_ABILITIES_FROM_BACKGROUND`权限
 - 跨应用场景下，目标Ability的exported属性若配置为false，调用方应用需申请`ohos.permission.START_INVISIBLE_ABILITY`权限
 - 组件启动规则详见：[组件启动规则（Stage模型）](../../application-models/component-startup-rules.md)

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md) | 是 | 启动Ability的want信息。 |
| callback | AsyncCallback&lt;void&gt; | 是 | callback形式返回启动结果。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 16000001 | The specified ability does not exist. |
| 16000002 | Incorrect ability type. |
| 16000004 | Can not start invisible component. |
| 16000005 | The specified process does not have the permission. |
| 16000006 | Cross-user operations are not allowed. |
| 16000008 | The crowdtesting application expires. |
| 16000009 | An ability cannot be started or stopped in Wukong mode. |
| 16000010 | The call with the continuation flag is forbidden.        |
| 16000011 | The context does not exist.        |
| 16000012 | The application is controlled.        |
| 16000013 | The application is controlled by EDM.       |
| 16000050 | Internal error. |
| 16000053 | The ability is not on the top of the UI. |
| 16000055 | Installation-free timed out. |
| 16200001 | The caller has been released. |

错误码详细介绍请参考[errcode-ability](../errorcodes/errorcode-ability.md)

**示例：**

  ```ts
let want = {
  bundleName: 'com.example.myapplication',
  abilityName: 'EntryAbility'
};

try {
  this.context.startAbility(want, (err) => {
    if (err.code) {
      // 处理业务逻辑错误
      console.error(`startAbility failed, code is ${err.code}, message is ${err.message}`);
      return;
    }
    // 执行正常业务
    console.info('startAbility succeed');
  });
} catch (err) {
  // 处理入参错误异常
  console.error(`startAbility failed failed, code is ${err.code}, message is ${err.message}`);
}
  ```

## UIAbilityContext.startAbility

startAbility(want: Want, options: StartOptions, callback: AsyncCallback&lt;void&gt;): void;

启动Ability（callback形式）。

使用规则：
 - 调用方应用位于后台时，使用该接口启动Ability需申请`ohos.permission.START_ABILITIES_FROM_BACKGROUND`权限
 - 跨应用场景下，目标Ability的exported属性若配置为false，调用方应用需申请`ohos.permission.START_INVISIBLE_ABILITY`权限
 - 组件启动规则详见：[组件启动规则（Stage模型）](../../application-models/component-startup-rules.md)

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md)  | 是 | 启动Ability的want信息。 |
| options | [StartOptions](js-apis-app-ability-startOptions.md) | 是 | 启动Ability所携带的参数。 |
| callback | AsyncCallback&lt;void&gt; | 是 | callback形式返回启动结果。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 16000001 | The specified ability does not exist. |
| 16000002 | Incorrect ability type. |
| 16000004 | Can not start invisible component. |
| 16000005 | The specified process does not have the permission. |
| 16000006 | Cross-user operations are not allowed. |
| 16000008 | The crowdtesting application expires. |
| 16000009 | An ability cannot be started or stopped in Wukong mode. |
| 16000010 | The call with the continuation flag is forbidden.        |
| 16000011 | The context does not exist.        |
| 16000012 | The application is controlled.        |
| 16000013 | The application is controlled by EDM.       |
| 16000050 | Internal error. |
| 16000053 | The ability is not on the top of the UI. |
| 16000055 | Installation-free timed out. |
| 16200001 | The caller has been released. |

错误码详细介绍请参考[errcode-ability](../errorcodes/errorcode-ability.md)

**示例：**

  ```ts
let want = {
  deviceId: '',
  bundleName: 'com.example.myapplication',
  abilityName: 'EntryAbility'
};
let options = {
  windowMode: 0
};

try {
  this.context.startAbility(want, options, (err) => {
    if (err.code) {
      // 处理业务逻辑错误
      console.error(`startAbility failed, code is ${err.code}, message is ${err.message}`);
      return;
    }
    // 执行正常业务
    console.info('startAbility succeed');
  });
} catch (err) {
  // 处理入参错误异常
  console.error(`startAbility failed failed, code is ${err.code}, message is ${err.message}`);
}
  ```

## UIAbilityContext.startAbility

startAbility(want: Want, options?: StartOptions): Promise&lt;void&gt;;

启动Ability（promise形式）。

使用规则：
 - 调用方应用位于后台时，使用该接口启动Ability需申请`ohos.permission.START_ABILITIES_FROM_BACKGROUND`权限
 - 跨应用场景下，目标Ability的exported属性若配置为false，调用方应用需申请`ohos.permission.START_INVISIBLE_ABILITY`权限
 - 组件启动规则详见：[组件启动规则（Stage模型）](../../application-models/component-startup-rules.md)

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md) | 是 | 启动Ability的want信息。 |
| options | [StartOptions](js-apis-app-ability-startOptions.md) | 否 | 启动Ability所携带的参数。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| Promise&lt;void&gt; | Promise形式返回启动结果。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 16000001 | The specified ability does not exist. |
| 16000002 | Incorrect ability type. |
| 16000004 | Can not start invisible component. |
| 16000005 | The specified process does not have the permission. |
| 16000006 | Cross-user operations are not allowed. |
| 16000008 | The crowdtesting application expires. |
| 16000009 | An ability cannot be started or stopped in Wukong mode. |
| 16000010 | The call with the continuation flag is forbidden.        |
| 16000011 | The context does not exist.        |
| 16000012 | The application is controlled.        |
| 16000013 | The application is controlled by EDM.       |
| 16000050 | Internal error. |
| 16000053 | The ability is not on the top of the UI. |
| 16000055 | Installation-free timed out. |
| 16200001 | The caller has been released. |

错误码详细介绍请参考[errcode-ability](../errorcodes/errorcode-ability.md)

**示例：**

  ```ts
let want = {
  bundleName: 'com.example.myapplication',
  abilityName: 'EntryAbility'
};
let options = {
  windowMode: 0,
};

try {
  this.context.startAbility(want, options)
    .then(() => {
      // 执行正常业务
      console.info('startAbility succeed');
    })
    .catch((err) => {
      // 处理业务逻辑错误
      console.error(`startAbility failed, code is ${err.code}, message is ${err.message}`);
    });
} catch (err) {
  // 处理入参错误异常
  console.error(`startAbility failed, code is ${err.code}, message is ${err.message}`);
}
  ```

## UIAbilityContext.startAbilityForResult

startAbilityForResult(want: Want, callback: AsyncCallback&lt;AbilityResult&gt;): void;

启动一个Ability。Ability被启动后，有如下情况(callback形式):
 - 正常情况下可通过调用[terminateSelfWithResult](#uiabilitycontextterminateselfwithresult)接口使之终止并且返回结果给调用方。
 - 异常情况下比如杀死Ability会返回异常信息给调用方, 异常信息中resultCode为-1。
 - 如果被启动的Ability模式是单实例模式, 不同应用多次调用该接口启动这个Ability，当这个Ability调用[terminateSelfWithResult](#uiabilitycontextterminateselfwithresult)接口使之终止时，只将正常结果返回给最后一个调用方, 其它调用方返回异常信息, 异常信息中resultCode为-1。

使用规则：
 - 调用方应用位于后台时，使用该接口启动Ability需申请`ohos.permission.START_ABILITIES_FROM_BACKGROUND`权限
 - 跨应用场景下，目标Ability的exported属性若配置为false，调用方应用需申请`ohos.permission.START_INVISIBLE_ABILITY`权限
 - 组件启动规则详见：[组件启动规则（Stage模型）](../../application-models/component-startup-rules.md)

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| want |[Want](js-apis-application-want.md) | 是 | 启动Ability的want信息。 |
| callback | AsyncCallback&lt;[AbilityResult](js-apis-inner-ability-abilityResult.md)&gt; | 是 | 执行结果回调函数。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 16000001 | The specified ability does not exist. |
| 16000002 | Incorrect ability type. |
| 16000004 | Can not start invisible component. |
| 16000005 | The specified process does not have the permission. |
| 16000006 | Cross-user operations are not allowed. |
| 16000008 | The crowdtesting application expires. |
| 16000009 | An ability cannot be started or stopped in Wukong mode. |
| 16000010 | The call with the continuation flag is forbidden. |
| 16000011 | The context does not exist. |
| 16000012 | The application is controlled.        |
| 16000013 | The application is controlled by EDM.       |
| 16000050 | Internal error. |
| 16000053 | The ability is not on the top of the UI. |
| 16000055 | Installation-free timed out. |
| 16200001 | The caller has been released. |

错误码详细介绍请参考[errcode-ability](../errorcodes/errorcode-ability.md)

**示例：**

  ```ts
let want = {
  deviceId: '',
  bundleName: 'com.example.myapplication',
  abilityName: 'EntryAbility'
};

try {
  this.context.startAbilityForResult(want, (err, result) => {
    if (err.code) {
      // 处理业务逻辑错误
      console.error(`startAbilityForResult failed, code is ${err.code}, message is ${err.message}`);
      return;
    }
    // 执行正常业务
    console.info('startAbilityForResult succeed');
  });
} catch (err) {
  // 处理入参错误异常
  console.error(`startAbilityForResult failed, code is ${err.code}, message is ${err.message}`);
}
  ```

## UIAbilityContext.startAbilityForResult

startAbilityForResult(want: Want, options: StartOptions, callback: AsyncCallback&lt;AbilityResult&gt;): void;

启动一个Ability。Ability被启动后，有如下情况(callback形式):
 - 正常情况下可通过调用[terminateSelfWithResult](#uiabilitycontextterminateselfwithresult)接口使之终止并且返回结果给调用方。
 - 异常情况下比如杀死Ability会返回异常信息给调用方，异常信息中resultCode为-1。
 - 如果被启动的Ability模式是单实例模式, 不同应用多次调用该接口启动这个Ability，当这个Ability调用[terminateSelfWithResult](#uiabilitycontextterminateselfwithresult)接口使之终止时，只将正常结果返回给最后一个调用方，其它调用方返回异常信息, 异常信息中resultCode为-1。

使用规则：
 - 调用方应用位于后台时，使用该接口启动Ability需申请`ohos.permission.START_ABILITIES_FROM_BACKGROUND`权限
 - 跨应用场景下，目标Ability的exported属性若配置为false，调用方应用需申请`ohos.permission.START_INVISIBLE_ABILITY`权限
 - 组件启动规则详见：[组件启动规则（Stage模型）](../../application-models/component-startup-rules.md)

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| want |[Want](js-apis-application-want.md) | 是 | 启动Ability的want信息。 |
| options | [StartOptions](js-apis-app-ability-startOptions.md) | 是 | 启动Ability所携带的参数。 |
| callback | AsyncCallback&lt;[AbilityResult](js-apis-inner-ability-abilityResult.md)&gt; | 是 | 执行结果回调函数。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 16000001 | The specified ability does not exist. |
| 16000002 | Incorrect ability type. |
| 16000004 | Can not start invisible component. |
| 16000005 | The specified process does not have the permission. |
| 16000006 | Cross-user operations are not allowed. |
| 16000008 | The crowdtesting application expires. |
| 16000009 | An ability cannot be started or stopped in Wukong mode. |
| 16000010 | The call with the continuation flag is forbidden. |
| 16000011 | The context does not exist. |
| 16000012 | The application is controlled.        |
| 16000013 | The application is controlled by EDM.       |
| 16000050 | Internal error. |
| 16000053 | The ability is not on the top of the UI. |
| 16000055 | Installation-free timed out. |
| 16200001 | The caller has been released. |

错误码详细介绍请参考[errcode-ability](../errorcodes/errorcode-ability.md)

**示例：**

  ```ts
let want = {
  deviceId: '',
  bundleName: 'com.example.myapplication',
  abilityName: 'EntryAbility'
};
let options = {
  windowMode: 0,
};

try {
  this.context.startAbilityForResult(want, options, (err, result) => {
    if (err.code) {
      // 处理业务逻辑错误
      console.error(`startAbilityForResult failed, code is ${err.code}, message is ${err.message}`);
      return;
    }
    // 执行正常业务
    console.info('startAbilityForResult succeed');
  });
} catch (err) {
  // 处理入参错误异常
  console.error(`startAbilityForResult failed, code is ${err.code}, message is ${err.message}`);
}
  ```


## UIAbilityContext.startAbilityForResult

startAbilityForResult(want: Want, options?: StartOptions): Promise&lt;AbilityResult&gt;;

启动一个Ability。Ability被启动后，有如下情况(promise形式):
 - 正常情况下可通过调用[terminateSelfWithResult](#uiabilitycontextterminateselfwithresult)接口使之终止并且返回结果给调用方。
 - 异常情况下比如杀死Ability会返回异常信息给调用方, 异常信息中resultCode为-1。
 - 如果被启动的Ability模式是单实例模式, 不同应用多次调用该接口启动这个Ability，当这个Ability调用[terminateSelfWithResult](#uiabilitycontextterminateselfwithresult)接口使之终止时，只将正常结果返回给最后一个调用方, 其它调用方返回异常信息, 异常信息中resultCode为-1。

使用规则：
 - 调用方应用位于后台时，使用该接口启动Ability需申请`ohos.permission.START_ABILITIES_FROM_BACKGROUND`权限
 - 跨应用场景下，目标Ability的exported属性若配置为false，调用方应用需申请`ohos.permission.START_INVISIBLE_ABILITY`权限
 - 组件启动规则详见：[组件启动规则（Stage模型）](../../application-models/component-startup-rules.md)

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md) | 是 | 启动Ability的want信息。 |
| options | [StartOptions](js-apis-app-ability-startOptions.md) | 否 | 启动Ability所携带的参数。 |


**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| Promise&lt;[AbilityResult](js-apis-inner-ability-abilityResult.md)&gt; | Promise形式返回执行结果。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 16000001 | The specified ability does not exist. |
| 16000002 | Incorrect ability type. |
| 16000004 | Can not start invisible component. |
| 16000005 | The specified process does not have the permission. |
| 16000006 | Cross-user operations are not allowed. |
| 16000008 | The crowdtesting application expires. |
| 16000009 | An ability cannot be started or stopped in Wukong mode. |
| 16000010 | The call with the continuation flag is forbidden. |
| 16000011 | The context does not exist. |
| 16000012 | The application is controlled.        |
| 16000013 | The application is controlled by EDM.       |
| 16000050 | Internal error. |
| 16000053 | The ability is not on the top of the UI. |
| 16000055 | Installation-free timed out. |
| 16200001 | The caller has been released. |

错误码详细介绍请参考[errcode-ability](../errorcodes/errorcode-ability.md)

**示例：**

  ```ts
let want = {
  bundleName: 'com.example.myapplication',
  abilityName: 'EntryAbility'
};
let options = {
  windowMode: 0,
};

try {
  this.context.startAbilityForResult(want, options)
    .then((result) => {
      // 执行正常业务
      console.info('startAbilityForResult succeed');
    })
    .catch((err) => {
      // 处理业务逻辑错误
      console.error(`startAbilityForResult failed, code is ${err.code}, message is ${err.message}`);
    });
} catch (err) {
  // 处理入参错误异常
  console.error(`startAbilityForResult failed, code is ${err.code}, message is ${err.message}`);
}
  ```

## UIAbilityContext.startAbilityForResultWithAccount

startAbilityForResultWithAccount(want: Want, accountId: number, callback: AsyncCallback\<AbilityResult>): void;

启动一个Ability并在该Ability销毁时返回执行结果（callback形式）。

使用规则：
 - 调用方应用位于后台时，使用该接口启动Ability需申请`ohos.permission.START_ABILITIES_FROM_BACKGROUND`权限
 - 跨应用场景下，目标Ability的exported属性若配置为false，调用方应用需申请`ohos.permission.START_INVISIBLE_ABILITY`权限
 - 组件启动规则详见：[组件启动规则（Stage模型）](../../application-models/component-startup-rules.md)

> **说明：**
> 
> 当accountId为当前用户时，不需要校验该权限。

**需要权限**: ohos.permission.INTERACT_ACROSS_LOCAL_ACCOUNTS

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**系统API**: 此接口为系统接口，三方应用不支持调用。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md) | 是 | 启动Ability的want信息。 |
| accountId | number | 是 | 系统帐号的帐号ID，详情参考[getCreatedOsAccountsCount](js-apis-osAccount.md#getCreatedOsAccountsCount)。 |
| callback | AsyncCallback&lt;[AbilityResult](js-apis-inner-ability-abilityResult.md)&gt; | 是 | 启动Ability的回调函数，返回Ability结果。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 16000001 | The specified ability does not exist. |
| 16000002 | Incorrect ability type. |
| 16000004 | Can not start invisible component. |
| 16000005 | The specified process does not have the permission. |
| 16000006 | Cross-user operations are not allowed. |
| 16000008 | The crowdtesting application expires. |
| 16000009 | An ability cannot be started or stopped in Wukong mode. |
| 16000010 | The call with the continuation flag is forbidden. |
| 16000011 | The context does not exist. |
| 16000012 | The application is controlled.        |
| 16000013 | The application is controlled by EDM.       |
| 16000050 | Internal error. |
| 16000053 | The ability is not on the top of the UI. |
| 16000055 | Installation-free timed out. |
| 16200001 | The caller has been released. |

错误码详细介绍请参考[errcode-ability](../errorcodes/errorcode-ability.md)

**示例：**

  ```ts
let want = {
  deviceId: '',
  bundleName: 'com.example.myapplication',
  abilityName: 'EntryAbility'
};
let accountId = 100;

try {
  this.context.startAbilityForResultWithAccount(want, accountId, (err, result) => {
    if (err.code) {
      // 处理业务逻辑错误
      console.error(`startAbilityForResultWithAccount failed, code is ${err.code}, message is ${err.message}`);
      return;
    }
    // 执行正常业务
    console.info('startAbilityForResultWithAccount succeed');
  });
} catch (err) {
  // 处理入参错误异常
  console.error(`startAbilityForResultWithAccount failed, code is ${err.code}, message is ${err.message}`);
}
  ```


## UIAbilityContext.startAbilityForResultWithAccount

startAbilityForResultWithAccount(want: Want, accountId: number, options: StartOptions, callback: AsyncCallback\<void\>): void;

启动一个Ability并在该Ability销毁时返回执行结果（callback形式）。

使用规则：
 - 调用方应用位于后台时，使用该接口启动Ability需申请`ohos.permission.START_ABILITIES_FROM_BACKGROUND`权限
 - 跨应用场景下，目标Ability的exported属性若配置为false，调用方应用需申请`ohos.permission.START_INVISIBLE_ABILITY`权限
 - 组件启动规则详见：[组件启动规则（Stage模型）](../../application-models/component-startup-rules.md)

> **说明：**
> 
> 当accountId为当前用户时，不需要校验该权限。

**需要权限**: ohos.permission.INTERACT_ACROSS_LOCAL_ACCOUNTS

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**系统API**: 此接口为系统接口，三方应用不支持调用。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md) | 是 | 启动Ability的want信息。 |
| accountId | number | 是 | 系统帐号的帐号ID，详情参考[getCreatedOsAccountsCount](js-apis-osAccount.md#getCreatedOsAccountsCount)。 |
| options | [StartOptions](js-apis-app-ability-startOptions.md) | 是 | 启动Ability所携带的参数。 |
| callback | AsyncCallback\<void\> | 是 | 启动Ability后，Ability被销毁时的回调函数。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 16000001 | The specified ability does not exist. |
| 16000002 | Incorrect ability type. |
| 16000004 | Can not start invisible component. |
| 16000005 | The specified process does not have the permission. |
| 16000006 | Cross-user operations are not allowed. |
| 16000008 | The crowdtesting application expires. |
| 16000009 | An ability cannot be started or stopped in Wukong mode. |
| 16000010 | The call with the continuation flag is forbidden. |
| 16000011 | The context does not exist. |
| 16000012 | The application is controlled.        |
| 16000013 | The application is controlled by EDM.       |
| 16000050 | Internal error. |
| 16000053 | The ability is not on the top of the UI. |
| 16000055 | Installation-free timed out. |
| 16200001 | The caller has been released. |

错误码详细介绍请参考[errcode-ability](../errorcodes/errorcode-ability.md)

**示例：**

  ```ts
let want = {
  deviceId: '',
  bundleName: 'com.example.myapplication',
  abilityName: 'EntryAbility'
};
let accountId = 100;
let options = {
  windowMode: 0
};

try {
  this.context.startAbilityForResultWithAccount(want, accountId, options, (err) => {
    if (err.code) {
      // 处理业务逻辑错误
      console.error(`startAbilityForResultWithAccount failed, code is ${err.code}, message is ${err.message}`);
      return;
    }
    // 执行正常业务
    console.info('startAbilityForResultWithAccount succeed');
  });
} catch (err) {
  // 处理入参错误异常
  console.error(`startAbilityForResultWithAccount failed, code is ${err.code}, message is ${err.message}`);
}
  ```


## UIAbilityContext.startAbilityForResultWithAccount

startAbilityForResultWithAccount(want: Want, accountId: number, options?: StartOptions): Promise\<AbilityResult\>;

启动一个Ability并在该Ability销毁时返回执行结果（promise形式）。

使用规则：
 - 调用方应用位于后台时，使用该接口启动Ability需申请`ohos.permission.START_ABILITIES_FROM_BACKGROUND`权限
 - 跨应用场景下，目标Ability的exported属性若配置为false，调用方应用需申请`ohos.permission.START_INVISIBLE_ABILITY`权限
 - 组件启动规则详见：[组件启动规则（Stage模型）](../../application-models/component-startup-rules.md)

> **说明：**
> 
> 当accountId为当前用户时，不需要校验该权限。

**需要权限**: ohos.permission.INTERACT_ACROSS_LOCAL_ACCOUNTS

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**系统API**: 此接口为系统接口，三方应用不支持调用。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md) | 是 | 启动Ability的want信息。 |
| accountId | number | 是 | 系统帐号的帐号ID，详情参考[getCreatedOsAccountsCount](js-apis-osAccount.md#getCreatedOsAccountsCount)。 |
| options | [StartOptions](js-apis-app-ability-startOptions.md) | 否 | 启动Ability所携带的参数。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| Promise&lt;[AbilityResult](js-apis-inner-ability-abilityResult.md)&gt; | Ability被销毁时的回调函数，包含AbilityResult参数。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 16000001 | The specified ability does not exist. |
| 16000002 | Incorrect ability type. |
| 16000004 | Can not start invisible component. |
| 16000005 | The specified process does not have the permission. |
| 16000006 | Cross-user operations are not allowed. |
| 16000008 | The crowdtesting application expires. |
| 16000009 | An ability cannot be started or stopped in Wukong mode. |
| 16000010 | The call with the continuation flag is forbidden. |
| 16000011 | The context does not exist. |
| 16000012 | The application is controlled.        |
| 16000013 | The application is controlled by EDM.       |
| 16000050 | Internal error. |
| 16000053 | The ability is not on the top of the UI. |
| 16000055 | Installation-free timed out. |
| 16200001 | The caller has been released. |

错误码详细介绍请参考[errcode-ability](../errorcodes/errorcode-ability.md)

**示例：**

  ```ts
let want = {
  deviceId: '',
  bundleName: 'com.example.myapplication',
  abilityName: 'EntryAbility'
};
let accountId = 100;
let options = {
  windowMode: 0
};

try {
  this.context.startAbilityForResultWithAccount(want, accountId, options)
    .then((result) => {
      // 执行正常业务
      console.info('startAbilityForResultWithAccount succeed');
    })
    .catch((err) => {
      // 处理业务逻辑错误
      console.error(`startAbilityForResultWithAccount failed, code is ${err.code}, message is ${err.message}`);
    });
} catch (err) {
  // 处理入参错误异常
  console.error(`startAbilityForResultWithAccount failed, code is ${err.code}, message is ${err.message}`);
}
  ```
## UIAbilityContext.startServiceExtensionAbility

startServiceExtensionAbility(want: Want, callback: AsyncCallback\<void>): void;

启动一个新的ServiceExtensionAbility（callback形式）。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**系统API**: 此接口为系统接口，三方应用不支持调用。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md) | 是 | 启动ServiceExtensionAbility的want信息。 |
| callback | AsyncCallback\<void\> | 是 | 启动ServiceExtensionAbility的回调函数。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 16000001 | The specified ability does not exist. |
| 16000002 | Incorrect ability type. |
| 16000004 | Can not start invisible component. |
| 16000005 | The specified process does not have the permission. |
| 16000006 | Cross-user operations are not allowed. |
| 16000008 | The crowdtesting application expires. |
| 16000011 | The context does not exist. |
| 16000012 | The application is controlled.        |
| 16000013 | The application is controlled by EDM.       |
| 16000050 | Internal error. |
| 16200001 | The caller has been released. |

错误码详细介绍请参考[errcode-ability](../errorcodes/errorcode-ability.md)

**示例：**

  ```ts
let want = {
  deviceId: '',
  bundleName: 'com.example.myapplication',
  abilityName: 'ServiceExtensionAbility'
};

try {
  this.context.startServiceExtensionAbility(want)
    .then(() => {
      // 执行正常业务
      console.info('startServiceExtensionAbility succeed');
    })
    .catch((err) => {
      // 处理业务逻辑错误
      console.error(`startServiceExtensionAbility failed, code is ${err.code}, message is ${err.message}`);
    });
} catch (err) {
  // 处理入参错误异常
  console.error(`startServiceExtensionAbility failed, code is ${err.code}, message is ${err.message}`);
}
  ```

## UIAbilityContext.startServiceExtensionAbility

startServiceExtensionAbility(want: Want): Promise\<void>;

启动一个新的ServiceExtensionAbility（Promise形式）。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**系统API**: 此接口为系统接口，三方应用不支持调用。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md) | 是 | 启动ServiceExtensionAbility的want信息。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 16000001 | The specified ability does not exist. |
| 16000002 | Incorrect ability type. |
| 16000004 | Can not start invisible component. |
| 16000005 | The specified process does not have the permission. |
| 16000006 | Cross-user operations are not allowed. |
| 16000008 | The crowdtesting application expires. |
| 16000011 | The context does not exist. |
| 16000012 | The application is controlled.        |
| 16000013 | The application is controlled by EDM.       |
| 16000050 | Internal error. |
| 16200001 | The caller has been released. |

错误码详细介绍请参考[errcode-ability](../errorcodes/errorcode-ability.md)

**示例：**

  ```ts
let want = {
  deviceId: '',
  bundleName: 'com.example.myapplication',
  abilityName: 'ServiceExtensionAbility'
};

try {
  this.context.startServiceExtensionAbility(want)
    .then(() => {
      // 执行正常业务
      console.info('startServiceExtensionAbility succeed');
    })
    .catch((err) => {
      // 处理业务逻辑错误
      console.error(`startServiceExtensionAbility failed, code is ${err.code}, message is ${err.message}`);
    });
} catch (err) {
  // 处理入参错误异常
  console.error(`startServiceExtensionAbility failed, code is ${err.code}, message is ${err.message}`);
}
  ```

## UIAbilityContext.startServiceExtensionAbilityWithAccount

startServiceExtensionAbilityWithAccount(want: Want, accountId: number, callback: AsyncCallback\<void>): void;

启动一个新的ServiceExtensionAbility（callback形式）。

> **说明：**
> 
> 当accountId为当前用户时，不需要校验该权限。

**需要权限**: ohos.permission.INTERACT_ACROSS_LOCAL_ACCOUNTS

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**系统API**: 此接口为系统接口，三方应用不支持调用。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md) | 是 | 启动ServiceExtensionAbility的want信息。 |
| accountId | number | 是 | 系统帐号的帐号ID，详情参考[getCreatedOsAccountsCount](js-apis-osAccount.md#getCreatedOsAccountsCount)。 |
| callback | AsyncCallback\<void\> | 是 | 启动ServiceExtensionAbility的回调函数。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 16000001 | The specified ability does not exist. |
| 16000002 | Incorrect ability type. |
| 16000004 | Can not start invisible component. |
| 16000005 | The specified process does not have the permission. |
| 16000006 | Cross-user operations are not allowed. |
| 16000008 | The crowdtesting application expires. |
| 16000011 | The context does not exist. |
| 16000012 | The application is controlled.        |
| 16000013 | The application is controlled by EDM.       |
| 16000050 | Internal error. |
| 16200001 | The caller has been released. |

错误码详细介绍请参考[errcode-ability](../errorcodes/errorcode-ability.md)

**示例：**

  ```ts
let want = {
  deviceId: '',
  bundleName: 'com.example.myapplication',
  abilityName: 'ServiceExtensionAbility'
};
let accountId = 100;

try {
  this.context.startServiceExtensionAbilityWithAccount(want, accountId, (err) => {
    if (err.code) {
      // 处理业务逻辑错误
      console.error(`startServiceExtensionAbilityWithAccount failed, code is ${err.code}, message is ${err.message}`);
      return;
    }
    // 执行正常业务
    console.info('startServiceExtensionAbilityWithAccount succeed');
  });
} catch (err) {
  // 处理入参错误异常
  console.error(`startServiceExtensionAbilityWithAccount failed, code is ${err.code}, message is ${err.message}`);
}
  ```

## UIAbilityContext.startServiceExtensionAbilityWithAccount

startServiceExtensionAbilityWithAccount(want: Want, accountId: number): Promise\<void>;

启动一个新的ServiceExtensionAbility（Promise形式）。

> **说明：**
> 
> 当accountId为当前用户时，不需要校验该权限。

**需要权限**: ohos.permission.INTERACT_ACROSS_LOCAL_ACCOUNTS

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**系统API**: 此接口为系统接口，三方应用不支持调用。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md) | 是 | 启动Ability的want信息。 |
| accountId | number | 是 | 系统帐号的帐号ID，详情参考[getCreatedOsAccountsCount](js-apis-osAccount.md#getCreatedOsAccountsCount)。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 16000001 | The specified ability does not exist. |
| 16000002 | Incorrect ability type. |
| 16000004 | Can not start invisible component. |
| 16000005 | The specified process does not have the permission. |
| 16000006 | Cross-user operations are not allowed. |
| 16000008 | The crowdtesting application expires. |
| 16000011 | The context does not exist. |
| 16000012 | The application is controlled.        |
| 16000013 | The application is controlled by EDM.       |
| 16000050 | Internal error. |
| 16200001 | The caller has been released. |

错误码详细介绍请参考[errcode-ability](../errorcodes/errorcode-ability.md)

**示例：**

  ```ts
let want = {
  deviceId: '',
  bundleName: 'com.example.myapplication',
  abilityName: 'ServiceExtensionAbility'
};
let accountId = 100;

try {
  this.context.startServiceExtensionAbilityWithAccount(want, accountId)
    .then(() => {
      // 执行正常业务
      console.info('startServiceExtensionAbilityWithAccount succeed');
    })
    .catch((err) => {
      // 处理业务逻辑错误
      console.error(`startServiceExtensionAbilityWithAccount failed, code is ${err.code}, message is ${err.message}`);
    });
} catch (err) {
  // 处理入参错误异常
  console.error(`startServiceExtensionAbilityWithAccount failed, code is ${err.code}, message is ${err.message}`);
}
  ```
## UIAbilityContext.stopServiceExtensionAbility

stopServiceExtensionAbility(want: Want, callback: AsyncCallback\<void>): void;

停止同一应用程序内的服务（callback形式）。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**系统API**: 此接口为系统接口，三方应用不支持调用。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md) | 是 | 停止ServiceExtensionAbility的want信息。 |
| callback | AsyncCallback\<void\> | 是 | 停止ServiceExtensionAbility的回调函数。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 16000001 | The specified ability does not exist. |
| 16000002 | Incorrect ability type. |
| 16000004 | Can not start invisible component. |
| 16000005 | The specified process does not have the permission. |
| 16000006 | Cross-user operations are not allowed. |
| 16000011 | The context does not exist. |
| 16000012 | The application is controlled.        |
| 16000013 | The application is controlled by EDM.       |
| 16000050 | Internal error. |
| 16200001 | The caller has been released. |

错误码详细介绍请参考[errcode-ability](../errorcodes/errorcode-ability.md)

**示例：**

  ```ts
let want = {
  deviceId: '',
  bundleName: 'com.example.myapplication',
  abilityName: 'ServiceExtensionAbility'
};

try {
  this.context.stopServiceExtensionAbility(want, (err) => {
    if (err.code) {
      // 处理业务逻辑错误
      console.error(`stopServiceExtensionAbility failed, code is ${err.code}, message is ${err.message}`);
      return;
    }
    // 执行正常业务
    console.info('stopServiceExtensionAbility succeed');
  });
} catch (err) {
  // 处理入参错误异常
  console.error(`stopServiceExtensionAbility failed, code is ${err.code}, message is ${err.message}`);
}
  ```

## UIAbilityContext.stopServiceExtensionAbility

stopServiceExtensionAbility(want: Want): Promise\<void>;

停止同一应用程序内的服务（Promise形式）。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**系统API**: 此接口为系统接口，三方应用不支持调用。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md) | 是 | 停止ServiceExtensionAbility的want信息。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 16000001 | The specified ability does not exist. |
| 16000002 | Incorrect ability type. |
| 16000004 | Can not start invisible component. |
| 16000005 | The specified process does not have the permission. |
| 16000006 | Cross-user operations are not allowed. |
| 16000011 | The context does not exist. |
| 16000050 | Internal error. |
| 16200001 | The caller has been released. |

错误码详细介绍请参考[errcode-ability](../errorcodes/errorcode-ability.md)

**示例：**

  ```ts
let want = {
  deviceId: '',
  bundleName: 'com.example.myapplication',
  abilityName: 'ServiceExtensionAbility'
};

try {
  this.context.stopServiceExtensionAbility(want)
    .then(() => {
      // 执行正常业务
      console.info('stopServiceExtensionAbility succeed');
    })
    .catch((err) => {
      // 处理业务逻辑错误
      console.error(`stopServiceExtensionAbility failed, code is ${err.code}, message is ${err.message}`);
    });
} catch (err) {
  // 处理入参错误异常
  console.error(`stopServiceExtensionAbility failed, code is ${err.code}, message is ${err.message}`);
}
  ```

## UIAbilityContext.stopServiceExtensionAbilityWithAccount

stopServiceExtensionAbilityWithAccount(want: Want, accountId: number, callback: AsyncCallback\<void>): void;

停止同一应用程序内指定账户的服务（callback形式）。

> **说明：**
> 
> 当accountId为当前用户时，不需要校验该权限。

**需要权限**: ohos.permission.INTERACT_ACROSS_LOCAL_ACCOUNTS

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**系统API**: 此接口为系统接口，三方应用不支持调用。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md) | 是 | 停止ServiceExtensionAbility的want信息。 |
| accountId | number | 是 | 系统帐号的帐号ID，详情参考[getCreatedOsAccountsCount](js-apis-osAccount.md#getCreatedOsAccountsCount)。 |
| callback | AsyncCallback\<void\> | 是 | 停止ServiceExtensionAbility的回调函数。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 16000001 | The specified ability does not exist. |
| 16000002 | Incorrect ability type. |
| 16000004 | Can not start invisible component. |
| 16000005 | The specified process does not have the permission. |
| 16000006 | Cross-user operations are not allowed. |
| 16000011 | The context does not exist. |
| 16000050 | Internal error. |
| 16200001 | The caller has been released. |

错误码详细介绍请参考[errcode-ability](../errorcodes/errorcode-ability.md)

**示例：**

  ```ts
let want = {
  deviceId: '',
  bundleName: 'com.example.myapplication',
  abilityName: 'ServiceExtensionAbility'
};
let accountId = 100;

try {
  this.context.stopServiceExtensionAbilityWithAccount(want, accountId, (err) => {
    if (err.code) {
      // 处理业务逻辑错误
      console.error(`stopServiceExtensionAbilityWithAccount failed, code is ${err.code}, message is ${err.message}`);
      return;
    }
    // 执行正常业务
    console.info('stopServiceExtensionAbilityWithAccount succeed');
  });
} catch (err) {
  // 处理入参错误异常
  console.error(`stopServiceExtensionAbilityWithAccount failed, code is ${err.code}, message is ${err.message}`);
}
  ```

## UIAbilityContext.stopServiceExtensionAbilityWithAccount

stopServiceExtensionAbilityWithAccount(want: Want, accountId: number): Promise\<void>;

停止同一应用程序内指定账户的服务（Promise形式）。

> **说明：**
> 
> 当accountId为当前用户时，不需要校验该权限。

**需要权限**: ohos.permission.INTERACT_ACROSS_LOCAL_ACCOUNTS

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**系统API**: 此接口为系统接口，三方应用不支持调用。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md) | 是 | 停止ServiceExtensionAbility的want信息。 |
| accountId | number | 是 | 系统帐号的帐号ID，详情参考[getCreatedOsAccountsCount](js-apis-osAccount.md#getCreatedOsAccountsCount)。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 16000001 | The specified ability does not exist. |
| 16000002 | Incorrect ability type. |
| 16000004 | Can not start invisible component. |
| 16000005 | The specified process does not have the permission. |
| 16000006 | Cross-user operations are not allowed. |
| 16000011 | The context does not exist. |
| 16000050 | Internal error. |
| 16200001 | The caller has been released. |

错误码详细介绍请参考[errcode-ability](../errorcodes/errorcode-ability.md)

**示例：**

  ```ts
let want = {
  deviceId: '',
  bundleName: 'com.example.myapplication',
  abilityName: 'ServiceExtensionAbility'
};
let accountId = 100;

try {
  this.context.stopServiceExtensionAbilityWithAccount(want, accountId)
    .then(() => {
      // 执行正常业务
      console.info('stopServiceExtensionAbilityWithAccount succeed');
    })
    .catch((err) => {
      // 处理业务逻辑错误
      console.error(`stopServiceExtensionAbilityWithAccount failed, code is ${err.code}, message is ${err.message}`);
    });
} catch (err) {
  // 处理入参错误异常
  console.error(`stopServiceExtensionAbilityWithAccount failed, code is ${err.code}, message is ${err.message}`);
}
  ```

## UIAbilityContext.terminateSelf

terminateSelf(callback: AsyncCallback&lt;void&gt;): void;

停止Ability自身（callback形式）。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| callback | AsyncCallback&lt;void&gt; | 是 | 停止Ability自身的回调函数。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 16000001 | The specified ability does not exist. |
| 16000004 | Can not start invisible component. |
| 16000005 | The specified process does not have the permission. |
| 16000009 | An ability cannot be started or stopped in Wukong mode. |
| 16000011 | The context does not exist. |
| 16000050 | Internal error. |

错误码详细介绍请参考[errcode-ability](../errorcodes/errorcode-ability.md)

**示例：**

  ```ts
  try {
    this.context.terminateSelf((err) => {
      if (err.code) {
        // 处理业务逻辑错误
        console.error(`terminateSelf failed, code is ${err.code}, message is ${err.message}`);
        return;
      }
      // 执行正常业务
      console.info('terminateSelf succeed');
    });
  } catch (err) {
    // 捕获同步的参数错误
    console.error(`terminateSelf failed, code is ${err.code}, message is ${err.message}`);
  }
  ```


## UIAbilityContext.terminateSelf

terminateSelf(): Promise&lt;void&gt;;

停止Ability自身（promise形式）。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| Promise&lt;void&gt; | 停止Ability自身的回调函数。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 16000001 | The specified ability does not exist. |
| 16000004 | Can not start invisible component. |
| 16000005 | The specified process does not have the permission. |
| 16000009 | An ability cannot be started or stopped in Wukong mode. |
| 16000011 | The context does not exist. |
| 16000050 | Internal error. |

错误码详细介绍请参考[errcode-ability](../errorcodes/errorcode-ability.md)

**示例：**

  ```ts
  try {
    this.context.terminateSelf()
      .then(() => {
        // 执行正常业务
        console.info('terminateSelf succeed');
      })
      .catch((err) => {
        // 处理业务逻辑错误
        console.error(`terminateSelf failed, code is ${err.code}, message is ${err.message}`);
      });
  } catch (err) {
    // 捕获同步的参数错误
    console.error(`terminateSelf failed, code is ${err.code}, message is ${err.message}`);
  }
  ```


## UIAbilityContext.terminateSelfWithResult

terminateSelfWithResult(parameter: AbilityResult, callback: AsyncCallback&lt;void&gt;): void;

停止当前的Ability。如果该Ability是通过调用[startAbilityForResult](#uiabilitycontextstartabilityforresult)接口被拉起的，调用terminateSelfWithResult接口时会将结果返回给调用者，如果该Ability不是通过调用[startAbilityForResult](#uiabilitycontextstartabilityforresult)接口被拉起的，调用terminateSelfWithResult接口时不会有结果返回给调用者（callback形式）。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| parameter | [AbilityResult](js-apis-inner-ability-abilityResult.md) | 是 | 返回给调用startAbilityForResult&nbsp;接口调用方的相关信息。 |
| callback | AsyncCallback&lt;void&gt; | 是 | callback形式返回停止结果。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 16000001 | The specified ability does not exist. |
| 16000004 | Can not start invisible component. |
| 16000005 | The specified process does not have the permission. |
| 16000009 | An ability cannot be started or stopped in Wukong mode. |
| 16000011 | The context does not exist. |
| 16000050 | Internal error. |

错误码详细介绍请参考[errcode-ability](../errorcodes/errorcode-ability.md)

**示例：**

  ```ts
let want = {
  bundleName: 'com.example.myapplication',
  abilityName: 'EntryAbility'
};
let resultCode = 100;
// 返回给接口调用方AbilityResult信息
let abilityResult = {
  want,
  resultCode
};

try {
  this.context.terminateSelfWithResult(abilityResult, (err) => {
    if (err.code) {
      // 处理业务逻辑错误
      console.error(`terminateSelfWithResult failed, code is ${err.code}, message is ${err.message}`);
      return;
    }
    // 执行正常业务
    console.info('terminateSelfWithResult succeed');
  });
} catch (err) {
  // 处理入参错误异常
  console.error(`terminateSelfWithResult failed, code is ${err.code}, message is ${err.message}`);
}
  ```


## UIAbilityContext.terminateSelfWithResult

terminateSelfWithResult(parameter: AbilityResult): Promise&lt;void&gt;;

停止当前的Ability。如果该Ability是通过调用[startAbilityForResult](#uiabilitycontextstartabilityforresult)接口被拉起的，调用terminateSelfWithResult接口时会将结果返回给调用者，如果该Ability不是通过调用[startAbilityForResult](#uiabilitycontextstartabilityforresult)接口被拉起的，调用terminateSelfWithResult接口时不会有结果返回给调用者（promise形式）。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| parameter | [AbilityResult](js-apis-inner-ability-abilityResult.md) | 是 | 返回给startAbilityForResult&nbsp;调用方的信息。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| Promise&lt;void&gt; | promise形式返回停止结果。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 16000001 | The specified ability does not exist. |
| 16000004 | Can not start invisible component. |
| 16000005 | The specified process does not have the permission. |
| 16000009 | An ability cannot be started or stopped in Wukong mode. |
| 16000011 | The context does not exist. |
| 16000050 | Internal error. |

错误码详细介绍请参考[errcode-ability](../errorcodes/errorcode-ability.md)

**示例：**

  ```ts
let want = {
  bundleName: 'com.example.myapplication',
  abilityName: 'EntryAbility'
};
let resultCode = 100;
// 返回给接口调用方AbilityResult信息
let abilityResult = {
  want,
  resultCode
};

try {
  this.context.terminateSelfWithResult(abilityResult)
    .then(() => {
      // 执行正常业务
      console.info('terminateSelfWithResult succeed');
    })
    .catch((err) => {
      // 处理业务逻辑错误
      console.error(`terminateSelfWithResult failed, code is ${err.code}, message is ${err.message}`);
    });
} catch (err) {
  // 处理入参错误异常
  console.error(`terminateSelfWithResult failed, code is ${err.code}, message is ${err.message}`);
}
  ```

## UIAbilityContext.connectServiceExtensionAbility

connectServiceExtensionAbility(want: Want, options: ConnectOptions): number;

将当前Ability连接到一个使用AbilityInfo.AbilityType.SERVICE模板的Ability。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md) | 是 | 连接ServiceExtensionAbility的want信息。 |
| options | [ConnectOptions](js-apis-inner-ability-connectOptions.md) | 是 | 与ServiceExtensionAbility建立连接后回调函数的实例。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| number | 返回Ability连接的结果code。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 16000001 | The specified ability does not exist. |
| 16000002 | Incorrect ability type. |
| 16000004 | Can not start invisible component. |
| 16000005 | The specified process does not have the permission. |
| 16000006 | Cross-user operations are not allowed. |
| 16000008 | The crowdtesting application expires. |
| 16000053 | The ability is not on the top of the UI. |
| 16000055 | Installation-free timed out. |
| 16000011 | The context does not exist.        |
| 16000050 | Internal error. |

错误码详细介绍请参考[errcode-ability](../errorcodes/errorcode-ability.md)

**示例：**

  ```ts
let want = {
  deviceId: '',
  bundleName: 'com.example.myapplication',
  abilityName: 'ServiceExtensionAbility'
};
let commRemote;
let options = {
  onConnect(elementName, remote) {
    commRemote = remote;
    console.info('onConnect...')
  },
  onDisconnect(elementName) {
    console.info('onDisconnect...')
  },
  onFailed(code) {
    console.info('onFailed...')
  }
};

let connection = null;
try {
  connection = this.context.connectServiceExtensionAbility(want, options);
} catch (err) {
  // 处理入参错误异常
  console.error(`connectServiceExtensionAbility failed, code is ${err.code}, message is ${err.message}`);
}
  ```


## UIAbilityContext.connectServiceExtensionAbilityWithAccount

connectServiceExtensionAbilityWithAccount(want: Want, accountId: number, options: ConnectOptions): number;

将当前Ability连接到一个使用AbilityInfo.AbilityType.SERVICE模板的指定account的Ability。

> **说明：**
> 
> 当accountId为当前用户时，不需要校验该权限。

**需要权限：** ohos.permission.INTERACT_ACROSS_LOCAL_ACCOUNTS

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**系统API**: 此接口为系统接口，三方应用不支持调用。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md) | 是 | 启动Ability的want信息。 |
| accountId | number | 是 | 系统帐号的帐号ID，详情参考[getCreatedOsAccountsCount](js-apis-osAccount.md#getCreatedOsAccountsCount)。 |
| options | [ConnectOptions](js-apis-inner-ability-connectOptions.md) | 是 | 与ServiceExtensionAbility建立连接后回调函数的实例。。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| number | 返回Ability连接的结果code。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 16000001 | The specified ability does not exist. |
| 16000002 | Incorrect ability type. |
| 16000004 | Can not start invisible component. |
| 16000006 | Cross-user operations are not allowed. |
| 16000008 | The crowdtesting application expires. |
| 16000053 | The ability is not on the top of the UI. |
| 16000055 | Installation-free timed out. |
| 16000011 | The context does not exist.        |
| 16000050 | Internal error. |

错误码详细介绍请参考[errcode-ability](../errorcodes/errorcode-ability.md)

**示例：**

  ```ts
let want = {
  deviceId: '',
  bundleName: 'com.example.myapplication',
  abilityName: 'ServiceExtensionAbility'
};
let accountId = 100;
let commRemote;
let options = {
  onConnect(elementName, remote) {
    commRemote = remote;
    console.info('onConnect...')
  },
  onDisconnect(elementName) {
    console.info('onDisconnect...')
  },
  onFailed(code) {
    console.info('onFailed...')
  }
};

let connection = null;
try {
  connection = this.context.connectServiceExtensionAbilityWithAccount(want, accountId, options);
} catch (err) {
  // 处理入参错误异常
  console.error(`connectServiceExtensionAbility failed, code is ${err.code}, message is ${err.message}`);
}
  ```

## UIAbilityContext.disconnectServiceExtensionAbility

disconnectServiceExtensionAbility(connection: number): Promise\<void>;

断开与ServiceExtensionAbility的连接，断开连接之后需要将连接成功时返回的remote对象置空（promise形式）。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| connection | number | 是 | 连接的ServiceExtensionAbility的数字代码，即connectServiceExtensionAbility返回的connectionId。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| Promise\<void> | 返回执行结果。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 16000011 | The context does not exist. |
| 16000050 | Internal error. |

错误码详细介绍请参考[errcode-ability](../errorcodes/errorcode-ability.md)

**示例：**

  ```ts
// connection为connectServiceExtensionAbility中的返回值
let connection = 1;
let commRemote;

try {
  this.context.disconnectServiceExtensionAbility(connection, (err) => {
    commRemote = null;
    if (err.code) {
      // 处理业务逻辑错误
      console.error(`disconnectServiceExtensionAbility failed, code is ${err.code}, message is ${err.message}`);
      return;
    }
    // 执行正常业务
    console.info('disconnectServiceExtensionAbility succeed');
  });
} catch (err) {
  commRemote = null;
  // 处理入参错误异常
  console.error(`disconnectServiceExtensionAbility failed, code is ${err.code}, message is ${err.message}`);
}
  ```

## UIAbilityContext.disconnectServiceExtensionAbility

disconnectServiceExtensionAbility(connection: number, callback:AsyncCallback\<void>): void;

断开与ServiceExtensionAbility的连接，断开连接之后需要将连接成功时返回的remote对象置空（callback形式）。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| connection | number | 是 | 连接的ServiceExtensionAbility的数字代码，即connectServiceExtensionAbility返回的connectionId。 |
| callback | AsyncCallback\<void> | 是 | callback形式返回断开连接的结果。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 16000011 | The context does not exist. |
| 16000050 | Internal error. |

错误码详细介绍请参考[errcode-ability](../errorcodes/errorcode-ability.md)

**示例：**

  ```ts
// connection为connectServiceExtensionAbility中的返回值
let connection = 1;
let commRemote;

try {
  this.context.disconnectServiceExtensionAbility(connection, (err) => {
    commRemote = null;
    if (err.code) {
      // 处理业务逻辑错误
      console.error(`disconnectServiceExtensionAbility failed, code is ${err.code}, message is ${err.message}`);
      return;
    }
    // 执行正常业务
    console.info('disconnectServiceExtensionAbility succeed');
  });
} catch (err) {
  commRemote = null;
  // 处理入参错误异常
  console.error(`disconnectServiceExtensionAbility failed, code is ${err.code}, message is ${err.message}`);
}

try {
  this.context.disconnectServiceExtensionAbility(connection, (err) => {
    commRemote = null;
    if (err.code) {
      // 处理业务逻辑错误
      console.error(`disconnectServiceExtensionAbility failed, code is ${err.code}, message is ${err.message}`);
      return;
    }
    // 执行正常业务
    console.info('disconnectServiceExtensionAbility succeed');
  });
} catch (err) {
  commRemote = null;
  // 处理入参错误异常
  console.error(`disconnectServiceExtensionAbility failed, code is ${err.code}, message is ${err.message}`);
}
  ```

## UIAbilityContext.startAbilityByCall

startAbilityByCall(want: Want): Promise&lt;Caller&gt;;

启动指定Ability至前台或后台，同时获取其Caller通信接口，调用方可使用Caller与被启动的Ability进行通信。

使用规则：
 - 调用方应用位于后台时，使用该接口启动Ability需申请`ohos.permission.START_ABILITIES_FROM_BACKGROUND`权限
 - 跨应用场景下，目标Ability的exported属性若配置为false，调用方应用需申请`ohos.permission.START_INVISIBLE_ABILITY`权限
 - 同设备与跨设备场景下，该接口的使用规则存在差异，详见：[组件启动规则（Stage模型）](../../application-models/component-startup-rules.md)

**需要权限：** ohos.permission.ABILITY_BACKGROUND_COMMUNICATION

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md) | 是 | 传入需要启动的Ability的信息，包含abilityName、moduleName、bundleName、deviceId(可选)、parameters(可选)，其中deviceId缺省或为空表示启动本地Ability，parameters缺省或为空表示后台启动Ability。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| Promise&lt;Caller&gt; | 获取要通讯的caller对象。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 16000001 | The specified ability does not exist. |
| 16000002 | Incorrect ability type. |
| 16000004 | Can not start invisible component. |
| 16000005 | The specified process does not have the permission. |
| 16000006 | Cross-user operations are not allowed. |
| 16000008 | The crowdtesting application expires. |
| 16000011 | The context does not exist. |
| 16000012 | The application is controlled.        |
| 16000013 | The application is controlled by EDM.       |
| 16000050 | Internal error. |
| 16200001 | The caller has been released. |

错误码详细介绍请参考[errcode-ability](../errorcodes/errorcode-ability.md)

**示例：**

  后台启动：

  ```ts
let caller;

// 后台启动Ability，不配置parameters
let wantBackground = {
  bundleName: 'com.example.myapplication',
  moduleName: 'entry',
  abilityName: 'EntryAbility',
  deviceId: ''
};

try {
  this.context.startAbilityByCall(wantBackground)
    .then((obj) => {
      // 执行正常业务
      caller = obj;
      console.info('startAbilityByCall succeed');
    }).catch((err) => {
    // 处理业务逻辑错误
    console.error(`startAbilityByCall failed, code is ${err.code}, message is ${err.message}`);
  });
} catch (err) {
  // 处理入参错误异常
  console.error(`startAbilityByCall failed, code is ${err.code}, message is ${err.message}`);
}
  ```

前台启动：

  ```ts
let caller;

// 前台启动Ability，将parameters中的'ohos.aafwk.param.callAbilityToForeground'配置为true
let wantForeground = {
  bundleName: 'com.example.myapplication',
  moduleName: 'entry',
  abilityName: 'EntryAbility',
  deviceId: '',
  parameters: {
    'ohos.aafwk.param.callAbilityToForeground': true
  }
};

try {
  this.context.startAbilityByCall(wantForeground)
    .then((obj) => {
      // 执行正常业务
      caller = obj;
      console.info('startAbilityByCall succeed');
    }).catch((err) => {
    // 处理业务逻辑错误
    console.error(`startAbilityByCall failed, code is ${err.code}, message is ${err.message}`);
  });
} catch (err) {
  // 处理入参错误异常
  console.error(`startAbilityByCall failed, code is ${err.code}, message is ${err.message}`);
}
  ```

## UIAbilityContext.startAbilityWithAccount

startAbilityWithAccount(want: Want, accountId: number, callback: AsyncCallback\<void\>): void;

根据want和accountId启动Ability（callback形式）。

使用规则：
 - 调用方应用位于后台时，使用该接口启动Ability需申请`ohos.permission.START_ABILITIES_FROM_BACKGROUND`权限
 - 跨应用场景下，目标Ability的exported属性若配置为false，调用方应用需申请`ohos.permission.START_INVISIBLE_ABILITY`权限
 - 组件启动规则详见：[组件启动规则（Stage模型）](../../application-models/component-startup-rules.md)

> **说明：**
> 
> 当accountId为当前用户时，不需要校验该权限。

**需要权限：** ohos.permission.INTERACT_ACROSS_LOCAL_ACCOUNTS

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**系统API**: 此接口为系统接口，三方应用不支持调用。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md) | 是 | 启动Ability的want信息。 |
| accountId | number | 是 | 系统帐号的帐号ID，详情参考[getCreatedOsAccountsCount](js-apis-osAccount.md#getCreatedOsAccountsCount)。 |
| callback | AsyncCallback\<void\> | 是 | 启动Ability的回调函数。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 16000001 | The specified ability does not exist. |
| 16000002 | Incorrect ability type. |
| 16000004 | Can not start invisible component. |
| 16000005 | The specified process does not have the permission. |
| 16000006 | Cross-user operations are not allowed. |
| 16000008 | The crowdtesting application expires. |
| 16000009 | An ability cannot be started or stopped in Wukong mode. |
| 16000010 | The call with the continuation flag is forbidden. |
| 16000011 | The context does not exist. |
| 16000012 | The application is controlled.        |
| 16000013 | The application is controlled by EDM.       |
| 16000050 | Internal error. |
| 16000053 | The ability is not on the top of the UI. |
| 16000055 | Installation-free timed out. |
| 16200001 | The caller has been released. |

错误码详细介绍请参考[errcode-ability](../errorcodes/errorcode-ability.md)

**示例：**

  ```ts
let want = {
  deviceId: '',
  bundleName: 'com.example.myapplication',
  abilityName: 'EntryAbility'
};
let accountId = 100;

try {
  this.context.startAbilityWithAccount(want, accountId, (err) => {
    if (err.code) {
      // 处理业务逻辑错误
      console.error(`startAbilityWithAccount failed, code is ${err.code}, message is ${err.message}`);
      return;
    }
    // 执行正常业务
    console.info('startAbilityWithAccount succeed');
  });
} catch (err) {
  // 处理入参错误异常
  console.error(`startAbilityWithAccount failed, code is ${err.code}, message is ${err.message}`);
}
  ```


## UIAbilityContext.startAbilityWithAccount

startAbilityWithAccount(want: Want, accountId: number, options: StartOptions, callback: AsyncCallback\<void\>): void;

根据want、accountId及startOptions启动Ability（callback形式）。

使用规则：
 - 调用方应用位于后台时，使用该接口启动Ability需申请`ohos.permission.START_ABILITIES_FROM_BACKGROUND`权限
 - 跨应用场景下，目标Ability的exported属性若配置为false，调用方应用需申请`ohos.permission.START_INVISIBLE_ABILITY`权限
 - 组件启动规则详见：[组件启动规则（Stage模型）](../../application-models/component-startup-rules.md)

> **说明：**
> 
> 当accountId为当前用户时，不需要校验该权限。

**需要权限：** ohos.permission.INTERACT_ACROSS_LOCAL_ACCOUNTS

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**系统API**: 此接口为系统接口，三方应用不支持调用。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md) | 是 | 启动Ability的want信息。 |
| accountId | number | 是 | 系统帐号的帐号ID，详情参考[getCreatedOsAccountsCount](js-apis-osAccount.md#getCreatedOsAccountsCount)。|
| options | [StartOptions](js-apis-app-ability-startOptions.md) | 是 | 启动Ability所携带的参数。 |
| callback | AsyncCallback\<void\> | 是 | 启动Ability的回调函数。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 16000001 | The specified ability does not exist. |
| 16000002 | Incorrect ability type. |
| 16000004 | Can not start invisible component. |
| 16000005 | The specified process does not have the permission. |
| 16000006 | Cross-user operations are not allowed. |
| 16000008 | The crowdtesting application expires. |
| 16000009 | An ability cannot be started or stopped in Wukong mode. |
| 16000010 | The call with the continuation flag is forbidden. |
| 16000011 | The context does not exist. |
| 16000012 | The application is controlled.        |
| 16000013 | The application is controlled by EDM.       |
| 16000050 | Internal error. |
| 16000053 | The ability is not on the top of the UI. |
| 16000055 | Installation-free timed out. |
| 16200001 | The caller has been released. |

错误码详细介绍请参考[errcode-ability](../errorcodes/errorcode-ability.md)

**示例：**

  ```ts
let want = {
  deviceId: '',
  bundleName: 'com.example.myapplication',
  abilityName: 'EntryAbility'
};
let accountId = 100;
let options = {
  windowMode: 0
};

try {
  this.context.startAbilityWithAccount(want, accountId, options, (err) => {
    if (err.code) {
      // 处理业务逻辑错误
      console.error(`startAbilityWithAccount failed, code is ${err.code}, message is ${err.message}`);
      return;
    }
    // 执行正常业务
    console.info('startAbilityWithAccount succeed');
  });
} catch (err) {
  // 处理入参错误异常
  console.error(`startAbilityWithAccount failed, code is ${err.code}, message is ${err.message}`);
}
  ```


## UIAbilityContext.startAbilityWithAccount

startAbilityWithAccount(want: Want, accountId: number, options?: StartOptions): Promise\<void\>;

根据want、accountId和startOptions启动Ability（Promise形式）。

使用规则：
 - 调用方应用位于后台时，使用该接口启动Ability需申请`ohos.permission.START_ABILITIES_FROM_BACKGROUND`权限
 - 跨应用场景下，目标Ability的exported属性若配置为false，调用方应用需申请`ohos.permission.START_INVISIBLE_ABILITY`权限
 - 组件启动规则详见：[组件启动规则（Stage模型）](../../application-models/component-startup-rules.md)

> **说明：**
> 
> 当accountId为当前用户时，不需要校验该权限。

**需要权限：** ohos.permission.INTERACT_ACROSS_LOCAL_ACCOUNTS

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**系统API**: 此接口为系统接口，三方应用不支持调用。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md) | 是 | 启动Ability的want信息。 |
| accountId | number | 是 | 系统帐号的帐号ID，详情参考[getCreatedOsAccountsCount](js-apis-osAccount.md#getCreatedOsAccountsCount)。 |
| options | [StartOptions](js-apis-app-ability-startOptions.md) | 否 | 启动Ability所携带的参数。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 16000001 | The specified ability does not exist. |
| 16000002 | Incorrect ability type. |
| 16000004 | Can not start invisible component. |
| 16000005 | The specified process does not have the permission. |
| 16000006 | Cross-user operations are not allowed. |
| 16000008 | The crowdtesting application expires. |
| 16000009 | An ability cannot be started or stopped in Wukong mode. |
| 16000010 | The call with the continuation flag is forbidden. |
| 16000011 | The context does not exist. |
| 16000012 | The application is controlled.        |
| 16000013 | The application is controlled by EDM.       |
| 16000050 | Internal error. |
| 16000053 | The ability is not on the top of the UI. |
| 16000055 | Installation-free timed out. |
| 16200001 | The caller has been released. |

错误码详细介绍请参考[errcode-ability](../errorcodes/errorcode-ability.md)

**示例：**

  ```ts
let want = {
  deviceId: '',
  bundleName: 'com.example.myapplication',
  abilityName: 'EntryAbility'
};
let accountId = 100;
let options = {
  windowMode: 0
};

try {
  this.context.startAbilityWithAccount(want, accountId, options)
    .then(() => {
      // 执行正常业务
      console.info('startAbilityWithAccount succeed');
    })
    .catch((err) => {
      // 处理业务逻辑错误
      console.error(`startAbilityWithAccount failed, code is ${err.code}, message is ${err.message}`);
    });
} catch (err) {
  // 处理入参错误异常
  console.error(`startAbilityWithAccount failed, code is ${err.code}, message is ${err.message}`);
}
  ```

## UIAbilityContext.setMissionLabel

setMissionLabel(label: string, callback:AsyncCallback&lt;void&gt;): void;

设置UIAbility在任务中显示的名称（callback形式）。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| label | string | 是 | 显示名称。 |
| callback | AsyncCallback&lt;void&gt; | 是 | 回调函数，返回接口调用是否成功的结果。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 16000011 | The context does not exist. |
| 16000050 | Internal error. |

错误码详细介绍请参考[errcode-ability](../errorcodes/errorcode-ability.md)

**示例：**

  ```ts
  this.context.setMissionLabel('test', (result) => {
    console.info(`setMissionLabel: ${JSON.stringify(result)}`);
  });
  ```

## UIAbilityContext.setMissionLabel

setMissionLabel(label: string): Promise&lt;void&gt;;

设置UIAbility在任务中显示的名称（promise形式）。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| label | string | 是 | 显示名称。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| Promise&lt;void&gt; | 返回一个Promise，包含接口的结果。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 16000011 | The context does not exist. |
| 16000050 | Internal error. |

错误码详细介绍请参考[errcode-ability](../errorcodes/errorcode-ability.md)

**示例：**

  ```ts
  this.context.setMissionLabel('test').then(() => {
    console.info('success');
  }).catch((err) => {
    console.error(`setMissionLabel failed, code is ${err.code}, message is ${err.message}`);
  });
  ```
## UIAbilityContext.setMissionIcon

setMissionIcon(icon: image.PixelMap, callback:AsyncCallback\<void>): void;

设置当前ability在任务中显示的图标, 图标大小最大为600M（callback形式）。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**系统API**: 此接口为系统接口，三方应用不支持调用。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| icon | image.PixelMap | 是 | 在最近的任务中显示的ability图标。 |
| callback | AsyncCallback\<void> | 是 | 指定的回调函数的结果。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 16000011 | The context does not exist. |
| 16000050 | Internal error. |

错误码详细介绍请参考[errcode-ability](../errorcodes/errorcode-ability.md)

**示例：**

  ```ts
  import image from '@ohos.multimedia.image';
  
  let imagePixelMap;
  let color = new ArrayBuffer(0);
  let initializationOptions = {
    size: {
      height: 100,
      width: 100
    }
  };
  image.createPixelMap(color, initializationOptions)
    .then((data) => {
      imagePixelMap = data;
    })
    .catch((err) => {
      console.error(`createPixelMap failed, code is ${err.code}, message is ${err.message}`);
    });
  this.context.setMissionIcon(imagePixelMap, (err) => {
    console.error(`setMissionLabel failed, code is ${err.code}, message is ${err.message}`);
  })
  ```


## UIAbilityContext.setMissionIcon

setMissionIcon(icon: image.PixelMap): Promise\<void>;

设置当前ability在任务中显示的图标, 图标大小最大为600M（promise形式）。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**系统API**: 此接口为系统接口，三方应用不支持调用。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| icon | image.PixelMap | 是 | 在最近的任务中显示的ability图标。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| Promise&lt;void&gt; | 返回一个Promise，包含接口的结果。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 16000011 | The context does not exist. |
| 16000050 | Internal error. |

错误码详细介绍请参考[errcode-ability](../errorcodes/errorcode-ability.md)

**示例：**

  ```ts
  import image from '@ohos.multimedia.image';

  let imagePixelMap;
  let color = new ArrayBuffer(0);
  let initializationOptions = {
    size: {
      height: 100,
      width: 100
    }
  };
  image.createPixelMap(color, initializationOptions)
    .then((data) => {
      imagePixelMap = data;
    })
    .catch((err) => {
      console.error(`createPixelMap failed, code is ${err.code}, message is ${err.message}`);
    });
  this.context.setMissionIcon(imagePixelMap)
    .then(() => {
      console.info('setMissionIcon succeed');
    })
    .catch((err) => {
      console.error(`setMissionLabel failed, code is ${err.code}, message is ${err.message}`);
    });
  ```

## UIAbilityContext.setMissionContinueState<sup>10+</sup>

setMissionContinueState(state: AbilityConstant.ContinueState, callback:AsyncCallback&lt;void&gt;): void;

设置UIAbility任务中流转状态（callback形式）。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| state | [AbilityConstant.ContinueState](js-apis-app-ability-abilityConstant.md#abilityconstantcontinuestate10) | 是 | 流转状态。 |
| callback | AsyncCallback&lt;void&gt; | 是 | 回调函数，返回接口调用是否成功的结果。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 16000011 | The context does not exist. |
| 16000050 | Internal error. |

错误码详细介绍请参考[errcode-ability](../errorcodes/errorcode-ability.md)

**示例：**

  ```ts
  import AbilityConstant from '@ohos.app.ability.AbilityConstant';

  this.context.setMissionContinueState(AbilityConstant.ContinueState.INACTIVE, (result) => {
    console.info(`setMissionContinueState: ${JSON.stringify(result)}`);
  });
  ```

## UIAbilityContext.setMissionContinueState<sup>10+</sup>

setMissionContinueState(state: AbilityConstant.ContinueState): Promise&lt;void&gt;;

设置UIAbility任务中流转状态（promise形式）。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| state | [AbilityConstant.ContinueState](js-apis-app-ability-abilityConstant.md#abilityconstantcontinuestate10) | 是 | 流转状态。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| Promise&lt;void&gt; | 返回一个Promise，包含接口的结果。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 16000011 | The context does not exist. |
| 16000050 | Internal error. |

错误码详细介绍请参考[errcode-ability](../errorcodes/errorcode-ability.md)

**示例：**

  ```ts
  import AbilityConstant from '@ohos.app.ability.AbilityConstant';

  this.context.setMissionContinueState(AbilityConstant.ContinueState.INACTIVE).then(() => {
    console.info('success');
  }).catch((err) => {
    console.error(`setMissionContinueState failed, code is ${err.code}, message is ${err.message}`);
  });
  ```

## UIAbilityContext.restoreWindowStage

restoreWindowStage(localStorage: LocalStorage) : void;

恢复UIAbility中的WindowStage数据。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| localStorage | LocalStorage | 是 | 用于恢复window stage的存储数据。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 16000011 | The context does not exist. |
| 16000050 | Internal error. |

错误码详细介绍请参考[errcode-ability](../errorcodes/errorcode-ability.md)

**示例：**

  ```ts
  let storage = new LocalStorage();
  this.context.restoreWindowStage(storage);
  ```

## UIAbilityContext.isTerminating

isTerminating(): boolean;

查询UIAbility是否在terminating状态。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| bool | true：ability当前处于terminating状态；false：不处于terminating状态。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 16000011 | The context does not exist. |

错误码详细介绍请参考[errcode-ability](../errorcodes/errorcode-ability.md)

**示例：**

  ```ts
  let isTerminating = this.context.isTerminating();
  console.info(`ability state is ${isTerminating}`);
  ```

## UIAbilityContext.requestDialogService

requestDialogService(want: Want, result: AsyncCallback&lt;dialogRequest.RequestResult&gt;): void;

启动一个支持模态弹框的ServiceExtensionAbility。ServiceExtensionAbility被启动后，应用弹出模态弹框，通过调用[setRequestResult](js-apis-app-ability-dialogRequest.md#requestcallbacksetrequestresult)接口返回结果给调用者。

使用规则：
 - 调用方应用位于后台时，使用该接口启动Ability需申请`ohos.permission.START_ABILITIES_FROM_BACKGROUND`权限。
 - 跨应用场景下，目标Ability的exported属性若配置为false，调用方应用需申请`ohos.permission.START_INVISIBLE_ABILITY`权限。
 - 组件启动规则详见：[组件启动规则（Stage模型）](../../application-models/component-startup-rules.md)。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| want |[Want](js-apis-application-want.md) | 是 | 启动ServiceExtensionAbility的want信息。 |
| result | AsyncCallback&lt;[dialogRequest.RequestResult](js-apis-app-ability-dialogRequest.md)&gt; | 是 | 执行结果回调函数。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 16000001 | The specified ability does not exist. |
| 16000002 | Incorrect ability type. |
| 16000004 | Can not start invisible component. |
| 16000005 | The specified process does not have the permission. |
| 16000006 | Cross-user operations are not allowed. |
| 16000008 | The crowdtesting application expires. |
| 16000009 | An ability cannot be started or stopped in Wukong mode. |
| 16000010 | The call with the continuation flag is forbidden. |
| 16000011 | The context does not exist. |
| 16000012 | The application is controlled.        |
| 16000013 | The application is controlled by EDM.       |
| 16000050 | Internal error. |
| 16000053 | The ability is not on the top of the UI. |
| 16000055 | Installation-free timed out. |
| 16200001 | The caller has been released. |

错误码详细介绍请参考[errcode-ability](../errorcodes/errorcode-ability.md)

**示例：**

  ```ts
import dialogRequest from '@ohos.app.ability.dialogRequest';

let want = {
  deviceId: '',
  bundleName: 'com.example.myapplication',
  abilityName: 'AuthAccountServiceExtension'
};

try {
  this.context.requestDialogService(want, (err, result) => {
    if (err.code) {
      // 处理业务逻辑错误
      console.error(`requestDialogService failed, code is ${err.code}, message is ${err.message}`);
      return;
    }
    // 执行正常业务
    console.info('requestDialogService succeed, result = ${JSON.stringify(result)}');
  });
} catch (err) {
  // 处理入参错误异常
  console.error(`requestDialogService failed, code is ${err.code}, message is ${err.message}`);
}
  ```

  ## UIAbilityContext.requestDialogService

requestDialogService(want: Want): Promise&lt;dialogRequest.RequestResult&gt;;

启动一个支持模态弹框的ServiceExtensionAbility。ServiceExtensionAbility被启动后，应用弹出模态弹框，通过调用[setRequestResult](js-apis-app-ability-dialogRequest.md#requestcallbacksetrequestresult)接口返回结果给调用者（promise形式）。

使用规则：
 - 调用方应用位于后台时，使用该接口启动Ability需申请`ohos.permission.START_ABILITIES_FROM_BACKGROUND`权限。
 - 跨应用场景下，目标Ability的exported属性若配置为false，调用方应用需申请`ohos.permission.START_INVISIBLE_ABILITY`权限。
 - 组件启动规则详见：[组件启动规则（Stage模型）](../../application-models/component-startup-rules.md)。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md) | 是 | 启动ServiceExtensionAbility的want信息。 |


**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| Promise&lt;[dialogRequest.RequestResult](js-apis-app-ability-dialogRequest.md)&gt; | Promise形式返回执行结果。

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 16000001 | The specified ability does not exist. |
| 16000002 | Incorrect ability type. |
| 16000004 | Can not start invisible component. |
| 16000005 | The specified process does not have the permission. |
| 16000006 | Cross-user operations are not allowed. |
| 16000008 | The crowdtesting application expires. |
| 16000009 | An ability cannot be started or stopped in Wukong mode. |
| 16000010 | The call with the continuation flag is forbidden. |
| 16000011 | The context does not exist. |
| 16000012 | The application is controlled.        |
| 16000013 | The application is controlled by EDM.       |
| 16000050 | Internal error. |
| 16000053 | The ability is not on the top of the UI. |
| 16000055 | Installation-free timed out. |
| 16200001 | The caller has been released. |

错误码详细介绍请参考[errcode-ability](../errorcodes/errorcode-ability.md)

**示例：**

  ```ts
import dialogRequest from '@ohos.app.ability.dialogRequest';

let want = {
  bundleName: 'com.example.myapplication',
  abilityName: 'AuthAccountServiceExtension'
};

try {
  this.context.requestDialogService(want)
    .then((result) => {
      // 执行正常业务
      console.info('requestDialogService succeed, result = ${JSON.stringify(result)}');
    })
    .catch((err) => {
      // 处理业务逻辑错误
      console.error(`requestDialogService failed, code is ${err.code}, message is ${err.message}`);
    });
} catch (err) {
  // 处理入参错误异常
  console.error(`requestDialogService failed, code is ${err.code}, message is ${err.message}`);
}
  ```
  ## UIAbilityContext.startRecentAbility

startRecentAbility(want: Want, callback: AsyncCallback&lt;void&gt;): void;

启动一个指定的Ability，如果这个Ability有多个实例，将拉起最近启动的那个实例。启动结果以callback的形式返回开发者。

使用规则：
 - 调用方应用位于后台时，使用该接口启动Ability需申请`ohos.permission.START_ABILITIES_FROM_BACKGROUND`权限
 - 跨应用场景下，目标Ability的exported属性若配置为false，调用方应用需申请`ohos.permission.START_INVISIBLE_ABILITY`权限
 - 组件启动规则详见：[组件启动规则（Stage模型）](../../application-models/component-startup-rules.md)

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**系统API**: 此接口为系统接口，三方应用不支持调用。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md) | 是 | 需要启动Ability的want信息。 |
| callback | AsyncCallback\<void> | 是 | 指定的回调函数的结果。 |

**错误码：**

以下错误码的详细介绍请参见[errcode-ability](../errorcodes/errorcode-ability.md)。

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 16000001 | The specified ability does not exist. |
| 16000002 | Incorrect ability type. |
| 16000004 | Can not start invisible component. |
| 16000005 | The specified process does not have the permission. |
| 16000006 | Cross-user operations are not allowed. |
| 16000008 | The crowdtesting application expires. |
| 16000009 | An ability cannot be started or stopped in Wukong mode. |
| 16000010 | The call with the continuation flag is forbidden. |
| 16000011 | The context does not exist. |
| 16000012 | The application is controlled.        |
| 16000013 | The application is controlled by EDM.       |
| 16000050 | Internal error. |
| 16000053 | The ability is not on the top of the UI. |
| 16000055 | Installation-free timed out. |
| 16200001 | The caller has been released. |

**示例：**

  ```ts
let want = {
  bundleName: 'com.example.myapplication',
  abilityName: 'EntryAbility'
};

try {
  this.context.startRecentAbility(want, (err) => {
    if (err.code) {
      // 处理业务逻辑错误
      console.error(`startRecentAbility failed, code is ${err.code}, message is ${err.message}`);
      return;
    }
    // 执行正常业务
    console.info('startRecentAbility succeed');
  });
} catch (err) {
  // 处理入参错误异常
  console.error(`startRecentAbility failed failed, code is ${err.code}, message is ${err.message}`);
}
  ```
## UIAbilityContext.startRecentAbility

startRecentAbility(want: Want, options: StartOptions, callback: AsyncCallback&lt;void&gt;): void;

启动一个指定的Ability，如果这个Ability有多个实例，将拉起最近启动的那个实例。启动结果以callback的形式返回开发者。
当开发者需要携带启动参数时可以选择此API。

使用规则：
 - 调用方应用位于后台时，使用该接口启动Ability需申请`ohos.permission.START_ABILITIES_FROM_BACKGROUND`权限
 - 跨应用场景下，目标Ability的exported属性若配置为false，调用方应用需申请`ohos.permission.START_INVISIBLE_ABILITY`权限
 - 组件启动规则详见：[组件启动规则（Stage模型）](../../application-models/component-startup-rules.md)

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**系统API**: 此接口为系统接口，三方应用不支持调用。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md) | 是 | 需要启动Ability的want信息。 |
| options | [StartOptions](js-apis-app-ability-startOptions.md) | 是 | 启动Ability所携带的参数。 |
| callback | AsyncCallback\<void> | 是 | 指定的回调函数的结果。 |

**错误码：**

以下错误码的详细介绍请参见[errcode-ability](../errorcodes/errorcode-ability.md)。

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 16000001 | The specified ability does not exist. |
| 16000002 | Incorrect ability type. |
| 16000004 | Can not start invisible component. |
| 16000005 | The specified process does not have the permission. |
| 16000006 | Cross-user operations are not allowed. |
| 16000008 | The crowdtesting application expires. |
| 16000009 | An ability cannot be started or stopped in Wukong mode. |
| 16000010 | The call with the continuation flag is forbidden. |
| 16000011 | The context does not exist. |
| 16000012 | The application is controlled.        |
| 16000013 | The application is controlled by EDM.       |
| 16000050 | Internal error. |
| 16000053 | The ability is not on the top of the UI. |
| 16000055 | Installation-free timed out. |
| 16200001 | The caller has been released. |

**示例：**

  ```ts
let want = {
  deviceId: '',
  bundleName: 'com.example.myapplication',
  abilityName: 'EntryAbility'
};
let options = {
  windowMode: 0
};

try {
  this.context.startRecentAbility(want, options, (err) => {
    if (err.code) {
      // 处理业务逻辑错误
      console.error(`startRecentAbility failed, code is ${err.code}, message is ${err.message}`);
      return;
    }
    // 执行正常业务
    console.info('startRecentAbility succeed');
  });
} catch (err) {
  // 处理入参错误异常
  console.error(`startRecentAbility failed failed, code is ${err.code}, message is ${err.message}`);
}
  ```
## UIAbilityContext.startRecentAbility

startRecentAbility(want: Want, options?: StartOptions): Promise&lt;void&gt;;

启动一个指定的Ability，如果这个Ability有多个实例，将拉起最近启动的那个实例。
当开发者期望启动结果以Promise形式返回时可以选择此API。

使用规则：
 - 调用方应用位于后台时，使用该接口启动Ability需申请`ohos.permission.START_ABILITIES_FROM_BACKGROUND`权限
 - 跨应用场景下，目标Ability的exported属性若配置为false，调用方应用需申请`ohos.permission.START_INVISIBLE_ABILITY`权限
 - 组件启动规则详见：[组件启动规则（Stage模型）](../../application-models/component-startup-rules.md)

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**系统API**: 此接口为系统接口，三方应用不支持调用。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md) | 是 | 需要启动Ability的want信息。 |
| options | [StartOptions](js-apis-app-ability-startOptions.md) | 否 | 启动Ability所携带的参数。 |

**错误码：**

以下错误码的详细介绍请参见[errcode-ability](../errorcodes/errorcode-ability.md)。

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 16000001 | The specified ability does not exist. |
| 16000002 | Incorrect ability type. |
| 16000004 | Can not start invisible component. |
| 16000005 | The specified process does not have the permission. |
| 16000006 | Cross-user operations are not allowed. |
| 16000008 | The crowdtesting application expires. |
| 16000009 | An ability cannot be started or stopped in Wukong mode. |
| 16000010 | The call with the continuation flag is forbidden. |
| 16000011 | The context does not exist. |
| 16000012 | The application is controlled.        |
| 16000013 | The application is controlled by EDM.       |
| 16000050 | Internal error. |
| 16000053 | The ability is not on the top of the UI. |
| 16000055 | Installation-free timed out. |
| 16200001 | The caller has been released. |

**示例：**

  ```ts
let want = {
  bundleName: 'com.example.myapplication',
  abilityName: 'EntryAbility'
};
let options = {
  windowMode: 0,
};

try {
  this.context.startRecentAbility(want, options)
    .then(() => {
      // 执行正常业务
      console.info('startRecentAbility succeed');
    })
    .catch((err) => {
      // 处理业务逻辑错误
      console.error(`startRecentAbility failed, code is ${err.code}, message is ${err.message}`);
    });
} catch (err) {
  // 处理入参错误异常
  console.error(`startRecentAbility failed, code is ${err.code}, message is ${err.message}`);
}
  ```

## UIAbilityContext.startAbilityByCallWithAccount<sup>10+</sup>

startAbilityByCallWithAccount(want: Want, accountId: number): Promise&lt;Caller&gt;;

根据accountId对指定的Ability进行call调用，并且可以使用返回的Caller通信接口与被调用方进行通信。

使用规则：
 - 跨用户场景下，Call调用目标Ability时，调用方应用需同时申请`ohos.permission.ABILITY_BACKGROUND_COMMUNICATION`与`ohos.permission.INTERACT_ACROSS_LOCAL_ACCOUNTS`权限
 - 调用方应用位于后台时，使用该接口启动Ability需申请`ohos.permission.START_ABILITIES_FROM_BACKGROUND`权限
 - 跨应用场景下，目标Ability的exported属性若配置为false，调用方应用需申请`ohos.permission.START_INVISIBLE_ABILITY`权限
 - 同设备与跨设备场景下，该接口的使用规则存在差异，详见：[组件启动规则（Stage模型）](../../application-models/component-startup-rules.md)

**需要权限**: ohos.permission.ABILITY_BACKGROUND_COMMUNICATION, ohos.permission.INTERACT_ACROSS_LOCAL_ACCOUNTS

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**系统API**：此接口为系统接口，三方应用不支持调用。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md) | 是 | 传入需要启动的Ability的信息，包含abilityName、moduleName、bundleName、deviceId(可选)、parameters(可选)，其中deviceId缺省或为空表示启动本地Ability，parameters缺省或为空表示后台启动Ability。 |
| accountId | number | 是 | 系统帐号的帐号ID，-1表示当前活动用户，详情参考[getCreatedOsAccountsCount](js-apis-osAccount.md#getosaccountlocalidfromprocess)。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| Promise&lt;Caller&gt; | 获取要通讯的caller对象。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 16000001 | The specified ability does not exist. |
| 16000002 | Incorrect ability type. |
| 16000004 | Can not start invisible component. |
| 16000005 | Static permission denied. The specified process does not have the permission. |
| 16000006 | Cross-user operations are not allowed. |
| 16000008 | The crowdtesting application expires. |
| 16000011 | The context does not exist. |
| 16000012 | The application is controlled.        |
| 16000013 | The application is controlled by EDM.       |
| 16000050 | Internal error. |
| 16200001 | The caller has been released.        |

以上错误码详细介绍请参考[errcode-ability](../errorcodes/errorcode-ability.md)。

**示例：**

  ```ts
  let caller;

  // 系统账号的账号ID, -1表示当前激活用户
  let accountId = -1;

  // 指定启动的Ability
  let want = {
      bundleName: 'com.acts.actscalleeabilityrely',
      moduleName: 'entry',
      abilityName: 'EntryAbility',
      deviceId: '',
      parameters: {
        // 'ohos.aafwk.param.callAbilityToForeground' 值设置为true时为前台启动, 设置false或不设置为后台启动
        'ohos.aafwk.param.callAbilityToForeground': true
      }
  };

  try {
    this.context.startAbilityByCallWithAccount(want, accountId)
      .then((obj) => {
        // 执行正常业务
        caller = obj;
        console.log('startAbilityByCallWithAccount succeed');
      }).catch((error) => {
        // 处理业务逻辑错误
        console.error('startAbilityByCallWithAccount failed, error.code: ${error.code}, error.message: ${error.message}');
      });
  } catch (paramError) {
    // 处理入参错误异常
    console.error('error.code: ${paramError.code}, error.message: ${paramError.message}');
  }
  ```

## UIAbilityContext.reportDrawnCompleted<sup>10+</sup>

reportDrawnCompleted(callback: AsyncCallback\<void>): void;

当页面加载完成（loadContent成功）时，为开发者提供打点功能（callback形式）。
 **系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| callback | AsyncCallback&lt;void&gt; | 是 | 页面加载完成打点的回调函数。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 16000011 | The context does not exist. |
| 16000050 | Internal error. |

错误码详细介绍请参考[errcode-ability](../errorcodes/errorcode-ability.md)

**示例：**

  ```ts
import UIAbility from '@ohos.app.ability.UIAbility';
import window from '@ohos.window';

export default class EntryAbility extends UIAbility {
  onWindowStageCreate(windowStage: window.WindowStage) {
    windowStage.loadContent('pages/Index', (err, data) => {
      if (err.code) {
        return;
      }
      try {
        this.context.reportDrawnCompleted((err) => {
          if (err.code) {
            // 处理业务逻辑错误
            console.error(`reportDrawnCompleted failed, code is ${err.code}, message is ${err.message}`);
            return;
          }
          // 执行正常业务
          console.info('reportDrawnCompleted succeed');
        });
      } catch (err) {
        // 捕获同步的参数错误
        console.error(`reportDrawnCompleted failed, code is ${err.code}, message is ${err.message}`);
      }
    });
    console.log("MainAbility onWindowStageCreate")
  }
};
  ```