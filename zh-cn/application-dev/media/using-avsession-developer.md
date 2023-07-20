# 媒体会话提供方

音视频应用在实现音视频功能的同时，需要作为媒体会话提供方接入媒体会话，在媒体会话控制方（例如播控中心）中展示媒体相关信息，及响应媒体会话控制方下发的播控命令。

## 基本概念

- 媒体会话元数据（AVMetadata）： 用于描述媒体数据相关属性，包含标识当前媒体的ID（assetId），上一首媒体的ID（previousAssetId），下一首媒体的ID（nextAssetId），标题（title），专辑作者（author），专辑名称（album），词作者（writer），媒体时长（duration）等属性。

- 媒体播放状态（AVPlaybackState）：用于描述媒体播放状态的相关属性，包含当前媒体的播放状态（state）、播放位置（position）、播放倍速（speed）、缓冲时间（bufferedTime）、循环模式（loopMode）、是否收藏（isFavorite）、正在播放的媒体Id（activeItemId）、自定义媒体数据（extras）等属性。

## 接口说明

媒体会话提供方使用的关键接口如下表所示。接口返回值有两种返回形式：callback和promise，下表中为callback形式接口，promise和callback只是返回值方式不一样，功能相同。

更多API说明请参见[API文档](../reference/apis/js-apis-avsession.md)。

| 接口名 | 说明 | 
| -------- | -------- |
| createAVSession(context: Context, tag: string, type: AVSessionType, callback: AsyncCallback&lt;AVSession&gt;): void<sup>10+<sup> | 创建媒体会话。<br/>一个UIAbility只能存在一个媒体会话，重复创建会失败。 | 
| setAVMetadata(data: AVMetadata, callback: AsyncCallback&lt;void&gt;): void<sup>10+<sup> | 设置媒体会话元数据。 | 
| setAVPlaybackState(state: AVPlaybackState, callback: AsyncCallback&lt;void&gt;): void<sup>10+<sup> | 设置媒体会话播放状态。 | 
| setLaunchAbility(ability: WantAgent, callback: AsyncCallback&lt;void&gt;): void<sup>10+<sup> | 设置启动UIAbility。 | 
| getController(callback: AsyncCallback&lt;AVSessionController&gt;): void<sup>10+<sup> | 获取当前会话自身控制器。 | 
| getOutputDevice(callback: AsyncCallback&lt;OutputDeviceInfo&gt;): void<sup>10+<sup> | 获取播放设备相关信息。 |
| activate(callback: AsyncCallback&lt;void&gt;): void<sup>10+<sup> | 激活媒体会话。 | 
| deactivate(callback: AsyncCallback&lt;void&gt;): void<sup>10+<sup> | 禁用当前会话。 |
| destroy(callback: AsyncCallback&lt;void&gt;): void<sup>10+<sup> | 销毁媒体会话。 | 
| setAVQueueItems(items: Array&lt;AVQueueItem&gt;, callback: AsyncCallback&lt;void&gt;): void <sup>10+<sup> | 设置媒体播放列表。 |
| setAVQueueTitle(title: string, callback: AsyncCallback&lt;void&gt;): void<sup>10+<sup> | 设置媒体播放列表名称。 |
| dispatchSessionEvent(event: string, args: {[key: string]: Object}, callback: AsyncCallback&lt;void&gt;): void<sup>10+<sup> | 设置会话内自定义事件。 |
| setExtras(extras: {[key: string]: Object}, callback: AsyncCallback&lt;void&gt;): void<sup>10+<sup> | 设置键值对形式的自定义媒体数据包。|

## 开发步骤

音视频应用作为媒体会话提供方接入媒体会话的基本步骤如下所示：

