# @ohos.vibrator (振动)

vibrator模块提供控制马达振动启、停的能力。

> **说明：**
>
> 本模块首批接口从API version 8开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。


## 导入模块

```ts
import vibrator from '@ohos.vibrator';
```

## vibrator.startVibration<sup>9+</sup>

startVibration(effect: VibrateEffect, attribute: VibrateAttribute, callback: AsyncCallback&lt;void&gt;): void

根据指定振动效果和振动属性触发马达振动。

**需要权限**：ohos.permission.VIBRATE

**系统能力**：SystemCapability.Sensors.MiscDevice

**参数：**

| 参数名    | 类型                                   | 必填 | 说明                                                       |
| --------- | -------------------------------------- | ---- | :--------------------------------------------------------- |
| effect    | [VibrateEffect](#vibrateeffect9)       | 是   | 马达振动效果。                                             |
| attribute | [VibrateAttribute](#vibrateattribute9) | 是   | 马达振动属性。                                             |
| callback  | AsyncCallback&lt;void&gt;              | 是   | 回调函数，当马达振动成功，err为undefined，否则为错误对象。 |

**错误码**：

以下错误码的详细介绍请参见 [ohos.vibrator错误码](../errorcodes/errorcode-vibrator.md)

| 错误码ID | 错误信息                 |
| -------- | ------------------------ |
| 14600101 | Device operation failed. |

示例：

```ts
import vibrator from '@ohos.vibrator';

try {
  vibrator.startVibration({
    type: 'time',
    duration: 1000,
  }, {
    id: 0,
    usage: 'alarm'
  }, (error) => {
    if (error) {
      console.error(`Failed to start vibration. Code: ${error.code}, message: ${error.message}`);
      return;
    }
    console.info('Succeed in starting vibration');
  });
} catch (err) {
  console.error(`An unexpected error occurred. Code: ${err.code}, message: ${err.message}`);
}
```

## vibrator.startVibration<sup>9+</sup>

startVibration(effect: VibrateEffect, attribute: VibrateAttribute): Promise&lt;void&gt;

根据指定振动效果和振动属性触发马达振动。

**需要权限**：ohos.permission.VIBRATE

**系统能力**：SystemCapability.Sensors.MiscDevice

**参数：** 

| 参数名    | 类型                                   | 必填 | 说明           |
| --------- | -------------------------------------- | ---- | -------------- |
| effect    | [VibrateEffect](#vibrateeffect9)       | 是   | 马达振动效果。 |
| attribute | [VibrateAttribute](#vibrateattribute9) | 是   | 马达振动属性。 |

**返回值：** 

| 类型                | 说明                                   |
| ------------------- | -------------------------------------- |
| Promise&lt;void&gt; | Promise对象。 |

**错误码**：

以下错误码的详细介绍请参见 [ohos.vibrator错误码](../errorcodes/errorcode-vibrator.md)

| 错误码ID | 错误信息                 |
| -------- | ------------------------ |
| 14600101 | Device operation failed. |

**示例：** 

```ts
import vibrator from '@ohos.vibrator';

try {
  vibrator.startVibration({
    type: 'time',
    duration: 1000
  }, {
    id: 0,
    usage: 'alarm'
  }).then(() => {
    console.info('Succeed in starting vibration');
  }, (error) => {
    console.error(`Failed to start vibration. Code: ${error.code}, message: ${error.message}`);
  });
} catch (err) {
  console.error(`An unexpected error occurred. Code: ${err.code}, message: ${err.message}`);
}
```

## vibrator.stopVibration<sup>9+</sup>

stopVibration(stopMode: VibratorStopMode, callback: AsyncCallback&lt;void&gt;): void

按照指定模式停止马达的振动。

**需要权限**：ohos.permission.VIBRATE

**系统能力**：SystemCapability.Sensors.MiscDevice

**参数：** 

| 参数名   | 类型                                  | 必填 | 说明                                                         |
| -------- | ------------------------------------- | ---- | ------------------------------------------------------------ |
| stopMode | [VibratorStopMode](#vibratorstopmode) | 是   | 指定的停止振动模式。                                     |
| callback | AsyncCallback&lt;void&gt;             | 是   | 回调函数，当马达停止振动成功，err为undefined，否则为错误对象。 |

**示例：** 

```ts
import vibrator from '@ohos.vibrator';

try {
  // 按照固定时长振动
  vibrator.startVibration({
    type: 'time',
    duration: 1000,
  }, {
    id: 0,
    usage: 'alarm'
  }, (error) => {
    if (error) {
      console.error(`Failed to start vibration. Code: ${error.code}, message: ${error.message}`);
      return;
    }
    console.info('Succeed in starting vibration');
  });
} catch (err) {
  console.error(`An unexpected error occurred. Code: ${err.code}, message: ${err.message}`);
}

try {
  // 按照VIBRATOR_STOP_MODE_TIME模式停止振动
  vibrator.stopVibration(vibrator.VibratorStopMode.VIBRATOR_STOP_MODE_TIME, function (error) {
    if (error) {
      console.error(`Failed to stop vibration. Code: ${error.code}, message: ${error.message}`);
      return;
    }
    console.info('Succeed in stopping vibration');
  })
} catch (err) {
  console.error(`An unexpected error occurred. Code: ${err.code}, message: ${err.message}`);
}
```

## vibrator.stopVibration<sup>9+</sup>

stopVibration(stopMode: VibratorStopMode): Promise&lt;void&gt;

按照指定模式停止马达的振动。

**需要权限**：ohos.permission.VIBRATE

**系统能力**：SystemCapability.Sensors.MiscDevice

**参数：** 

| 参数名   | 类型                                  | 必填 | 说明                     |
| -------- | ------------------------------------- | ---- | ------------------------ |
| stopMode | [VibratorStopMode](#vibratorstopmode) | 是   | 马达停止指定的振动模式。 |

**返回值：** 

| 类型                | 说明                                   |
| ------------------- | -------------------------------------- |
| Promise&lt;void&gt; | Promise对象。 |

**示例：** 

```ts
import vibrator from '@ohos.vibrator';

try {
  // 按照固定时长振动
  vibrator.startVibration({
    type: 'time',
    duration: 1000
  }, {
    id: 0,
    usage: 'alarm'
  }).then(() => {
    console.info('Succeed in starting vibration');
  }, (error) => {
    console.error(`Failed to start vibration. Code: ${error.code}, message: ${error.message}`);
  });
} catch (err) {
  console.error(`An unexpected error occurred. Code: ${err.code}, message: ${err.message}`);
}

try {
  // 按照VIBRATOR_STOP_MODE_TIME模式停止振动
  vibrator.stopVibration(vibrator.VibratorStopMode.VIBRATOR_STOP_MODE_PRESET).then(() => {
    console.info('Succeed in stopping vibration');
  }, (error) => {
    console.error(`Failed to stop vibration. Code: ${error.code}, message: ${error.message}`);
  });
} catch (err) {
  console.error(`An unexpected error occurred. Code: ${err.code}, message: ${err.message}`);
}
```

## vibrator.stopVibration<sup>10+</sup>

stopVibration(callback: AsyncCallback&lt;void&gt;): void

停止所有模式的马达振动。

**需要权限**：ohos.permission.VIBRATE

**系统能力**：SystemCapability.Sensors.MiscDevice

**参数：** 

| 参数名   | 类型                      | 必填 | 说明                                                         |
| -------- | ------------------------- | ---- | ------------------------------------------------------------ |
| callback | AsyncCallback&lt;void&gt; | 是   | 回调函数，当马达停止振动成功，err为undefined，否则为错误对象。 |

**示例：** 

```ts
import vibrator from '@ohos.vibrator';

try {
  // 按照固定时长振动
  vibrator.startVibration({
    type: 'time',
    duration: 1000,
  }, {
    id: 0,
    usage: 'alarm'
  }, (error) => {
    if (error) {
      console.error(`Failed to start vibration. Code: ${error.code}, message: ${error.message}`);
      return;
    }
    console.info('Succeed in starting vibration');
  });
} catch (error) {
  console.error(`An unexpected error occurred. Code: ${error.code}, message: ${error.message}`);
}

try {
  // 停止所有模式的马达振动
  vibrator.stopVibration(function (error) {
    if (error) {
      console.error(`Failed to stop vibration. Code: ${error.code}, message: ${error.message}`);
      return;
    }
    console.info('Succeed in stopping vibration');
  })
} catch (error) {
  console.error(`An unexpected error occurred. Code: ${error.code}, message: ${error.message}`);
}
```

## vibrator.stopVibration<sup>10+</sup>

stopVibration(): Promise&lt;void&gt;

停止所有模式的马达振动。

**需要权限**：ohos.permission.VIBRATE

**系统能力**：SystemCapability.Sensors.MiscDevice

**返回值：** 

| 类型                | 说明          |
| ------------------- | ------------- |
| Promise&lt;void&gt; | Promise对象。 |

**示例：** 

```ts
import vibrator from '@ohos.vibrator';

try {
  // 按照固定时长振动
  vibrator.startVibration({
    type: 'time',
    duration: 1000
  }, {
    id: 0,
    usage: 'alarm'
  }).then(() => {
    console.info('Succeed in starting vibration');
  }, (error) => {
    console.error(`Failed to start vibration. Code: ${error.code}, message: ${error.message}`);
  });
} catch (error) {
  console.error(`An unexpected error occurred. Code: ${error.code}, message: ${error.message}`);
}

try {
  // 停止所有模式的马达振动
  vibrator.stopVibration().then(() => {
    console.info('Succeed in stopping vibration');
  }, (error) => {
    console.error(`Failed to stop vibration. Code: ${error.code}, message: ${error.message}`);
  });
} catch (error) {
  console.error(`An unexpected error occurred. Code: ${error.code}, message: ${error.message}`);
}
```

## vibrator.isSupportEffect<sup>10+</sup>

isSupportEffect(effectId: string, callback: AsyncCallback&lt;boolean&gt;): void

查询是否支持传入的参数effectId。

**系统能力**：SystemCapability.Sensors.MiscDevice

**参数：** 

| 参数名   | 类型                         | 必填 | 说明                                                   |
| -------- | ---------------------------- | ---- | ------------------------------------------------------ |
| effectId | string                       | 是   | 振动效果id                                             |
| callback | AsyncCallback&lt;boolean&gt; | 是   | 回调函数，当返回true则表示支持该effectId，否则不支持。 |

**示例：** 

```ts
import vibrator from '@ohos.vibrator';

try {
  // 查询是否支持'haptic.clock.timer'
  vibrator.isSupportEffect('haptic.clock.timer', function (err, state) {
    if (err) {
      console.error(`Failed to query effect. Code: ${err.code}, message: ${err.message}`);
      return;
    }
    console.info('Succeed in querying effect');
    if (state) {
      try {
        vibrator.startVibration({ // 使用startVibration需要添加ohos.permission.VIBRATE权限
          type: 'preset',
          effectId: 'haptic.clock.timer',
          count: 1,
        }, {
          usage: 'unknown'
        }, (error) => {
          if (error) {
            console.error(`Failed to start vibration. Code: ${error.code}, message: ${error.message}`);
          } else {
            console.info('Succeed in starting vibration');
          }
        });
      } catch (error) {
        console.error(`An unexpected error occurred. Code: ${error.code}, message: ${error.message}`);
      }
    }
  })
} catch (error) {
  console.error(`An unexpected error occurred. Code: ${error.code}, message: ${error.message}`);
}
```

## vibrator.isSupportEffect<sup>10+</sup>

isSupportEffect(effectId: string): Promise&lt;boolean&gt;

查询是否支持传入的参数effectId。

**系统能力**：SystemCapability.Sensors.MiscDevice

**参数：** 

| 参数名   | 类型   | 必填 | 说明         |
| -------- | ------ | ---- | ------------ |
| effectId | string | 是   | 振动效果id。 |

**返回值：** 

| 类型                   | 说明                                                      |
| ---------------------- | --------------------------------------------------------- |
| Promise&lt;boolean&gt; | Promise对象。当返回true则表示支持该effectId，否则不支持。 |

**示例：** 

```ts
import vibrator from '@ohos.vibrator';

try {
  // 查询是否支持'haptic.clock.timer'
  vibrator.isSupportEffect('haptic.clock.timer').then((state) => {
    console.info(`The query result is ${state}`);
    if (state) {
      try {
        vibrator.startVibration({
          type: 'preset',
          effectId: 'haptic.clock.timer',
          count: 1,
        }, {
          usage: 'unknown'
        }).then(() => {
          console.info('Succeed in starting vibration');
        }).catch((error) => {
          console.error(`Failed to start vibration. Code: ${error.code}, message: ${error.message}`);
        });
      } catch (error) {
        console.error(`An unexpected error occurred. Code: ${error.code}, message: ${error.message}`);
      }
    }
  }, (error) => {
    console.error(`Failed to query effect. Code: ${error.code}, message: ${error.message}`);
  })
} catch (error) {
  console.error(`An unexpected error occurred. Code: ${error.code}, message: ${error.message}`);
}
```

## EffectId

预置的振动效果。

**系统能力**：SystemCapability.Sensors.MiscDevice

| 名称               | 值                   | 说明                             |
| ------------------ | -------------------- | -------------------------------- |
| EFFECT_CLOCK_TIMER | "haptic.clock.timer" | 描述用户调整计时器时的振动效果。 |


## VibratorStopMode

停止的振动模式。

**系统能力**：SystemCapability.Sensors.MiscDevice

| 名称                      | 值       | 说明                           |
| ------------------------- | -------- | ------------------------------ |
| VIBRATOR_STOP_MODE_TIME   | "time"   | 停止模式为duration模式的振动。 |
| VIBRATOR_STOP_MODE_PRESET | "preset" | 停止模式为预置EffectId的振动。 |

## VibrateEffect<sup>9+</sup>

马达振动效果。

**系统能力**：SystemCapability.Sensors.MiscDevice

| 类型                             | 说明                           |
| -------------------------------- | ------------------------------ |
| [VibrateTime](#vibratetime9)     | 按照指定持续时间触发马达振动。 |
| [VibratePreset](#vibratepreset9) | 按照预置振动类型触发马达振动。 |
| [VibrateFromFile<sup>10+</sup>](#vibratefromfile10) | 按照自定义振动配置文件触发马达振动。 |

## VibrateTime<sup>9+</sup>

马达振动时长。

**系统能力**：SystemCapability.Sensors.MiscDevice

| 名称     | 类型    | 必填 | 说明                           |
| -------- | ------ | ----- | ------------------------------ |
| type     | string |  是   | 值为"time"，按照指定持续时间触发马达振动。 |
| duration | number |  是   | 马达持续振动时长, 单位ms。         |

## VibratePreset<sup>9+</sup>

马达预置振动类型。

**系统能力**：SystemCapability.Sensors.MiscDevice

| 名称     | 类型      | 必填 | 说明                           |
| -------- | -------- | ---- |------------------------------ |
| type     | string   |  是  | 值为"preset"，按照预置振动效果触发马达振动。 |
| effectId | string   |  是  | 预置的振动效果ID。             |
| count    | number   |  是  | 重复振动的次数。               |

## VibrateFromFile<sup>10+</sup>

自定义振动类型，仅部分设备支持，当设备不支持此振动类型时，返回[设备不支持错误码](../errorcodes/errorcode-universal.md)。

**系统能力**：SystemCapability.Sensors.MiscDevice

| 名称     | 类型       | 必填 | 说明                           |
| -------- | --------  | ---- | ------------------------------ |
| type     | string    |  是  | 值为"file"，按照振动配置文件触发马达振动。 |
| hapticFd | [HapticFileDescriptor](#hapticfiledescriptor10) | 是 | 振动配置文件的描述符。|

## HapticFileDescriptor<sup>10+</sup>

自定义振动配置文件的描述符，必须确认资源文件可用，其参数可通过[文件管理API](js-apis-file-fs.md#fsopen)从沙箱路径获取或者通过[资源管理API](js-apis-resource-manager.md#getrawfd9)从HAP资源获取。使用场景：振动序列被存储在一个文件中，需要根据偏移量和长度进行振动，振动序列存储格式，请参考[自定义振动格式](../../device/vibrator-guidelines.md#自定义振动格式)。

**系统能力**：SystemCapability.Sensors.MiscDevice

| 名称     | 类型      |  必填  | 说明                           |
| -------- | -------- |--------| ------------------------------|
| fd       | number   |  是    | 资源文件描述符。                |
| offset   | number   |  否    | 距文件起始位置的偏移量，单位为字节，默认为文件起始位置，不可超出文件有效范围。|
| length   | number   |  否    | 资源长度，单位为字节，默认值为从偏移位置至文件结尾的长度，不可超出文件有效范围。|

## VibrateAttribute<sup>9+</sup>

马达振动属性。

**系统能力**：SystemCapability.Sensors.MiscDevice

| 名称  | 类型 | 必填 | 说明           |
| ----- | ------ | ---- | -------------- |
| id    | number      |  否 | 默认值为0，振动器id。     |
| usage | [Usage](#usage9)      | 是 | 马达振动的使用场景。 |

## Usage<sup>9+</sup>

振动使用场景。

**系统能力**：SystemCapability.Sensors.MiscDevice

| 名称             | 类型   | 说明                           |
| ---------------- | ------ | ------------------------------ |
| unknown          | string | 没有明确使用场景，最低优先级。 |
| alarm            | string | 用于警报场景。           |
| ring             | string | 用于铃声场景。           |
| notification     | string | 用于通知场景。           |
| communication    | string | 用于通信场景。           |
| touch            | string | 用于触摸场景。           |
| media            | string | 用于多媒体场景。         |
| physicalFeedback | string | 用于物理反馈场景。       |
| simulateReality  | string | 用于模拟现实场景。       |

## vibrator.vibrate<sup>(deprecated)</sup>

vibrate(duration: number): Promise&lt;void&gt;

按照指定持续时间触发马达振动。

从API version 9 开始不再维护，建议使用 [vibrator.startVibration](#vibratorstartvibration9-1) 代替。

**需要权限**：ohos.permission.VIBRATE

**系统能力**：SystemCapability.Sensors.MiscDevice

**参数：** 

| 参数名   | 类型   | 必填 | 说明                   |
| -------- | ------ | ---- | ---------------------- |
| duration | number | 是   | 马达振动时长, 单位ms。 |

**返回值：** 

| 类型                | 说明                                   |
| ------------------- | -------------------------------------- |
| Promise&lt;void&gt; | Promise对象。 |

**示例：** 

```ts
vibrator.vibrate(1000).then(() => {
  console.info('Succeed in vibrating');
}, (error) => {
  console.error(`Failed to vibrate. Code: ${error.code}, message: ${error.message}`);
});
```

## vibrator.vibrate<sup>(deprecated)</sup>

vibrate(duration: number, callback?: AsyncCallback&lt;void&gt;): void

按照指定持续时间触发马达振动。

从API version 9 开始不再维护，建议使用 [vibrator.startVibration](#vibratorstartvibration9) 代替。

**需要权限**：ohos.permission.VIBRATE

**系统能力**：SystemCapability.Sensors.MiscDevice

**参数：** 

| 参数名   | 类型                      | 必填 | 说明                                                       |
| -------- | ------------------------- | ---- | ---------------------------------------------------------- |
| duration | number                    | 是   | 马达振动时长, 单位ms。                                     |
| callback | AsyncCallback&lt;void&gt; | 否   | 回调函数，当马达振动成功，err为undefined，否则为错误对象。 |

**示例：** 

```ts
vibrator.vibrate(1000, function (error) {
  if (error) {
    console.error(`Failed to vibrate. Code: ${error.code}, message: ${error.message}`);
  } else {
    console.info('Succeed in vibrating');
  }
})
```


## vibrator.vibrate<sup>(deprecated)</sup>

vibrate(effectId: EffectId): Promise&lt;void&gt;

按照预置振动效果触发马达振动。

从API version 9 开始不再维护，建议使用 [vibrator.startVibration](#vibratorstartvibration9-1) 代替。

**需要权限**：ohos.permission.VIBRATE

**系统能力**：SystemCapability.Sensors.MiscDevice

**参数：** 

| 参数名   | 类型                  | 必填 | 说明               |
| -------- | --------------------- | ---- | ------------------ |
| effectId | [EffectId](#effectid) | 是   | 预置的振动效果ID。 |

**返回值：** 

| 类型                | 说明                                   |
| ------------------- | -------------------------------------- |
| Promise&lt;void&gt; | Promise对象。 |

**示例：** 

```ts
vibrator.vibrate(vibrator.EffectId.EFFECT_CLOCK_TIMER).then(() => {
  console.info('Succeed in vibrating');
}, (error) => {
  console.error(`Failed to vibrate. Code: ${error.code}, message: ${error.message}`);
});
```


## vibrator.vibrate<sup>(deprecated)</sup>

vibrate(effectId: EffectId, callback?: AsyncCallback&lt;void&gt;): void

按照指定振动效果触发马达振动。

从API version 9 开始不再维护，建议使用 [vibrator.startVibration](#vibratorstartvibration9) 代替。

**需要权限**：ohos.permission.VIBRATE

**系统能力**：SystemCapability.Sensors.MiscDevice

**参数：** 

| 参数名   | 类型                      | 必填 | 说明                                                       |
| -------- | ------------------------- | ---- | ---------------------------------------------------------- |
| effectId | [EffectId](#effectid)     | 是   | 预置的振动效果ID。                                         |
| callback | AsyncCallback&lt;void&gt; | 否   | 回调函数，当马达振动成功，err为undefined，否则为错误对象。 |

**示例：** 

```ts
vibrator.vibrate(vibrator.EffectId.EFFECT_CLOCK_TIMER, function (error) {
  if (error) {
    console.error(`Failed to vibrate. Code: ${error.code}, message: ${error.message}`);
  } else {
    console.info('Succeed in vibrating');
  }
})
```

## vibrator.stop<sup>(deprecated)</sup>

stop(stopMode: VibratorStopMode): Promise&lt;void&gt;

按照指定模式停止马达的振动。

从API version 9 开始不再维护，建议使用 [vibrator.stopVibration](#vibratorstopvibration9-1) 代替。

**需要权限**：ohos.permission.VIBRATE

**系统能力**：SystemCapability.Sensors.MiscDevice

**参数：** 

| 参数名   | 类型                                  | 必填 | 说明                     |
| -------- | ------------------------------------- | ---- | ------------------------ |
| stopMode | [VibratorStopMode](#vibratorstopmode) | 是   | 马达停止指定的振动模式。 |

**返回值：** 

| 类型                | 说明                                   |
| ------------------- | -------------------------------------- |
| Promise&lt;void&gt; | Promise对象。 |

**示例：** 

```ts
// 按照effectId类型启动振动
vibrator.vibrate(vibrator.EffectId.EFFECT_CLOCK_TIMER, function (error) {
  if (error) {
    console.error(`Failed to vibrate. Code: ${error.code}, message: ${error.message}`);
  } else {
    console.info('Succeed in vibrating');
  }
})
// 使用VIBRATOR_STOP_MODE_PRESET模式停止振动
vibrator.stop(vibrator.VibratorStopMode.VIBRATOR_STOP_MODE_PRESET).then(() => {
  console.info('Succeed in stopping');
}, (error) => {
  console.error(`Failed to stop. Code: ${error.code}, message: ${error.message}`);
});
```


## vibrator.stop<sup>(deprecated)</sup>

stop(stopMode: VibratorStopMode, callback?: AsyncCallback&lt;void&gt;): void

按照指定模式停止马达的振动。

从API version 9 开始不再维护，建议使用 [vibrator.stopVibration](#vibratorstopvibration9) 代替。

**需要权限**：ohos.permission.VIBRATE

**系统能力**：SystemCapability.Sensors.MiscDevice

**参数：** 

| 参数名   | 类型                                  | 必填 | 说明                                                         |
| -------- | ------------------------------------- | ---- | ------------------------------------------------------------ |
| stopMode | [VibratorStopMode](#vibratorstopmode) | 是   | 马达停止指定的振动模式。                                     |
| callback | AsyncCallback&lt;void&gt;             | 否   | 回调函数，当马达停止振动成功，err为undefined，否则为错误对象。 |

**示例：** 

```ts
// 按照effectId类型启动振动
vibrator.vibrate(vibrator.EffectId.EFFECT_CLOCK_TIMER, function (error) {
  if (error) {
    console.error(`Failed to vibrate. Code: ${error.code}, message: ${error.message}`);
  } else {
    console.info('Succeed in vibrating');
  }
})
// 使用VIBRATOR_STOP_MODE_PRESET模式停止振动
vibrator.stop(vibrator.VibratorStopMode.VIBRATOR_STOP_MODE_PRESET, function (error) {
  if (error) {
    console.error(`Failed to stop. Code: ${error.code}, message: ${error.message}`);
  } else {
    onsole.info('Succeed in stopping');
  }
})
```
