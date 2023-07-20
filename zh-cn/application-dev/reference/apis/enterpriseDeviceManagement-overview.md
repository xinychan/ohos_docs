# 企业设备管理概述（仅对系统应用开放）

## 概述
OpenHarmony通过企业设备管理（Enterprise Device Management）API支持企业应用，该API提供了系统级别的管理功能，用于实现企业对员工设备的管理和配置。如在企业场景下，IT人员需要员工设备进行管理和控制，安装企业应用、设置安全策略、设置企业邮箱、企业网络接入以及远程清除（即恢复出厂默认设置）丢失或者被盗设备上的数据。

## 开发企业管理应用

### 基本概念
- 设备管理应用：具备[企业设备管理扩展能力](../../application-models/enterprise-extensionAbility.md)的系统应用。

### 约束与限制
- 仅支持Stage模型

### 环境准备
- DevEco Studio可参考其官网介绍进行[下载](https://developer.harmonyos.com/cn/develop/deveco-studio#download)，并进行相关的配置动作。
- ohos-sdk-full可参考OpenHarmony网站进行[下载](https://gitee.com/openharmony/docs/blob/master/zh-cn/release-notes/OpenHarmony-v3.2-beta2.md#%E4%BB%8E%E9%95%9C%E5%83%8F%E7%AB%99%E7%82%B9%E8%8E%B7%E5%8F%96)。

### 开发步骤

1. 使用DevEco Studio新建工程、[替换full-sdk](https://gitee.com/openharmony/docs/blob/master/zh-cn/application-dev/faqs/full-sdk-switch-guide.md)。

2. 在[应用签名文件](../../security/accesstoken-overview.md#应用apl等级说明)中设置应用为系统应用，即app-feature字段为hos_system_app。

3. 创建EnterpriseAdminExtensionAbility，创建过程详情请见[EnterpriseAdminExtensionAbility开发指南](../../application-models/enterprise-extensionAbility.md)。

4. 声明接口所需权限。在申请权限前，请保证符合[权限使用的基本原则](../../security/accesstoken-overview.md#权限使用的基本原则)。然后参考[配置文件权限声明指导文档](../../security/accesstoken-guidelines.md#acl方式声明)声明对应权限。

### API参考

> **说明：**
>
> - 若想进行网络管理，WiFi管理等开发，请参考以下内容。
- [@ohos.enterprise.accountManager (帐户管理)](js-apis-enterprise-accountManager.md)
- [@ohos.enterprise.adminManager (企业设备管理)](js-apis-enterprise-adminManager.md)
- [@ohos.enterprise.applicationManager (应用管理)](js-apis-enterprise-applicationManager.md)
- [@ohos.enterprise.browser (浏览器管理)](js-apis-enterprise-browser.md)
- [@ohos.enterprise.bundleManager (包管理)](js-apis-enterprise-bundleManager.md)
- [@ohos.enterprise.dateTimeManager (系统时间管理)](js-apis-enterprise-dateTimeManager.md)
- [@ohos.enterprise.deviceControl (设备控制管理)](js-apis-enterprise-deviceControl.md)
- [@ohos.enterprise.deviceInfo (设备信息管理)](js-apis-enterprise-deviceInfo.md)
- [@ohos.enterprise.deviceSettings (设备设置管理)](js-apis-enterprise-deviceSettings.md)
- [@ohos.enterprise.EnterpriseAdminExtensionAbility (企业设备管理扩展能力)](js-apis-EnterpriseAdminExtensionAbility.md)
- [@ohos.enterprise.networkManager (网络管理)](js-apis-enterprise-networkManager.md)
- [@ohos.enterprise.restrictions (限制类策略)](js-apis-enterprise-restrictions.md)
- [@ohos.enterprise.wifiManager (WiFi管理)](js-apis-enterprise-wifiManager.md)