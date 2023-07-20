# 长时任务开发指导

## 场景说明

如果应用需要在后台长时间执行用户可感知的任务，如后台播放音乐、导航、设备连接、VoIP等，则使用长时任务避免进入挂起（Suspend）状态。
长时任务在后台执行没有时间限制。为了避免该机制被滥用，系统只允许申请有限个数的长时任务类型，同时会有相应的通知提示与长时任务相关联，使用户可感知，并且系统会添加相应的校验机制，确保应用是的确在执行相应的长时任务。

## 接口说明

**表1** 长时任务主要接口

| 接口名                                      | 描述                           |
| ---------------------------------------- | ---------------------------- |
| startBackgroundRunning(context: Context, bgMode: BackgroundMode, wantAgent: WantAgent): Promise&lt;void&gt; | 服务启动后，向系统申请长时任务，使服务一直保持后台运行。 |
| stopBackgroundRunning(context: Context): Promise&lt;void&gt; | 停止后台长时任务的运行。                 |


其中，wantAgent的信息详见（[WantAgent](../reference/apis/js-apis-app-ability-wantAgent.md)）

**表2** 后台模式类型

| 参数名                     | 描述             | 配置项                   |
| ----------------------- | -------------- | --------------------- |
| DATA_TRANSFER           | 数据传输           | dataTransfer          |
| AUDIO_PLAYBACK          | 音频播放           | audioPlayback         |
| AUDIO_RECORDING         | 录音             | audioRecording        |
| LOCATION                | 定位导航           | location              |
| BLUETOOTH_INTERACTION   | 蓝牙相关           | bluetoothInteraction  |
| MULTI_DEVICE_CONNECTION | 多设备互联          | multiDeviceConnection |
| WIFI_INTERACTION        | WLAN相关（系统保留）   | wifiInteraction       |
| VOIP                    | 音视频通话（系统保留）    | voip                  |
| TASK_KEEPING            | 计算任务（仅供特定设备使用） | taskKeeping           |


## 开发步骤

### 基于Stage模型

Stage模型的相关信息参考[Stage模型开发概述](../application-models/stage-model-development-overview.md)。

1、在module.json5文件中配置长时任务权限ohos.permission.KEEP_BACKGROUND_RUNNING、同时为需要使用长时任务的ability声明相应的后台模式类型。

```
"module": {
    "abilities": [
        {
            "backgroundModes": [
            "dataTransfer",
            "location"
            ], // 后台模式类型
        }
    ],
    "requestPermissions": [
        {
            "name": "ohos.permission.KEEP_BACKGROUND_RUNNING"  // 长时任务权限
        }
    ]
}
```

2、在应用内执行长时任务时，由于元能力启动管控规则限制，不支持同应用通过startAbilityByCall的形式在后台创建并运行Ability。可以直接在page中，执行相应的代码。Stage模型的Ability使用参考[Stage模型开发指导-UIAbility组件](../application-models/uiability-overview.md)。