1. 通过AVSessionManager的方法创建并激活媒体会话。
     
   ```ts
   // 创建媒体会话需要获取应用的上下文（context）。开发者可以在应用的EntryAbility文件中设置一个全局变量来存储应用的上下文
   export default class EntryAbility extends UIAbility {
       onCreate(want, launchParam) {
           globalThis.context = this.context; // 设置一个全局变量globalThis.context来存储应用的上下文
       }
       // 其它EntryAbility类的方法
    }

   // 开始创建并激活媒体会话
   import AVSessionManager from '@ohos.multimedia.avsession'; //导入AVSessionManager模块
   
   // 创建session
   async createSession() {
       let session: AVSessionManager.AVSession = await AVSessionManager.createAVSession(globalThis.context, 'SESSION_NAME', 'audio');
       session.activate();
       console.info(`session create done : sessionId : ${session.sessionId}`);
   }
   ```

2. 跟随媒体信息的变化，及时设置媒体会话信息。需要设置的媒体会话信息主要包括：
   - 媒体会话元数据AVMetadata。
   - 媒体播放状态AVPlaybackState。

   音视频应用设置的媒体会话信息，会被媒体会话控制方通过AVSessionController相关方法获取后进行显示或处理。
     
   ```ts
   async setSessionInfo() {
     // 假设已经创建了一个session，如何创建session可以参考之前的案例
     let session: AVSessionManager.AVSession = ALREADY_CREATE_A_SESSION;
     // 播放器逻辑··· 引发媒体信息与播放状态的变更
     // 设置必要的媒体信息
     let metadata: AVSessionManager.AVMetadata = {
       assetId: '0',
       title: 'TITLE',
       artist: 'ARTIST'
     };
     session.setAVMetadata(metadata).then(() => {
       console.info(`SetAVMetadata successfully`);
     }).catch((err) => {
       console.error(`Failed to set AVMetadata. Code: ${err.code}, message: ${err.message}`);
     });
     // 简单设置一个播放状态 - 暂停 未收藏
     let playbackState: AVSessionManager.AVPlaybackState = {
       state:AVSessionManager.PlaybackState.PLAYBACK_STATE_PAUSE,
       isFavorite:false
     };
     session.setAVPlaybackState(playbackState, function (err) {
       if (err) {
         console.error(`Failed to set AVPlaybackState. Code: ${err.code}, message: ${err.message}`);
       } else {
         console.info(`SetAVPlaybackState successfully`);
       }
     });
     // 设置一个播放列表
     let queueItemDescription_1 = {
       mediaId: '001',
       title: 'music_name',
       subtitle: 'music_sub_name',
       description: 'music_description',
       icon: PIXELMAP_OBJECT,
       iconUri: 'http://www.xxx.com',
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
       icon: PIXELMAP_OBJECT,
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
       console.error(`Failed to set AVQueueItem, error code: ${err.code}, error message: ${err.message}`);
     });
     // 设置媒体播放列表名称
     let queueTitle = 'QUEUE_TITLE';
       session.setAVQueueTitle(queueTitle).then(() => {
         console.info(`SetAVQueueTitle successfully`);
       }).catch((err) => {
       console.info(`Failed to set AVQueueTitle, error code: ${err.code}, error message: ${err.message}`);
     });
   }
   ```

3. 设置用于被媒体会话控制方拉起的UIAbility。当用户操作媒体会话控制方的界面时，例如点击播控中心的卡片，可以拉起此处配置的UIAbility。
   设置UIAbility时通过WantAgent接口实现，更多关于WantAgent的信息请参考[WantAgent](../reference/apis/js-apis-app-ability-wantAgent.md)。
 
   ```ts
   import wantAgent from "@ohos.app.ability.wantAgent";
   ```

   ```ts
   // 假设已经创建了一个session，如何创建session可以参考之前的案例
   let session: AVSessionManager.AVSession = ALREADY_CREATE_A_SESSION;
   let wantAgentInfo = {
       wants: [
           {
               bundleName: 'com.example.musicdemo',
               abilityName: 'com.example.musicdemo.MainAbility'
           }
       ],
       operationType: wantAgent.OperationType.START_ABILITIES,
       requestCode: 0,
       wantAgentFlags: [wantAgent.WantAgentFlags.UPDATE_PRESENT_FLAG]
   }
   wantAgent.getWantAgent(wantAgentInfo).then((agent) => {
       session.setLaunchAbility(agent);
   })
   ```

