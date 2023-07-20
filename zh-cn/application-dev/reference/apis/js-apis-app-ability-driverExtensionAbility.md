# @ohos.app.ability.DriverExtensionAbility (DriverExtensionAbility)

DriverExtensionAbility模块提供驱动相关扩展能力，提供驱动创建、销毁、连接、断开等生命周期回调。

> **说明：**
> 
> 本模块首批接口从API version 10开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。  
> 本模块接口仅可在Stage模型下使用。

## 导入模块

```ts
import DriverExtension from '@ohos.app.ability.DriverExtensionAbility';
```

## 权限

无

## 属性

**系统能力**：SystemCapability.Driver.ExternalDevice


| 名称 | 类型 | 可读 | 可写 | 说明 |
| -------- | -------- | -------- | -------- | -------- |
| context | [DriverExtensionContext](js-apis-inner-application-driverExtensionContext.md)  | 是 | 否 | DriverExtension的上下文环境，继承自ExtensionContext。 |


## DriverExtensionAbility.onInit

onInit(want: Want): void;

Extension生命周期回调，在创建时回调，执行初始化业务逻辑操作。

**系统能力**：SystemCapability.Driver.ExternalDevice

**系统API**: 此接口为系统接口，三方应用不支持调用。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| want |  [Want](js-apis-app-ability-want.md) | 是 | 当前Extension相关的Want类型信息，包括ability名称、bundle名称等。 |

**示例：**

  ```ts
  class DriverExt extends DriverExtension {
    onInit(want) {
      console.log('onInit, want: ${want.abilityName}');
    }
  }
  ```


## DriverExtensionAbility.onRelease

onRelease(): void;

Extension生命周期回调，在销毁时回调，执行资源清理等操作。

**系统能力**：SystemCapability.Driver.ExternalDevice

**系统API**: 此接口为系统接口，三方应用不支持调用。

**示例：**

  ```ts
  class DriverExt extends DriverExtension {
    onRelease() {
      console.log('onRelease');
    }
  }
  ```


## DriverExtensionAbility.onConnect

onConnect(want: Want): rpc.RemoteObject | Promise<rpc.RemoteObject>;

Extension生命周期回调，如果是connectAbility拉起的服务，会在onCreate之后回调。返回一个RemoteObject对象，用于客户端和服务端进行通信。

**系统能力**：SystemCapability.Driver.ExternalDevice

**系统API**: 此接口为系统接口，三方应用不支持调用。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| want |  [Want](js-apis-app-ability-want.md)| 是 | 当前Extension相关的Want类型信息，包括ability名称、bundle名称等。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| rpc.RemoteObject | 一个RemoteObject对象，用于客户端和服务端进行通信。 |

**示例：**

  ```ts
  import rpc from '@ohos.rpc';
  class StubTest extends rpc.RemoteObject{
      constructor(des) {
          super(des);
      }
      onRemoteRequest(code, data, reply, option) {
      }
  }
  class DriverExt extends DriverExtension {
    onConnect(want) {
      console.log('onConnect , want: ${want.abilityName}');
      return new StubTest('test');
    }
  }
  ```

如果生成返回值RemoteObject依赖一个异步接口，可以使用异步生命周期：

  ```ts
import rpc from '@ohos.rpc';
class StubTest extends rpc.RemoteObject{
    constructor(des) {
        super(des);
    }
    onRemoteRequest(code, data, reply, option) {
    }
}
async function getDescriptor() {
    // 调用异步函数...
    return "asyncTest"
}
class DriverExt extends DriverExtension {
  async onConnect(want) {
    console.log(`onConnect , want: ${want.abilityName}`);
    let descriptor = await getDescriptor();
    return new StubTest(descriptor);
  }
}
  ```

## DriverExtensionAbility.onDisconnect

onDisconnect(want: Want): void | Promise\<void>;

Extension的生命周期回调，客户端执行断开连接服务时回调。

**系统能力**：SystemCapability.Driver.ExternalDevice

**系统API**: 此接口为系统接口，三方应用不支持调用。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| want |[Want](js-apis-app-ability-want.md)| 是 | 当前Extension相关的Want类型信息，包括ability名称、bundle名称等。 |

**示例：**

  ```ts
  class DriverExt extends DriverExtension {
    onDisconnect(want) {
      console.log('onDisconnect, want: ${want.abilityName}');
    }
  }
  ```

在执行完onDisconnect生命周期回调后，应用可能会退出，从而可能导致onDisconnect中的异步函数未能正确执行，比如异步写入数据库。可以使用异步生命周期，以确保异步onDisconnect完成后再继续后续的生命周期。

  ```ts
class DriverExt extends DriverExtension {
  async onDisconnect(want) {
    console.log('onDisconnect, want: ${want.abilityName}');
    // 调用异步函数...
  }
}
  ```


## DriverExtensionAbility.onDump

onDump(params: Array\<string>): Array\<string>;

转储客户端信息时调用。

**系统能力**：SystemCapability.Driver.ExternalDevice

**系统API**: 此接口为系统接口，三方应用不支持调用。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| params | Array\<string> | 是 | 表示命令形式的参数。|

**示例：**
    
  ```ts
  class DriverExt extends DriverExtension {
      onDump(params) {
          console.log('dump, params: ${JSON.stringify(params)}');
          return ['params'];
      }
  }
  ```