```ts
import wantAgent from '@ohos.app.ability.wantAgent';
import backgroundTaskManager from '@ohos.resourceschedule.backgroundTaskManager';

@Entry
@Component
struct Index {
  @State message: string = 'test'
  // 通过getContext方法，来获取page所在的Ability上下文。
  private context: any = getContext(this)

  startContinuousTask() {
    let wantAgentInfo = {
      // 点击通知后，将要执行的动作列表
      wants: [
        {
          bundleName: "com.example.myapplication",
          abilityName: "EntryAbility",
        }
      ],
      // 点击通知后，动作类型
      operationType: wantAgent.OperationType.START_ABILITY,
      // 使用者自定义的一个私有值
      requestCode: 0,
      // 点击通知后，动作执行属性
      wantAgentFlags: [wantAgent.WantAgentFlags.UPDATE_PRESENT_FLAG]
    };

    // 通过wantAgent模块的getWantAgent方法获取WantAgent对象
    try {
        wantAgent.getWantAgent(wantAgentInfo).then((wantAgentObj) => {
            try {
                backgroundTaskManager.startBackgroundRunning(this.context,
                    backgroundTaskManager.BackgroundMode.DATA_TRANSFER, wantAgentObj).then(() => {
                    console.info("Operation startBackgroundRunning succeeded");
                }).catch((err) => {
                    console.error("Operation startBackgroundRunning failed Cause: " + err);
                });
            } catch (error) {
                console.error(`Operation startBackgroundRunning failed. code is ${error.code} message is ${error.message}`);
            }
        });
    } catch (error) {
        console.error(`Operation getWantAgent failed. code is ${error.code} message is ${error.message}`);
    }
  }

  stopContinuousTask() {
    try {
        backgroundTaskManager.stopBackgroundRunning(this.context).then(() => {
        console.info("Operation stopBackgroundRunning succeeded");
        }).catch((err) => {
        console.error("Operation stopBackgroundRunning failed Cause: " + err);
        });
    } catch (error) {
        console.error(`Operation stopBackgroundRunning failed. code is ${error.code} message is ${error.message}`);
    }
  }

  build() {
    Row() {
      Column() {
        Text("Index")
          .fontSize(50)
          .fontWeight(FontWeight.Bold)

        Button() { Text('申请长时任务').fontSize(25).fontWeight(FontWeight.Bold) }.type(ButtonType.Capsule)
        .margin({ top: 10 }).backgroundColor('#0D9FFB').width(250).height(40)
        .onClick(() => {
          // 通过按钮申请长时任务
          this.startContinuousTask();

          // 此处执行具体的长时任务逻辑，如放音等。
        })

        Button() { Text('取消长时任务').fontSize(25).fontWeight(FontWeight.Bold) }.type(ButtonType.Capsule)
        .margin({ top: 10 }).backgroundColor('#0D9FFB').width(250).height(40)
        .onClick(() => {
          // 此处结束具体的长时任务的执行

          // 通过按钮取消长时任务
          this.stopContinuousTask();
        })
      }
      .width('100%')
    }
    .height('100%')
  }
}
```

