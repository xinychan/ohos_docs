# StartAbilityParameter

定义启动Ability参数，可以作为入参，调用[startAbility](js-apis-ability-featureAbility.md#featureabilitystartability)启动指定的Ability。

> **说明：**
> 
> 本接口从API version 6开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。
> 本接口仅可在FA模型下使用

## 导入模块

```ts
import ability from '@ohos.ability.ability';
```

## 属性

**系统能力**：以下各项对应的系统能力均为SystemCapability.Ability.AbilityRuntime.FAModel

| 名称               |   类型   | 必填   | 说明                                    |
| ------------------- | -------- | ---- | -------------------------------------- |
| want                | [Want](js-apis-application-want.md)|   是   | 启动Ability的want信息。                     |
| abilityStartSetting | {[key: string]: any} | 否    | 启动Ability的特殊属性，当开发者启动Ability时，该属性可以作为调用中的输入参数传递。 |

**示例：**
```ts
import featureAbility from '@ohos.ability.featureAbility';

let Want = {
    bundleName: 'com.example.abilityStartSettingApp2',
    abilityName: 'com.example.abilityStartSettingApp.EntryAbility',
};

let abilityStartSetting ={
    [featureAbility.AbilityStartSetting.BOUNDS_KEY] : [100,200,300,400],
    [featureAbility.AbilityStartSetting.WINDOW_MODE_KEY] :
    featureAbility.AbilityWindowConfiguration.WINDOW_MODE_UNDEFINED,
    [featureAbility.AbilityStartSetting.DISPLAY_ID_KEY] : 1,
};

let startAbilityParameter: ability.StartAbilityParameter = {
    want : Want,
    abilityStartSetting : abilityStartSetting
};

try {
    featureAbility.startAbility(startAbilityParameter, (error, data) => {
        if (error && error.code !== 0) {
            console.error('startAbility fail, error: ${JSON.stringify(error)}');
        } else {
            console.log('startAbility success, data: ${JSON.stringify(data)}');
        }
    });
} catch(error) {
    console.error('startAbility error: ${JSON.stringify(error)}');
}
```