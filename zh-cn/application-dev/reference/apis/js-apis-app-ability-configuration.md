# @ohos.app.ability.Configuration (Configuration)

定义环境变化信息。Configuration是接口定义，仅做字段声明。

> **说明：**
> 
> 本模块首批接口从API version 9开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。

## 导入模块

```ts
import Configuration from '@ohos.app.ability.Configuration';
```

## 属性

**系统能力**：以下各项对应的系统能力均为SystemCapability.Ability.AbilityBase

| 名称 | 类型 | 可读 | 可写 | 说明 |
| -------- | -------- | -------- | -------- | -------- |
| language | string | 是 | 是 | 表示应用程序的当前语言，例如“zh"。 |
| colorMode | [ColorMode](js-apis-app-ability-configurationConstant.md#configurationconstantcolormode) | 是 | 是 | 表示深浅色模式，默认为浅色。取值范围：<br />- COLOR_MODE_NOT_SET：未设置<br />- COLOR_MODE_LIGHT：浅色模式<br />- COLOR_MODE_DARK：深色模式 |
| direction | [Direction](js-apis-app-ability-configurationConstant.md#configurationconstantdirection) | 是 | 否 | 表示屏幕方向，取值范围：<br />- DIRECTION_NOT_SET：未设置<br />- DIRECTION_HORIZONTAL：水平方向<br />- DIRECTION_VERTICAL：垂直方向 |
| screenDensity  | [ScreenDensity](js-apis-app-ability-configurationConstant.md#configurationconstantscreendensity) | 是 | 否 | 表示屏幕像素密度，取值范围：<br />- SCREEN_DENSITY_NOT_SET：未设置<br />- SCREEN_DENSITY_SDPI：120<br />- SCREEN_DENSITY_MDPI：160<br />- SCREEN_DENSITY_LDPI：240<br />- SCREEN_DENSITY_XLDPI：320<br />- SCREEN_DENSITY_XXLDPI：480<br />- SCREEN_DENSITY_XXXLDPI：640 |
| displayId  | number | 是 | 否 | 表示应用所在的物理屏幕ID。 |
| hasPointerDevice  | boolean | 是 | 否 | 指示指针类型设备是否已连接，如键鼠、触控板等。 |

具体字段描述参考ohos.app.ability.Configuration.d.ts文件

**示例：**

  ```ts
import UIAbility from '@ohos.app.ability.UIAbility';

export default class EntryAbility extends UIAbility {
    onCreate(want, launchParam) {
        let envCallback = {
            onConfigurationUpdated(config) {
                console.info(`envCallback onConfigurationUpdated success: ${JSON.stringify(config)}`);
                let language = config.language;
                let colorMode = config.colorMode;
                let direction = config.direction;
                let screenDensity = config.screenDensity;
                let displayId = config.displayId;
                let hasPointerDevice = config.hasPointerDevice;
            }
        };
        try {
            let applicationContext = this.context.getApplicationContext();
            let callbackId = applicationContext.on('environment', envCallback);
            console.log('callbackId: ${callbackId}');
        } catch (paramError) {
            console.error('error: ${paramError.code}, ${paramError.message}');
        }
    }
}
  ```