4. 设置一个即时的自定义会话事件，以供媒体控制方接收到事件后进行相应的操作。

   > **说明：**<br>
   > 通过dispatchSessionEvent方法设置的数据不会保存在会话对象或AVSession服务中。

   ```ts
   // 假设已经创建了一个session，如何创建session可以参考 "1. 通过AVSessionManager的方法创建并激活媒体会话"
   let session: AVSessionManager.AVSession = ALREADY_CREATE_A_SESSION;
   let eventName = 'dynamic_lyric';
   let args = {
     lyric : 'This is my lyric'
   }
   await session.dispatchSessionEvent(eventName, args).then(() => {
      console.info(`Dispatch session event successfully`);
   }).catch((err) => {
      console.error(`Failed to dispatch session event. Code: ${err.code}, message: ${err.message}`);
   })
   ```

5. 设置与当前会话相关的自定义媒体数据包，以供媒体控制方接收到事件后进行相应的操作。

   > **说明：**<br>
   > 通过setExtras方法设置的数据包会被存储在AVSession服务中，数据的生命周期与会话一致；会话对应的Controller可以使用getExtras来获取该数据。

   ```ts
   // 假设已经创建了一个session，如何创建session可以参考之前的案例
   let session: AVSessionManager.AVSession = ALREADY_CREATE_A_SESSION;
   let extras = {
     extra : 'This is my custom meida packet'
   }
   await session.setExtras(extras).then(() => {
      console.info(`Set extras successfully`);
   }).catch((err) => {
      console.error(`Failed to set extras. Code: ${err.code}, message: ${err.message}`);
   })
   ```

6. 注册播控命令事件监听，便于响应用户通过媒体会话控制方，例如播控中心，下发的播控命令。

   在session侧注册的监听分为`固定播控命令`和`高级播控事件`两种。

   4.1 固定控制命令的监听

   > **说明：**
   >
   > 媒体会话提供方在注册相关固定播控命令事件监听时，监听的事件会在媒体会话控制方的getValidCommands()方法中体现，即媒体会话控制方会认为对应的方法有效，进而根据需要触发相应的事件。为了保证媒体会话控制方下发的播控命令可以被正常执行，媒体会话提供方请勿进行无逻辑的空实现监听。

   Session侧的固定播控命令主要包括播放、暂停、上一首、下一首等基础操作命令，详细介绍请参见[AVControlCommand](../reference/apis/js-apis-avsession.md)
     
   ```ts
   async setListenerForMesFromController() {
     // 假设已经创建了一个session，如何创建session可以参考之前的案例
     let session: AVSessionManager.AVSession = ALREADY_CREATE_A_SESSION;
     // 一般在监听器中会对播放器做相应逻辑处理
     // 不要忘记处理完后需要通过set接口同步播放相关信息，参考上面的用例
     session.on('play', () => {
       console.info(`on play , do play task`);
       // do some tasks ···
     });
     session.on('pause', () => {
       console.info(`on pause , do pause task`);
       // do some tasks ···
     });
     session.on('stop', () => {
       console.info(`on stop , do stop task`);
       // do some tasks ···
     });
     session.on('playNext', () => {
       console.info(`on playNext , do playNext task`);
       // do some tasks ···
     });
     session.on('playPrevious', () => {
       console.info(`on playPrevious , do playPrevious task`);
       // do some tasks ···
     });
     session.on('fastForward', () => {
       console.info(`on fastForward , do fastForward task`);
       // do some tasks ···
     });
     session.on('rewind', () => {
       console.info(`on rewind , do rewind task`);
       // do some tasks ···
     });

     session.on('seek', (time) => {
       console.info(`on seek , the seek time is ${time}`);
       // do some tasks ···
     });
     session.on('setSpeed', (speed) => {
       console.info(`on setSpeed , the speed is ${speed}`);
       // do some tasks ···
     });
     session.on('setLoopMode', (mode) => {
       console.info(`on setLoopMode , the loop mode is ${mode}`);
       // do some tasks ···
     });
     session.on('toggleFavorite', (assetId) => {
       console.info(`on toggleFavorite , the target asset Id is ${assetId}`);
       // do some tasks ···
     });
   }
   ```

   4.2 高级播控事件的监听

   Session侧的可以注册的高级播控事件主要包括：

   - skipToQueueItem: 播放列表其中某项被选中的事件。
   - handleKeyEvent: 按键事件。
   - outputDeviceChange: 播放设备变化的事件。
   - commonCommand: 自定义控制命令变化的事件。

   ```ts
   async setListenerForMesFromController() {
     // 假设已经创建了一个session，如何创建session可以参考之前的案例
     let session: AVSessionManager.AVSession = ALREADY_CREATE_A_SESSION;
     // 一般在监听器中会对播放器做相应逻辑处理
     // 不要忘记处理完后需要通过set接口同步播放相关信息，参考上面的用例
     session.on('skipToQueueItem', (itemId) => {
       console.info(`on skipToQueueItem , do skip task`);
       // do some tasks ···
     });
     session.on('handleKeyEvent', (event) => {
       console.info(`on handleKeyEvent , the event is ${JSON.stringify(event)}`);
       // do some tasks ···
     });
     session.on('outputDeviceChange', (device) => {
       console.info(`on outputDeviceChange , the device info is ${JSON.stringify(device)}`);
       // do some tasks ···
     });
     session.on('commonCommand', (commandString, args) => {
       console.info(`on commonCommand , command is ${commandString}, args are ${JSON.stringify(args)}`);
       // do some tasks ···
     });
   }
   ```

