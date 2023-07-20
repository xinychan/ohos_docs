# @ohos.multimedia.avsession (媒体会话管理)

媒体会话管理提供媒体播控相关功能的接口，目的是让应用接入播控中心。

该模块提供以下媒体会话相关的常用功能：

- [AVSession](#avsession10) : 会话，可用于设置元数据、播放状态信息等操作。
- [AVSessionController](#avsessioncontroller10): 会话控制器，可用于查看会话ID，完成对会话发送命令及事件，获取会话元数据、播放状态信息等操作。
- [AVCastController](#avcastcontroller10): 投播控制器，可用于投播场景下，完成播放控制、远端播放状态监听、远端播放状态信息获取等操作。

> **说明：**
>
> 本模块首批接口从API version 9开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。

## 导入模块

```js
import avSession from '@ohos.multimedia.avsession';
```

## avSession.createAVSession<sup>10+</sup>

createAVSession(context: Context, tag: string, type: AVSessionType): Promise\<AVSession>

创建会话对象，一个Ability只能存在一个会话，重复创建会失败，结果通过Promise异步回调方式返回。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**参数：**

| 参数名 | 类型                            | 必填 | 说明                           |
| ------ | ------------------------------- | ---- | ------------------------------ |
| context| [Context](js-apis-inner-app-context.md) | 是| 应用上下文，提供获取应用程序环境信息的能力。 |
| tag    | string                          | 是   | 会话的自定义名称。             |
| type   | [AVSessionType](#avsessiontype10) | 是   | 会话类型，当前支持音频和视频。 |

**返回值：**

| 类型                              | 说明                                                         |
| --------------------------------- | ------------------------------------------------------------ |
| Promise<[AVSession](#avsession10)\> | Promise对象。回调返回会话实例对象，可用于获取会话ID，以及设置元数据、播放状态，发送按键事件等操作。|

**错误码：**

以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |

**示例：**

```js
import featureAbility from '@ohos.ability.featureAbility';

let session;
let tag = "createNewSession";
let context = featureAbility.getContext();

await avSession.createAVSession(context, tag, "audio").then((data) => {
    session = data;
    console.info(`CreateAVSession : SUCCESS : sessionId = ${session.sessionId}`);
}).catch((err) => {
    console.info(`CreateAVSession BusinessError: code: ${err.code}, message: ${err.message}`);
});
```

## avSession.createAVSession<sup>10+</sup>

createAVSession(context: Context, tag: string, type: AVSessionType, callback: AsyncCallback\<AVSession>): void

创建会话对象，一个Ability只能存在一个会话，重复创建会失败，结果通过callback异步回调方式返回。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**参数：**

| 参数名   | 类型                                    | 必填 | 说明                                                         |
| -------- | --------------------------------------- | ---- | ------------------------------------------------------------ |
| context| [Context](js-apis-inner-app-context.md) | 是| 应用上下文，提供获取应用程序环境信息的能力。     |
| tag      | string                                  | 是   | 会话的自定义名称。                                           |
| type     | [AVSessionType](#avsessiontype10)         | 是   | 会话类型，当前支持音频和视频。                               |
| callback | AsyncCallback<[AVSession](#avsession10)\> | 是   | 回调函数。回调返回会话实例对象，可用于获取会话ID，以及设置元数据、播放状态，发送按键事件等操作。 |

**错误码：**

以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |

**示例：**

```js
import featureAbility from '@ohos.ability.featureAbility';

let session;
let tag = "createNewSession";
let context = featureAbility.getContext();

avSession.createAVSession(context, tag, "audio", function (err, data) {
    if (err) {
        console.info(`CreateAVSession BusinessError: code: ${err.code}, message: ${err.message}`);
    } else {
        session = data;
        console.info(`CreateAVSession : SUCCESS : sessionId = ${session.sessionId}`);
    }
});
```

## avSession.getAllSessionDescriptors

getAllSessionDescriptors(): Promise\<Array\<Readonly\<AVSessionDescriptor>>>

获取所有会话的相关描述。结果通过Promise异步回调方式返回。

**需要权限：** ohos.permission.MANAGE_MEDIA_RESOURCES，仅系统应用可用。

**系统能力：** SystemCapability.Multimedia.AVSession.Manager

**系统接口：** 该接口为系统接口。

**返回值：**

| 类型                                                         | 说明                                          |
| ------------------------------------------------------------ | --------------------------------------------- |
| Promise\<Array\<Readonly\<[AVSessionDescriptor](#avsessiondescriptor)\>\>\> | Promise对象。返回所有会话描述的只读对象。 |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |

**示例：**

```js
avSession.getAllSessionDescriptors().then((descriptors) => {
    console.info(`getAllSessionDescriptors : SUCCESS : descriptors.length : ${descriptors.length}`);
    if(descriptors.length > 0 ){
        console.info(`getAllSessionDescriptors : SUCCESS : descriptors[0].isActive : ${descriptors[0].isActive}`);
        console.info(`GetAllSessionDescriptors : SUCCESS : descriptors[0].type : ${descriptors[0].type}`);
        console.info(`GetAllSessionDescriptors : SUCCESS : descriptors[0].sessionTag : ${descriptors[0].sessionTag}`);
    }
}).catch((err) => {
    console.info(`GetAllSessionDescriptors BusinessError: code: ${err.code}, message: ${err.message}`);
});
```

## avSession.getAllSessionDescriptors

getAllSessionDescriptors(callback: AsyncCallback\<Array\<Readonly\<AVSessionDescriptor>>>): void

获取所有会话的相关描述。结果通过callback异步回调方式返回。

**需要权限：** ohos.permission.MANAGE_MEDIA_RESOURCES

**系统能力：** SystemCapability.Multimedia.AVSession.Manager

**系统接口：** 该接口为系统接口。

**参数：**

| 参数名   | 类型                                                         | 必填 | 说明                                       |
| -------- | ------------------------------------------------------------ | ---- | ------------------------------------------ |
| callback | AsyncCallback<Array<Readonly<[AVSessionDescriptor](#avsessiondescriptor)\>\>\> | 是   | 回调函数。返回所有会话描述的只读对象。 |

**错误码：**

以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  |Session service exception. |

**示例：**

```js
avSession.getAllSessionDescriptors(function (err, descriptors) {
    if (err) {
        console.info(`GetAllSessionDescriptors BusinessError: code: ${err.code}, message: ${err.message}`);
    } else {
        console.info(`GetAllSessionDescriptors : SUCCESS : descriptors.length : ${descriptors.length}`);
        if(descriptors.length > 0 ){
            console.info(`getAllSessionDescriptors : SUCCESS : descriptors[0].isActive : ${descriptors[0].isActive}`);
            console.info(`getAllSessionDescriptors : SUCCESS : descriptors[0].type : ${descriptors[0].type}`);
            console.info(`getAllSessionDescriptors : SUCCESS : descriptors[0].sessionTag : ${descriptors[0].sessionTag}`);
        }
    }
});
```

## avSession.getHistoricalSessionDescriptors<sup>10+</sup>

getHistoricalSessionDescriptors(maxSize?: number): Promise\<Array\<Readonly\<AVSessionDescriptor>>>

获取所有会话的相关描述。结果通过Promise异步回调方式返回。

**需要权限：** ohos.permission.MANAGE_MEDIA_RESOURCES

**系统能力：** SystemCapability.Multimedia.AVSession.Manager

**系统接口：** 该接口为系统接口。

**参数：**

| 参数名   | 类型    | 必填 | 说明                                                             |
| -------- | ------ | ---- | -----------------------------------------------------------------|
| maxSize  | number | 否   | 指定获取描述符数量的最大值，可选范围是0-10，不填则取默认值，默认值为3。|

**返回值：**

| 类型                                                                        | 说明                                   |
| --------------------------------------------------------------------------- | -------------------------------------- |
| Promise\<Array\<Readonly\<[AVSessionDescriptor](#avsessiondescriptor)\>\>\> | Promise对象。返回所有会话描述的只读对象。 |

**错误码：**

以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |

**示例：**

```js
avSession.getHistoricalSessionDescriptors().then((descriptors) => {
    console.info(`getHistoricalSessionDescriptors : SUCCESS : descriptors.length : ${descriptors.length}`);
    if(descriptors.length > 0 ){
        console.info(`getHistoricalSessionDescriptors : SUCCESS : descriptors[0].isActive : ${descriptors[0].isActive}`);
        console.info(`getHistoricalSessionDescriptors : SUCCESS : descriptors[0].type : ${descriptors[0].type}`);
        console.info(`getHistoricalSessionDescriptors : SUCCESS : descriptors[0].sessionTag : ${descriptors[0].sessionTag}`);
        console.info(`getHistoricalSessionDescriptors : SUCCESS : descriptors[0].sessionId : ${descriptors[0].sessionId}`);
        console.info(`getHistoricalSessionDescriptors : SUCCESS : descriptors[0].elementName.bundleName : ${descriptors[0].elementName.bundleName}`);
    }
}).catch((err) => {
    console.info(`getHistoricalSessionDescriptors BusinessError: code: ${err.code}, message: ${err.message}`);
});
```

## avSession.getHistoricalSessionDescriptors<sup>10+</sup>

getHistoricalSessionDescriptors(maxSize: number, callback: AsyncCallback\<Array\<Readonly\<AVSessionDescriptor>>>): void

获取所有会话的相关描述。结果通过callback异步回调方式返回。

**需要权限：** ohos.permission.MANAGE_MEDIA_RESOURCES。

**系统能力：** SystemCapability.Multimedia.AVSession.Manager

**系统接口：** 该接口为系统接口。

**参数：**

| 参数名   | 类型                                                                            | 必填 | 说明                                                             |
| -------- | ------------------------------------------------------------------------------ | ---- | -----------------------------------------------------------------|
| maxSize  | number                                                                         | 是   | 指定获取描述符数量的最大值，可选范围是0-10，不填则取默认值，默认值为3。|
| callback | AsyncCallback<Array<Readonly<[AVSessionDescriptor](#avsessiondescriptor)\>\>\> | 是   | 回调函数。返回所有会话描述的只读对象。                              |

**错误码：**

以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  |Session service exception. |

**示例：**

```js
avSession.getHistoricalSessionDescriptors(1, function (err, descriptors) {
    if (err) {
        console.info(`getHistoricalSessionDescriptors BusinessError: code: ${err.code}, message: ${err.message}`);
    } else {
        console.info(`getHistoricalSessionDescriptors : SUCCESS : descriptors.length : ${descriptors.length}`);
        if(descriptors.length > 0 ){
            console.info(`getHistoricalSessionDescriptors : SUCCESS : descriptors[0].isActive : ${descriptors[0].isActive}`);
            console.info(`getHistoricalSessionDescriptors : SUCCESS : descriptors[0].type : ${descriptors[0].type}`);
            console.info(`getHistoricalSessionDescriptors : SUCCESS : descriptors[0].sessionTag : ${descriptors[0].sessionTag}`);
            console.info(`getHistoricalSessionDescriptors : SUCCESS : descriptors[0].sessionId : ${descriptors[0].sessionId}`);
            console.info(`getHistoricalSessionDescriptors : SUCCESS : descriptors[0].elementName.bundleName : ${descriptors[0].elementName.bundleName}`);
        }
    }
});
```

## avSession.createController

createController(sessionId: string): Promise\<AVSessionController>

根据会话ID创建会话控制器，可以创建多个会话控制器。结果通过Promise异步回调方式返回。

**需要权限：** ohos.permission.MANAGE_MEDIA_RESOURCES，仅系统应用可用。

**系统能力：** SystemCapability.Multimedia.AVSession.Manager

**系统接口：** 该接口为系统接口。

**参数：**

| 参数名    | 类型   | 必填 | 说明     |
| --------- | ------ | ---- | -------- |
| sessionId | string | 是   | 会话ID。 |

**返回值：**

| 类型                                                  | 说明                                                         |
| ----------------------------------------------------- | ------------------------------------------------------------ |
| Promise<[AVSessionController](#avsessioncontroller10)\> | Promise对象。返回会话控制器实例，可查看会话ID，<br>并完成对会话发送命令及事件，获取元数据、播放状态信息等操作。|

**错误码：**

以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |
| 6600102  | The session does not exist. |

**示例：**

```js
import featureAbility from '@ohos.ability.featureAbility';

let session;
let tag = "createNewSession";
let context = featureAbility.getContext();

await avSession.createAVSession(context, tag, "audio").then((data) => {
    session = data;
    console.info(`CreateAVSession : SUCCESS : sessionId = ${session.sessionId}`);
}).catch((err) => {
    console.info(`CreateAVSession BusinessError: code: ${err.code}, message: ${err.message}`);
});

let controller;
await avSession.createController(session.sessionId).then((avcontroller) => {
    controller = avcontroller;
    console.info(`CreateController : SUCCESS : ${controller.sessionId}`);
}).catch((err) => {
    console.info(`CreateController BusinessError: code: ${err.code}, message: ${err.message}`);
});
```

## avSession.createController

createController(sessionId: string, callback: AsyncCallback\<AVSessionController>): void

根据会话ID创建会话控制器，可以创建多个会话控制器。结果通过callback异步回调方式返回。

**需要权限：** ohos.permission.MANAGE_MEDIA_RESOURCES，仅系统应用可用。

**系统能力：** SystemCapability.Multimedia.AVSession.Manager

**系统接口：** 该接口为系统接口。

**参数：**

| 参数名    | 类型                                                        | 必填 | 说明                                                         |
| --------- | ----------------------------------------------------------- | ---- | ------------------------------------------------------------ |
| sessionId | string                                                      | 是   | 会话ID。                                                     |
| callback  | AsyncCallback<[AVSessionController](#avsessioncontroller10)\> | 是   | 回调函数。返回会话控制器实例，可查看会话ID，<br>并完成对会话发送命令及事件，获取元数据、播放状态信息等操作。 |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |
| 6600102  | The session does not exist. |

**示例：**

```js
import featureAbility from '@ohos.ability.featureAbility';

let session;
let tag = "createNewSession";
let context = featureAbility.getContext();

await avSession.createAVSession(context, tag, "audio").then((data) => {
    session = data;
    console.info(`CreateAVSession : SUCCESS : sessionId = ${session.sessionId}`);
}).catch((err) => {
    console.info(`CreateAVSession BusinessError: code: ${err.code}, message: ${err.message}`);
});

let controller;
avSession.createController(session.sessionId, function (err, avcontroller) {
    if (err) {
        console.info(`CreateController BusinessError: code: ${err.code}, message: ${err.message}`);
    } else {
        controller = avcontroller;
        console.info(`CreateController : SUCCESS : ${controller.sessionId}`);
    }
});
```

## avSession.castAudio

castAudio(session: SessionToken | 'all', audioDevices: Array<audio.AudioDeviceDescriptor>): Promise\<void>

投播会话到指定设备列表。结果通过Promise异步回调方式返回。

调用此接口之前，需要导入`ohos.multimedia.audio`模块获取AudioDeviceDescriptor的相关描述。

**需要权限：** ohos.permission.MANAGE_MEDIA_RESOURCES，仅系统应用可用。

**系统能力：** SystemCapability.Multimedia.AVSession.Manager

**系统接口：** 该接口为系统接口。

**参数：**

| 参数名       | 类型                                                                                                                                                                 | 必填 | 说明                                                         |
| ------------ |--------------------------------------------------------------------------------------------------------------------------------------------------------------------| ---- | ------------------------------------------------------------ |
| session      | [SessionToken](#sessiontoken) &#124; 'all'                                                                                                                         | 是   | 会话令牌。SessionToken表示单个token；字符串`'all'`指所有token。 |
| audioDevices | Array\<[audio.AudioDeviceDescriptor](js-apis-audio.md#audiodevicedescriptor)\> | 是   | 媒体设备列表。                          |

**返回值：**

| 类型           | 说明                          |
| -------------- | ----------------------------- |
| Promise\<void> | Promise对象。当投播成功，无返回结果，否则返回错误对象。 |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |
| 6600102  | The session does not exist. |
| 6600104  | The remote session connection failed. |

**示例：**

```js
import audio from '@ohos.multimedia.audio';

let audioManager = audio.getAudioManager();
let audioRoutingManager = audioManager.getRoutingManager();
let audioDevices;
await audioRoutingManager.getDevices(audio.DeviceFlag.OUTPUT_DEVICES_FLAG).then((data) => {
    audioDevices = data;
    console.info(`Promise returned to indicate that the device list is obtained.`);
}).catch((err) => {
    console.info(`GetDevices BusinessError: code: ${err.code}, message: ${err.message}`);
});

avSession.castAudio('all', audioDevices).then(() => {
    console.info(`CreateController : SUCCESS`);
}).catch((err) => {
    console.info(`CreateController BusinessError: code: ${err.code}, message: ${err.message}`);
});
```

## avSession.castAudio

castAudio(session: SessionToken | 'all', audioDevices: Array<audio.AudioDeviceDescriptor>, callback: AsyncCallback\<void>): void

投播会话到指定设备列表。结果通过callback异步回调方式返回。

需要导入`ohos.multimedia.audio`模块获取AudioDeviceDescriptor的相关描述。

**需要权限：** ohos.permission.MANAGE_MEDIA_RESOURCES，仅系统应用可用。

**系统能力：** SystemCapability.Multimedia.AVSession.Manager

**系统接口：** 该接口为系统接口。

**参数：**

| 参数名       | 类型                                         | 必填 | 说明                                                         |
| ------------ |--------------------------------------------| ---- | ------------------------------------------------------------ |
| session      | [SessionToken](#sessiontoken) &#124; 'all' | 是   | 会话令牌。SessionToken表示单个token；字符串`'all'`指所有token。 |
| audioDevices | Array\<[audio.AudioDeviceDescriptor](js-apis-audio.md#audiodevicedescriptor)\>   | 是   | 媒体设备列表。                       |
| callback     | AsyncCallback\<void>                      | 是   | 回调函数。当投播成功，err为undefined，否则返回错误对象。                        |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |
| 6600102  | The session does not exist. |
| 6600104  | The remote session connection failed. |

**示例：**

```js
import audio from '@ohos.multimedia.audio';

let audioManager = audio.getAudioManager();
let audioRoutingManager = audioManager.getRoutingManager();
let audioDevices;
await audioRoutingManager.getDevices(audio.DeviceFlag.OUTPUT_DEVICES_FLAG).then((data) => {
    audioDevices = data;
    console.info(`Promise returned to indicate that the device list is obtained.`);
}).catch((err) => {
    console.info(`GetDevices BusinessError: code: ${err.code}, message: ${err.message}`);
});

avSession.castAudio('all', audioDevices, function (err) {
    if (err) {
        console.info(`CastAudio BusinessError: code: ${err.code}, message: ${err.message}`);
    } else {
        console.info(`CastAudio : SUCCESS `);
    }
});
```

## avSession.on('sessionCreate')

on(type: 'sessionCreate', callback: (session: AVSessionDescriptor) => void): void

会话的创建监听事件。

**需要权限：** ohos.permission.MANAGE_MEDIA_RESOURCES，仅系统应用可用。

**系统能力：** SystemCapability.Multimedia.AVSession.Manager

**系统接口：** 该接口为系统接口。

**参数：**

| 参数名    | 类型                   | 必填 | 说明                                                         |
| -------- | ---------------------- | ---- | ------------------------------------------------------------ |
| type     | string                 | 是   | 事件回调类型，支持的事件是'sessionCreate'`：会话创建事件，检测到会话创建时触发。|
| callback | (session: [AVSessionDescriptor](#avsessiondescriptor)) => void | 是   | 回调函数。参数为会话相关描述。 |

**错误码：**
以下错误码的详细介绍请参见[ohos.multimedia.avsession(多媒体会话)错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |

**示例：**

```js
avSession.on('sessionCreate', (descriptor) => {
    console.info(`on sessionCreate : isActive : ${descriptor.isActive}`);
    console.info(`on sessionCreate : type : ${descriptor.type}`);
    console.info(`on sessionCreate : sessionTag : ${descriptor.sessionTag}`);
});

```

## avSession.on('sessionDestroy')

on(type: 'sessionDestroy', callback: (session: AVSessionDescriptor) => void): void

会话的销毁监听事件。

**需要权限：** ohos.permission.MANAGE_MEDIA_RESOURCES，仅系统应用可用。

**系统能力：** SystemCapability.Multimedia.AVSession.Manager

**系统接口：** 该接口为系统接口。

**参数：**

| 参数名   | 类型            | 必填 | 说明                                                         |
| -------- | ---------------| ---- | ------------------------------------------------------------ |
| type     | string         | 是   | 事件回调类型，支持的事件包括是`'sessionDestroy'`：会话销毁事件，检测到会话销毁时触发。|
| callback | (session: [AVSessionDescriptor](#avsessiondescriptor)) => void | 是   | 回调函数。参数为会话相关描述。 |

**错误码：**
以下错误码的详细介绍请参见[ohos.multimedia.avsession(多媒体会话)错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |

**示例：**

```js
avSession.on('sessionDestroy', (descriptor) => {
    console.info(`on sessionDestroy : isActive : ${descriptor.isActive}`);
    console.info(`on sessionDestroy : type : ${descriptor.type}`);
    console.info(`on sessionDestroy : sessionTag : ${descriptor.sessionTag}`);
});
```

## avSession.on('topSessionChange')

on(type: 'topSessionChange', callback: (session: AVSessionDescriptor) => void): void

最新会话变更的监听事件。

**需要权限：** ohos.permission.MANAGE_MEDIA_RESOURCES，仅系统应用可用。

**系统能力：** SystemCapability.Multimedia.AVSession.Manager

**系统接口：** 该接口为系统接口。

**参数：**

| 参数名   | 类型                 | 必填 | 说明                                                         |
| -------- | --------------------| ---- | ------------------------------------------------------------ |
| type     | string      | 是   | 事件回调类型，支持的事件包括是 `'topSessionChange'`：最新会话的变化事件，检测到最新的会话改变时触发。|
| callback | (session: [AVSessionDescriptor](#avsessiondescriptor)) => void | 是   | 回调函数。参数为会话相关描述。 |

**错误码：**
以下错误码的详细介绍请参见[ohos.multimedia.avsession(多媒体会话)错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |

**示例：**

```js
avSession.on('topSessionChange', (descriptor) => {
    console.info(`on topSessionChange : isActive : ${descriptor.isActive}`);
    console.info(`on topSessionChange : type : ${descriptor.type}`);
    console.info(`on topSessionChange : sessionTag : ${descriptor.sessionTag}`);
});
```

## avSession.off('sessionCreate')

off(type: 'sessionCreate', callback?: (session: AVSessionDescriptor) => void): void

取消会话创建事件监听，取消后，不再进行该事件的监听。

**需要权限：** ohos.permission.MANAGE_MEDIA_RESOURCES，仅系统应用可用。

**系统能力：** SystemCapability.Multimedia.AVSession.Manager

**系统接口：** 该接口为系统接口。

**参数：**

| 参数名   | 类型       | 必填 | 说明       |
| -------- | ----------| ---- | ----------|
| type     | string    | 是   | 事件回调类型，支持的事件为：`'sessionCreate'`。|
| callback | (session: [AVSessionDescriptor](#avsessiondescriptor)) => void | 否   | 回调函数。当监听事件取消成功，err为undefined，否则返回错误对象。<br>该参数为会话相关描述，为可选参数，若不填写该参数，则认为取消所有相关会话的事件监听。                               |

**错误码：**
以下错误码的详细介绍请参见[ohos.multimedia.avsession(多媒体会话)错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |

**示例：**

```js
avSession.off('sessionCreate');
```

## avSession.off('sessionDestroy')

off(type: 'sessionDestroy', callback?: (session: AVSessionDescriptor) => void): void

取消会话销毁事件监听，取消后，不再进行该事件的监听。

**需要权限：** ohos.permission.MANAGE_MEDIA_RESOURCES，仅系统应用可用。

**系统能力：** SystemCapability.Multimedia.AVSession.Manager

**系统接口：** 该接口为系统接口。

**参数：**

| 参数名   | 类型        | 必填 | 说明                      |
| -------- | -----------| ---- | -------------------------|
| type     | string     | 是   | 事件回调类型，支持的事件为`'sessionDestroy'`。|
| callback | (session: [AVSessionDescriptor](#avsessiondescriptor)) => void | 否   | 回调函数。当监听事件取消成功，err为undefined，否则返回错误对象。<br>该参数为会话相关描述，为可选参数，若不填写该参数，则认为取消所有相关会话的事件监听。|

**错误码：**
以下错误码的详细介绍请参见[ohos.multimedia.avsession(多媒体会话)错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |

**示例：**

```js
avSession.off('sessionDestroy');
```

## avSession.off('topSessionChange')

off(type: 'topSessionChange', callback?: (session: AVSessionDescriptor) => void): void

取消最新会话变更事件监听，取消后，不再进行该事件的监听。

**需要权限：** ohos.permission.MANAGE_MEDIA_RESOURCES，仅系统应用可用。

**系统能力：** SystemCapability.Multimedia.AVSession.Manager

**系统接口：** 该接口为系统接口。

**参数：**

| 参数名   | 类型              | 必填 | 说明                        |
| -------- | -----------------| ---- | ---------------------------- |
| type     | string           | 是   | 事件回调类型，支持的事件为`'topSessionChange'`。|
| callback | (session: [AVSessionDescriptor](#avsessiondescriptor)) => void | 否   | 回调函数。当监听事件取消成功，err为undefined，否则返回错误对象。<br>该参数为会话相关描述，为可选参数，若不填写该参数，则认为取消所有相关会话的事件监听。 |

**错误码：**
以下错误码的详细介绍请参见[ohos.multimedia.avsession(多媒体会话)错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |

**示例：**

```js
avSession.off('topSessionChange');
```

## avSession.on('sessionServiceDie')

on(type: 'sessionServiceDie', callback: () => void): void

监听会话的服务死亡事件。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**系统接口：** 该接口为系统接口

**参数：**

| 参数名   | 类型                 | 必填 | 说明                                                         |
| -------- | -------------------- | ---- | ------------------------------------------------------------ |
| type     | string               | 是   | 事件回调类型，支持事件`'sessionServiceDie'`：会话服务死亡事件，检测到会话的服务死亡时触发。 |
| callback | callback: () => void | 是   | 回调函数。当监听事件注册成功，err为undefined，否则返回错误对象。                                |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |

**示例：**

```js
avSession.on('sessionServiceDie', () => {
    console.info(`on sessionServiceDie  : session is  Died `);
});
```

## avSession.off('sessionServiceDie')

off(type: 'sessionServiceDie', callback?: () => void): void

取消会话服务死亡监听，取消后，不再进行服务死亡监听。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**系统接口：** 该接口为系统接口

**参数：**

| 参数名    | 类型                    | 必填  |      说明                                               |
| ------   | ---------------------- | ---- | ------------------------------------------------------- |
| type     | string                 | 是    | 事件回调类型，支持事件`'sessionServiceDie'`：会话服务死亡事件。|
| callback | callback: () => void   | 否    | 回调函数。当监听事件取消成功，err为undefined，否则返回错误对象。<br>该参数为可选参数，若不填写该参数，则认为取消所有相关会话的服务死亡监听。            |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |

**示例：**

```js
avSession.off('sessionServiceDie');
```

## avSession.sendSystemAVKeyEvent

sendSystemAVKeyEvent(event: KeyEvent): Promise\<void>

发送按键事件给置顶会话。结果通过Promise异步回调方式返回。

**需要权限：** ohos.permission.MANAGE_MEDIA_RESOURCES，仅系统应用可用。

**系统能力：** SystemCapability.Multimedia.AVSession.Manager

**系统接口：** 该接口为系统接口。

**参数：**

| 参数名 | 类型                            | 必填 | 说明       |
| ------ | ------------------------------- | ---- | ---------- |
| event  | [KeyEvent](js-apis-keyevent.md) | 是   | 按键事件。 |

**返回值：**

| 类型           | 说明                          |
| -------------- | ----------------------------- |
| Promise\<void> | Promise对象。当事件发送成功，无返回结果，否则返回错误对象。 |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |
| 6600105  | Invalid session command. |

**示例：**

```js

let keyItem = {code:0x49, pressedTime:2, deviceId:0};
let event = {id:1, deviceId:0, actionTime:1, screenId:1, windowId:1, action:2, key:keyItem, unicodeChar:0, keys:[keyItem], ctrlKey:false, altKey:false, shiftKey:false, logoKey:false, fnKey:false, capsLock:false, numLock:false, scrollLock:false}; 

avSession.sendSystemAVKeyEvent(event).then(() => {
    console.info(`SendSystemAVKeyEvent Successfully`);
}).catch((err) => {
    console.info(`SendSystemAVKeyEvent BusinessError: code: ${err.code}, message: ${err.message}`);
});

```

## avSession.sendSystemAVKeyEvent

sendSystemAVKeyEvent(event: KeyEvent, callback: AsyncCallback\<void>): void

发送按键事件给置顶会话。结果通过callback异步回调方式返回。

**需要权限：** ohos.permission.MANAGE_MEDIA_RESOURCES，仅系统应用可用。

**系统能力：** SystemCapability.Multimedia.AVSession.Manager

**系统接口：** 该接口为系统接口。

**参数：**

| 参数名   | 类型                                                         | 必填 | 说明                                  |
| -------- | ------------------------------------------------------------ | ---- | ------------------------------------- |
| event    | [KeyEvent](js-apis-keyevent.md) | 是   | 按键事件。                            |
| callback | AsyncCallback\<void>                                         | 是   | 回调函数。当事件发送成功，err为undefined，否则返回错误对象。 |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |
| 6600105  | Invalid session command. |

**示例：**

```js
let keyItem = {code:0x49, pressedTime:2, deviceId:0};
let event = {id:1, deviceId:0, actionTime:1, screenId:1, windowId:1, action:2, key:keyItem, unicodeChar:0, keys:[keyItem], ctrlKey:false, altKey:false, shiftKey:false, logoKey:false, fnKey:false, capsLock:false, numLock:false, scrollLock:false}; 

avSession.sendSystemAVKeyEvent(event, function (err) {
    if (err) {
        console.info(`SendSystemAVKeyEvent BusinessError: code: ${err.code}, message: ${err.message}`);
    } else {
        console.info(`SendSystemAVKeyEvent : SUCCESS `);
    }
});
```

## avSession.sendSystemControlCommand

sendSystemControlCommand(command: AVControlCommand): Promise\<void>

发送控制命令给置顶会话。结果通过Promise异步回调方式返回。

**需要权限：** ohos.permission.MANAGE_MEDIA_RESOURCES，仅系统应用可用。

**系统能力：** SystemCapability.Multimedia.AVSession.Manager

**系统接口：** 该接口为系统接口。

**参数：**

| 参数名  | 类型                                  | 必填 | 说明                                |
| ------- | ------------------------------------- | ---- | ----------------------------------- |
| command | [AVControlCommand](#avcontrolcommand10) | 是   | AVSession的相关命令和命令相关参数。 |

**返回值：**

| 类型           | 说明                          |
| -------------- | ----------------------------- |
| Promise\<void> | Promise对象。当命令发送成功，无返回结果，否则返回错误对象。 |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |
| 6600105  | Invalid session command. |
| 6600107  | Too many commands or events. |

**示例：**

```js
let cmd : avSession.AVControlCommandType = 'play';
// let cmd : avSession.AVControlCommandType = 'pause';
// let cmd : avSession.AVControlCommandType = 'stop';
// let cmd : avSession.AVControlCommandType = 'playNext';
// let cmd : avSession.AVControlCommandType = 'playPrevious';
// let cmd : avSession.AVControlCommandType = 'fastForward';
// let cmd : avSession.AVControlCommandType = 'rewind';
let avcommand = {command:cmd};
// let cmd : avSession.AVControlCommandType = 'seek';
// let avcommand = {command:cmd, parameter:10};
// let cmd : avSession.AVControlCommandType = 'setSpeed';
// let avcommand = {command:cmd, parameter:2.6};
// let cmd : avSession.AVControlCommandType = 'setLoopMode';
// let avcommand = {command:cmd, parameter:avSession.LoopMode.LOOP_MODE_SINGLE};
// let cmd : avSession.AVControlCommandType = 'toggleFavorite';
// let avcommand = {command:cmd, parameter:"false"};
avSession.sendSystemControlCommand(avcommand).then(() => {
    console.info(`SendSystemControlCommand successfully`);
}).catch((err) => {
    console.info(`SendSystemControlCommand BusinessError: code: ${err.code}, message: ${err.message}`);
});
```

## avSession.sendSystemControlCommand

sendSystemControlCommand(command: AVControlCommand, callback: AsyncCallback\<void>): void

发送控制命令给置顶会话。结果通过callback异步回调方式返回。

**需要权限：** ohos.permission.MANAGE_MEDIA_RESOURCES，仅系统应用可用。

**系统能力：** SystemCapability.Multimedia.AVSession.Manager

**系统接口：** 该接口为系统接口。

**参数：**

| 参数名   | 类型                                  | 必填 | 说明                                  |
| -------- | ------------------------------------- | ---- | ------------------------------------- |
| command  | [AVControlCommand](#avcontrolcommand10) | 是   | AVSession的相关命令和命令相关参数。   |
| callback | AsyncCallback\<void>                  | 是   | 回调函数。当命令发送成功，err为undefined，否则返回错误对象。 |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |
| 6600105  | Invalid session command. |
| 6600107  | Too many commands or events. |

**示例：**

```js
let cmd : avSession.AVControlCommandType = 'play';
// let cmd : avSession.AVControlCommandType = 'pause';
// let cmd : avSession.AVControlCommandType = 'stop';
// let cmd : avSession.AVControlCommandType = 'playNext';
// let cmd : avSession.AVControlCommandType = 'playPrevious';
// let cmd : avSession.AVControlCommandType = 'fastForward';
// let cmd : avSession.AVControlCommandType = 'rewind';
let avcommand = {command:cmd};
// let cmd : avSession.AVControlCommandType = 'seek';
// let avcommand = {command:cmd, parameter:10};
// let cmd : avSession.AVControlCommandType = 'setSpeed';
// let avcommand = {command:cmd, parameter:2.6};
// let cmd : avSession.AVControlCommandType = 'setLoopMode';
// let avcommand = {command:cmd, parameter:avSession.LoopMode.LOOP_MODE_SINGLE};
// let cmd : avSession.AVControlCommandType = 'toggleFavorite';
// let avcommand = {command:cmd, parameter:"false"};
avSession.sendSystemControlCommand(avcommand, function (err) {
    if (err) {
        console.info(`SendSystemControlCommand BusinessError: code: ${err.code}, message: ${err.message}`);
    } else {
        console.info(`sendSystemControlCommand successfully`);
    }
});
```

## avSession.startCastDeviceDiscovery<sup>10+</sup>

startCastDeviceDiscovery(callback: AsyncCallback\<void>): void

开始设备搜索发现。结果通过callback异步回调方式返回。

**系统能力：** SystemCapability.Multimedia.AVSession.AVCast

**系统接口：** 该接口为系统接口。

**参数：**

| 参数名   | 类型                                  | 必填 | 说明                                  |
| -------- | ------------------------------------- | ---- | ------------------------------------- |
| callback | AsyncCallback\<void>                  | 是   | 回调函数。当命令发送成功，err为undefined，否则返回错误对象。 |


**示例：**

```js
avSession.startCastDeviceDiscovery(function (err) {
    if (err) {
        console.info(`startCastDeviceDiscovery BusinessError: code: ${err.code}, message: ${err.message}`);
    } else {
        console.info(`startCastDeviceDiscovery successfully`);
    }
});
```

## avSession.startCastDeviceDiscovery<sup>10+</sup>

startCastDeviceDiscovery(filter: number, callback: AsyncCallback\<void>): void

开始设备搜索发现。结果通过callback异步回调方式返回。

**系统能力：** SystemCapability.Multimedia.AVSession.AVCast

**系统接口：** 该接口为系统接口。

**参数：**

| 参数名   | 类型                                  | 必填 | 说明                                  |
| -------- | ------------------------------------- | ---- | ------------------------------------- |
| filter | number | 是 | 进行设备发现的过滤条件，由ProtocolType的组合而成 |
| callback | AsyncCallback\<void>                  | 是   | 回调函数。当命令发送成功，err为undefined，否则返回错误对象。 |


**示例：**

```js
let filter = 2;
avSession.startCastDeviceDiscovery(filter, function (err) {
    if (err) {
        console.info(`startCastDeviceDiscovery BusinessError: code: ${err.code}, message: ${err.message}`);
    } else {
        console.info(`startCastDeviceDiscovery successfully`);
    }
});
```

## avSession.startCastDeviceDiscovery<sup>10+</sup>

startCastDeviceDiscovery(filter?: number): Promise\<void>

开始设备搜索发现。结果通过Promise异步回调方式返回。

**系统能力：** SystemCapability.Multimedia.AVSession.AVCast

**系统接口：** 该接口为系统接口。

**参数：**

| 参数名   | 类型                                  | 必填 | 说明                                  |
| -------- | ------------------------------------- | ---- | ------------------------------------- |
| filter | number | 否 | 进行设备发现的过滤条件，由ProtocolType的组合而成 |

**返回值：**
| 类型           | 说明                          |
| -------------- | ----------------------------- |
| Promise\<void> | Promise对象。当开始设备搜索成功，无返回结果，否则返回错误对象。 |

**示例：**

```js
let filter = 2;
avSession.startCastDeviceDiscovery(filter).then(() => {
    console.info(`startCastDeviceDiscovery successfully`);
}).catch((err) => {
    console.info(`startCastDeviceDiscovery BusinessError: code: ${err.code}, message: ${err.message}`);
});
```

## avSession.on('deviceAvailable')<sup>10+</sup>

on(type: 'deviceAvailable', callback: (device: OutputDeviceInfo) => void): void

设备发现回调监听。

**系统能力：** SystemCapability.Multimedia.AVSession.AVCast

**系统接口：** 该接口为系统接口

**参数：**

| 参数名   | 类型                 | 必填 | 说明                                                         |
| -------- | -------------------- | ---- | ------------------------------------------------------------ |
| type     | string               | 是   | 事件回调类型，支持事件`'deviceAvailable'`，有设备更新时触发回调。 |
| callback | (device: OutputDeviceInfo) => void | 是   | 回调函数。当监听事件注册成功，err为undefined，否则返回错误对象。                                |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |

**示例：**

```js
avSession.on('deviceAvailable', (device) => {
    console.info(`on deviceAvailable  : ${device} `);
});
```

## avSession.off('deviceAvailable')<sup>10+</sup>

off(type: 'deviceAvailable', callback?: (device: OutputDeviceInfo) => void): void

取消设备发现回调的监听。

**系统能力：** SystemCapability.Multimedia.AVSession.AVCast

**系统接口：** 该接口为系统接口

**参数：**

| 参数名    | 类型                    | 必填  |      说明                                               |
| ------   | ---------------------- | ---- | ------------------------------------------------------- |
| type     | string                 | 是    | 事件回调类型，支持事件`'deviceAvailable'`：设备发现回调。|

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |

**示例：**

```js
avSession.off('deviceAvailable');
```

## avSession.stopCastDeviceDiscovery<sup>10+</sup>

stopCastDeviceDiscovery(callback: AsyncCallback\<void>): void

结束设备搜索发现。结果通过callback异步回调方式返回。

**系统能力：** SystemCapability.Multimedia.AVSession.AVCast

**系统接口：** 该接口为系统接口。

**参数：**

| 参数名   | 类型                                  | 必填 | 说明                                  |
| -------- | ------------------------------------- | ---- | ------------------------------------- |
| callback | AsyncCallback\<void>                  | 是   | 回调函数。当命令发送成功，err为undefined，否则返回错误对象。 |


**示例：**

```js
avSession.stopCastDeviceDiscovery(function (err) {
    if (err) {
        console.info(`stopCastDeviceDiscovery BusinessError: code: ${err.code}, message: ${err.message}`);
    } else {
        console.info(`stopCastDeviceDiscovery successfully`);
    }
});
```

## avSession.stopCastDeviceDiscovery<sup>10+</sup>

stopCastDeviceDiscovery(): Promise\<void>

结束设备搜索发现。结果通过Promise异步回调方式返回。

**系统能力：** SystemCapability.Multimedia.AVSession.AVCast

**系统接口：** 该接口为系统接口。

**返回值：**

| 类型           | 说明                          |
| -------------- | ----------------------------- |
| Promise\<void> | Promise对象。当停止搜索成功，无返回结果，否则返回错误对象。 |

**示例：**

```js
avSession.stopCastDeviceDiscovery().then(() => {
    console.info(`startCastDeviceDiscovery successfully`);
}).catch((err) => {
    console.info(`startCastDeviceDiscovery BusinessError: code: ${err.code}, message: ${err.message}`);
});
```

## avSession.startCasting<sup>10+</sup>

startCasting(session: SessionToken, device: OutputDeviceInfo, callback: AsyncCallback\<void>): void

启动投播。结果通过callback异步回调方式返回。

**需要权限：** ohos.permission.MANAGE_MEDIA_RESOURCES，仅系统应用可用。

**系统能力：** SystemCapability.Multimedia.AVSession.AVCast

**系统接口：** 该接口为系统接口。

**参数：**

| 参数名   | 类型                                  | 必填 | 说明                                  |
| -------- | ------------------------------------- | ---- | ------------------------------------- |
| session      | [SessionToken](#sessiontoken) | 是   | 会话令牌。SessionToken表示单个token。 |
| device | [OutputDeviceInfo](#outputdeviceinfo10)                        | 是   | 设备相关信息 | 
| callback | AsyncCallback\<void>                  | 是   | 回调函数。当命令发送成功，err为undefined，否则返回错误对象。 |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |
| 6600108 | Device connecting failed.       |

**示例：**

```js
let castDevice;
avSession.on('deviceAvailable', (device) => {
    castDevice = device;
    console.info(`on deviceAvailable  : ${device} `);
});
let myToken = {
    sessionId: avSession.sessionId;
}
avSession.startCasting(myToken, castDevice, function (err) {
    if (err) {
        console.info(`startCasting BusinessError: code: ${err.code}, message: ${err.message}`);
    } else {
        console.info(`startCasting successfully`);
    }
});
```

## avSession.startCasting<sup>10+</sup>

startCasting(session: SessionToken, device: OutputDeviceInfo): Promise\<void>

启动投播。结果通过Promise异步回调方式返回。

**需要权限：** ohos.permission.MANAGE_MEDIA_RESOURCES，仅系统应用可用。

**系统能力：** SystemCapability.Multimedia.AVSession.AVCast

**系统接口：** 该接口为系统接口。

**参数：**

| 参数名   | 类型                                  | 必填 | 说明                                  |
| -------- | ------------------------------------- | ---- | ------------------------------------- |
| session      | [SessionToken](#sessiontoken) | 是   | 会话令牌。SessionToken表示单个token。 |
| device | [OutputDeviceInfo](#outputdeviceinfo10)                        | 是   | 设备相关信息 |

**返回值：**

| 类型           | 说明                          |
| -------------- | ----------------------------- |
| Promise\<void> | Promise对象。当停止搜索成功，无返回结果，否则返回错误对象。 |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |
| 6600108 | Device connecting failed.       |

**示例：**

```js
let castDevice;
avSession.on('deviceAvailable', (device) => {
    castDevice = device;
    console.info(`on deviceAvailable  : ${device} `);
});
let myToken = {
    sessionId: avSession.sessionId;
}
avSession.startCasting(myToken, castDevice).then(() => {
    console.info(`startCasting successfully`);
}).catch((err) => {
    console.info(`startCasting BusinessError: code: ${err.code}, message: ${err.message}`);
});
```

## avSession.stopCasting<sup>10+</sup>

stopCasting(session: SessionToken, callback: AsyncCallback\<void>): void

结束投播。结果通过callback异步回调方式返回。

**系统能力：** SystemCapability.Multimedia.AVSession.AVCast

**系统接口：** 该接口为系统接口。

**参数：**

| 参数名   | 类型                                  | 必填 | 说明                                  |
| -------- | ------------------------------------- | ---- | ------------------------------------- |
| session      | [SessionToken](#sessiontoken) | 是   | 会话令牌。SessionToken表示单个token。 | 
| callback | AsyncCallback\<void>                  | 是   | 回调函数。当命令发送成功，err为undefined，否则返回错误对象。 |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600109  | The remote connection is not established. |

**示例：**

```js
let myToken = {
    sessionId: avSession.sessionId;
}
avSession.stopCasting(myToken, castDevice, function (err) {
    if (err) {
        console.info(`stopCasting BusinessError: code: ${err.code}, message: ${err.message}`);
    } else {
        console.info(`stopCasting successfully`);
    }
});
```

## avSession.stopCasting<sup>10+</sup>

stopCasting(session: SessionToken): Promise\<void>

结束投播。结果通过Promise异步回调方式返回。

**系统能力：** SystemCapability.Multimedia.AVSession.AVCast

**系统接口：** 该接口为系统接口。

**参数：**

| 参数名   | 类型                                  | 必填 | 说明                                  |
| -------- | ------------------------------------- | ---- | ------------------------------------- |
| session      | [SessionToken](#sessiontoken) | 是   | 会话令牌。SessionToken表示单个token。 |

**返回值：**

| 类型           | 说明                          |
| -------------- | ----------------------------- |
| Promise\<void> | Promise对象。当停止搜索成功，无返回结果，否则返回错误对象。 |

**错误码：**
错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600109  | The remote connection is not established. |

**示例：**

```js
let myToken = {
    sessionId: avSession.sessionId;
}
avSession.stopCasting(myToken).then(() => {
    console.info(`stopCasting successfully`);
}).catch((err) => {
    console.info(`stopCasting BusinessError: code: ${err.code}, message: ${err.message}`);
});
```


## avSession.setDiscoverable<sup>10+</sup>

setDiscoverable(enable: boolean, callback: AsyncCallback\<void>): void

设置设备是否可被发现，用于投播接收端。结果通过callback异步回调方式返回。

**系统能力：** SystemCapability.Multimedia.AVSession.AVCast

**系统接口：** 该接口为系统接口。

**参数：**

| 参数名   | 类型                                  | 必填 | 说明                                  |
| -------- | ------------------------------------- | ---- | ------------------------------------- |
| enable | boolean | 是 | 是否允许本设备被发现. true: 允许被发现， false：不允许被发现 |
| callback | AsyncCallback\<void>                  | 是   | 回调函数。当命令发送成功，err为undefined，否则返回错误对象。 |


**示例：**

```js
avSession.setDiscoverable(true, function (err) {
    if (err) {
        console.info(`setDiscoverable BusinessError: code: ${err.code}, message: ${err.message}`);
    } else {
        console.info(`setDiscoverable successfully`);
    }
});
```

## avSession.setDiscoverable<sup>10+</sup>

setDiscoverable(enable: boolean): Promise\<void>

设置设备是否可被发现，用于投播接收端。结果通过Promise异步回调方式返回。

**系统能力：** SystemCapability.Multimedia.AVSession.AVCast

**系统接口：** 该接口为系统接口。

**参数：**

| 参数名   | 类型                                  | 必填 | 说明                                  |
| -------- | ------------------------------------- | ---- | ------------------------------------- |
| enable | boolean | 是 | 是否允许本设备被发现. true: 允许被发现， false：不允许被发现 |

**返回值：**

| 类型           | 说明                          |
| -------------- | ----------------------------- |
| Promise\<void> | Promise对象。当停止搜索成功，无返回结果，否则返回错误对象。 |

**示例：**

```js
avSession.setDiscoverable(true).then(() => {
    console.info(`setDiscoverable successfully`);
}).catch((err) => {
    console.info(`setDiscoverable BusinessError: code: ${err.code}, message: ${err.message}`);
});
```

## AVSession<sup>10+</sup>

调用[avSession.createAVSession](#avsessioncreateavsession10)后，返回会话的实例，可以获得会话ID，完成设置元数据，播放状态信息等操作。

### 属性

**系统能力：** SystemCapability.Multimedia.AVSession.Core

| 名称      | 类型   | 可读 | 可写 | 说明                          |
| :-------- | :----- | :--- | :--- | :---------------------------- |
| sessionId | string | 是   | 否   | AVSession对象唯一的会话标识。 |
| sessionType<sup>10+</sup> | AVSessionType | 是   | 否   | AVSession会话类型。 |


**示例：**
```js
let sessionId = session.sessionId;
```

### setAVMetadata<sup>10+</sup>

setAVMetadata(data: AVMetadata): Promise\<void>

设置会话元数据。结果通过Promise异步回调方式返回。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**参数：**

| 参数名 | 类型                      | 必填 | 说明         |
| ------ | ------------------------- | ---- | ------------ |
| data   | [AVMetadata](#avmetadata10) | 是   | 会话元数据。 |

**返回值：**

| 类型           | 说明                          |
| -------------- | ----------------------------- |
| Promise\<void> | Promise对象。当元数据设置成功，无返回结果，否则返回错误对象。 |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |
| 6600102  | The session does not exist. |

**示例：**

```js
let metadata  = {
    assetId: "121278",
    title: "lose yourself",
    artist: "Eminem",
    author: "ST",
    album: "Slim shady",
    writer: "ST",
    composer: "ST",
    duration: 2222,
    mediaImage: "https://www.example.com/example.jpg",
    subtitle: "8 Mile",
    description: "Rap",
    lyric: "https://www.example.com/example.lrc",
    previousAssetId: "121277",
    nextAssetId: "121279",
};
session.setAVMetadata(metadata).then(() => {
    console.info(`SetAVMetadata successfully`);
}).catch((err) => {
    console.info(`SetAVMetadata BusinessError: code: ${err.code}, message: ${err.message}`);
});
```

### setAVMetadata<sup>10+</sup>

setAVMetadata(data: AVMetadata, callback: AsyncCallback\<void>): void

设置会话元数据。结果通过callback异步回调方式返回。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**参数：**

| 参数名   | 类型                      | 必填 | 说明                                  |
| -------- | ------------------------- | ---- | ------------------------------------- |
| data     | [AVMetadata](#avmetadata10) | 是   | 会话元数据。                          |
| callback | AsyncCallback\<void>      | 是   | 回调函数。当元数据设置成功，err为undefined，否则返回错误对象。 |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |
| 6600102  | The session does not exist. |

**示例：**

```js
let metadata  = {
    assetId: "121278",
    title: "lose yourself",
    artist: "Eminem",
    author: "ST",
    album: "Slim shady",
    writer: "ST",
    composer: "ST",
    duration: 2222,
    mediaImage: "https://www.example.com/example.jpg",
    subtitle: "8 Mile",
    description: "Rap",
    lyric: "https://www.example.com/example.lrc",
    previousAssetId: "121277",
    nextAssetId: "121279",
};
session.setAVMetadata(metadata, function (err) {
    if (err) {
        console.info(`SetAVMetadata BusinessError: code: ${err.code}, message: ${err.message}`);
    } else {
        console.info(`SetAVMetadata successfully`);
    }
});
```

### setAVPlaybackState<sup>10+</sup>

setAVPlaybackState(state: AVPlaybackState): Promise\<void>

设置会话播放状态。结果通过Promise异步回调方式返回。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**参数：**

| 参数名 | 类型                                | 必填 | 说明                                           |
| ------ | ----------------------------------- | ---- | ---------------------------------------------- |
| data   | [AVPlaybackState](#avplaybackstate10) | 是   | 会话播放状态，包括状态、倍数、循环模式等信息。 |

**返回值：**

| 类型           | 说明                          |
| -------------- | ----------------------------- |
| Promise\<void> | Promise对象。当播放状态设置成功，无返回结果，否则返回错误对象。 |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |
| 6600102  | The session does not exist. |

**示例：**

```js
let playbackState = {
    state:avSession.PlaybackState.PLAYBACK_STATE_PLAY,
    speed: 1.0,
    position:{elapsedTime:10, updateTime:(new Date()).getTime()},
    bufferedTime:1000,
    loopMode:avSession.LoopMode.LOOP_MODE_SINGLE,
    isFavorite:true,
};
session.setAVPlaybackState(playbackState).then(() => {
    console.info(`SetAVPlaybackState successfully`);
}).catch((err) => {
    console.info(`SetAVPlaybackState BusinessError: code: ${err.code}, message: ${err.message}`);
});
```

### setAVPlaybackState<sup>10+</sup>

setAVPlaybackState(state: AVPlaybackState, callback: AsyncCallback\<void>): void

设置会话播放状态。结果通过callback异步回调方式返回。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**参数：**

| 参数名   | 类型                                | 必填 | 说明                                           |
| -------- | ----------------------------------- | ---- | ---------------------------------------------- |
| data     | [AVPlaybackState](#avplaybackstate10) | 是   | 会话播放状态，包括状态、倍数、循环模式等信息。 |
| callback | AsyncCallback\<void>                | 是   | 回调函数。当播放状态设置成功，err为undefined，否则返回错误对象。          |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |
| 6600102  | The session does not exist. |

**示例：**

```js
let PlaybackState = {
    state:avSession.PlaybackState.PLAYBACK_STATE_PLAY,
    speed: 1.0,
    position:{elapsedTime:10, updateTime:(new Date()).getTime()},
    bufferedTime:1000,
    loopMode:avSession.LoopMode.LOOP_MODE_SINGLE,
    isFavorite:true,
};
session.setAVPlaybackState(PlaybackState, function (err) {
    if (err) {
        console.info(`SetAVPlaybackState BusinessError: code: ${err.code}, message: ${err.message}`);
    } else {
        console.info(`SetAVPlaybackState successfully`);
    }
});
```

### setAVQueueItems<sup>10+</sup>

setAVQueueItems(items: Array\<AVQueueItem>): Promise\<void>

设置媒体播放列表。结果通过Promise异步回调方式返回。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**参数：**

| 参数名  | 类型                                 | 必填 | 说明                               |
| ------ | ------------------------------------ | ---- | ---------------------------------- |
| items  | Array<[AVQueueItem](#avqueueitem10)\> | 是   | 播放列表单项的队列，用以表示播放列表。 |

**返回值：**

| 类型           | 说明                          |
| -------------- | ----------------------------- |
| Promise\<void> | Promise对象。当播放列表设置成功，无返回结果，否则返回错误对象。 |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |
| 6600102  | The session does not exist. |

**示例：**

```js
import image from '@ohos.multimedia.image';
import resourceManager from '@ohos.resourceManager';

let value : Uint8Array = await resourceManager.getRawFileContent('IMAGE_URI');
let imageSource : imageImageSource = image.createImageSource(value.buffer);
let imagePixel : image.PixelMap = await imageSource.createPixelMap({desiredSize:{width: 150, height: 150}});
let queueItemDescription_1 = {
    mediaId: '001',
    title: 'music_name',
    subtitle: 'music_sub_name',
    description: 'music_description',
    icon : imagePixel,
    iconUri: 'http://www.icon.uri.com',
    extras: {'extras':'any'}
};
let queueItem_1 = {
    itemId: 1,
    description: queueItemDescription_1
};
let queueItemDescription_2 = {
    mediaId: '002',
    title: 'music_name',
    subtitle: 'music_sub_name',
    description: 'music_description',
    icon: imagePixel,
    iconUri: 'http://www.xxx.com',
    extras: {'extras':'any'}
};
let queueItem_2 = {
    itemId: 2,
    description: queueItemDescription_2
};
let queueItemsArray = [queueItem_1, queueItem_2];
session.setAVQueueItems(queueItemsArray).then(() => {
    console.info(`SetAVQueueItems successfully`);
}).catch((err) => {
    console.info(`SetAVQueueItems BusinessError: code: ${err.code}, message: ${err.message}`);
});
```

### setAVQueueItems<sup>10+</sup>

setAVQueueItems(items: Array\<AVQueueItem>, callback: AsyncCallback\<void>): void

设置媒体播放列表。结果通过callback异步回调方式返回。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**参数：**

| 参数名   | 类型                                  | 必填 | 说明                                                         |
| -------- | ------------------------------------ | ---- | ----------------------------------------------------------- |
| items    | Array<[AVQueueItem](#avqueueitem10)\> | 是   | 播放列表单项的队列，用以表示播放列表。                          |
| callback | AsyncCallback\<void>                 | 是   | 回调函数。当播放状态设置成功，err为undefined，否则返回错误对象。 |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |
| 6600102  | The session does not exist. |

**示例：**

```js
import image from '@ohos.multimedia.image';
import resourceManager from '@ohos.resourceManager';

let value : Uint8Array = await resourceManager.getRawFileContent('IMAGE_URI');
let imageSource : imageImageSource = image.createImageSource(value.buffer);
let imagePixel : image.PixelMap = await imageSource.createPixelMap({desiredSize:{width: 150, height: 150}});
let queueItemDescription_1 = {
    mediaId: '001',
    title: 'music_name',
    subtitle: 'music_sub_name',
    description: 'music_description',
    icon: imagePixel,
    iconUri: 'http://www.icon.uri.com',
    extras: {'extras':'any'}
};
let queueItem_1 = {
    itemId: 1,
    description: queueItemDescription_1
};
let queueItemDescription_2 = {
    mediaId: '002',
    title: 'music_name',
    subtitle: 'music_sub_name',
    description: 'music_description',
    icon: imagePixel,
    iconUri: 'http://www.icon.uri.com',
    extras: {'extras':'any'}
};
let queueItem_2 = {
    itemId: 2,
    description: queueItemDescription_2
};
let queueItemsArray = [queueItem_1, queueItem_2];
session.setAVQueueItems(queueItemsArray, function (err) {
    if (err) {
        console.info(`SetAVQueueItems BusinessError: code: ${err.code}, message: ${err.message}`);
    } else {
        console.info(`SetAVQueueItems successfully`);
    }
});
```

### setAVQueueTitle<sup>10+</sup>

setAVQueueTitle(title: string): Promise\<void>

设置媒体播放列表名称。结果通过Promise异步回调方式返回。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**参数：**

| 参数名  | 类型   | 必填 | 说明           |
| ------ | ------ | ---- | -------------- |
| title  | string | 是   | 播放列表的名称。 |

**返回值：**

| 类型           | 说明                          |
| -------------- | ----------------------------- |
| Promise\<void> | Promise对象。当播放列表设置成功，无返回结果，否则返回错误对象。 |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |
| 6600102  | The session does not exist. |

**示例：**

```js
let queueTitle = 'QUEUE_TITLE';
session.setAVQueueTitle(queueTitle).then(() => {
    console.info(`SetAVQueueTitle successfully`);
}).catch((err) => {
    console.info(`SetAVQueueTitle BusinessError: code: ${err.code}, message: ${err.message}`);
});
```

### setAVQueueTitle<sup>10+</sup>

setAVQueueTitle(title: string, callback: AsyncCallback\<void>): void

设置媒体播放列表名称。结果通过callback异步回调方式返回。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**参数：**

| 参数名   | 类型                                  | 必填 | 说明                                                         |
| -------- | --------------------- | ---- | ----------------------------------------------------------- |
| title    | string                | 是   | 播放列表名称字段。                          |
| callback | AsyncCallback\<void>  | 是   | 回调函数。当播放状态设置成功，err为undefined，否则返回错误对象。 |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |
| 6600102  | The session does not exist. |

**示例：**

```js
let queueTitle = 'QUEUE_TITLE';
session.setAVQueueTitle(queueTitle, function (err) {
    if (err) {
        console.info(`SetAVQueueTitle BusinessError: code: ${err.code}, message: ${err.message}`);
    } else {
        console.info(`SetAVQueueTitle successfully`);
    }
});
```

### setLaunchAbility<sup>10+</sup>

setLaunchAbility(ability: WantAgent): Promise\<void>

设置一个WantAgent用于拉起会话的Ability。结果通过Promise异步回调方式返回。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**参数：**

| 参数名  | 类型                                          | 必填 | 说明                                                        |
| ------- | --------------------------------------------- | ---- | ----------------------------------------------------------- |
| ability | [WantAgent](js-apis-app-ability-wantAgent.md) | 是   | 应用的相关属性信息，如bundleName，abilityName，deviceId等。 |

**返回值：**

| 类型           | 说明                          |
| -------------- | ----------------------------- |
| Promise\<void> | Promise对象。当Ability设置成功，无返回结果，否则返回错误对象。 |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |
| 6600102  | The session does not exist. |

**示例：**

```js
import wantAgent from '@ohos.app.ability.wantAgent';

//WantAgentInfo对象
let wantAgentInfo = {
    wants: [
        {
            deviceId: "deviceId",
            bundleName: "com.example.myapplication",
            abilityName: "EntryAbility",
            action: "action1",
            entities: ["entity1"],
            type: "MIMETYPE",
            uri: "key={true,true,false}",
            parameters:
                {
                    mykey0: 2222,
                    mykey1: [1, 2, 3],
                    mykey2: "[1, 2, 3]",
                    mykey3: "ssssssssssssssssssssssssss",
                    mykey4: [false, true, false],
                    mykey5: ["qqqqq", "wwwwww", "aaaaaaaaaaaaaaaaa"],
                    mykey6: true,
                }
        }
    ],
    operationType: wantAgent.OperationType.START_ABILITIES,
    requestCode: 0,
    wantAgentFlags:[wantAgent.WantAgentFlags.UPDATE_PRESENT_FLAG]
}

wantAgent.getWantAgent(wantAgentInfo).then((agent) => {
    session.setLaunchAbility(agent).then(() => {
        console.info(`SetLaunchAbility successfully`);
    }).catch((err) => {
        console.info(`SetLaunchAbility BusinessError: code: ${err.code}, message: ${err.message}`);
    });
});
```

### setLaunchAbility<sup>10+</sup>

setLaunchAbility(ability: WantAgent, callback: AsyncCallback\<void>): void

设置一个WantAgent用于拉起会话的Ability。结果通过callback异步回调方式返回。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**参数：**

| 参数名   | 类型                                          | 必填 | 说明                                                         |
| -------- | --------------------------------------------- | ---- | ------------------------------------------------------------ |
| ability  | [WantAgent](js-apis-app-ability-wantAgent.md) | 是   | 应用的相关属性信息，如bundleName，abilityName，deviceId等。  |
| callback | AsyncCallback\<void>                          | 是   | 回调函数。当Ability设置成功，err为undefined，否则返回错误对象。 |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |
| 6600102  | The session does not exist. |

**示例：**

```js
import wantAgent from '@ohos.app.ability.wantAgent';

//WantAgentInfo对象
let wantAgentInfo = {
    wants: [
        {
            deviceId: "deviceId",
            bundleName: "com.example.myapplication",
            abilityName: "EntryAbility",
            action: "action1",
            entities: ["entity1"],
            type: "MIMETYPE",
            uri: "key={true,true,false}",
            parameters:
                {
                    mykey0: 2222,
                    mykey1: [1, 2, 3],
                    mykey2: "[1, 2, 3]",
                    mykey3: "ssssssssssssssssssssssssss",
                    mykey4: [false, true, false],
                    mykey5: ["qqqqq", "wwwwww", "aaaaaaaaaaaaaaaaa"],
                    mykey6: true,
                }
        }
    ],
    operationType: wantAgent.OperationType.START_ABILITIES,
    requestCode: 0,
    wantAgentFlags:[wantAgent.WantAgentFlags.UPDATE_PRESENT_FLAG]
}

wantAgent.getWantAgent(wantAgentInfo).then((agent) => {
    session.setLaunchAbility(agent, function (err) {
        if (err) {
            console.info(`SetLaunchAbility BusinessError: code: ${err.code}, message: ${err.message}`);
        } else {
            console.info(`SetLaunchAbility successfully`);
        }
    });
});
```

### dispatchSessionEvent<sup>10+</sup>

dispatchSessionEvent(event: string, args: {[key: string]: Object}): Promise\<void>

媒体提供方设置一个会话内自定义事件，包括事件名和键值对形式的事件内容, 结果通过Promise异步回调方式返回。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**参数：**

| 参数名  | 类型                                          | 必填 | 说明                                                        |
| ------- | --------------------------------------------- | ---- | ----------------------------------------------------------- |
| event | string | 是   | 需要设置的会话事件的名称 |
| args | {[key: string]: any} | 是   | 需要传递的会话事件键值对 |

> **说明：**
> 参数args支持的数据类型有：字符串、数字、布尔、对象、数组和文件描述符等，详细介绍请参见[@ohos.app.ability.Want(Want)](./js-apis-app-ability-want.md)。

**返回值：**

| 类型           | 说明                          |
| -------------- | ----------------------------- |
| Promise\<void> | Promise对象。当事件设置成功，无返回结果，否则返回错误对象。 |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |
| 6600102  | The session does not exist. |

**示例：**

```js
let eventName = "dynamic_lyric";
let args = {
    lyric : "This is lyric"
}
await session.dispatchSessionEvent(eventName, args).catch((err) => {
    console.info(`dispatchSessionEvent BusinessError: code: ${err.code}, message: ${err.message}`);
})
```

### dispatchSessionEvent<sup>10+</sup>

dispatchSessionEvent(event: string, args: {[key: string]: Object}, callback: AsyncCallback\<void>): void

媒体提供方设置一个会话内自定义事件，包括事件名和键值对形式的事件内容, 结果通过callback异步回调方式返回。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**参数：**

| 参数名  | 类型                                          | 必填 | 说明                                                        |
| ------- | --------------------------------------------- | ---- | ----------------------------------------------------------- |
| event | string | 是   | 需要设置的会话事件的名称 |
| args | {[key: string]: any} | 是   | 需要传递的会话事件键值对 |
| callback | AsyncCallback\<void>                          | 是   | 回调函数。当会话事件设置成功，err为undefined，否则返回错误对象。 |

> **说明：**
> 参数args支持的数据类型有：字符串、数字、布尔、对象、数组和文件描述符等，详细介绍请参见[@ohos.app.ability.Want(Want)](./js-apis-app-ability-want.md)。

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |
| 6600102  | The session does not exist. |

**示例：**

```js
let eventName = "dynamic_lyric";
let args = {
    lyric : "This is lyric"
}
await session.dispatchSessionEvent(eventName, args, (err) => {
    if(err) {
        console.info(`dispatchSessionEvent BusinessError: code: ${err.code}, message: ${err.message}`);
    }
})
```

### setExtras<sup>10+</sup>

setExtras(extras: {[key: string]: Object}): Promise\<void>

媒体提供方设置键值对形式的自定义媒体数据包, 结果通过Promise异步回调方式返回。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**参数：**

| 参数名  | 类型                                          | 必填 | 说明                                                        |
| ------- | --------------------------------------------- | ---- | ----------------------------------------------------------- |
| extras | {[key: string]: Object} | 是   | 需要传递的自定义媒体数据包键值对 |

> **说明：**
> 参数extras支持的数据类型有：字符串、数字、布尔、对象、数组和文件描述符等，详细介绍请参见[@ohos.app.ability.Want(Want)](./js-apis-app-ability-want.md)。

**返回值：**

| 类型           | 说明                          |
| -------------- | ----------------------------- |
| Promise\<void> | Promise对象。当自定义媒体数据包设置成功，无返回结果，否则返回错误对象。 |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |
| 6600102  | The session does not exist. |

**示例：**

```js
let extras = {
    extras : "This is custom media packet"
}
await session.setExtras(extras).catch((err) => {
    console.info(`setExtras BusinessError: code: ${err.code}, message: ${err.message}`);
})
```

### setExtras<sup>10+</sup>

setExtras(extras: {[key: string]: Object}, callback: AsyncCallback\<void>): void

媒体提供方设置键值对形式的自定义媒体数据包, 结果通过callback异步回调方式返回。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**参数：**

| 参数名  | 类型                                          | 必填 | 说明                                                        |
| ------- | --------------------------------------------- | ---- | ----------------------------------------------------------- |
| extras | {[key: string]: any} | 是   | 需要传递的自定义媒体数据包键值对 |
| callback | AsyncCallback\<void>                          | 是   | 回调函数。当自定义媒体数据包设置成功，err为undefined，否则返回错误对象。 |

> **说明：**
> 参数extras支持的数据类型有：字符串、数字、布尔、对象、数组和文件描述符等，详细介绍请参见[@ohos.app.ability.Want(Want)](./js-apis-app-ability-want.md)。

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |
| 6600102  | The session does not exist. |

**示例：**

```js
let extras = {
    extras : "This is custom media packet"
}
await session.setExtras(extras, (err) => {
    if(err) {
        console.info(`setExtras BusinessError: code: ${err.code}, message: ${err.message}`);
    }
})
```

### getController<sup>10+</sup>

getController(): Promise\<AVSessionController>

获取本会话对应的控制器。结果通过Promise异步回调方式返回。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**返回值：**

| 类型                                                 | 说明                          |
| ---------------------------------------------------- | ----------------------------- |
| Promise<[AVSessionController](#avsessioncontroller10)> | Promise对象。返回会话控制器。 |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |
| 6600102  | The session does not exist. |

**示例：**

```js
let controller;
session.getController().then((avcontroller) => {
    controller = avcontroller;
    console.info(`GetController : SUCCESS : sessionid : ${controller.sessionId}`);
}).catch((err) => {
    console.info(`GetController BusinessError: code: ${err.code}, message: ${err.message}`);
});
```

### getController<sup>10+</sup>

getController(callback: AsyncCallback\<AVSessionController>): void

获取本会话相应的控制器。结果通过callback异步回调方式返回。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**参数：**

| 参数名   | 类型                                                        | 必填 | 说明                       |
| -------- | ----------------------------------------------------------- | ---- | -------------------------- |
| callback | AsyncCallback<[AVSessionController](#avsessioncontroller10)\> | 是   | 回调函数。返回会话控制器。 |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |
| 6600102  | The session does not exist. |

**示例：**

```js
let controller;
session.getController(function (err, avcontroller) {
    if (err) {
        console.info(`GetController BusinessError: code: ${err.code}, message: ${err.message}`);
    } else {
        controller = avcontroller;
        console.info(`GetController : SUCCESS : sessionid : ${controller.sessionId}`);
    }
});
```

### getAVCastController<sup>10+</sup>

getAVCastController(callback: AsyncCallback\<AVCastController>): void

设备建立连接后，获取投播控制器。结果通过callback异步回调方式返回。

**系统能力：** SystemCapability.Multimedia.AVSession.AVCast

**参数：**

| 参数名    | 类型                                                        | 必填 | 说明                                                         |
| --------- | ----------------------------------------------------------- | ---- | ------------------------------------------------------------ |
| callback  | AsyncCallback<[AVCastController](#avcastcontroller10)\> | 是   | 回调函数，返回投播控制器实例。 |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600102  | The session does not exist. |
| 6600110  | The remote connection is not established. |

**示例：**

```js
let controller;
session.getAVCastController().then((avcontroller) => {
    controller = avcontroller;
    console.info(`getAVCastController : SUCCESS : sessionid : ${controller.sessionId}`);
}).catch((err) => {
    console.info(`getAVCastController BusinessError: code: ${err.code}, message: ${err.message}`);
});
```

### getAVCastController<sup>10+</sup>

getAVCastController(): Promise\<AVCastController>;

设备建立连接后，获取投播控制器。结果通过callback异步回调方式返回。

**系统能力：** SystemCapability.Multimedia.AVSession.AVCast

**返回值：**

| 类型                                                        | 说明                                                         |
| --------- | ------------------------------------------------------------ |
| Promise<[AVCastController](#avcastcontroller10)\>  | Promise对象。返回投播控制器实例。 |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600102  | The session does not exist. |
| 6600110  | The remote connection is not established. |

**示例：**

```js
let controller;
session.getAVCastController(function (err, avcontroller) {
    if (err) {
        console.info(`getAVCastController BusinessError: code: ${err.code}, message: ${err.message}`);
    } else {
        controller = avcontroller;
        console.info(`getAVCastController : SUCCESS : sessionid : ${controller.sessionId}`);
    }
});
```

### stopCasting<sup>10+</sup>

stopCasting(callback: AsyncCallback\<void>): void

停止投播。

**系统能力：** SystemCapability.Multimedia.AVSession.AVCast

**参数：**

| 参数名 | 类型                      | 必填 | 说明         |
| ------ | ------------------------- | ---- | ------------ |
| callback   | AsyncCallback\<void\> | 是   | 回调函数。 |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600109  | The remote connection is not established. |

**示例：**

```js
session.stopCasting(function (err) {
    if (err) {
        console.info(`GetController BusinessError: code: ${err.code}, message: ${err.message}`);
    } else {
        controller = avcontroller;
        console.info(`GetController : SUCCESS : sessionid : ${controller.sessionId}`);
    }
});
```

### stopCasting<sup>10+</sup>

stopCasting(): Promise\<void>;

停止投播。

**系统能力：** SystemCapability.Multimedia.AVSession.AVCast

**返回值：**

| 类型           | 说明                          |
| -------------- | ----------------------------- |
| Promise\<void> | Promise对象。当停止投播成功，无返回结果，否则返回错误对象。 |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600109  | The remote connection is not established. |

**示例：**

```js
session.stopCasting().then(() => {
    console.info(`stopCasting successfully`);
}).catch((err) => {
    console.info(`stopCasting BusinessError: code: ${err.code}, message: ${err.message}`);
});
```


### getOutputDevice<sup>10+</sup>

getOutputDevice(): Promise\<OutputDeviceInfo>

通过会话获取播放设备信息。结果通过Promise异步回调方式返回。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**返回值：**

| 类型                                           | 说明                              |
| ---------------------------------------------- | --------------------------------- |
| Promise<[OutputDeviceInfo](#outputdeviceinfo10)> | Promise对象。返回播放设备信息。 |

**错误码：**

以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |
| 6600102  | The session does not exist. |

**示例：**

```js
session.getOutputDevice().then((outputDeviceInfo) => {
    console.info(`GetOutputDevice : SUCCESS : isRemote : ${outputDeviceInfo.isRemote}`);
}).catch((err) => {
    console.info(`GetOutputDevice BusinessError: code: ${err.code}, message: ${err.message}`);
});
```

### getOutputDevice<sup>10+</sup>

getOutputDevice(callback: AsyncCallback\<OutputDeviceInfo>): void

通过会话获取播放设备相关信息。结果通过callback异步回调方式返回。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**参数：**

| 参数名   | 类型                                                  | 必填 | 说明                           |
| -------- | ----------------------------------------------------- | ---- | ------------------------------ |
| callback | AsyncCallback<[OutputDeviceInfo](#outputdeviceinfo10)\> | 是   | 回调函数，返回播放设备信息。 |

**错误码：**

以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |
| 6600102  | The session does not exist. |

**示例：**

```js
session.getOutputDevice(function (err, outputDeviceInfo) {
    if (err) {
        console.info(`GetOutputDevice BusinessError: code: ${err.code}, message: ${err.message}`);
    } else {
        console.info(`GetOutputDevice : SUCCESS : isRemote : ${outputDeviceInfo.isRemote}`);
    }
});
```

### activate<sup>10+</sup>

activate(): Promise\<void>

激活会话，激活后可正常使用会话。结果通过Promise异步回调方式返回。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**返回值：**

| 类型           | 说明                          |
| -------------- | ----------------------------- |
| Promise\<void> | Promise对象。当会话激活成功，无返回结果，否则返回错误对象。 |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |
| 6600102  | The session does not exist. |

**示例：**

```js
session.activate().then(() => {
    console.info(`Activate : SUCCESS `);
}).catch((err) => {
    console.info(`Activate BusinessError: code: ${err.code}, message: ${err.message}`);
});
```

### activate<sup>10+</sup>

activate(callback: AsyncCallback\<void>): void

激活会话，激活后可正常使用会话。结果通过callback异步回调方式返回。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**参数：**

| 参数名   | 类型                 | 必填 | 说明       |
| -------- | -------------------- | ---- | ---------- |
| callback | AsyncCallback\<void> | 是   | 回调函数。当会话激活成功，err为undefined，否则返回错误对象。 |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |
| 6600102  | The session does not exist. |

**示例：**

```js
session.activate(function (err) {
    if (err) {
        console.info(`Activate BusinessError: code: ${err.code}, message: ${err.message}`);
    } else {
        console.info(`Activate : SUCCESS `);
    }
});
```

### deactivate<sup>10+</sup>

deactivate(): Promise\<void>

禁用当前会话的功能，可通过[activate](#activate10)恢复。结果通过Promise异步回调方式返回。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**返回值：**

| 类型           | 说明                          |
| -------------- | ----------------------------- |
| Promise\<void> | Promise对象。当禁用会话成功，无返回结果，否则返回错误对象。|

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |
| 6600102  | The session does not exist. |

**示例：**

```js
session.deactivate().then(() => {
    console.info(`Deactivate : SUCCESS `);
}).catch((err) => {
    console.info(`Deactivate BusinessError: code: ${err.code}, message: ${err.message}`);
});
```

### deactivate<sup>10+</sup>

deactivate(callback: AsyncCallback\<void>): void

禁用当前会话。结果通过callback异步回调方式返回。

禁用当前会话的功能，可通过[activate](#activate10)恢复。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**参数：**

| 参数名   | 类型                 | 必填 | 说明       |
| -------- | -------------------- | ---- | ---------- |
| callback | AsyncCallback\<void> | 是   | 回调函数。当禁用会话成功，err为undefined，否则返回错误对象。|

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |
| 6600102  | The session does not exist. |

**示例：**

```js
session.deactivate(function (err) {
    if (err) {
        console.info(`Deactivate BusinessError: code: ${err.code}, message: ${err.message}`);
    } else {
        console.info(`Deactivate : SUCCESS `);
    }
});
```

### destroy<sup>10+</sup>

destroy(): Promise\<void>

销毁当前会话，使当前会话完全失效。结果通过Promise异步回调方式返回。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**返回值：**

| 类型           | 说明                          |
| -------------- | ----------------------------- |
| Promise\<void> | Promise对象。当会话销毁成功，无返回结果，否则返回错误对象。 |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |
| 6600102  | The session does not exist. |

**示例：**

```js
session.destroy().then(() => {
    console.info(`Destroy : SUCCESS `);
}).catch((err) => {
    console.info(`Destroy BusinessError: code: ${err.code}, message: ${err.message}`);
});
```

### destroy<sup>10+</sup>

destroy(callback: AsyncCallback\<void>): void

销毁当前会话，使当前会话完全失效。结果通过callback异步回调方式返回。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**参数：**

| 参数名   | 类型                 | 必填 | 说明       |
| -------- | -------------------- | ---- | ---------- |
| callback | AsyncCallback\<void> | 是   | 回调函数。当会话销毁成功，err为undefined，否则返回错误对象。 |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |
| 6600102  | The session does not exist. |

**示例：**

```js
session.destroy(function (err) {
    if (err) {
        console.info(`Destroy BusinessError: code: ${err.code}, message: ${err.message}`);
    } else {
        console.info(`Destroy : SUCCESS `);
    }
});
```

### on('play')<sup>10+</sup>

on(type: 'play', callback: () => void): void

设置播放命令监听事件。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**参数：**

| 参数名   | 类型                 | 必填 | 说明                                                         |
| -------- | -------------------- | ---- | ------------------------------------------------------------ |
| type     | string               | 是   | 事件回调类型，支持的事件为`'play'`当播放命令被发送到会话时，触发该事件回调。 |
| callback | callback: () => void | 是   | 回调函数。当监听事件注册成功，err为undefined，否则为错误对象。                                        |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |
| 6600102  | The session does not exist. |

**示例：**

```js
session.on('play', () => {
    console.info(`on play entry`);
});
```

### on('pause')<sup>10+</sup>

on(type: 'pause', callback: () => void): void

设置暂停命令监听事件。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**参数：**

| 参数名   | 类型                 | 必填 | 说明                                                         |
| -------- | -------------------- | ---- | ------------------------------------------------------------ |
| type     | string               | 是   | 事件回调类型，支持的事件为`'pause'`，当暂停命令被发送到会话时，触发该事件回调。 |
| callback | callback: () => void | 是   | 回调函数。当监听事件注册成功，err为undefined，否则为错误对象。     |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |
| 6600102  | The session does not exist. |

**示例：**

```js
session.on('pause', () => {
    console.info(`on pause entry`);
});
```

### on('stop')<sup>10+</sup>

on(type:'stop', callback: () => void): void

设置停止命令监听事件。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**参数：**

| 参数名   | 类型                 | 必填 | 说明                                                         |
| -------- | -------------------- | ---- | ------------------------------------------------------------ |
| type     | string               | 是   | 事件回调类型，支持的事件是`'stop'`，当停止命令被发送到会话时，触发该事件回调。 |
| callback | callback: () => void | 是   | 回调函数。当监听事件注册成功，err为undefined，否则为错误对象。          |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |
| 6600102  | The session does not exist. |

**示例：**

```js
session.on('stop', () => {
    console.info(`on stop entry`);
});
```

### on('playNext')<sup>10+</sup>

on(type:'playNext', callback: () => void): void

设置播放下一首命令监听事件。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**参数：**

| 参数名   | 类型                 | 必填 | 说明                                                         |
| -------- | -------------------- | ---- | ------------------------------------------------------------ |
| type     | string               | 是   | 事件回调类型，支持的事件是` 'playNext'`，当播放下一首命令被发送到会话时，触发该事件回调。 |
| callback | callback: () => void | 是   | 回调函数。当监听事件注册成功，err为undefined，否则为错误对象。     |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |
| 6600102  | The session does not exist. |

**示例：**

```js
session.on('playNext', () => {
    console.info(`on playNext entry`);
});
```

### on('playPrevious')<sup>10+</sup>

on(type:'playPrevious', callback: () => void): void

设置播放上一首命令监听事件。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**参数：**

| 参数名   | 类型                 | 必填 | 说明                                                         |
| -------- | -------------------- | ---- | ------------------------------------------------------------ |
| type     | string               | 是   | 事件回调类型，支持的事件是` 'playPrevious'`当播放上一首命令被发送到会话时，触发该事件回调。 |
| callback | callback: () => void | 是   | 回调函数。当监听事件注册成功，err为undefined，否则为错误对象。       |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |
| 6600102  | The session does not exist. |

**示例：**

```js
session.on('playPrevious', () => {
    console.info(`on playPrevious entry`);
});
```

### on('fastForward')<sup>10+</sup>

on(type: 'fastForward', callback: () => void): void

设置快进命令监听事件。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**参数：**

| 参数名   | 类型                 | 必填 | 说明                                                         |
| -------- | -------------------- | ---- | ------------------------------------------------------------ |
| type     | string               | 是   | 事件回调类型，支持的事件是 `'fastForward'`，当快进命令被发送到会话时，触发该事件回调。 |
| callback | callback: () => void | 是   | 回调函数。当监听事件注册成功，err为undefined，否则为错误对象。    |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |
| 6600102  | The session does not exist. |

**示例：**

```js
session.on('fastForward', () => {
    console.info(`on fastForward entry`);
});
```

### on('rewind')<sup>10+</sup>

on(type:'rewind', callback: () => void): void

设置快退命令监听事件。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**参数：**

| 参数名   | 类型                 | 必填 | 说明                                                         |
| -------- | -------------------- | ---- | ------------------------------------------------------------ |
| type     | string               | 是   | 事件回调类型，支持的事件是` 'rewind'`，当快退命令被发送到会话时，触发该事件回调。 |
| callback | callback: () => void | 是   | 回调函数。当监听事件注册成功，err为undefined，否则为错误对象。      |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |
| 6600102  | The session does not exist. |

**示例：**

```js
session.on('rewind', () => {
    console.info(`on rewind entry`);
});
```

### on('seek')<sup>10+</sup>

on(type: 'seek', callback: (time: number) => void): void

设置跳转节点监听事件。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**参数：**

| 参数名   | 类型                   | 必填 | 说明                                                         |
| -------- | ---------------------- | ---- | ------------------------------------------------------------ |
| type     | string                 | 是   | 事件回调类型，支持事件`'seek'`：当跳转节点命令被发送到会话时，触发该事件。 |
| callback | (time: number) => void | 是   | 回调函数。参数time是时间节点，单位为毫秒。                   |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |
| 6600102  | The session does not exist. |

**示例：**
The session does not exist
```js
session.on('seek', (time) => {
    console.info(`on seek entry time : ${time}`);
});
```

### on('setSpeed')<sup>10+</sup>

on(type: 'setSpeed', callback: (speed: number) => void): void

设置播放速率的监听事件。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**参数：**

| 参数名   | 类型                    | 必填 | 说明                                                         |
| -------- | ----------------------- | ---- | ------------------------------------------------------------ |
| type     | string                  | 是   | 事件回调类型，支持事件`'setSpeed'`：当设置播放速率的命令被发送到会话时，触发该事件。 |
| callback | (speed: number) => void | 是   | 回调函数。参数speed是播放倍速。                              |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |
| 6600102  | The session does not exist. |

**示例：**

```js
session.on('setSpeed', (speed) => {
    console.info(`on setSpeed speed : ${speed}`);
});
```

### on('setLoopMode')<sup>10+</sup>

on(type: 'setLoopMode', callback: (mode: LoopMode) => void): void

设置循环模式的监听事件。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**参数：**

| 参数名    | 类型                                   | 必填 | 说明  |
| -------- | ------------------------------------- | ---- | ---- |
| type     | string                                | 是   | 事件回调类型，支持事件`'setLoopMode'`：当设置循环模式的命令被发送到会话时，触发该事件。 |
| callback | (mode: [LoopMode](#loopmode10)) => void | 是   | 回调函数。参数mode是循环模式。                               |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |
| 6600102  | The session does not exist. |

**示例：**

```js
session.on('setLoopMode', (mode) => {
    console.info(`on setLoopMode mode : ${mode}`);
});
```

### on('toggleFavorite')<sup>10+</sup>

on(type: 'toggleFavorite', callback: (assetId: string) => void): void

设置是否收藏的监听事件

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**参数：**

| 参数名   | 类型                      | 必填 | 说明                                                         |
| -------- | ------------------------- | ---- | ------------------------------------------------------------ |
| type     | string                    | 是   | 事件回调类型，支持事件`'toggleFavorite'`：当是否收藏的命令被发送到会话时，触发该事件。 |
| callback | (assetId: string) => void | 是   | 回调函数。参数assetId是媒体ID。                              |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |
| 6600102  | The session does not exist. |

**示例：**

```js
session.on('toggleFavorite', (assetId) => {
    console.info(`on toggleFavorite mode : ${assetId}`);
});
```

### on('skipToQueueItem')<sup>10+</sup>

on(type: 'skipToQueueItem', callback: (itemId: number) => void): void

设置播放列表其中某项被选中的监听事件，session端可以选择对这个单项歌曲进行播放。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**参数：**

| 参数名   | 类型                      | 必填 | 说明                                                                                      |
| -------- | ------------------------ | ---- | ---------------------------------------------------------------------------------------- |
| type     | string                   | 是   | 事件回调类型，支持事件`'skipToQueueItem'`：当播放列表选中单项的命令被发送到会话时，触发该事件。 |
| callback | (itemId: number) => void | 是   | 回调函数。参数itemId是选中的播放列表项的ID。                                                |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |
| 6600102  | The session does not exist. |

**示例：**

```js
session.on('skipToQueueItem', (itemId) => {
    console.info(`on skipToQueueItem id : ${itemId}`);
});
```

### on('handleKeyEvent')<sup>10+</sup>

on(type: 'handleKeyEvent', callback: (event: KeyEvent) => void): void

设置按键事件的监听

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**参数：**

| 参数名   | 类型                                                         | 必填 | 说明                                                         |
| -------- | ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| type     | string                                                       | 是   | 事件回调类型，支持事件`'handleKeyEvent'`：当按键事件被发送到会话时，触发该事件。 |
| callback | (event: [KeyEvent](js-apis-keyevent.md)) => void | 是   | 回调函数。参数event是按键事件。                              |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |
| 6600102  | The session does not exist. |

**示例：**

```js
session.on('handleKeyEvent', (event) => {
    console.info(`on handleKeyEvent event : ${event}`);
});
```

### on('outputDeviceChange')<sup>10+</sup>

on(type: 'outputDeviceChange', callback: (state: ConnectionState, device: OutputDeviceInfo) => void): void

设置播放设备变化的监听事件。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**参数：**

| 参数名   | 类型                                                    | 必填 | 说明                                                         |
| -------- | ------------------------------------------------------- | ---- | ------------------------------------------------------------ |
| type     | string                                                  | 是   | 事件回调类型，支持事件`'outputDeviceChange'`：当播放设备变化时，触发该事件。 |
| callback | (state: [ConnectionState](#connectionstate10), device: [OutputDeviceInfo](#outputdeviceinfo10)) => void | 是   | 回调函数，参数device是设备相关信息。<br>该参数为可选参数，若不填写该参数，则认为取消所有相关会话的事件监听。                         |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |
| 6600102  | The session does not exist. |

**示例：**

```js
session.on('outputDeviceChange', (state, device) => {
    console.info(`on outputDeviceChange device : ${device}`);
});
```

### on('commonCommand')<sup>10+</sup>

on(type: 'commonCommand', callback: (command: string, args: {[key: string]: Object}) => void): void

设置自定义控制命令变化的监听器。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**参数：**

| 参数名   | 类型                                                         | 必填 | 说明                                                         |
| -------- | ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| type     | string                                                       | 是   | 事件回调类型，支持事件`'commonCommand'`：当自定义控制命令变化时，触发该事件。 |
| callback | (commonCommand: string, args: {[key:string]: Object}) => void         | 是   | 回调函数，commonCommand为变化的自定义控制命令名，args为自定义控制命令的参数，参数内容与sendCommand方法设置的参数内容完全一致。          |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ------------------------------ |
| 6600101  | Session service exception. |
| 6600102  | The session does not exist. |

**示例：**

```js
session.on('commonCommand', (commonCommand, args) => {
    console.info(`OnCommonCommand, the command is ${commonCommand}, args: ${JSON.stringify(args)}`);
});
```

### off('play')<sup>10+</sup>

off(type: 'play', callback?: () => void): void

取消会话播放事件监听，关闭后，不再进行该事件回调。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**参数：**

| 参数名    | 类型                  | 必填 | 说明                                                                                                                         |
| -------- | -------------------- | ---- | ---------------------------------------------------------------------------------------------------------------------------- |
| type     | string               | 是   | 关闭对应的监听事件，支持的事件是`'play'`|
| callback | callback: () => void | 否   | 回调函数。当监听事件取消成功，err为undefined，否则返回错误对象。<br>该参数为可选参数，若不填写该参数，则认为取消所有相关会话的事件监听。                            |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |
| 6600102  | The session does not exist. |

**示例：**

```js
session.off('play');
```

### off('pause')<sup>10+</sup>

off(type: 'pause', callback?: () => void): void

取消会话暂停事件监听，关闭后，不再进行该事件回调。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**参数：**

| 参数名    | 类型                  | 必填 | 说明                                                                                                                         |
| -------- | -------------------- | ---- | ---------------------------------------------------------------------------------------------------------------------------- |
| type     | string               | 是   | 关闭对应的监听事件，支持的事件是` 'pause'`。 |
| callback | callback: () => void | 否   | 回调函数。当监听事件取消成功，err为undefined，否则返回错误对象。<br>该参数为可选参数，若不填写该参数，则认为取消所有相关会话的事件监听。 |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |
| 6600102  | The session does not exist. |

**示例：**

```js
session.off('pause');
```

### off('stop')<sup>10+</sup>

off(type: 'stop', callback?: () => void): void

取消会话停止事件监听，关闭后，不再进行该事件回调。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**参数：**

| 参数名    | 类型                  | 必填 | 说明                                                                                                                         |
| -------- | -------------------- | ---- | ---------------------------------------------------------------------------------------------------------------------------- |
| type     | string               | 是   | 关闭对应的监听事件，支持的事件是`'stop'`。 |
| callback | callback: () => void | 否   | 回调函数。当监听事件取消成功，err为undefined，否则返回错误对象。<br>该参数为可选参数，若不填写该参数，则认为取消所有相关会话的事件监听。                            |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |
| 6600102  | The session does not exist. |

**示例：**

```js
session.off('stop');
```

### off('playNext')<sup>10+</sup>

off(type: 'playNext', callback?: () => void): void

取消会话播放下一首事件监听，关闭后，不再进行该事件回调。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**参数：**

| 参数名    | 类型                  | 必填 | 说明                                                                                                                         |
| -------- | -------------------- | ---- | ---------------------------------------------------------------------------------------------------------------------------- |
| type     | string               | 是   | 关闭对应的监听事件，支持的事件是 `'playNext'`。 |
| callback | callback: () => void | 否   | 回调函数。当监听事件取消成功，err为undefined，否则返回错误对象。<br>该参数为可选参数，若不填写该参数，则认为取消所有相关会话的事件监听。                            |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |
| 6600102  | The session does not exist. |

**示例：**

```js
session.off('playNext');
```

### off('playPrevious')<sup>10+</sup>

off(type: 'playPrevious', callback?: () => void): void

取消会话播放上一首事件监听，关闭后，不再进行该事件回调。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**参数：**

| 参数名    | 类型                  | 必填 | 说明                                                                                                                         |
| -------- | -------------------- | ---- | ---------------------------------------------------------------------------------------------------------------------------- |
| type     | string               | 是   | 关闭对应的监听事件，支持的事件是` 'playPrevious'`。 |
| callback | callback: () => void | 否   | 回调函数。当监听事件取消成功，err为undefined，否则返回错误对象。<br>该参数为可选参数，若不填写该参数，则认为取消所有相关会话的事件监听。                            |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |
| 6600102  | The session does not exist. |

**示例：**

```js
session.off('playPrevious');
```

### off('fastForward')<sup>10+</sup>

off(type: 'fastForward', callback?: () => void): void

取消会话快进事件监听，关闭后，不再进行该事件回调。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**参数：**

| 参数名    | 类型                  | 必填 | 说明                                                                                                                         |
| -------- | -------------------- | ---- | ---------------------------------------------------------------------------------------------------------------------------- |
| type     | string               | 是   | 关闭对应的监听事件，支持的事件是` 'fastForward'`。 |
| callback | callback: () => void | 否   | 回调函数。当监听事件取消成功，err为undefined，否则返回错误对象。<br>该参数为可选参数，若不填写该参数，则认为取消所有相关会话的事件监听。                            |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |
| 6600102  | The session does not exist. |

**示例：**

```js
session.off('fastForward');
```

### off('rewind')<sup>10+</sup>

off(type: 'rewind', callback?: () => void): void

取消会话快退事件监听，关闭后，不再进行该事件回调。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**参数：**

| 参数名    | 类型                  | 必填 | 说明                                                                                                                         |
| -------- | -------------------- | ---- | ---------------------------------------------------------------------------------------------------------------------------- |
| type     | string               | 是   | 关闭对应的监听事件，支持的事件是` 'rewind'`。 |
| callback | callback: () => void | 否   | 回调函数。当监听事件取消成功，err为undefined，否则返回错误对象。<br>该参数为可选参数，若不填写该参数，则认为取消所有相关会话的事件监听。                            |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |
| 6600102  | The session does not exist. |

**示例：**

```js
session.off('rewind');
```

### off('seek')<sup>10+</sup>

off(type: 'seek', callback?: (time: number) => void): void

取消监听跳转节点事件。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**参数：**

| 参数名   | 类型                   | 必填 | 说明                                          |
| -------- | ---------------------- | ---- | ----------------------------------------- |
| type     | string                 | 是   | 关闭对应的监听事件，支持关闭事件`'seek'`。       |
| callback | (time: number) => void | 否   | 回调函数，参数time是时间节点，单位为毫秒。<br>当监听事件取消成功，err为undefined，否则返回错误对象。<br>该参数为可选参数，若不填写该参数，则认为取消所有相关会话的事件监听。        |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |
| 6600102  | The session does not exist. |

**示例：**

```js
session.off('seek');
```

### off('setSpeed')<sup>10+</sup>

off(type: 'setSpeed', callback?: (speed: number) => void): void

取消监听播放速率变化事件。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**参数：**

| 参数名   | 类型                    | 必填 | 说明                                           |
| -------- | ----------------------- | ---- | -------------------------------------------|
| type     | string                  | 是   | 关闭对应的监听事件，支持关闭事件`'setSpeed'`。    |
| callback | (speed: number) => void | 否   | 回调函数，参数speed是播放倍速。<br>当监听事件取消成功，err为undefined，否则返回错误对象。<br>该参数为可选参数，若不填写该参数，则认为取消所有相关会话的事件监听。                 |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |
| 6600102  | The session does not exist. |

**示例：**

```js
session.off('setSpeed');
```

### off('setLoopMode')<sup>10+</sup>

off(type: 'setLoopMode', callback?: (mode: LoopMode) => void): void

取消监听循环模式变化事件。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**参数：**

| 参数名   | 类型                                  | 必填 | 说明     |
| -------- | ------------------------------------- | ---- | ----- |
| type     | string | 是   | 关闭对应的监听事件，支持关闭事件`'setLoopMode'`。|
| callback | (mode: [LoopMode](#loopmode10)) => void | 否   | 回调函数，参数mode是循环模式。<br>当监听事件取消成功，err为undefined，否则返回错误对象。<br>该参数为可选参数，若不填写该参数，则认为取消所有相关会话的事件监听。 |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |
| 6600102  | The session does not exist. |

**示例：**

```js
session.off('setLoopMode');
```

### off('toggleFavorite')<sup>10+</sup>

off(type: 'toggleFavorite', callback?: (assetId: string) => void): void

取消监听是否收藏的事件

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**参数：**

| 参数名   | 类型                      | 必填 | 说明                                                         |
| -------- | ------------------------- | ---- | -------------------------------------------------------- |
| type     | string                    | 是   | 关闭对应的监听事件，支持关闭事件`'toggleFavorite'`。            |
| callback | (assetId: string) => void | 否   | 回调函数，参数assetId是媒体ID。<br>当监听事件取消成功，err为undefined，否则返回错误对象。<br>该参数为可选参数，若不填写该参数，则认为取消所有相关会话的事件监听。                               |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |
| 6600102  | The session does not exist. |

**示例：**

```js
session.off('toggleFavorite');
```

### off('skipToQueueItem')<sup>10+</sup>

off(type: 'skipToQueueItem', callback?: (itemId: number) => void): void

取消监听播放列表单项选中的事件

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**参数：**

| 参数名   | 类型                      | 必填 | 说明                                                                                                                                                        |
| -------- | ------------------------ | ---- | ----------------------------------------------------------------------------------------------------------------------------------------------------------- |
| type     | string                   | 是   | 关闭对应的监听事件，支持关闭事件`'skipToQueueItem'`。                                                                                                          |
| callback | (itemId: number) => void | 否   | 回调函数，参数itemId是播放列表单项ID。<br>当监听事件取消成功，err为undefined，否则返回错误对象。<br>该参数为可选参数，若不填写该参数，则认为取消所有相关会话的事件监听。 |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |
| 6600102  | The session does not exist. |

**示例：**

```js
session.off('skipToQueueItem');
```

### off('handleKeyEvent')<sup>10+</sup>

off(type: 'handleKeyEvent', callback?: (event: KeyEvent) => void): void

取消监听按键事件。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**参数：**

| 参数名   | 类型                                                         | 必填 | 说明                                                         |
| -------- | ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| type     | string                                                       | 是   | 关闭对应的监听事件，支持关闭事件`'handleKeyEvent'`。             |
| callback | (event: [KeyEvent](js-apis-keyevent.md)) => void | 否   | 回调函数，参数event是按键事件。<br>当监听事件取消成功，err为undefined，否则返回错误对象。<br>该参数为可选参数，若不填写该参数，则认为取消所有相关会话的事件监听。                              |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |
| 6600102  | The session does not exist. |

**示例：**

```js
session.off('handleKeyEvent');
```

### off('outputDeviceChange')<sup>10+</sup>

off(type: 'outputDeviceChange', callback?: (state: ConnectionState, device: OutputDeviceInfo) => void): void

取消监听播放设备变化的事件。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**参数：**

| 参数名   | 类型                                                    | 必填 | 说明                                                      |
| -------- | ------------------------------------------------------- | ---- | ------------------------------------------------------ |
| type     | string                                                  | 是   | 关闭对应的监听事件，支持关闭事件`'outputDeviceChange'`。     |
| callback | (state: [ConnectionState](#connectionstate10), device: [OutputDeviceInfo](#outputdeviceinfo10)) => void | 否   | 回调函数，参数device是设备相关信息。<br>当监听事件取消成功，err为undefined，否则返回错误对象。<br>该参数为可选参数，若不填写该参数，则认为取消所有相关会话的事件监听。                        |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |
| 6600102  | The session does not exist. |

**示例：**

```js
session.off('outputDeviceChange');
```


### off('commonCommand')<sup>10+</sup>

off(type: 'commonCommand', callback?: (command: string, args: {[key:string]: Object}) => void): void

取消监听自定义控制命令的变化。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**参数：**

| 参数名   | 类型                                                         | 必填 | 说明                                                     |
| -------- | ------------------------------------------------------------ | ---- | ----------------------------------------------------- |
| type     | string                                                       | 是   | 取消对应的监听事件，支持事件`'commonCommand'`。    |
| callback | (command: string, args: {[key:string]: Object}) => void         | 否   | 回调函数，参数command是变化的自定义控制命令名，args为自定义控制命令的参数。<br>该参数为可选参数，若不填写该参数，则认为取消所有对command事件的监听。                      |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------- |
| 6600101  | Session service exception. |
| 6600102  | The session does not exist. |

**示例：**

```js
session.off('commonCommand');
```



## AVSessionController<sup>10+</sup>

调用[avSession.createController](#avsessioncreatecontroller)后，返回会话控制器实例。控制器可查看会话ID，并可完成对会话发送命令及事件，获取会话元数据，播放状态信息等操作。

### 属性

**系统能力：** SystemCapability.Multimedia.AVSession.Core

| 名称      | 类型   | 可读 | 可写 | 说明                                    |
| :-------- | :----- | :--- | :--- | :-------------------------------------- |
| sessionId | string | 是   | 否   | AVSessionController对象唯一的会话标识。 |


**示例：**
```js
let sessionId;
await avSession.createController(session.sessionId).then((controller) => {
    sessionId = controller.sessionId;
}).catch((err) => {
    console.info(`CreateController BusinessError: code: ${err.code}, message: ${err.message}`);
});
```

### getAVQueueItems<sup>10+</sup>

getAVQueueItems(): Promise\<Array\<AVQueueItem>>

获取当前会话播放列表相关信息。结果通过Promise异步回调方式返回。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**返回值：**

| 类型                                          | 说明                           |
| --------------------------------------------- | ----------------------------- |
| Promise<Array<[AVQueueItem](#avqueueitem10)\>\> | Promise对象。返回播放列表队列。 |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |
| 6600102  | The session does not exist. |
| 6600103  | The session controller does not exist. |

**示例：**
```js
controller.getAVQueueItems().then((items) => {
    console.info(`GetAVQueueItems : SUCCESS : length : ${items.length}`);
}).catch((err) => {
    console.info(`GetAVQueueItems BusinessError: code: ${err.code}, message: ${err.message}`);
});
```

### getAVQueueItems<sup>10+</sup>

getAVQueueItems(callback: AsyncCallback\<Array\<AVQueueItem>>): void

获取当前播放列表相关信息。结果通过callback异步回调方式返回。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**参数：**

| 参数名   | 类型                                                 | 必填 | 说明                      |
| -------- | --------------------------------------------------- | ---- | ------------------------- |
| callback | AsyncCallback<Array<[AVQueueItem](#avqueueitem10)\>\> | 是   | 回调函数，返回播放列表队列。 |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |
| 6600102  | The session does not exist. |
| 6600103  | The session controller does not exist. |

**示例：**
```js
controller.getAVQueueItems(function (err, items) {
    if (err) {
        console.info(`GetAVQueueItems BusinessError: code: ${err.code}, message: ${err.message}`);
    } else {
        console.info(`GetAVQueueItems : SUCCESS : length : ${items.length}`);
    }
});
```

### getAVQueueTitle<sup>10+</sup>

getAVQueueTitle(): Promise\<string>

获取当前会话播放列表的名称。结果通过Promise异步回调方式返回。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**返回值：**

| 类型             | 说明                           |
| ---------------- | ----------------------------- |
| Promise<string\> | Promise对象。返回播放列表名称。 |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |
| 6600102  | The session does not exist. |
| 6600103  | The session controller does not exist. |

**示例：**
```js
controller.getAVQueueTitle().then((title) => {
    console.info(`GetAVQueueTitle : SUCCESS : title : ${title}`);
}).catch((err) => {
    console.info(`GetAVQueueTitle BusinessError: code: ${err.code}, message: ${err.message}`);
});
```

### getAVQueueTitle<sup>10+</sup>

getAVQueueTitle(callback: AsyncCallback\<string>): void

获取当前播放列表的名称。结果通过callback异步回调方式返回。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**参数：**

| 参数名   | 类型                    | 必填 | 说明                      |
| -------- | ---------------------- | ---- | ------------------------- |
| callback | AsyncCallback<string\> | 是   | 回调函数，返回播放列表名称。 |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |
| 6600102  | The session does not exist. |
| 6600103  | The session controller does not exist. |

**示例：**
```js
controller.getAVQueueTitle(function (err, title) {
    if (err) {
        console.info(`GetAVQueueTitle BusinessError: code: ${err.code}, message: ${err.message}`);
    } else {
        console.info(`GetAVQueueTitle : SUCCESS : title : ${title}`);
    }
});
```

### skipToQueueItem<sup>10+</sup>

skipToQueueItem(itemId: number): Promise\<void>

设置指定播放列表单项的ID，发送给session端处理，session端可以选择对这个单项歌曲进行播放。结果通过Promise异步回调方式返回。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**参数：**

| 参数名  | 类型    | 必填 | 说明                                        |
| ------ | ------- | ---- | ------------------------------------------- |
| itemId | number  | 是   | 播放列表单项的ID值，用以表示选中的播放列表单项。 |

**返回值：**

| 类型           | 说明                                                             |
| -------------- | --------------------------------------------------------------- |
| Promise\<void> | Promise对象。当播放列表单项ID设置成功，无返回结果，否则返回错误对象。 |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |
| 6600102  | The session does not exist. |
| 6600103  | The session controller does not exist. |

**示例：**

```js
let queueItemId = 0;
controller.skipToQueueItem(queueItemId).then(() => {
    console.info(`SkipToQueueItem successfully`);
}).catch((err) => {
    console.info(`SkipToQueueItem BusinessError: code: ${err.code}, message: ${err.message}`);
});
```

### skipToQueueItem<sup>10+</sup>

skipToQueueItem(itemId: number, callback: AsyncCallback\<void>): void

设置指定播放列表单项的ID，发送给session端处理，session端可以选择对这个单项歌曲进行播放。结果通过callback异步回调方式返回。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**参数：**

| 参数名    | 类型                  | 必填 | 说明                                                        |
| -------- | --------------------- | ---- | ----------------------------------------------------------- |
| itemId   | number                | 是   | 播放列表单项的ID值，用以表示选中的播放列表单项。                |
| callback | AsyncCallback\<void>  | 是   | 回调函数。当播放状态设置成功，err为undefined，否则返回错误对象。 |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |
| 6600102  | The session does not exist. |
| 6600103  | The session controller does not exist. |

**示例：**

```js
let queueItemId = 0;
controller.skipToQueueItem(queueItemId, function (err) {
    if (err) {
        console.info(`SkipToQueueItem BusinessError: code: ${err.code}, message: ${err.message}`);
    } else {
        console.info(`SkipToQueueItem successfully`);
    }
});
```

### getAVMetadata<sup>10+</sup>

getAVMetadata(): Promise\<AVMetadata>

获取会话元数据。结果通过Promise异步回调方式返回。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**返回值：**

| 类型                                | 说明                          |
| ----------------------------------- | ----------------------------- |
| Promise<[AVMetadata](#avmetadata10)\> | Promise对象，返回会话元数据。 |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |
| 6600102  | The session does not exist. |
| 6600103  | The session controller does not exist. |

**示例：**
```js
controller.getAVMetadata().then((metadata) => {
    console.info(`GetAVMetadata : SUCCESS : assetId : ${metadata.assetId}`);
}).catch((err) => {
    console.info(`GetAVMetadata BusinessError: code: ${err.code}, message: ${err.message}`);
});
```

### getAVMetadata<sup>10+</sup>

getAVMetadata(callback: AsyncCallback\<AVMetadata>): void

获取会话元数据。结果通过callback异步回调方式返回。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**参数：**

| 参数名   | 类型                                      | 必填 | 说明                       |
| -------- | ----------------------------------------- | ---- | -------------------------- |
| callback | AsyncCallback<[AVMetadata](#avmetadata10)\> | 是   | 回调函数，返回会话元数据。 |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |
| 6600102  | The session does not exist. |
| 6600103  | The session controller does not exist. |

**示例：**
```js
controller.getAVMetadata(function (err, metadata) {
    if (err) {
        console.info(`GetAVMetadata BusinessError: code: ${err.code}, message: ${err.message}`);
    } else {
        console.info(`GetAVMetadata : SUCCESS : assetId : ${metadata.assetId}`);
    }
});
```

### getOutputDevice<sup>10+</sup>

getOutputDevice(): Promise\<OutputDeviceInfo>

获取播放设备信息。结果通过Promise异步回调方式返回。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**返回值：**

| 类型                                            | 说明                              |
| ----------------------------------------------- | --------------------------------- |
| Promise<[OutputDeviceInfo](#outputdeviceinfo10)\> | Promise对象，返回播放设备信息。 |

**错误码：**

以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 600101  | Session service exception. |
| 600103  | The session controller does not exist. |

**示例：**
```js
controller.getOutputDevice().then((deviceInfo) => {
    console.info(`GetOutputDevice : SUCCESS : isRemote : ${deviceInfo.isRemote}`);
}).catch((err) => {
    console.info(`GetOutputDevice BusinessError: code: ${err.code}, message: ${err.message}`);
});
```

### getOutputDevice<sup>10+</sup>

getOutputDevice(callback: AsyncCallback\<OutputDeviceInfo>): void

获取播放设备信息。结果通过callback异步回调方式返回。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**参数：**

| 参数名   | 类型                                                  | 必填 | 说明                           |
| -------- | ----------------------------------------------------- | ---- | ------------------------------ |
| callback | AsyncCallback<[OutputDeviceInfo](#outputdeviceinfo10)\> | 是   | 回调函数，返回播放设备信息。 |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 600101  | Session service exception. |
| 600103  | The session controller does not exist. |

**示例：**

```js
controller.getOutputDevice(function (err, deviceInfo) {
    if (err) {
        console.info(`GetOutputDevice BusinessError: code: ${err.code}, message: ${err.message}`);
    } else {
        console.info(`GetOutputDevice : SUCCESS : isRemote : ${deviceInfo.isRemote}`);
    }
});
```

### getExtras<sup>10+</sup>

getExtras(): Promise\<{[key: string]: Object}>

获取媒体提供方设置的自定义媒体数据包。结果通过Promise异步回调方式返回。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**返回值：**

| 类型                                | 说明                          |
| ----------------------------------- | ----------------------------- |
| Promise<{[key: string]: Object}\>   | Promise对象，返回媒体提供方设置的自定义媒体数据包，数据包的内容与setExtras设置的内容完全一致。 |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |
| 6600102  | The session does not exist. |
| 6600103  | The session controller does not exist. |
| 6600105  | Invalid session command. |
| 6600107  | Too many commands or events. |

**示例：**
```js
let extras = await controller.getExtras().catch((err) => {
    console.info(`getExtras BusinessError: code: ${err.code}, message: ${err.message}`);
});
```

### getExtras<sup>10+</sup>

getExtras(callback: AsyncCallback\<{[key: string]: Object}>): void

获取媒体提供方设置的自定义媒体数据包,结果通过callback异步回调方式返回。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**参数：**

| 参数名   | 类型                                      | 必填 | 说明                       |
| -------- | ----------------------------------------- | ---- | -------------------------- |
| callback | AsyncCallback<{[key: string]: Object}\> | 是   | 回调函数，返回媒体提供方设置的自定义媒体数据包，数据包的内容与setExtras设置的内容完全一致。 |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |
| 6600102  | The session does not exist. |
| 6600103  | The session controller does not exist. |
| 6600105  | Invalid session command. |
| 6600107  | Too many commands or events. |

**示例：**
```js
let metadata  = {
    assetId: "121278",
    title: "lose yourself",
    artist: "Eminem",
    author: "ST",
    album: "Slim shady",
    writer: "ST",
    composer: "ST",
    duration: 2222,
    mediaImage: "https://www.example.com/example.jpg",
    subtitle: "8 Mile",
    description: "Rap",
    lyric: "https://www.example.com/example.lrc",
    previousAssetId: "121277",
    nextAssetId: "121279",
};
controller.getExtras(function (err, extras) {
    if (err) {
        console.info(`getExtras BusinessError: code: ${err.code}, message: ${err.message}`);
    } else {
        console.info(`getExtras : SUCCESS : assetId : ${metadata.assetId}`);
    }
});
```

### sendAVKeyEvent<sup>10+</sup>

sendAVKeyEvent(event: KeyEvent): Promise\<void>

发送按键事件到控制器对应的会话。结果通过Promise异步回调方式返回。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**参数：**

| 参数名 | 类型                                                         | 必填 | 说明       |
| ------ | ------------------------------------------------------------ | ---- | ---------- |
| event  | [KeyEvent](js-apis-keyevent.md) | 是   | 按键事件。 |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 600101  | Session service exception. |
| 600102  | The session does not exist. |
| 600103  | The session controller does not exist. |
| 600105  | Invalid session command. |
| 600106  | The session is not activated. |

**返回值：**

| 类型           | 说明                          |
| -------------- | ----------------------------- |
| Promise\<void> | Promise对象。当事件发送成功，无返回结果，否则返回错误对象。 |

**示例：**

```js
let keyItem = {code:0x49, pressedTime:2, deviceId:0};
let event = {action:2, key:keyItem, keys:[keyItem]};

controller.sendAVKeyEvent(event).then(() => {
    console.info(`SendAVKeyEvent Successfully`);
}).catch((err) => {
    console.info(`SendAVKeyEvent BusinessError: code: ${err.code}, message: ${err.message}`);
});
```

### sendAVKeyEvent<sup>10+</sup>

sendAVKeyEvent(event: KeyEvent, callback: AsyncCallback\<void>): void

发送按键事件到会话。结果通过callback异步回调方式返回。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**参数：**

| 参数名   | 类型                                                         | 必填 | 说明       |
| -------- | ------------------------------------------------------------ | ---- | ---------- |
| event    | [KeyEvent](js-apis-keyevent.md) | 是   | 按键事件。 |
| callback | AsyncCallback\<void>                                         | 是   | 回调函数。当事件发送成功，err为undefined，否则返回错误对象。 |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 600101  | Session service exception. |
| 600102  | The session does not exist. |
| 600103  | The session controller does not exist. |
| 600105  | Invalid session command. |
| 600106  | The session is not activated. |

**示例：**

```js
let keyItem = {code:0x49, pressedTime:2, deviceId:0};
let event = {action:2, key:keyItem, keys:[keyItem]};

controller.sendAVKeyEvent(event, function (err) {
    if (err) {
        console.info(`SendAVKeyEvent BusinessError: code: ${err.code}, message: ${err.message}`);
    } else {
        console.info(`SendAVKeyEvent Successfully`);
    }
});
```

### getLaunchAbility<sup>10+</sup>

getLaunchAbility(): Promise\<WantAgent>

获取应用在会话中保存的WantAgent对象。结果通过Promise异步回调方式返回。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**返回值：**

| 类型                                                    | 说明                                                         |
| ------------------------------------------------------- | ------------------------------------------------------------ |
| Promise<[WantAgent](js-apis-app-ability-wantAgent.md)\> | Promise对象，返回在[setLaunchAbility](#setlaunchability10)保存的对象，包括应用的相关属性信息，如bundleName，abilityName，deviceId等。 |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |
| 6600102  | The session does not exist. |
| 6600103  | The session controller does not exist. |

**示例：**

```js
import wantAgent from '@ohos.app.ability.wantAgent';

controller.getLaunchAbility().then((agent) => {
    console.info(`GetLaunchAbility : SUCCESS : wantAgent : ${agent}`);
}).catch((err) => {
    console.info(`GetLaunchAbility BusinessError: code: ${err.code}, message: ${err.message}`);
});
```

### getLaunchAbility<sup>10+</sup>

getLaunchAbility(callback: AsyncCallback\<WantAgent>): void

获取应用在会话中保存的WantAgent对象。结果通过callback异步回调方式返回。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**参数：**

| 参数名   | 类型                                                         | 必填 | 说明                                                         |
| -------- | ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| callback | AsyncCallback<[WantAgent](js-apis-app-ability-wantAgent.md)\> | 是   | 回调函数。返回在[setLaunchAbility](#setlaunchability10)保存的对象，包括应用的相关属性信息，如bundleName，abilityName，deviceId等。 |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |
| 6600102  | The session does not exist. |
| 6600103  | The session controller does not exist. |

**示例：**

```js
import wantAgent from '@ohos.app.ability.wantAgent';

controller.getLaunchAbility(function (err, agent) {
    if (err) {
        console.info(`GetLaunchAbility BusinessError: code: ${err.code}, message: ${err.message}`);
    } else {
        console.info(`GetLaunchAbility : SUCCESS : wantAgent : ${agent}`);
    }
});
```

### getRealPlaybackPositionSync<sup>10+</sup>

getRealPlaybackPositionSync(): number

获取当前播放位置。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**返回值：**

| 类型   | 说明               |
| ------ | ------------------ |
| number | 时间节点，毫秒数。 |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |
| 6600103  | The session controller does not exist. |

**示例：**

```js
let time = controller.getRealPlaybackPositionSync();
```

### isActive<sup>10+</sup>

isActive(): Promise\<boolean>

获取会话是否被激活。结果通过Promise异步回调方式返回。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**返回值：**

| 类型              | 说明                                                         |
| ----------------- | ------------------------------------------------------------ |
| Promise<boolean\> | Promise对象，返回会话是否为激活状态，true表示被激活，false表示禁用。 |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |
| 6600102  | The session does not exist. |
| 6600103  | The session controller does not exist. |

**示例：**

```js
controller.isActive().then((isActive) => {
    console.info(`IsActive : SUCCESS : isactive : ${isActive}`);
}).catch((err) => {
    console.info(`IsActive BusinessError: code: ${err.code}, message: ${err.message}`);
});
```

### isActive<sup>10+</sup>

isActive(callback: AsyncCallback\<boolean>): void

判断会话是否被激活。结果通过callback异步回调方式返回。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**参数：**

| 参数名   | 类型                    | 必填 | 说明                                                         |
| -------- | ----------------------- | ---- | ------------------------------------------------------------ |
| callback | AsyncCallback<boolean\> | 是   | 回调函数，返回会话是否为激活状态，true表示被激活，false表示禁用。 |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |
| 6600102  | The session does not exist. |
| 6600103  | The session controller does not exist. |

**示例：**

```js
controller.isActive(function (err, isActive) {
    if (err) {
        console.info(`IsActive BusinessError: code: ${err.code}, message: ${err.message}`);
    } else {
        console.info(`IsActive : SUCCESS : isactive : ${isActive}`);
    }
});
```

### destroy<sup>10+</sup>

destroy(): Promise\<void>

销毁当前控制器，销毁后当前控制器不可再用。结果通过Promise异步回调方式返回。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**返回值：**

| 类型           | 说明                          |
| -------------- | ----------------------------- |
| Promise\<void> | Promise对象。当控制器销毁成功，无返回结果，否则返回错误对象。 |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |
| 6600103  | The session controller does not exist. |

**示例：**

```js
controller.destroy().then(() => {
    console.info(`Destroy : SUCCESS `);
}).catch((err) => {
    console.info(`Destroy BusinessError: code: ${err.code}, message: ${err.message}`);
});
```

### destroy<sup>10+</sup>

destroy(callback: AsyncCallback\<void>): void

销毁当前控制器，销毁后当前控制器不可再用。结果通过callback异步回调方式返回。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**参数：**

| 参数名   | 类型                 | 必填 | 说明       |
| -------- | -------------------- | ---- | ---------- |
| callback | AsyncCallback\<void> | 是   | 回调函数。当控制器销毁成功，err为undefined，否则返回错误对象。 |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |
| 6600103  | The session controller does not exist. |

**示例：**

```js
controller.destroy(function (err) {
    if (err) {
        console.info(`Destroy BusinessError: code: ${err.code}, message: ${err.message}`);
    } else {
        console.info(`Destroy : SUCCESS `);
    }
});
```

### getValidCommands<sup>10+</sup>

getValidCommands(): Promise\<Array\<AVControlCommandType>>

获取会话支持的有效命令。结果通过Promise异步回调方式返回。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**返回值：**

| 类型                                                         | 说明                              |
| ------------------------------------------------------------ | --------------------------------- |
| Promise<Array<[AVControlCommandType](#avcontrolcommandtype10)\>\> | Promise对象。返回有效命令的集合。 |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |
| 6600102  | The session does not exist. |
| 6600103  | The session controller does not exist. |

**示例：**

```js
controller.getValidCommands.then((validCommands) => {
    console.info(`GetValidCommands : SUCCESS : size : ${validCommands.length}`);
}).catch((err) => {
    console.info(`GetValidCommands BusinessError: code: ${err.code}, message: ${err.message}`);
});
```

### getValidCommands<sup>10+</sup>

getValidCommands(callback: AsyncCallback\<Array\<AVControlCommandType>>): void

获取会话支持的有效命令。结果通过callback异步回调方式返回。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**参数：**

| 参数名   | 类型                                                         | 必填 | 说明                           |
| -------- | ------------------------------------------------------------ | ---- | ------------------------------ |
| callback | AsyncCallback\<Array\<[AVControlCommandType](#avcontrolcommandtype10)\>\> | 是   | 回调函数，返回有效命令的集合。 |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |
| 6600102  | The session does not exist. |
| 6600103  | The session controller does not exist. |

**示例：**

```js
controller.getValidCommands(function (err, validCommands) {
    if (err) {
        console.info(`GetValidCommands BusinessError: code: ${err.code}, message: ${err.message}`);
    } else {
        console.info(`GetValidCommands : SUCCESS : size : ${validCommands.length}`);
    }
});
```

### sendControlCommand<sup>10+</sup>

sendControlCommand(command: AVControlCommand): Promise\<void>

通过控制器发送命令到其对应的会话。结果通过Promise异步回调方式返回。

> **说明：**
>
> 媒体控制方在使用sendControlCommand命令前，需要确保控制对应的媒体会话注册了对应的监听，注册媒体会话相关监听的方法请参见接口[注册媒体会话相关监听](#onplaypausestopplaynextplaypreviousfastforwardrewind10)。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**参数：**

| 参数名    | 类型                                  | 必填 | 说明                           |
| ------- | ------------------------------------- | ---- | ------------------------------ |
| command | [AVControlCommand](#avcontrolcommand10) | 是   | 会话的相关命令和命令相关参数。 |

**返回值：**

| 类型           | 说明                          |
| -------------- | ----------------------------- |
| Promise\<void> | Promise对象。当命令发送成功，无返回结果，否则返回错误对象。 |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |
| 6600102  | The session does not exist. |
| 6600103  | The session controller does not exist. |
| 6600105  | Invalid session command. |
| 6600106  | The session is not activated. |
| 6600107  | Too many commands or events. |

**示例：**

```js
let avCommand = {command:'play'};
// let avCommand = {command:'pause'};
// let avCommand = {command:'stop'};
// let avCommand = {command:'playNext'};
// let avCommand = {command:'playPrevious'};
// let avCommand = {command:'fastForward'};
// let avCommand = {command:'rewind'};
// let avCommand = {command:'seek', parameter:10};
// let avCommand = {command:'setSpeed', parameter:2.6};
// let avCommand = {command:'setLoopMode', parameter:avSession.LoopMode.LOOP_MODE_SINGLE};
// let avCommand = {command:'toggleFavorite', parameter:"false"};
controller.sendControlCommand(avCommand).then(() => {
    console.info(`SendControlCommand successfully`);
}).catch((err) => {
    console.info(`SendControlCommand BusinessError: code: ${err.code}, message: ${err.message}`);
});
```

### sendControlCommand<sup>10+</sup>

sendControlCommand(command: AVControlCommand, callback: AsyncCallback\<void>): void

通过会话控制器发送命令到其对应的会话。结果通过callback异步回调方式返回。

> **说明：**
>
> 媒体控制方在使用sendControlCommand命令前，需要确保控制对应的媒体会话注册了对应的监听，注册媒体会话相关监听的方法请参见接口[注册媒体会话相关监听](#onplaypausestopplaynextplaypreviousfastforwardrewind10)。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**参数：**

| 参数名   | 类型                                  | 必填 | 说明                           |
| -------- | ------------------------------------- | ---- | ------------------------------ |
| command  | [AVControlCommand](#avcontrolcommand10) | 是   | 会话的相关命令和命令相关参数。 |
| callback | AsyncCallback\<void>                  | 是   | 回调函数。当命令发送成功，err为undefined，否则返回错误对象。                     |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ------------------------------- |
| 6600101  | Session service exception.                |
| 6600102  | The session does not exist.     |
| 6600103  | The session controller does not exist.   |
| 6600105  | Invalid session command.           |
| 6600106  | The session is not activated.                |
| 6600107  | Too many commands or events.      |

**示例：**

```js
let avCommand = {command:'play'};
// let avCommand = {command:'pause'};
// let avCommand = {command:'stop'};
// let avCommand = {command:'playNext'};
// let avCommand = {command:'playPrevious'};
// let avCommand = {command:'fastForward'};
// let avCommand = {command:'rewind'};
// let avCommand = {command:'seek', parameter:10};
// let avCommand = {command:'setSpeed', parameter:2.6};
// let avCommand = {command:'setLoopMode', parameter:avSession.LoopMode.LOOP_MODE_SINGLE};
// let avCommand = {command:'toggleFavorite', parameter:"false"};
controller.sendControlCommand(avCommand, function (err) {
    if (err) {
        console.info(`SendControlCommand BusinessError: code: ${err.code}, message: ${err.message}`);
    } else {
        console.info(`SendControlCommand successfully`);
    }
});
```

### sendCommonCommand<sup>10+</sup>

sendCommonCommand(command: string, args: {[key: string]: Object}): Promise\<void>

通过会话控制器发送自定义控制命令到其对应的会话。结果通过Promise异步回调方式返回。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**参数：**

| 参数名    | 类型                                  | 必填 | 说明                           |
| ------- | ------------------------------------- | ---- | ------------------------------ |
| command | string | 是   | 需要设置的自定义控制命令的名称 |
| args | {[key: string]: any} | 是   | 需要传递的控制命令键值对 |

> **说明：**
> 参数args支持的数据类型有：字符串、数字、布尔、对象、数组和文件描述符等，详细介绍请参见[@ohos.app.ability.Want(Want)](./js-apis-app-ability-want.md)。

**返回值：**

| 类型           | 说明                          |
| -------------- | ----------------------------- |
| Promise\<void> | Promise对象。当命令发送成功，无返回结果，否则返回错误对象。 |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |
| 6600102  | The session does not exist. |
| 6600103  | The session controller does not exist. |
| 6600105  | Invalid session command. |
| 6600106  | The session is not activated. |
| 6600107  | Too many commands or events. |

**示例：**

```js
let commandName = "my_command";
let args = {
    command : "This is my command"
}
await controller.sendCommonCommand(commandName, args).catch((err) => {
    console.info(`SendCommonCommand BusinessError: code: ${err.code}, message: ${err.message}`);
})
```

### sendCommonCommand<sup>10+</sup>

sendCommonCommand(command: string, args: {[key: string]: Object}, callback: AsyncCallback\<void>): void

通过会话控制器发送自定义命令到其对应的会话。结果通过callback异步回调方式返回。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**参数：**

| 参数名    | 类型                                  | 必填 | 说明                           |
| ------- | ------------------------------------- | ---- | ------------------------------ |
| command | string | 是   | 需要设置的自定义控制命令的名称 |
| args | {[key: string]: any} | 是   | 需要传递的控制命令键值对 |
| callback | AsyncCallback\<void>                  | 是   | 回调函数。当命令发送成功，err为undefined，否则返回错误对象。                     |

> **说明：**
> 参数args支持的数据类型有：字符串、数字、布尔、对象、数组和文件描述符等，详细介绍请参见[@ohos.app.ability.Want(Want)](./js-apis-app-ability-want.md)。

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ------------------------------- |
| 6600101  | Session service exception.                |
| 6600102  | The session does not exist.     |
| 6600103  | The session controller does not exist.   |
| 6600105  | Invalid session command.           |
| 6600106  | The session is not activated.                |
| 6600107  | Too many commands or events.      |

**示例：**

```js
let commandName = "my_command";
let args = {
    command : "This is my command"
}
controller.sendCommonCommand(commandName, args, (err) => {
    if(err) {
        console.info(`SendCommonCommand BusinessError: code: ${err.code}, message: ${err.message}`);
    }
})
```

### on('metadataChange')<sup>10+</sup>

on(type: 'metadataChange', filter: Array\<keyof AVMetadata> | 'all', callback: (data: AVMetadata) => void)

设置元数据变化的监听事件。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**参数：**

| 参数名   | 类型                                                         | 必填 | 说明                                                         |
| -------- | ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| type     | string                                                       | 是   | 事件回调类型，支持事件`'metadataChange'`：当元数据变化时，触发该事件。 |
| filter   | Array\<keyof&nbsp;[AVMetadata](#avmetadata10)\>&nbsp;&#124;&nbsp;'all' | 是   | 'all' 表示关注元数据所有字段变化；Array<keyof&nbsp;[AVMetadata](#avmetadata10)\> 表示关注Array中的字段变化。 |
| callback | (data: [AVMetadata](#avmetadata10)) => void                    | 是   | 回调函数，参数data是变化后的元数据。                         |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ------------------------------ |
| 6600101  | Session service exception. |
| 6600103  | The session controller does not exist. |

**示例：**

```js
controller.on('metadataChange', 'all', (metadata) => {
    console.info(`on metadataChange assetId : ${metadata.assetId}`);
});

let metaFilter = ['assetId', 'title', 'description'];
controller.on('metadataChange', metaFilter, (metadata) => {
    console.info(`on metadataChange assetId : ${metadata.assetId}`);
});
```

### on('playbackStateChange')<sup>10+</sup>

on(type: 'playbackStateChange', filter: Array\<keyof AVPlaybackState> | 'all', callback: (state: AVPlaybackState) => void)

设置播放状态变化的监听事件。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**参数：**

| 参数名   | 类型                                                         | 必填 | 说明                                                         |
| -------- | ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| type     | string                                                       | 是   | 事件回调类型，支持事件`'playbackStateChange'`：当播放状态变化时，触发该事件。 |
| filter   | Array\<keyof&nbsp;[AVPlaybackState](#avplaybackstate10)\>&nbsp;&#124;&nbsp;'all' | 是   | 'all' 表示关注播放状态所有字段变化；Array<keyof&nbsp;[AVPlaybackState](#avplaybackstate10)\> 表示关注Array中的字段变化。 |
| callback | (state: [AVPlaybackState](#avplaybackstate10)) => void         | 是   | 回调函数，参数state是变化后的播放状态。                      |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ------------------------------ |
| 6600101  | Session service exception. |
| 6600103  | The session controller does not exist. |

**示例：**

```js
controller.on('playbackStateChange', 'all', (playbackState) => {
    console.info(`on playbackStateChange state : ${playbackState.state}`);
});

let playbackFilter = ['state', 'speed', 'loopMode'];
controller.on('playbackStateChange', playbackFilter, (playbackState) => {
    console.info(`on playbackStateChange state : ${playbackState.state}`);
});
```

### on('sessionEvent')<sup>10+</sup>

on(type: 'sessionEvent', callback: (sessionEvent: string, args: {[key:string]: Object}) => void): void

媒体控制器设置会话自定义事件变化的监听器。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**参数：**

| 参数名   | 类型                                                         | 必填 | 说明                                                         |
| -------- | ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| type     | string                                                       | 是   | 事件回调类型，支持事件`'sessionEvent'`：当会话事件变化时，触发该事件。 |
| callback | (sessionEvent: string, args: {[key:string]: object}) => void         | 是   | 回调函数，sessionEvent为变化的会话事件名，args为事件的参数。          |

**错误码：**

以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ------------------------------ |
| 6600101  | Session service exception. |
| 6600103  | The session controller does not exist. |

**示例：**

```js
controller.on('sessionEvent', (sessionEvent, args) => {
    console.info(`OnSessionEvent, sessionEvent is ${sessionEvent}, args: ${JSON.stringify(args)}`);
});
```

### on('queueItemsChange')<sup>10+</sup>

on(type: 'queueItemsChange', callback: (items: Array<[AVQueueItem](#avqueueitem10)\>) => void): void

媒体控制器设置会话自定义播放列表变化的监听器。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**参数：**

| 参数名   | 类型                                                   | 必填 | 说明                                                                         |
| -------- | ----------------------------------------------------- | ---- | ---------------------------------------------------------------------------- |
| type     | string                                                | 是   | 事件回调类型，支持事件`'queueItemsChange'`：当session修改播放列表时，触发该事件。 |
| callback | (items: Array<[AVQueueItem](#avqueueitem10)\>) => void  | 是   | 回调函数，items为变化的播放列表。                            |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ------------------------------ |
| 6600101  | Session service exception. |
| 6600103  | The session controller does not exist. |

**示例：**

```js
controller.on('queueItemsChange', (items) => {
    console.info(`OnQueueItemsChange, items length is ${items.length}`);
});
```

### on('queueTitleChange')<sup>10+</sup>

on(type: 'queueTitleChange', callback: (title: string) => void): void

媒体控制器设置会话自定义播放列表的名称变化的监听器。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**参数：**

| 参数名   | 类型                     | 必填 | 说明                                                                             |
| -------- | ----------------------- | ---- | ------------------------------------------------------------------------------- |
| type     | string                  | 是   | 事件回调类型，支持事件`'queueTitleChange'`：当session修改播放列表名称时，触发该事件。 |
| callback | (title: string) => void | 是   | 回调函数，title为变化的播放列表名称。                                |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ------------------------------ |
| 6600101  | Session service exception. |
| 6600103  | The session controller does not exist. |

**示例：**

```js
controller.on('queueTitleChange', (title) => {
    console.info(`queueTitleChange, title is ${title}`);
});
```

### on('extrasChange')<sup>10+</sup>

on(type: 'extrasChange', callback: (extras: {[key:string]: Object}) => void): void

媒体控制器设置自定义媒体数据包事件变化的监听器。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**参数：**

| 参数名   | 类型                                                         | 必填 | 说明                                                         |
| -------- | ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| type     | string                                                       | 是   | 事件回调类型，支持事件`'extrasChange'`：当媒体提供方设置自定义媒体数据包时，触发该事件。 |
| callback | (extras: {[key:string]: object}) => void         | 是   | 回调函数，extras为媒体提供方新设置的自定义媒体数据包，该自定义媒体数据包与dispatchSessionEvent方法设置的数据包完全一致。          |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ------------------------------ |
| 6600101  | Session service exception. |
| 6600103  | The session controller does not exist. |

**示例：**

```js
controller.on('extrasChange', (extras) => {
    console.info(`Caught extrasChange event,the new extra is: ${JSON.stringify(extras)}`);
});
```

### on('sessionDestroy')<sup>10+</sup>

on(type: 'sessionDestroy', callback: () => void)

会话销毁的监听事件。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**参数：**

| 参数名   | 类型       | 必填 | 说明                                                         |
| -------- | ---------- | ---- | ------------------------------------------------------------ |
| type     | string     | 是   | 事件回调类型，支持事件`'sessionDestroy'`：当检测到会话销毁时，触发该事件）。 |
| callback | () => void | 是   | 回调函数。当监听事件注册成功，err为undefined，否则为错误对象。                  |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ------------------------------ |
| 6600101  | Session service exception. |
| 6600103  | The session controller does not exist. |

**示例：**

```js
controller.on('sessionDestroy', () => {
    console.info(`on sessionDestroy : SUCCESS `);
});
```

### on('activeStateChange')<sup>10+</sup>

on(type: 'activeStateChange', callback: (isActive: boolean) => void)

会话的激活状态的监听事件。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**参数：**

| 参数名   | 类型                        | 必填 | 说明                                                         |
| -------- | --------------------------- | ---- | ------------------------------------------------------------ |
| type     | string                      | 是   | 事件回调类型，支持事件`'activeStateChange'`：当检测到会话的激活状态发生改变时，触发该事件。 |
| callback | (isActive: boolean) => void | 是   | 回调函数。参数isActive表示会话是否被激活。true表示被激活，false表示禁用。                   |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ----------------------------- |
| 6600101  | Session service exception. |
| 6600103  |The session controller does not exist. |

**示例：**

```js
controller.on('activeStateChange', (isActive) => {
    console.info(`on activeStateChange : SUCCESS : isActive ${isActive}`);
});
```

### on('validCommandChange')<sup>10+</sup>

on(type: 'validCommandChange', callback: (commands: Array\<AVControlCommandType>) => void)

会话支持的有效命令变化监听事件。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**参数：**

| 参数名   | 类型                                                         | 必填 | 说明                                                         |
| -------- | ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| type     | string                                                       | 是   | 事件回调类型，支持事件`'validCommandChange'`：当检测到会话的合法命令发生改变时，触发该事件。 |
| callback | (commands: Array<[AVControlCommandType](#avcontrolcommandtype10)\>) => void | 是   | 回调函数。参数commands是有效命令的集合。                     |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ------------------------------ |
| 6600101  | Session service exception. |
| 6600103  | The session controller does not exist. |

**示例：**

```js
controller.on('validCommandChange', (validCommands) => {
    console.info(`validCommandChange : SUCCESS : size : ${validCommands.size}`);
    console.info(`validCommandChange : SUCCESS : validCommands : ${validCommands.values()}`);
});
```

### on('outputDeviceChange')<sup>10+</sup>

on(type: 'outputDeviceChange', callback: (state: ConnectionState, device: OutputDeviceInfo) => void): void

设置播放设备变化的监听事件。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**参数：**

| 参数名   | 类型                                                    | 必填 | 说明                                                         |
| -------- | ------------------------------------------------------- | ---- | ------------------------------------------------------------ |
| type     | string                                                  | 是   | 事件回调类型，支持事件为`'outputDeviceChange'`：当播放设备变化时，触发该事件）。 |
| callback | (state: [ConnectionState](#connectionstate10), device: [OutputDeviceInfo](#outputdeviceinfo10)) => void | 是   | 回调函数，参数device是设备相关信息。                         |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ----------------------- |
| 6600101  | Session service exception. |
| 6600103  | The session controller does not exist. |

**示例：**

```js
controller.on('outputDeviceChange', (state, device) => {
    console.info(`on outputDeviceChange state: ${state}, device : ${device}`);
});
```

### off('metadataChange')<sup>10+</sup>

off(type: 'metadataChange', callback?: (data: AVMetadata) => void)

媒体控制器取消监听元数据变化的事件。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**参数：**

| 参数名   | 类型                                               | 必填 | 说明                                                    |
| -------- | ------------------------------------------------ | ---- | ------------------------------------------------------ |
| type     | string                                           | 是   | 取消对应的监听事件，支持事件`'metadataChange'`。         |
| callback | (data: [AVMetadata](#avmetadata10)) => void        | 否   | 回调函数，参数data是变化后的元数据。<br>该参数为可选参数，若不填写该参数，则认为取消所有相关会话的事件监听。                         |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------- |
| 6600101  | Session service exception. |
| 6600103  | The session controller does not exist. |

**示例：**

```js
controller.off('metadataChange');
```

### off('playbackStateChange')<sup>10+</sup>

off(type: 'playbackStateChange', callback?: (state: AVPlaybackState) => void)

媒体控制器取消监听播放状态变化的事件。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**参数：**

| 参数名   | 类型                                                         | 必填 | 说明                                                     |
| -------- | ------------------------------------------------------------ | ---- | ----------------------------------------------------- |
| type     | string                                                       | 是   | 取消对应的监听事件，支持事件`'playbackStateChange'`。    |
| callback | (state: [AVPlaybackState](#avplaybackstate10)) => void         | 否   | 回调函数，参数state是变化后的播放状态。<br>该参数为可选参数，若不填写该参数，则认为取消所有相关会话的事件监听。                      |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------- |
| 6600101  | Session service exception. |
| 6600103  | The session controller does not exist. |

**示例：**

```js
controller.off('playbackStateChange');
```

### off('sessionEvent')<sup>10+</sup>

off(type: 'sessionEvent', callback?: (sessionEvent: string, args: {[key:string]: Object}) => void): void

媒体控制器取消监听会话事件的变化通知。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**参数：**

| 参数名   | 类型                                                         | 必填 | 说明                                                     |
| -------- | ------------------------------------------------------------ | ---- | ----------------------------------------------------- |
| type     | string                                                       | 是   | 取消对应的监听事件，支持事件`'sessionEvent'`。    |
| callback | (sessionEvent: string, args: {[key:string]: Object}) => void         | 否   | 回调函数，参数sessionEvent是变化的事件名，args为事件的参数。<br>该参数为可选参数，若不填写该参数，则认为取消所有对sessionEvent事件的监听。                      |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------- |
| 6600101  | Session service exception. |
| 6600103  | The session controller does not exist. |

**示例：**

```js
controller.off('sessionEvent');
```

### off('queueItemsChange')<sup>10+</sup>

off(type: 'queueItemsChange', callback?: (items: Array<[AVQueueItem](#avqueueitem10)\>) => void): void

媒体控制器取消监听播放列表变化的事件。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**参数：**

| 参数名    | 类型                                                 | 必填 | 说明                                                                                                |
| -------- | ---------------------------------------------------- | ---- | --------------------------------------------------------------------------------------------------- |
| type     | string                                               | 是   | 取消对应的监听事件，支持事件`'queueItemsChange'`。                                                     |
| callback | (items: Array<[AVQueueItem](#avqueueitem10)\>) => void | 否   | 回调函数，参数items是变化的播放列表。<br>该参数为可选参数，若不填写该参数，则认为取消所有相关会话的事件监听。 |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------- |
| 6600101  | Session service exception. |
| 6600103  | The session controller does not exist. |

**示例：**

```js
controller.off('queueItemsChange');
```

### off('queueTitleChange')<sup>10+</sup>

off(type: 'queueTitleChange', callback?: (title: string) => void): void

媒体控制器取消监听播放列表名称变化的事件。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**参数：**

| 参数名    | 类型                    | 必填 | 说明                                                                                                    |
| -------- | ----------------------- | ---- | ------------------------------------------------------------------------------------------------------- |
| type     | string                  | 是   | 取消对应的监听事件，支持事件`'queueTitleChange'`。                                                         |
| callback | (title: string) => void | 否   | 回调函数，参数items是变化的播放列表名称。<br>该参数为可选参数，若不填写该参数，则认为取消所有相关会话的事件监听。 |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------- |
| 6600101  | Session service exception. |
| 6600103  | The session controller does not exist. |

**示例：**

```js
controller.off('queueTitleChange');
```

### off('extrasChange')<sup>10+</sup>

off(type: 'extrasChange', callback?: (extras: {[key:string]: Object}) => void): void

媒体控制器取消监听自定义媒体数据包变化事件。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**参数：**

| 参数名    | 类型                    | 必填 | 说明                                                                                                    |
| -------- | ----------------------- | ---- | ------------------------------------------------------------------------------------------------------- |
| type     | string                  | 是   | 取消对应的监听事件，支持事件`'extrasChange'`。                                                         |
| callback | ({[key:string]: Object}) => void | 否   | 注册监听事件时的回调函数。<br>该参数为可选参数，若不填写该参数，则认为取消会话所有与此事件相关的监听。 |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ----------------                       |
| 6600101  | Session service exception.             |
| 6600103  | The session controller does not exist. |

**示例：**

```js
controller.off('extrasChange');
```

### off('sessionDestroy')<sup>10+</sup>

off(type: 'sessionDestroy', callback?: () => void)

媒体控制器取消监听会话的销毁事件。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**参数：**

| 参数名   | 类型       | 必填 | 说明                                                      |
| -------- | ---------- | ---- | ----------------------------------------------------- |
| type     | string     | 是   | 取消对应的监听事件，支持事件`'sessionDestroy'`。         |
| callback | () => void | 否   | 回调函数。当监听事件取消成功，err为undefined，否则返回错误对象。<br>该参数为可选参数，若不填写该参数，则认为取消所有相关会话的事件监听。                                               |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------- |
| 6600101  | Session service exception. |
| 6600103  | The session controller does not exist. |

**示例：**

```js
controller.off('sessionDestroy');
```

### off('activeStateChange')<sup>10+</sup>

off(type: 'activeStateChange', callback?: (isActive: boolean) => void)

媒体控制器取消监听会话激活状态变化的事件。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**参数：**

| 参数名   | 类型                        | 必填 | 说明                                                      |
| -------- | --------------------------- | ---- | ----------------------------------------------------- |
| type     | string                      | 是   | 取消对应的监听事件，支持事件`'activeStateChange'`。      |
| callback | (isActive: boolean) => void | 否   | 回调函数。参数isActive表示会话是否被激活。true表示被激活，false表示禁用。<br>该参数为可选参数，若不填写该参数，则认为取消所有相关会话的事件监听。                   |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------- |
| 6600101  | Session service exception. |
| 6600103  | The session controller does not exist. |

**示例：**

```js
controller.off('activeStateChange');
```

### off('validCommandChange')<sup>10+</sup>

off(type: 'validCommandChange', callback?: (commands: Array\<AVControlCommandType>) => void)

媒体控制器取消监听会话有效命令变化的事件。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**参数：**

| 参数名   | 类型                                                         | 必填 | 说明                                                        |
| -------- | ------------------------------------------------------------ | ---- | -------------------------------------------------------- |
| type     | string                                                       | 是   | 取消对应的监听事件，支持事件`'validCommandChange'`。         |
| callback | (commands: Array<[AVControlCommandType](#avcontrolcommandtype10)\>) => void | 否   | 回调函数。参数commands是有效命令的集合。<br>该参数为可选参数，若不填写该参数，则认为取消所有相关会话的事件监听。          |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息           |
| -------- | ---------------- |
| 6600101  | Session service exception. |
| 6600103  | The session controller does not exist. |

**示例：**

```js
controller.off('validCommandChange');
```

### off('outputDeviceChange')<sup>10+</sup>

off(type: 'outputDeviceChange', callback?: (state: ConnectionState, device: OutputDeviceInfo) => void): void

媒体控制器取消监听分布式设备变化的事件。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

**参数：**

| 参数名   | 类型                                                    | 必填 | 说明                                                      |
| -------- | ------------------------------------------------------- | ---- | ------------------------------------------------------ |
| type     | string                                                  | 是   | 取消对应的监听事件，支持事件`'outputDeviceChange'`。      |
| callback | (state: [ConnectionState](#connectionstate10), device: [OutputDeviceInfo](#outputdeviceinfo10)) => void | 否   | 回调函数，参数device是设备相关信息。<br>该参数为可选参数，若不填写该参数，则认为取消所有相关会话的事件监听。                         |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID  | 错误信息          |
| -------- | ---------------- |
| 6600101  | Session service exception. |
| 6600103  | The session controller does not exist. |

**示例：**

```js
controller.off('outputDeviceChange');
```

## AVCastController<sup>10+</sup>

在投播建立后，调用[avSession.getAVCastController](#getavcastcontroller10)后，返回会话控制器实例。控制器可查看会话ID，并可完成对会话发送命令及事件，获取会话元数据，播放状态信息等操作。

### getAVPlaybackState<sup>10+</sup>

getAVPlaybackState(callback: AsyncCallback\<AVPlaybackState>): void

设备建立连接后，获取投播控制器。结果通过callback异步回调方式返回。

**系统能力：** SystemCapability.Multimedia.AVSession.AVCast

**参数：**

| 参数名    | 类型                                                        | 必填 | 说明                                                         |
| --------- | ----------------------------------------------------------- | ---- | ------------------------------------------------------------ |
| callback  | AsyncCallback<[[AVPlaybackState](#avplaybackstate10))\> | 是   | 回调函数，返回投播控制器实例。 |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |

**示例：**

```js
controller.getAVPlaybackState(function (err, state) {
    if (err) {
        console.info(`getAVPlaybackState BusinessError: code: ${err.code}, message: ${err.message}`);
    } else {
        console.info(`getAVPlaybackState : SUCCESS`);
    }
});
```

### getAVPlaybackState<sup>10+</sup>

getAVPlaybackState(): Promise\<AVPlaybackState>;

获取当前的远端播放状态。结果通过callback异步回调方式返回。

**系统能力：** SystemCapability.Multimedia.AVSession.AVCast

**返回值：**

| 类型                                                        | 说明                                                         |
| --------- | ------------------------------------------------------------ |
| Promise<[AVPlaybackState](#avplaybackstate10)\>  | Promise对象。返回投播控制器实例。 |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |

**示例：**

```js
controller.getAVPlaybackState().then((state) => {
    console.info(`getAVPlaybackState : SUCCESS :`);
}).catch((err) => {
    console.info(`getAVPlaybackState BusinessError: code: ${err.code}, message: ${err.message}`);
});
```

### setDisplaySurface<sup>10+</sup>

setDisplaySurface(surfaceId: string): Promise\<void>

设置播放的surfaceId，在投播sink端使用。结果通过Promise异步回调方式返回。

**系统能力：** SystemCapability.Multimedia.AVSession.AVCast

**系统接口：** 该接口为系统接口。

**返回值：**

| 类型                                          | 说明                        |
| --------------------------------------------- | --------------------------- |
| Promise\<void> | Promise对象。返回设置结果。 |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600109  | The remote connection is not established. |


### setDisplaySurface<sup>10+</sup>

setDisplaySurface(surfaceId: string, callback: AsyncCallback\<void>): void

设置播放的surfaceId，在投播sink端使用。结果通过callback异步回调方式返回。

**系统能力：** SystemCapability.Multimedia.AVSession.AVCast

**系统接口：** 该接口为系统接口。

**参数：**

| 参数名   | 类型                                                | 必填 | 说明                         |
| -------- | --------------------------------------------------- | ---- | ---------------------------- |
| callback | AsyncCallback\<void> | 是   | 回调函数，返回当前设置结果。 |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600109  | The remote connection is not established. |

**示例：**
```js
controller.getAVPlaybackState(function (err, playbackState) {
    if (err) {
        console.info(`GetAVPlaybackState BusinessError: code: ${err.code}, message: ${err.message}`);
    } else {
        console.info(`GetAVPlaybackState : SUCCESS : state : ${playbackState.state}`);
    }
});
```

### on('playbackStateChange')<sup>10+</sup>

on(type: 'playbackStateChange', filter: Array\<keyof AVPlaybackState> | 'all', callback: (state: AVPlaybackState) => void): void

设置播放状态变化的监听事件。

**系统能力：** SystemCapability.Multimedia.AVSession.AVCast

**参数：**

| 参数名   | 类型                                                         | 必填 | 说明                                                         |
| -------- | ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| type     | string                                                       | 是   | 事件回调类型，支持事件`'playbackStateChange'`：当播放状态变化时，触发该事件。 |
| filter   | Array\<keyof&nbsp;[AVPlaybackState](#avplaybackstate10)\>&nbsp;&#124;&nbsp;'all' | 是   | 'all' 表示关注播放状态所有字段变化；Array<keyof&nbsp;[AVPlaybackState](#avplaybackstate10)\> 表示关注Array中的字段变化。 |
| callback | (state: [AVPlaybackState](#avplaybackstate10)) => void         | 是   | 回调函数，参数state是变化后的播放状态。                      |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ------------------------------ |
| 6600101  | Session service exception. |

**示例：**

```js
controller.on('playbackStateChange', 'all', (playbackState) => {
    console.info(`on playbackStateChange state : ${playbackState.state}`);
});

let playbackFilter = ['state', 'speed', 'loopMode'];
controller.on('playbackStateChange', playbackFilter, (playbackState) => {
    console.info(`on playbackStateChange state : ${playbackState.state}`);
});
```

### off('playbackStateChange')<sup>10+</sup>

off(type: 'playbackStateChange', callback?: (state: AVPlaybackState) => void): void

媒体控制器取消监听播放状态变化的事件。

**系统能力：** SystemCapability.Multimedia.AVSession.AVCast

**参数：**

| 参数名   | 类型                                                         | 必填 | 说明                                                     |
| -------- | ------------------------------------------------------------ | ---- | ----------------------------------------------------- |
| type     | string                                                       | 是   | 取消对应的监听事件，支持事件`'playbackStateChange'`。    |
| callback | (state: [AVPlaybackState](#avplaybackstate10)) => void         | 否   | 回调函数，参数state是变化后的播放状态。<br>该参数为可选参数，若不填写该参数，则认为取消所有相关会话的事件监听。                      |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------- |
| 6600101  | Session service exception. |

**示例：**

```js
controller.off('playbackStateChange');
```

### on('mediaItemChange')<sup>10+</sup>

on(type: 'mediaItemChange', callback: Callback\<AVQueueItem>): void

设置投播当前播放媒体内容的监听事件。

**系统能力：** SystemCapability.Multimedia.AVSession.AVCast

**参数：**

| 参数名   | 类型                                                         | 必填 | 说明                                                         |
| -------- | ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| type     | string                                                       | 是   | 事件回调类型，支持事件`'mediaItemChange'`：当播放状态变化时，触发该事件。 |
| callback | (state: [AVQueueItem](#avqueueitem10)) => void         | 是   | 回调函数，参数AVQueueItem是d当前正在播放的媒体内容。                      |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ------------------------------ |
| 6600101  | Session service exception. |

**示例：**

```js
controller.on('mediaItemChange', (item) => {
    console.info(`on mediaItemChange state : ${item.itemId}`);
});
```

### off('mediaItemChange')<sup>10+</sup>

off(type: 'mediaItemChange'): void

取消设置投播当前播放媒体内容的监听事件。

**系统能力：** SystemCapability.Multimedia.AVSession.AVCast

**参数：**

| 参数名   | 类型                                                         | 必填 | 说明                                                     |
| -------- | ------------------------------------------------------------ | ---- | ----------------------------------------------------- |
| type     | string                                                       | 是   | 取消对应的监听事件，支持事件`'mediaItemChange'`。    |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------- |
| 6600101  | Session service exception. |

**示例：**

```js
controller.off('mediaItemChange');
```

### on('playNext')<sup>10+</sup>

on(type: 'playNext', callback: Callback\<void>): void

设置播放下一首资源的监听事件。

**系统能力：** SystemCapability.Multimedia.AVSession.AVCast

**参数：**

| 参数名   | 类型                                                         | 必填 | 说明                                                         |
| -------- | ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| type     | string                                                       | 是   | 事件回调类型，支持事件`'playNext'`：当播放下一首状态变化时，触发该事件。 |
| callback | Callback\<void\>         | 是   | 回调函数                      |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ------------------------------ |
| 6600101  | Session service exception. |

**示例：**

```js
controller.on('playNext', () => {
    console.info(`on playNext`);
});
```

### off('playNext')<sup>10+</sup>

off(type: 'playNext'): void

取消设置播放下一首资源的监听事件。

**系统能力：** SystemCapability.Multimedia.AVSession.AVCast

**参数：**

| 参数名   | 类型                                                         | 必填 | 说明                                                     |
| -------- | ------------------------------------------------------------ | ---- | ----------------------------------------------------- |
| type     | string                                                       | 是   | 取消对应的监听事件，支持事件`'playNext'`。    |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------- |
| 6600101  | Session service exception. |

**示例：**

```js
controller.off('playNext');
```

### on('playPrevious')<sup>10+</sup>

on(type: 'playPrevious', callback: Callback\<void>): void

设置播放上一首资源的监听事件。

**系统能力：** SystemCapability.Multimedia.AVSession.AVCast

**参数：**

| 参数名   | 类型                                                         | 必填 | 说明                                                         |
| -------- | ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| type     | string                                                       | 是   | 事件回调类型，支持事件`'playPrevious'`：当播放下一首状态变化时，触发该事件。 |
| callback | Callback\<void\>         | 是   | 回调函数                      |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ------------------------------ |
| 6600101  | Session service exception. |

**示例：**

```js
controller.on('playPrevious', () => {
    console.info(`on playPrevious`);
    // 设置播放参数，开始播放
    var playItem = {
        itemId: 0,
        description: {
        mediaId: '12345',
        mediaName: 'song1',
        mediaType: 'AUDIO',
        mediaUri: 'http://resource1_address',
        mediaSize: 12345,
        startPosition: 0,
        duration: 0,
        artist: 'mysong',
        albumTitle: 'song1_title',
        albumCoverUri: "http://resource1_album_address",
        lyricUri: "http://resource1_lyric_address",
        iconUri: "http://resource1_icon_address",
        appName: 'MyMusic'
        }
    };
    // 准备播放，这个不会触发真正的播放，会进行加载和缓冲
    controller.prepare(playItem, () => {
        console.info('prepare done');
    });
    // 启动播放
    controller.start(playItem, () => {
        console.info('play done');
    });
});
```

### off('playPrevious')<sup>10+</sup>

off(type: 'playPrevious'): void

取消设置播放下一首资源的监听事件。

**系统能力：** SystemCapability.Multimedia.AVSession.AVCast

**参数：**

| 参数名   | 类型                                                         | 必填 | 说明                                                     |
| -------- | ------------------------------------------------------------ | ---- | ----------------------------------------------------- |
| type     | string                                                       | 是   | 取消对应的监听事件，支持事件`'playPrevious'`。    |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------- |
| 6600101  | Session service exception. |

**示例：**

```js
controller.off('playPrevious');
```

### on('seekDone')<sup>10+</sup>

on(type: 'seekDone', callback: Callback\<number>): void

设置seek结束的监听事件。

**系统能力：** SystemCapability.Multimedia.AVSession.AVCast

**参数：**

| 参数名   | 类型                                                         | 必填 | 说明                                                         |
| -------- | ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| type     | string                                                       | 是   | 事件回调类型，支持事件`'seekDone'`：当seek结束时，触发该事件。 |
| callback | Callback\<number\>         | 是   | 回调函数，返回seek后播放的位置                      |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ------------------------------ |
| 6600101  | Session service exception. |

**示例：**

```js
controller.on('seekDone', (pos) => {
    console.info(`on seekDone pos：${pos} `);
});
```

### off('seekDone')<sup>10+</sup>

off(type: 'seekDone'): void

取消设置seek结束的监听事件。

**系统能力：** SystemCapability.Multimedia.AVSession.AVCast

**参数：**

| 参数名   | 类型                                                         | 必填 | 说明                                                     |
| -------- | ------------------------------------------------------------ | ---- | ----------------------------------------------------- |
| type     | string                                                       | 是   | 取消对应的监听事件，支持事件`'seekDone'`。    |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------- |
| 6600101  | Session service exception. |

**示例：**

```js
controller.off('seekDone');
```

### on('error')<sup>10+</sup>

on(type: 'error', callback: ErrorCallback): void

监听远端播放器的错误事件，该事件仅用于错误提示，不需要用户停止播控动作。

**系统能力：** SystemCapability.Multimedia.AVSession.AVCast

**参数：**

| 参数名   | 类型     | 必填 | 说明                                                         |
| -------- | -------- | ---- | ------------------------------------------------------------ |
| type     | string   | 是   | 错误事件回调类型，支持的事件：'error'，用户操作和系统都会触发此事件。 |
| callback | function | 是   | 错误事件回调方法：远端播放过程中发生的错误，会提供错误码ID和错误信息。 |

**错误码：**

以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-media.md)。

| 错误码ID | 错误信息              |
| -------- | --------------------- |
| 5400101  | No memory.            |
| 5400102  | Operation not allowed.   |
| 5400103  | I/O error.             |
| 5400104  | Time out.      |
| 5400105  | Service died.         |
| 5400106  | Unsupport format.     |

**示例：**

```js
controller.on('error', (error) => {
  console.error('error happened,and error message is :' + error.message)
  console.error('error happened,and error code is :' + error.code)
})
```

### off('error')<sup>10+</sup>

off(type: 'error'): void

取消监听播放的错误事件。

**系统能力：** SystemCapability.Multimedia.AVSession.AVCast

**参数：**

| 参数名 | 类型   | 必填 | 说明                                      |
| ------ | ------ | ---- | ----------------------------------------- |
| type   | string | 是   | 错误事件回调类型，取消注册的事件：'error' |

**错误码：**

以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-media.md)。

| 错误码ID | 错误信息              |
| -------- | --------------------- |
| 5400101  | No memory.            |
| 5400102  | Operation not allowed.   |
| 5400103  | I/O error.             |
| 5400104  | Time out.      |
| 5400105  | Service died.         |
| 5400106  | Unsupport format.     |

**示例：**

```js
controller.off('error')
```

### sendControlCommand<sup>10+</sup>

sendControlCommand(command: AVCastControlCommand): Promise\<void>

通过控制器发送命令到其对应的会话。结果通过Promise异步回调方式返回。


**系统能力：** SystemCapability.Multimedia.AVSession.AVCast

**参数：**

| 参数名    | 类型                                  | 必填 | 说明                           |
| ------- | ------------------------------------- | ---- | ------------------------------ |
| command | [AVCastControlCommand](#avcastcontrolcommand10) | 是   | 会话的相关命令和命令相关参数。 |

**返回值：**

| 类型           | 说明                          |
| -------------- | ----------------------------- |
| Promise\<void> | Promise对象。当命令发送成功，无返回结果，否则返回错误对象。 |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |
| 6600105  | Invalid session command. |
| 6600109  | The remote connection is not established. |

**示例：**

```js
let avCommand = {command:'play'};
// let avCommand = {command:'pause'};
// let avCommand = {command:'stop'};
// let avCommand = {command:'playNext'};
// let avCommand = {command:'playPrevious'};
// let avCommand = {command:'fastForward'};
// let avCommand = {command:'rewind'};
// let avCommand = {command:'seek', parameter:10};
controller.sendControlCommand(avCommand).then(() => {
    console.info(`SendControlCommand successfully`);
}).catch((err) => {
    console.info(`SendControlCommand BusinessError: code: ${err.code}, message: ${err.message}`);
});
```

### sendControlCommand<sup>10+</sup>

sendControlCommand(command: AVCastControlCommand, callback: AsyncCallback\<void>): void

通过会话控制器发送命令到其对应的会话。结果通过callback异步回调方式返回。


**系统能力：** SystemCapability.Multimedia.AVSession.AVCast

**参数：**

| 参数名   | 类型                                  | 必填 | 说明                           |
| -------- | ------------------------------------- | ---- | ------------------------------ |
| command  | [AVCastControlCommand](#avcastcontrolcommand10) | 是   | 会话的相关命令和命令相关参数。 |
| callback | AsyncCallback\<void>                  | 是   | 回调函数。当命令发送成功，err为undefined，否则返回错误对象。                     |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ------------------------------- |
| 6600101  | Session service exception. |
| 6600105  | Invalid session command. |
| 6600109  | The remote connection is not established. |

**示例：**

```js
let avCommand = {command:'play'};
// let avCommand = {command:'pause'};
// let avCommand = {command:'stop'};
// let avCommand = {command:'playNext'};
// let avCommand = {command:'playPrevious'};
// let avCommand = {command:'fastForward'};
// let avCommand = {command:'rewind'};
// let avCommand = {command:'seek', parameter:10};
controller.sendControlCommand(avCommand, function (err) {
    if (err) {
        console.info(`SendControlCommand BusinessError: code: ${err.code}, message: ${err.message}`);
    } else {
        console.info(`SendControlCommand successfully`);
    }
});
```

### prepare<sup>10+</sup>

prepare(item: AVQueueItem, callback: AsyncCallback\<void>): void

启动播放某个媒体资源。结果通过callback异步回调方式返回。

**系统能力：** SystemCapability.Multimedia.AVSession.AVCast

**参数：**

| 参数名    | 类型                                  | 必填 | 说明                           |
| ------- | ------------------------------------- | ---- | ------------------------------ |
| item | [AVQueueItem](#avqueueitem10) | 是   | 播放列表中单项的相关属性。 |
| callback | AsyncCallback\<void>                  | 是   | 回调函数。当命令发送成功，err为undefined，否则返回错误对象。    

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |

**示例：**

```js
// 设置播放参数，开始播放
var playItem = {
    itemId: 0,
    description: {
    mediaId: '12345',
    mediaName: 'song1',
    mediaType: 'AUDIO',
    mediaUri: 'http://resource1_address',
    mediaSize: 12345,
    startPosition: 0,
    duration: 0,
    artist: 'mysong',
    albumTitle: 'song1_title',
    albumCoverUri: "http://resource1_album_address",
    lyricUri: "http://resource1_lyric_address",
    iconUri: "http://resource1_icon_address",
    appName: 'MyMusic'
    }
};
// 准备播放，这个不会触发真正的播放，会进行加载和缓冲
controller.prepare(playItem, () => {
  console.info('prepare done');
});
// 启动播放
controller.start(playItem, () => {
  console.info('play done');
});
```


### prepare<sup>10+</sup>

prepare(item: AVQueueItem): Promise\<void>

启动播放某个媒体资源。结果通过Promise异步回调方式返回。


**系统能力：** SystemCapability.Multimedia.AVSession.AVCast

**参数：**

| 参数名    | 类型                                  | 必填 | 说明                           |
| ------- | ------------------------------------- | ---- | ------------------------------ |
| item | [AVQueueItem](#avqueueitem10) | 是   | 播放列表中单项的相关属性。 |

**返回值：**

| 类型           | 说明                          |
| -------------- | ----------------------------- |
| Promise\<void> | Promise对象。当命令发送成功，无返回结果，否则返回错误对象。 |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |


**示例：**

```js
// 设置播放参数，开始播放
var playItem = {
    itemId: 0,
    description: {
        mediaId: '12345',
        mediaName: 'song1',
        mediaType: 'AUDIO',
        mediaUri: 'http://resource1_address',
        mediaSize: 12345,
        startPosition: 0,
        duration: 0,
        artist: 'mysong',
        albumTitle: 'song1_title',
        albumCoverUri: "http://resource1_album_address",
        lyricUri: "http://resource1_lyric_address",
        iconUri: "http://resource1_icon_address",
        appName: 'MyMusic'
    }
};
// 准备播放，这个不会触发真正的播放，会进行加载和缓冲
controller.prepare(playItem, () => {
    console.info('prepare done');
});
// 启动播放
controller.start(playItem).then(() => {
    console.info(`start successfully`);
}).catch((err) => {
    console.info(`start BusinessError: code: ${err.code}, message: ${err.message}`);
});
```

### start<sup>10+</sup>

start(item: AVQueueItem, callback: AsyncCallback\<void>): void

启动播放某个媒体资源。结果通过callback异步回调方式返回。

**系统能力：** SystemCapability.Multimedia.AVSession.AVCast

**参数：**

| 参数名    | 类型                                  | 必填 | 说明                           |
| ------- | ------------------------------------- | ---- | ------------------------------ |
| item | [AVQueueItem](#avqueueitem10) | 是   | 播放列表中单项的相关属性。 |
| callback | AsyncCallback\<void>                  | 是   | 回调函数。当命令发送成功，err为undefined，否则返回错误对象。    

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |

**示例：**

```js
// 设置播放参数，开始播放
var playItem = {
itemId: 0,
description: {
  mediaId: '12345',
  mediaName: 'song1',
  mediaType: 'AUDIO',
  mediaUri: 'http://resource1_address',
  mediaSize: 12345,
  startPosition: 0,
  duration: 0,
  artist: 'mysong',
  albumTitle: 'song1_title',
  albumCoverUri: "http://resource1_album_address",
  lyricUri: "http://resource1_lyric_address",
  iconUri: "http://resource1_icon_address",
  appName: 'MyMusic'
}
};
// 准备播放，这个不会触发真正的播放，会进行加载和缓冲
controller.prepare(playItem, () => {
  console.info('prepare done');
});
// 启动播放
controller.start(playItem, () => {
  console.info('play done');
});
```


### start<sup>10+</sup>

start(item: AVQueueItem): Promise\<void>

启动播放某个媒体资源。结果通过Promise异步回调方式返回。


**系统能力：** SystemCapability.Multimedia.AVSession.AVCast

**参数：**

| 参数名    | 类型                                  | 必填 | 说明                           |
| ------- | ------------------------------------- | ---- | ------------------------------ |
| item | [AVQueueItem](#avqueueitem10) | 是   | 播放列表中单项的相关属性。 |

**返回值：**

| 类型           | 说明                          |
| -------------- | ----------------------------- |
| Promise\<void> | Promise对象。当命令发送成功，无返回结果，否则返回错误对象。 |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |


**示例：**

```js
// 设置播放参数，开始播放
var playItem = {
itemId: 0,
description: {
    mediaId: '12345',
    mediaName: 'song1',
    mediaType: 'AUDIO',
    mediaUri: 'http://resource1_address',
    mediaSize: 12345,
    startPosition: 0,
    duration: 0,
    artist: 'mysong',
    albumTitle: 'song1_title',
    albumCoverUri: "http://resource1_album_address",
    lyricUri: "http://resource1_lyric_address",
    iconUri: "http://resource1_icon_address",
    appName: 'MyMusic'
}
};
// 准备播放，这个不会触发真正的播放，会进行加载和缓冲
controller.prepare(playItem, () => {
    console.info('prepare done');
});
// 启动播放
controller.start(playItem).then(() => {
    console.info(`start successfully`);
}).catch((err) => {
    console.info(`start BusinessError: code: ${err.code}, message: ${err.message}`);
});
```

### stopCasting<sup>10+</sup>

stopCasting(callback: AsyncCallback\<void>): void

结束投播。结果通过callback异步回调方式返回。

**系统能力：** SystemCapability.Multimedia.AVSession.AVCast

**参数：**

| 参数名   | 类型                                  | 必填 | 说明                                  |
| -------- | ------------------------------------- | ---- | ------------------------------------- |
| callback | AsyncCallback\<void>                  | 是   | 回调函数。当命令发送成功，err为undefined，否则返回错误对象。 |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600109  | The remote connection is not established. |

**示例：**

```js
avSession.stopCasting(function (err) {
    if (err) {
        console.info(`stopCasting BusinessError: code: ${err.code}, message: ${err.message}`);
    } else {
        console.info(`stopCasting successfully`);
    }
});
```

### stopCasting<sup>10+</sup>

stopCasting(): Promise\<void>

结束投播。结果通过Promise异步回调方式返回。

**系统能力：** SystemCapability.Multimedia.AVSession.AVCast

**返回值：**

| 类型           | 说明                          |
| -------------- | ----------------------------- |
| Promise\<void> | Promise对象。当停止投播索成功，无返回结果，否则返回错误对象。 |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600109  | The remote connection is not established. |

**示例：**

```js
avSession.stopCasting().then(() => {
    console.info(`stopCasting successfully`);
}).catch((err) => {
    console.info(`stopCasting BusinessError: code: ${err.code}, message: ${err.message}`);
});
```

### getCurrentItem<sup>10+</sup>

getCurrentItem(callback: AsyncCallback\<AVQueueItem>): void

获取当前投播的资源信息。结果通过callback异步回调方式返回。

**系统能力：** SystemCapability.Multimedia.AVSession.AVCast

**参数：**

| 参数名   | 类型                                  | 必填 | 说明                                  |
| -------- | ------------------------------------- | ---- | ------------------------------------- |
| callback | AsyncCallback\<[AVQueueItem](#avqueueitem10)>                  | 是   | 回调函数。当命令发送成功，err为undefined，否则返回错误对象。 |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |


### getCurrentItem<sup>10+</sup>

getCurrentItem(): Promise\<AVQueueItem>

结束投播。结果通过Promise异步回调方式返回。

**系统能力：** SystemCapability.Multimedia.AVSession.AVCast

**返回值：**

| 类型           | 说明                          |
| -------------- | ----------------------------- |
| Promise\<[AVQueueItem](#avqueueitem10)> | Promise对象，返回当前的播放资源，否则返回错误对象。 |

**错误码：**
以下错误码的详细介绍请参见[媒体会话管理错误码](../errorcodes/errorcode-avsession.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 6600101  | Session service exception. |


## SessionToken

会话令牌的信息。

**需要权限：** ohos.permission.MANAGE_MEDIA_RESOURCES，仅系统应用可用。

**系统能力：** SystemCapability.Multimedia.AVSession.Manager

**系统接口：** 该接口为系统接口。

| 名称      | 类型   | 必填 | 说明         |
| :-------- | :----- | :--- | :----------- |
| sessionId | string | 是   | 会话ID       |
| pid       | number | 否   | 会话的进程ID |
| uid       | number | 否   | 用户ID       |

## AVSessionType<sup>10+<sup>
当前会话支持的会话类型。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

| 名称  | 类型   | 说明 |
| ----- | ------ | ---- |
| audio | string | 音频 |
| video | string | 视频 |

## AVSessionDescriptor

会话的相关描述信息。

**系统能力：** SystemCapability.Multimedia.AVSession.Manager

**系统接口：** 该接口为系统接口。

| 名称         | 类型                                                         | 可读 | 可写 | 说明                                                |
| ------------ | ------------------------------------------------------------ | ---- | --------------------------------------------------- | --------------------------------------------------- |
| sessionId    | string                                                       | 是  | 否 | 会话ID                                              |
| type         | [AVSessionType](#avsessiontype10)                              | 是   | 否  | 会话类型                                            |
| sessionTag   | string                                                       | 是   | 否  | 会话的自定义名称                                    |
| elementName  | [ElementName](js-apis-bundle-ElementName.md)                 | 是   | 否  | 会话所属应用的信息（包含bundleName、abilityName等） |
| isActive     | boolean                                                      | 是   | 否  | 会话是否被激活                                      |
| isTopSession | boolean                                                      | 是   | 否  | 会话是否为最新的会话                                |
| outputDevice | [OutputDeviceInfo](#outputdeviceinfo10)                        | 是   | 否  | 分布式设备相关信息                                  |

## AVControlCommandType<sup>10+</sup>

会话可传递的命令。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

| 名称           | 类型   | 说明         |
| -------------- | ------ | ------------ |
| play           | string | 播放         |
| pause          | string | 暂停         |
| stop           | string | 停止         |
| playNext       | string | 下一首       |
| playPrevious   | string | 上一首       |
| fastForward    | string | 快进         |
| rewind         | string | 快退         |
| seek           | string | 跳转某一节点 |
| setSpeed       | string | 设置播放倍速 |
| setLoopMode    | string | 设置循环模式 |
| toggleFavorite | string | 是否收藏     |

## AVControlCommand<sup>10+</sup>

会话接受的命令的对象描述。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

| 名称      | 类型                                              | 必填 | 说明           |
| --------- | ------------------------------------------------- | ---- | -------------- |
| command   | [AVControlCommandType](#avcontrolcommandtype10)     | 是   | 命令           |
| parameter | [LoopMode](#loopmode10) &#124; string &#124; number | 否   | 命令对应的参数 |

## AVCastControlCommandType<sup>10+</sup>

投播控制器可传递的命令。

**系统能力：** SystemCapability.Multimedia.AVSession.AVCast

| 名称           | 类型   | 说明         |
| -------------- | ------ | ------------ |
| play           | string | 播放         |
| pause          | string | 暂停         |
| stop           | string | 停止         |
| playNext       | string | 下一首       |
| playPrevious   | string | 上一首       |
| fastForward    | string | 快进         |
| rewind         | string | 快退         |
| seek           | numbder | 跳转某一节点 |
| setSpeed       | number | 设置播放倍速 |
| setLoopMode    | string | 设置循环模式 |
| toggleFavorite | string | 是否收藏     |
| setVolume      | number | 设置音量     |

## AVCastControlCommand<sup>10+</sup>

投播控制器接受的命令的对象描述。

**系统能力：** SystemCapability.Multimedia.AVSession.AVCast

| 名称      | 类型                                              | 必填 | 说明           |
| --------- | ------------------------------------------------- | ---- | -------------- |
| command   | [AVCastControlCommandType](#avcastcontrolcommandtype10)     | 是   | 命令           |
| parameter | [LoopMode](#loopmode10) &#124; string &#124; number | 否   | 命令对应的参数 |

## AVMetadata<sup>10+</sup>

媒体元数据的相关属性。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

| 名称            | 类型                      | 必填 | 说明                                                                  |
| --------------- |-------------------------| ---- |---------------------------------------------------------------------|
| assetId         | string                  | 是   | 媒体ID。                                                               |
| title           | string                  | 否   | 标题。                                                                 |
| artist          | string                  | 否   | 艺术家。                                                                |
| author          | string                  | 否   | 专辑作者。                                                               |
| album           | string                  | 否   | 专辑名称。                                                               |
| writer          | string                  | 否   | 词作者。                                                                |
| composer        | string                  | 否   | 作曲者。                                                                |
| duration        | number                  | 否   | 媒体时长，单位毫秒（ms）。                                                  |
| mediaImage      | image.PixelMap &#124; string | 否   | 图片的像素数据或者图片路径地址(本地路径或网络路径)。                             |
| publishDate     | Date                    | 否   | 发行日期。                                                               |
| subtitle        | string                  | 否   | 子标题。                                                                |
| description     | string                  | 否   | 媒体描述。                                                               |
| lyric           | string                  | 否   | 歌词文件路径地址(本地路径或网络路径) |
| previousAssetId | string                  | 否   | 上一首媒体ID。                                                            |
| nextAssetId     | string                  | 否   | 下一首媒体ID。                                                            |

## AVMediaDescription<sup>10+</sup>

播放列表媒体元数据的相关属性。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

| 名称         | 类型                    | 必填  | 说明                     |
| ------------ | ----------------------- | ---- | ----------------------- |
| mediaId      | string                  | 是   | 播放列表媒体ID。          |
| title        | string                  | 否   | 播放列表媒体标题。        |
| subtitle     | string                  | 否   | 播放列表媒体子标题。      |
| description  | string                  | 否   | 播放列表媒体描述的文本。   |
| icon         | image.PixelMap          | 否   | 播放列表媒体图片像素数据。 |
| iconUri      | string                  | 否   | 播放列表媒体图片路径地址。 |
| extras       | {[key: string]: any}    | 否   | 播放列表媒体额外字段。     |
| mediaUri     | string                  | 否   | 播放列表媒体URI。         |
| mediaType     | string                  | 否   | 播放列表媒体类型。         |
| mediaSize     | number                  | 否   | 播放列表媒体的大小。         |
| albumTitle     | string                  | 否   | 播放列表媒体专辑标题。         |
| albumCoverUri     | string                  | 否   | 播放列表媒体专辑标题URI。    |
| lyricContent     | string                  | 否   | 播放列表媒体歌词内容。         |
| lyricUri     | string                  | 否   | 播放列表媒体歌词URI。         |
| artist     | string                  | 否   | 播放列表媒体专辑作者。         |
| fdSrc     | media.AVFileDescriptor        | 否   | 播放列表媒体本地文件的句柄。         |
| duration     | number                  | 否   | 播放列表媒体播放时长。         |
| startPosition     | number                  | 否   | 播放列表媒体起始播放位置。         |
| creditsPosition     | number                  | 否   | 播放列表媒体的片尾播放位置。         |
| appName     | string                  | 否   | 播放列表提供的应用的名字。         |

## AVQueueItem<sup>10+</sup>

播放列表中单项的相关属性。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

| 名称         | 类型                                        | 必填 | 说明                        |
| ------------ | ------------------------------------------ | ---- | --------------------------- |
| itemId       | number                                     | 是   | 播放列表中单项的ID。          |
| description  | [AVMediaDescription](#avmediadescription10)  | 是   | 播放列表中单项的媒体元数据。   |

## AVPlaybackState<sup>10+</sup>

媒体播放状态的相关属性。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

| 名称         | 类型                                  | 必填 | 说明     |
| ------------ | ------------------------------------- | ---- | ------- |
| state        | [PlaybackState](#playbackstate)       | 否   | 播放状态 |
| speed        | number                                | 否   | 播放倍速 |
| position     | [PlaybackPosition](#playbackposition) | 否   | 播放位置 |
| bufferedTime | number                                | 否   | 缓冲时间 |
| loopMode     | [LoopMode](#loopmode10)                 | 否   | 循环模式 |
| isFavorite   | boolean                               | 否   | 是否收藏 |
| activeItemId<sup>10+</sup> | number                  | 否   | 正在播放的媒体Id |
| volume<sup>10+</sup> | number                  | 否   | 正在播放的媒体音量 |
| extras<sup>10+</sup> | {[key: string]: Object}       | 否   | 自定义媒体数据 |

## PlaybackPosition<sup>10+</sup>

媒体播放位置的相关属性。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

| 名称        | 类型   | 必填 | 说明               |
| ----------- | ------ | ---- | ------------------ |
| elapsedTime | number | 是   | 已用时间，单位毫秒（ms）。 |
| updateTime  | number | 是   | 更新时间，单位毫秒（ms）。 |

## AVCastCategory<sup>10+</sup>

播放设备的类别枚举。

**系统能力：** SystemCapability.Multimedia.AVSession.AVCast

| 名称                        | 值   | 说明         |
| --------------------------- | ---- | ----------- |
| CATEGORY_LOCAL      | 0    | 本地播放，默认播放设备，声音从本机或者连接的蓝牙耳机设备出声。     |
| CATEGORY_REMOTE      | 1    | 远端播放，远端播放设备，声音从其他设备发出声音或者画面。  |

## ConnectionState<sup>10+</sup>

播放设备的类别枚举。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

| 名称                        | 值   | 说明         |
| --------------------------- | ---- | ----------- |
| STATE_CONNECTING      | 0    | 设备连接中    |
| STATE_CONNECTED      | 1    | 设备连接成功 |
| STATE_DISCONNECTED      | 6    | 设备断开连接 |

## ProtocolType<sup>10+</sup>

远端设备支持的协议类型。

**系统能力：** SystemCapability.Multimedia.AVSession.AVCast

**系统接口：** 该接口为系统接口。

| 名称                        | 值   | 说明         |
| --------------------------- | ---- | ----------- |
| TYPE_LOCAL      | 0    | 本地设备    |
| TYPE_CAST_PLUS_MIRROR      | 1    | Cast+的镜像模式 |
| TYPE_CAST_PLUS_STREAM      | 2    | Cast+的Stream模式 |

## DeviceType<sup>10+</sup>

播放设备的类型枚举。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

| 名称                        | 值   | 说明         |
| --------------------------- | ---- | ----------- |
| DEVICE_TYPE_LOCAL      | 0    | 本地播放类型     |
| DEVICE_TYPE_BLUETOOTH      | 10   | 蓝牙设备  |
| DEVICE_TYPE_TV      | 2    | 电视 <br> **系统能力：** SystemCapability.Multimedia.AVSession.AVCast |
| DEVICE_TYPE_SMART_SPEAKER      | 3   | 音箱设备 <br> **系统能力：** SystemCapability.Multimedia.AVSession.AVCast |

## DeviceInfo<sup>10+</sup>

播放设备的相关信息。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

| 名称       | 类型           | 必填 | 说明                   |
| ---------- | -------------- | ---- | ---------------------- |
| castCategory   | AVCastCategory        | 是   | 播放设备的类别         |
| deviceId   | string | 是   | 播放设备的ID。  |
| deviceName | string | 是   | 播放设备的名称。    |
| deviceType | DeviceType | 是   | 播放设备的类型。    |
| ipAddress | string | 否   | 播放设备的ip地址。<br/>此接口为系统接口。<br> **系统能力：** SystemCapability.Multimedia.AVSession.AVCast     |
| providerId | number | 否   | 播放设备提供商。<br/>此接口为系统接口。<br> **系统能力：** SystemCapability.Multimedia.AVSession.AVCast    |

## OutputDeviceInfo<sup>10+</sup>

播放设备的相关信息。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

| 名称       | 类型           | 必填 | 说明                   |
| ---------- | -------------- | ---- | ---------------------- |
| devices | Array\<DeviceInfo\> | 是   | 播放设备的集合。    |

## PlaybackState<sup>10+</sup>

表示媒体播放状态的枚举。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

| 名称                        | 值   | 说明         |
| --------------------------- | ---- | ----------- |
| PLAYBACK_STATE_INITIAL      | 0    | 初始状态     |
| PLAYBACK_STATE_PREPARE      | 1    | 播放准备状态  |
| PLAYBACK_STATE_PLAY         | 2    | 正在播放     |
| PLAYBACK_STATE_PAUSE        | 3    | 暂停         |
| PLAYBACK_STATE_FAST_FORWARD | 4    | 快进         |
| PLAYBACK_STATE_REWIND       | 5    | 快退         |
| PLAYBACK_STATE_STOP         | 6    | 停止         |
| PLAYBACK_STATE_COMPLETED    | 7    | 播放完成     |
| PLAYBACK_STATE_RELEASED     | 8    | 释放         |
| PLAYBACK_STATE_ERROR        | 9    | 错误         |


## LoopMode<sup>10+</sup>

表示媒体播放循环模式的枚举。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

| 名称               | 值   | 说明     |
| ------------------ | ---- | -------- |
| LOOP_MODE_SEQUENCE | 0    | 顺序播放 |
| LOOP_MODE_SINGLE   | 1    | 单曲循环 |
| LOOP_MODE_LIST     | 2    | 表单循环 |
| LOOP_MODE_SHUFFLE  | 3    | 随机播放 |

## AVSessionErrorCode<sup>10+</sup>

会话发生错误时的错误码。

**系统能力：** SystemCapability.Multimedia.AVSession.Core

| 名称                                   | 值      | 说明                             |
| -------------------------------------- | ------- | ------------------------------- |
| ERR_CODE_SERVICE_EXCEPTION             | 6600101 | Session service exception.               |
| ERR_CODE_SESSION_NOT_EXIST             | 6600102 | The session does not exist.      |
| ERR_CODE_CONTROLLER_NOT_EXIST          | 6600103 | The session controller does not exist.   |
| ERR_CODE_REMOTE_CONNECTION_ERR         | 6600104 | The remote session  connection failed.         |
| ERR_CODE_COMMAND_INVALID               | 6600105 | Invalid session command.           |
| ERR_CODE_SESSION_INACTIVE              | 6600106 | The session is not activated.                |
| ERR_CODE_MESSAGE_OVERLOAD              | 6600107 | Too many commands or events.       |
| ERR_CODE_DEVICE_CONNECTION_FAILED      | 6600108 | Device connecting failed.       |
| ERR_CODE_REMOTE_CONNECTION_NOT_EXIST   | 6600109 | The remote connection is not established.       |

<!--no_check-->
