# 短时任务开发指导 

## 场景说明

当应用退到后台默认有6到12秒的运行时长，超过该时间后，系统会将应用置为挂起状态。对于绝大多数应用，6到12秒的时间，足够执行一些重要的任务，但如果应用需要更多的时间，可以通过短时任务接口，扩展应用的执行时间。

建议不要等到应用退后台后，才调用[requestSuspendDelay()](../reference/apis/js-apis-resourceschedule-backgroundTaskManager.md#backgroundtaskmanagerrequestsuspenddelay)方法申请延迟挂起，而是应该在执行任何的耗时操作前，都应该调用该接口，向系统申明扩展应用的执行时间。

当应用在前台时，使用[requestSuspendDelay()](../reference/apis/js-apis-resourceschedule-backgroundTaskManager.md#backgroundtaskmanagerrequestsuspenddelay)方法，不会影响应用的短时任务配额。

根据需要调用[getRemainingDelayTime()](../reference/apis/js-apis-resourceschedule-backgroundTaskManager.md#backgroundtaskmanagergetremainingdelaytime)接口获取应用程序进入挂起状态前的剩余时间。由于每个应用每天的短时任务配额时间有限，当执行完耗时任务后，应当及时调用[cancelSuspendDelay()](../reference/apis/js-apis-resourceschedule-backgroundTaskManager.md#backgroundtaskmanagercancelsuspenddelay)接口取消延迟挂起的申请。

一些典型的耗时任务，例如保存一些状态数据到本地数据库、打开和处理一个大型文件、同步一些数据到应用的云端服务器等。


## 接口说明


**表1** 短时任务主要接口

| 接口名                                      | 描述                                       |
| ---------------------------------------- | ---------------------------------------- |
| requestSuspendDelay(reason:&nbsp;string,&nbsp;callback:&nbsp;Callback&lt;void&gt;):&nbsp;[DelaySuspendInfo](../reference/apis/js-apis-backgroundTaskManager.md#delaysuspendinfo) | 后台应用申请延迟挂起。<br/>延迟挂起时间一般情况下默认值为3分钟，低电量时默认值为1分钟。 |
| getRemainingDelayTime(requestId:&nbsp;number):&nbsp;Promise&lt;number&gt; | 获取应用程序进入挂起状态前的剩余时间。<br/>使用Promise形式返回。   |
| cancelSuspendDelay(requestId:&nbsp;number):&nbsp;void | 取消延迟挂起。                                  |


## 开发步骤

当应用需要开始执行一个耗时的任务时。调用短时任务申请接口，并且在任务执行完后，调用短时任务取消接口。

```js
import backgroundTaskManager from '@ohos.resourceschedule.backgroundTaskManager';

let id; // 申请延迟挂起任务ID
let delayTime; // 本次申请延迟挂起任务的剩余时间

// 申请延迟挂起
function requestSuspendDelay() {
  let myReason = 'test requestSuspendDelay'; // 申请原因

  try {
    let delayInfo = backgroundTaskManager.requestSuspendDelay(myReason, () => {
      // 此回调函数执行，表示应用的延迟挂起申请即将超时，应用需要执行一些清理和标注工作，并取消延时挂起
      console.info("[backgroundTaskManager] Request suspension delay will time out.");
      backgroundTaskManager.cancelSuspendDelay(id);
    })
    id = delayInfo.requestId;
    delayTime = delayInfo.actualDelayTime;
    console.info("[backgroundTaskManager] The requestId is: " + id);
    console.info("[backgroundTaskManager]The actualDelayTime is: " + delayTime);
  } catch (error) {
    console.error(`[backgroundTaskManager] requestSuspendDelay failed. code is ${error.code} message is ${error.message}`);
  }
}

// 获取进入挂起前的剩余时间
async function getRemainingDelayTime() {
  try {
    await backgroundTaskManager.getRemainingDelayTime(id).then(res => {
      console.log('[backgroundTaskManager] promise => Operation getRemainingDelayTime succeeded. Data: ' + JSON.stringify(res));
    }).catch(error => {
      console.error(`[backgroundTaskManager] promise => Operation getRemainingDelayTime failed. code is ${error.code} message is ${error.message}`);
    })
  } catch (error) {
    console.error(`[backgroundTaskManager] promise => Operation getRemainingDelayTime failed. code is ${error.code} message is ${error.message}`);
  }
}

// 取消延迟挂起
function cancelSuspendDelay() {
  backgroundTaskManager.cancelSuspendDelay(id);
}

async function performingLongRunningTask() {
  // 在执行具体的耗时任务前，调用短时任务申请接口。向系统申请延迟挂起，延长应用的后台执行时间。
  requestSuspendDelay();

  // 根据需要，通过剩余时间查询接口，获取可用时间配额。
  await getRemainingDelayTime();

  if (delayTime < 0) { // 如果时间配置少于一定的大小，考虑取消此次耗时操作。
    // 处理短时任务配额时间不够的场景
    cancelSuspendDelay();
    return;
  }

  // 此处执行具体的耗时任务

  // 耗时任务执行完，调用短时任务取消接口，避免配额浪费
  cancelSuspendDelay();
}
```

## 相关实例

针对短时任务开发，有以下相关实例可供参考：

- [短时任务（ArkTS）（API9）](https://gitee.com/openharmony/applications_app_samples/tree/master/code/BasicFeature/TaskManagement/TransientTask)