3、当需要跨设备或者跨应用在后台执行长时任务时，可以通过Call的方式在后台创建并运行Ability。使用方式参考[Call调用开发指南（同设备）](../application-models/uiability-intra-device-interaction.md#通过call调用实现uiability交互仅对系统应用开放)，[Call调用开发指南（跨设备）](../application-models/hop-multi-device-collaboration.md#通过跨设备call调用实现多端协同)。

```ts
import UIAbility from '@ohos.app.ability.UIAbility';
import backgroundTaskManager from '@ohos.resourceschedule.backgroundTaskManager';
import wantAgent from '@ohos.app.ability.wantAgent';

const MSG_SEND_METHOD: string = 'CallSendMsg';

let mContext = null;

function startContinuousTask() {
    let wantAgentInfo = {
        // 点击通知后，将要执行的动作列表
        wants: [
            {
                bundleName: "com.example.myapplication",
                abilityName: "EntryAbility",
            }
        ],
        // 点击通知后，动作类型
        operationType: wantAgent.OperationType.START_ABILITY,
        // 使用者自定义的一个私有值
        requestCode: 0,
        // 点击通知后，动作执行属性
        wantAgentFlags: [wantAgent.WantAgentFlags.UPDATE_PRESENT_FLAG]
    };

    // 通过wantAgent模块的getWantAgent方法获取WantAgent对象
    try {
        wantAgent.getWantAgent(wantAgentInfo).then((wantAgentObj) => {
            try {
                backgroundTaskManager.startBackgroundRunning(mContext,
                    backgroundTaskManager.BackgroundMode.DATA_TRANSFER, wantAgentObj).then(() => {
                    console.info("Operation startBackgroundRunning succeeded");
                }).catch((error) => {
                    console.error(`Operation startBackgroundRunning failed. code is ${error.code} message is ${error.message}`);
                });
            } catch (error) {
                console.error(`Operation startBackgroundRunning failed. code is ${error.code} message is ${error.message}`);
            }
        });
    } catch (error) {
        console.error(`Operation getWantAgent failed. code is ${error.code} message is ${error.message}`);
    }
}

function stopContinuousTask() {
    try {
        backgroundTaskManager.stopBackgroundRunning(mContext).then(() => {
            console.info("Operation stopBackgroundRunning succeeded");
        }).catch((error) => {
            console.error(`Operation stopBackgroundRunning failed. code is ${error.code} message is ${error.message}`);
        });
    } catch (error) {
        console.error(`Operation stopBackgroundRunning failed. code is ${error.code} message is ${error.message}`);
    }
}

class MyParcelable {
    num: number = 0;
    str: String = "";

    constructor(num, string) {
        this.num = num;
        this.str = string;
    }

    marshalling(messageSequence) {
        messageSequence.writeInt(this.num);
        messageSequence.writeString(this.str);
        return true;
    }

    unmarshalling(messageSequence) {
        this.num = messageSequence.readInt();
        this.str = messageSequence.readString();
        return true;
    }
}

function sendMsgCallback(data) {
    console.info('BgTaskAbility funcCallBack is called ' + data)
    let receivedData = new MyParcelable(0, "")
    data.readParcelable(receivedData)
    console.info(`receiveData[${receivedData.num}, ${receivedData.str}]`)
    // 可以根据Caller端发送的序列化数据的str值，执行不同的方法。
    if (receivedData.str === 'start_bgtask') {
        startContinuousTask()
    } else if (receivedData.str === 'stop_bgtask') {
        stopContinuousTask();
    }
    return new MyParcelable(10, "Callee test");
}

export default class BgTaskAbility extends UIAbility {
    onCreate(want, launchParam) {
        console.info("[Demo] BgTaskAbility onCreate")
        this.callee.on("test", sendMsgCallback);

        try {
            this.callee.on(MSG_SEND_METHOD, sendMsgCallback)
        } catch (error) {
            console.error(`${MSG_SEND_METHOD} register failed with error ${JSON.stringify(error)}`)
        }
        mContext = this.context;
    }

    onDestroy() {
        console.info("[Demo] BgTaskAbility onDestroy")
    }

    onWindowStageCreate(windowStage) {
        console.info("[Demo] BgTaskAbility onWindowStageCreate")

        windowStage.loadContent("pages/index").then((data)=> {
            console.info(`load content succeed with data ${JSON.stringify(data)}`)
        }).catch((error)=>{
            console.error(`load content failed with error ${JSON.stringify(error)}`)
        })
    }

    onWindowStageDestroy() {
        console.info("[Demo] BgTaskAbility onWindowStageDestroy")
    }

    onForeground() {
        console.info("[Demo] BgTaskAbility onForeground")
    }

    onBackground() {
        console.info("[Demo] BgTaskAbility onBackground")
    }
};
```

### 基于FA模型

基于FA的Service Ability使用，参考[ServiceAbility开发指导](../application-models/serviceability-overview.md)。

当不需要与后台执行的长时任务交互时，可以采用startAbility()方法启动Service Ability。并在Service Ability的onStart回调方法中，调用长时任务的申请接口，声明此服务需要在后台长时运行。当任务执行完，再调用长时任务取消接口，及时释放资源。

当需要与后台执行的长时任务交互时（如播放音乐等）。可以采用connectAbility()方法启动并连接Service Ability。在获取到服务的代理对象后，与服务进行通信，控制长时任务的申请和取消。

1、在config.json文件中配置长时任务权限ohos.permission.KEEP_BACKGROUND_RUNNING、同时为需要使用长时任务的Service Ability声明相应的后台模式类型。

```json
"module": {
    "package": "com.example.myapplication",
    "abilities": [
        {
            "backgroundModes": [
            "dataTransfer",
            "location"
            ], // 后台模式类型
            "type": "service"  // ability类型为service
        }
    ],
    "reqPermissions": [
        {
            "name": "ohos.permission.KEEP_BACKGROUND_RUNNING"  // 长时任务权限
        }
    ]
}
```

2、在Service Ability调用长时任务的申请和取消接口。

```js
import backgroundTaskManager from '@ohos.resourceschedule.backgroundTaskManager';
import featureAbility from '@ohos.ability.featureAbility';
import wantAgent from '@ohos.app.ability.wantAgent';
import rpc from "@ohos.rpc";

function startContinuousTask() {
    let wantAgentInfo = {
        // 点击通知后，将要执行的动作列表
        wants: [
            {
                bundleName: "com.example.myapplication",
                abilityName: "EntryAbility"
            }
        ],
        // 点击通知后，动作类型
        operationType: wantAgent.OperationType.START_ABILITY,
        // 使用者自定义的一个私有值
        requestCode: 0,
        // 点击通知后，动作执行属性
        wantAgentFlags: [wantAgent.WantAgentFlags.UPDATE_PRESENT_FLAG]
    };

    // 通过wantAgent模块的getWantAgent方法获取WantAgent对象
    try {
        wantAgent.getWantAgent(wantAgentInfo).then((wantAgentObj) => {
            try {
                backgroundTaskManager.startBackgroundRunning(featureAbility.getContext(),
                    backgroundTaskManager.BackgroundMode.DATA_TRANSFER, wantAgentObj).then(() => {
                    console.info("Operation startBackgroundRunning succeeded");
                }).catch((err) => {
                    console.error("Operation startBackgroundRunning failed Cause: " + err);
                });
            } catch (error) {
                console.error(`Operation startBackgroundRunning failed. code is ${error.code} message is ${error.message}`);
            }
        });
    } catch (error) {
        console.error(`Operation getWantAgent failed. code is ${error.code} message is ${error.message}`);
    }
}

function stopContinuousTask() {
    try {
        backgroundTaskManager.stopBackgroundRunning(featureAbility.getContext()).then(() => {
            console.info("Operation stopBackgroundRunning succeeded");
        }).catch((err) => {
            console.error("Operation stopBackgroundRunning failed Cause: " + err);
        });
    } catch (error) {
        console.error(`Operation stopBackgroundRunning failed. code is ${error.code} message is ${error.message}`);
    }
}

async function processAsyncJobs() {
    // 此处执行具体的长时任务。

    // 长时任务执行完，调用取消接口，释放资源。
    stopContinuousTask();
}

let mMyStub;

class MyStub extends rpc.RemoteObject {
    constructor(des) {
        if (typeof des === 'string') {
            super(des);
        } else {
            return null;
        }
    }
    onRemoteRequest(code, data, reply, option) {
        console.log('ServiceAbility onRemoteRequest called');
        // code 的具体含义用户自定义
        if (code === 1) {
            // 接收到申请长时任务的请求码
            startContinuousTask();
            // 此处执行具体长时任务
        } else if (code === 2) {
            // 接收到取消长时任务的请求码
            stopContinuousTask();
        } else {
            console.log('ServiceAbility unknown request code');
        }
        return true;
    }
}

export default {
    onStart() {
        console.info('ServiceAbility onStart');
        mMyStub = new MyStub("ServiceAbility-test");
        // 在执行后台长时任前，调用申请接口。
        startContinuousTask();
        processAsyncJobs();
    },
    onStop() {
        console.info('ServiceAbility onStop');
    },
    onConnect(want) {
        console.info('ServiceAbility onConnect');
        return mMyStub;
    },
    onReconnect(want) {
        console.info('ServiceAbility onReconnect');
    },
    onDisconnect() {
        console.info('ServiceAbility onDisconnect');
    },
    onCommand(want, startId) {
        console.info('ServiceAbility onCommand');
    }
};
```

## 相关实例

基于后台任务管理，有以下相关实例可供参考：

- [`ContinuousTask`：长时任务（ArkTS）（API9）](https://gitee.com/openharmony/applications_app_samples/tree/master/code/BasicFeature/TaskManagement/ContinuousTask)