7. 获取当前媒体会话自身的控制器，与媒体会话对应进行通信交互。
     
   ```ts
   async createControllerFromSession() {
     // 假设已经创建了一个session，如何创建session可以参考之前的案例
     let session: AVSessionManager.AVSession = ALREADY_CREATE_A_SESSION;
   
     // 通过已有session获取一个controller对象
     let controller: AVSessionManager.AVSessionController = await session.getController();
   
     // controller可以与原session对象进行基本的通信交互，比如下发播放命令
     let avCommand: AVSessionManager.AVControlCommand = {command:'play'};
     controller.sendControlCommand(avCommand);
   
     // 或者做状态变更监听
     controller.on('playbackStateChange', 'all', (state: AVSessionManager.AVPlaybackState) => {
   
       // do some things
     });
   
     // controller可以做的操作还有很多，具体可以参考媒体会话控制方相关的说明
   }
   ```

8. 音视频应用在退出，并且不需要继续播放时，及时取消监听以及销毁媒体会话释放资源。
   取消播控命令监听的示例代码如下所示 ：

   ```ts
   async unregisterSessionListener() {
     // 假设已经创建了一个session，如何创建session可以参考之前的案例
     let session: AVSessionManager.AVSession = ALREADY_CREATE_A_SESSION;
   
     // 取消指定session下的相关监听
     session.off('play');
     session.off('pause');
     session.off('stop');
     session.off('playNext');
     session.off('playPrevious');
     session.off('skipToQueueItem');
     session.off('handleKeyEvent');
     session.off('outputDeviceChange');
     session.off('commonCommand');
   }
   ```

     销毁媒体会话示例代码如下所示：
     
   ```ts
   async destroySession() {
     // 假设已经创建了一个session，如何创建session可以参考之前的案例
     let session: AVSessionManager.AVSession = ALREADY_CREATE_A_SESSION;
     // 主动销毁已创建的session
     session.destroy(function (err) {
       if (err) {
         console.error(`Failed to destroy session. Code: ${err.code}, message: ${err.message}`);
       } else {
         console.info(`Destroy : SUCCESS `);
       }
     });
   }
   ```
