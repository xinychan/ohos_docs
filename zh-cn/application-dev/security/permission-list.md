# 应用权限列表

在申请目标权限前，建议开发者先阅读[访问控制开发概述-权限的工作流程](accesstoken-overview.md#权限的工作流程)。对权限的工作流程有基本的了解后，再结合以下权限的具体说明，判断应用能否申请目标权限，提高开发效率。

权限的使用示例请参考[访问控制开发指导](accesstoken-guidelines.md)。

## ohos.permission.USE_BLUETOOTH

允许应用查看蓝牙的配置。

**权限级别**：normal

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：8

## ohos.permission.DISCOVER_BLUETOOTH

允许应用配置本地蓝牙，查找远端设备且与之配对连接。

**权限级别**：normal

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：8

## ohos.permission.MANAGE_BLUETOOTH

允许应用配对蓝牙设备，并对设备的电话簿或消息进行访问。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：7

## ohos.permission.ACCESS_BLUETOOTH

允许应用接入蓝牙并使用蓝牙能力，例如配对、连接外围设备等。

**权限级别**：normal

**授权方式**：user_grant

**ACL使能**：FALSE

**起始版本**：10

## ohos.permission.INTERNET

允许使用Internet网络。

**权限级别**：normal

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：9

## ohos.permission.MODIFY_AUDIO_SETTINGS

允许应用修改音频设置。

**权限级别**：normal

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：8

## ohos.permission.ACCESS_NOTIFICATION_POLICY

在本设备上允许应用访问通知策略。

**权限级别**：normal

**授权方式**：system_grant

**ACL使能**：FALSE

**起始版本**：7

## ohos.permission.GET_TELEPHONY_STATE

允许应用读取电话信息。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：8

## ohos.permission.REQUIRE_FORM

允许应用获取Ability Form。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：7

## ohos.permission.GET_NETWORK_INFO

允许应用获取数据网络信息。

**权限级别**：normal

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：8

## ohos.permission.PLACE_CALL

允许应用直接拨打电话。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：8

## ohos.permission.SET_NETWORK_INFO

允许应用配置数据网络。

**权限级别**：normal

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：8

## ohos.permission.REMOVE_CACHE_FILES

允许清理指定应用的缓存。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：7

## ohos.permission.REBOOT

允许应用重启设备。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：7

## ohos.permission.RUNNING_LOCK

允许应用获取运行锁，保证应用在后台的持续运行。

**权限级别**：normal

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：7

## ohos.permission.SET_TIME

允许应用修改系统时间。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：7

## ohos.permission.SET_TIME_ZONE

允许应用修改系统时区。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：7

## ohos.permission.DOWNLOAD_SESSION_MANAGER

允许应用管理下载任务会话。

**权限级别**：system_core

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：7

## ohos.permission.COMMONEVENT_STICKY

允许应用发布粘性公共事件。

**权限级别**：normal

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：7

## ohos.permission.SYSTEM_FLOAT_WINDOW

允许应用使用悬浮窗的能力。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：7

## ohos.permission.PRIVACY_WINDOW

允许应用将窗口设置为隐私窗口，禁止截屏录屏。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：9

## ohos.permission.POWER_MANAGER

允许应用调用电源管理子系统的接口休眠或者唤醒设备。

**权限级别**：system_core

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：7

## ohos.permission.REFRESH_USER_ACTION

允许应用在收到用户事件时，重新计算超时时间。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：7

## ohos.permission.POWER_OPTIMIZATION

允许系统应用设置省电模式、获取省电模式的配置信息并接收配置变化的通知。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：7

## ohos.permission.REBOOT_RECOVERY

允许系统应用重启设备并进入恢复模式。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：7

## ohos.permission.MANAGE_LOCAL_ACCOUNTS

允许应用管理本地用户帐号。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：7

## ohos.permission.INTERACT_ACROSS_LOCAL_ACCOUNTS

允许多个系统帐号之间相互访问。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：7

## ohos.permission.VIBRATE

允许应用控制马达振动。

**权限级别**：normal

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：7

## ohos.permission.CONNECT_IME_ABILITY

允许绑定输入法Ability（InputMethodAbility）。

**权限级别**：system_core

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：7

## ohos.permission.CONNECT_SCREEN_SAVER_ABILITY

允许绑定屏保Ability（ScreenSaverAbility）。

**权限级别**：system_core

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：7

## ohos.permission.READ_SCREEN_SAVER

允许应用查询屏保状态信息。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：7

## ohos.permission.WRITE_SCREEN_SAVER

允许应用修改屏保状态信息。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：7

## ohos.permission.SET_WALLPAPER

允许应用设置静态壁纸。

**权限级别**：normal

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：7

## ohos.permission.GET_WALLPAPER

允许应用读取壁纸文件。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：7

## ohos.permission.CHANGE_ABILITY_ENABLED_STATE

允许改变应用或者组件的使能状态。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：7

## ohos.permission.ACCESS_MISSIONS

允许应用访问任务栈信息。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：7

**废弃版本**：9

## ohos.permission.CLEAN_BACKGROUND_PROCESSES

允许应用根据包名清理相关后台进程。

**权限级别**：normal

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：7

## ohos.permission.KEEP_BACKGROUND_RUNNING

允许Service Ability在后台持续运行。

**权限级别**：normal

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：8

## ohos.permission.UPDATE_CONFIGURATION

允许更新系统配置。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：7

## ohos.permission.UPDATE_SYSTEM

允许调用升级接口。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：8

## ohos.permission.UPDATE_MIGRATE

允许升级过程中进行数据迁移。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：10

## ohos.permission.FACTORY_RESET

允许调用恢复出厂接口。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：8

## ohos.permission.GRANT_SENSITIVE_PERMISSIONS

允许应用为其他应用授予敏感权限。

**权限级别**：system_core

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：8

## ohos.permission.REVOKE_SENSITIVE_PERMISSIONS

允许应用撤销给其他应用授予的敏感信息。

**权限级别**：system_core

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：8

## ohos.permission.GET_SENSITIVE_PERMISSIONS

允许应用读取其他应用的敏感权限的状态。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：8

## ohos.permission.INTERACT_ACROSS_LOCAL_ACCOUNTS_EXTENSION

允许应用跨用户对其他应用的属性进行设置。

**权限级别**：system_core

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：7

## ohos.permission.LISTEN_BUNDLE_CHANGE

允许应用监听其他应用安装、更新、卸载状态的变化。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：7

## ohos.permission.GET_BUNDLE_INFO

允许查询应用的基本信息。

**权限级别**：normal

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：7

## ohos.permission.GET_BUNDLE_INFO_PRIVILEGED

允许查询应用的基本信息和其他敏感信息。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：7

## ohos.permission.ACCELEROMETER

允许应用读取加速度传感器的数据。

**权限级别**：normal

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：7

## ohos.permission.GYROSCOPE

允许应用读取陀螺仪传感器的数据。

**权限级别**：normal

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：7

## ohos.permission.INSTALL_BUNDLE

允许应用安装、卸载其他应用（除了企业相关应用，目前有企业InHouse应用，企业MDM应用和企业normal应用）。

**权限级别**：system_core

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：7

## ohos.permission.MANAGE_SHORTCUTS

允许应用查询其他应用的快捷方式信息、启动其他应用的快捷方式。

**权限级别**：system_core

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：7

## ohos.permission.radio.ACCESS_FM_AM

允许应用获取收音机相关服务。

**权限级别**：system_core

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：7

## ohos.permission.SET_TELEPHONY_STATE

允许应用修改telephone的状态。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：8

## ohos.permission.START_ABILITIES_FROM_BACKGROUND

允许应用在后台启动或者访问其他组件。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：9

## ohos.permission.BUNDLE_ACTIVE_INFO

允许系统应用查询其他应用在前台或后台的运行时间。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：7

## ohos.permission.START_INVISIBLE_ABILITY

无论Ability是否可见，都允许应用进行调用。

**权限级别**：system_core

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：9

## ohos.permission.sec.ACCESS_UDID

允许系统应用获取UDID。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：7

## ohos.permission.LAUNCH_DATA_PRIVACY_CENTER

允许应用从其隐私声明页面跳转至"数据与隐私"页面。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：7

## ohos.permission.MANAGE_MEDIA_RESOURCES

允许应用程序获取当前设备正在播放的媒体资源，并对其进行管理。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：9

## ohos.permission.PUBLISH_AGENT_REMINDER

允许该应用使用后台代理提醒。

**权限级别**：normal

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：7

## ohos.permission.CONTROL_TASK_SYNC_ANIMATOR

允许应用使用同步任务动画。

**权限级别**：system_core

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：7

## ohos.permission.INPUT_MONITORING

允许应用监听输入事件，仅系统签名应用可申请此权限。

**权限级别**：system_core

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：7

## ohos.permission.MANAGE_MISSIONS

允许用户管理元能力任务栈。

**权限级别**：system_core

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：9

## ohos.permission.NOTIFICATION_CONTROLLER

允许应用管理通知和订阅通知。

**权限级别**：system_core

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：8

## ohos.permission.CONNECTIVITY_INTERNAL

允许应用程序获取网络相关的信息或修改网络相关设置。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：8

## ohos.permission.MANAGE_VPN

允许应用程序启动或停止VPN功能。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：FALSE

**起始版本**：10

## ohos.permission.MANAGE_NET_STRATEGY

允许应用程序获取网络策略相关的信息或修改网络策略相关设置。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：10

## ohos.permission.GET_NETWORK_STATS

允许应用程序获取历史流量信息和监听流量变化。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：FALSE

**起始版本**：10

## ohos.permission.NETSYS_INTERNAL

允许SA服务调用网络管理netsys中的网络管理、wifi、网卡监听、iptables设置等功能接口。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：FALSE

**起始版本**：10

## ohos.permission.SET_ABILITY_CONTROLLER

允许设置ability组件启动和停止控制权。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：9

## ohos.permission.USE_USER_IDM

允许应用访问系统身份凭据信息。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：FALSE

**起始版本**：8

## ohos.permission.MANAGE_USER_IDM

允许应用使用系统身份凭据管理能力进行口令、人脸、指纹等录入、修改、删除等操作。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：FALSE

**起始版本**：8

## ohos.permission.ACCESS_BIOMETRIC

允许应用使用生物特征识别能力进行身份认证。

**权限级别**：normal

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：6

## ohos.permission.ACCESS_USER_AUTH_INTERNAL

允许应用使用系统身份认证能力进行用户身份认证或身份识别。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：FALSE

**起始版本**：8

## ohos.permission.ACCESS_PIN_AUTH

允许应用使用口令输入接口，用于系统应用完成口令输入框绘制场景。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：FALSE

**起始版本**：8

## ohos.permission.GET_RUNNING_INFO

允许应用获取运行态信息。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：7

## ohos.permission.CLEAN_APPLICATION_DATA

允许应用清理应用数据。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：7

## ohos.permission.RUNNING_STATE_OBSERVER

允许应用观察应用状态。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：7

## ohos.permission.CAPTURE_SCREEN

允许应用截取屏幕图像。

**权限级别**：system_core

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：7

## ohos.permission.GET_WIFI_INFO

允许应用获取Wi-Fi信息。

**权限级别**：normal

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：8

## ohos.permission.GET_WIFI_INFO_INTERNAL

允许系统应用获取Wi-Fi相关参数。

**权限级别**：system_core

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：8

## ohos.permission.SET_WIFI_INFO

允许应用配置Wi-Fi设备。

**权限级别**：normal

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：8

## ohos.permission.GET_WIFI_PEERS_MAC

允许应用获取对端的Wi-Fi设备的MAC地址。

**权限级别**：system_core

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：8

## ohos.permission.GET_WIFI_LOCAL_MAC

允许应用获取本机的Wi-Fi设备的MAC地址。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：8

## ohos.permission.GET_WIFI_CONFIG

允许应用获取Wi-Fi的配置信息。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：8

## ohos.permission.SET_WIFI_CONFIG

允许应用配置Wi-Fi信息。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：8

## ohos.permission.MANAGE_WIFI_CONNECTION

允许应用管理Wi-Fi的连接。

**权限级别**：system_core

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：8

## ohos.permission.MANAGE_WIFI_HOTSPOT

允许应用开启或关闭Wi-Fi热点。

**权限级别**：system_core

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：8

## ohos.permission.GET_ALL_APP_ACCOUNTS

允许应用获取所有应用账户信息。

**权限级别**：system_core

**授权方式**：system_grant

**ACL使能**：FALSE

**起始版本**：7

## ohos.permission.MANAGE_SECURE_SETTINGS

允许应用修改安全类系统设置。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：7

## ohos.permission.READ_DFX_SYSEVENT

允许应用访问系统事件打点数据。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：8

## ohos.permission.MANAGE_ENTERPRISE_DEVICE_ADMIN

允许应用激活设备管理员应用。

**权限级别**：system_core

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：9

## ohos.permission.SET_ENTERPRISE_INFO

允许设备管理员应用设置企业信息。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：9

## ohos.permission.ENTERPRISE_SUBSCRIBE_MANAGED_EVENT

允许设备管理员应用订阅管理事件。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：9

## ohos.permission.ENTERPRISE_SET_DATETIME

允许设备管理员应用设置系统时间。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：9

## ohos.permission.ENTERPRISE_GET_DEVICE_INFO

允许设备管理员读取设备信息。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：10

## ohos.permission.ENTERPRISE_RESET_DEVICE

允许设备管理员恢复设备出厂设置。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：10

## ohos.permission.ENTERPRISE_SET_WIFI

允许设备管理员应用设置和查询WiFi信息。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：10

## ohos.permission.ENTERPRISE_GET_NETWORK_INFO

允许设备管理员应用查询网络信息。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：10

## ohos.permission.ENTERPRISE_SET_ACCOUNT_POLICY

允许设备管理员设置账户管理策略。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：10

## ohos.permission.ENTERPRISE_SET_BUNDLE_INSTALL_POLICY

允许设备管理员设置包安装管理策略。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：10

## ohos.permission.ENTERPRISE_SET_NETWORK

允许设备管理员设置网络信息。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：10

## ohos.permission.ENTERPRISE_MANAGE_SET_APP_RUNNING_POLICY

允许设备管理员设置应用运行管理策略。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：10

## ohos.permission.ENTERPRISE_SET_SCREENOFF_TIME

允许设备管理员设置系统休眠时间。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：10

## ohos.permission.ENTERPRISE_INSTALL_BUNDLE

允许设备管理员安装和卸载包。

**权限级别**：system_core

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：10

## ohos.permission.ENTERPRISE_GET_SETTINGS

允许设备管理员查询“设置”应用数据。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：10

## ohos.permission.ENTERPRISE_MANAGE_CERTIFICATE

允许设备管理员管理证书。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：10

## ohos.permission.ENTERPRISE_RESTRICT_POLICY

允许设备管理员下发和获取限制类策略。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：10

## ohos.permission.ENTERPRISE_MANAGE_USB

允许设备管理员管理USB。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：10

## ohos.permission.ENTERPRISE_MANAGE_NETWORK

允许设备管理员管理网络。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：10

## ohos.permission.ENTERPRISE_SET_BROWSER_POLICY

允许设备设置/取消浏览器策略。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：10

## ohos.permission.NFC_TAG

允许应用读取Tag卡片。

**权限级别**：normal

**授权方式**：system_grant

**ACL使能**：FALSE

**起始版本**：7

## ohos.permission.NFC_CARD_EMULATION

允许应用实现卡模拟功能。

**权限级别**：normal

**授权方式**：system_grant

**ACL使能**：FALSE

**起始版本**：8

## ohos.permission.PERMISSION_USED_STATS

允许系统应用访问权限使用记录。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：9

## ohos.permission.NOTIFICATION_AGENT_CONTROLLER

允许应用发送代理通知。

**权限级别**：system_core

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：9

## ohos.permission.ANSWER_CALL

允许应用接听来电。

**权限级别**：system_basic

**授权方式**：user_grant

**ACL使能**：TRUE

**起始版本**：9

## ohos.permission.READ_CALENDAR

允许应用读取日历信息。

**权限级别**：normal

**授权方式**：user_grant

**ACL使能**：TRUE

**起始版本**：8

## ohos.permission.READ_CALL_LOG

允许应用读取通话记录。

**权限级别**：system_basic

**授权方式**：user_grant

**ACL使能**：TRUE

**起始版本**：8

## ohos.permission.READ_CELL_MESSAGES

允许应用读取设备收到的小区广播信息。

**权限级别**：system_basic

**授权方式**：user_grant

**ACL使能**：TRUE

**起始版本**：8

## ohos.permission.READ_CONTACTS

允许应用读取联系人数据。

**权限级别**：system_basic

**授权方式**：user_grant

**ACL使能**：TRUE

**起始版本**：8

## ohos.permission.READ_MESSAGES

允许应用读取短信息。

**权限级别**：system_basic

**授权方式**：user_grant

**ACL使能**：TRUE

**起始版本**：8

## ohos.permission.RECEIVE_MMS

允许应用接收和处理彩信。

**权限级别**：system_basic

**授权方式**：user_grant

**ACL使能**：TRUE

**起始版本**：8

## ohos.permission.RECEIVE_SMS

允许应用接收和处理短信。

**权限级别**：system_basic

**授权方式**：user_grant

**ACL使能**：TRUE

**起始版本**：8

## ohos.permission.RECEIVE_WAP_MESSAGES

允许应用接收和处理WAP消息。

**权限级别**：system_basic

**授权方式**：user_grant

**ACL使能**：TRUE

**起始版本**：8

## ohos.permission.MICROPHONE

允许应用使用麦克风。

**权限级别**：normal

**授权方式**：user_grant

**ACL使能**：TRUE

**起始版本**：8

## ohos.permission.SEND_MESSAGES

允许应用发送短信。

**权限级别**：system_basic

**授权方式**：user_grant

**ACL使能**：TRUE

**起始版本**：8

## ohos.permission.WRITE_CALENDAR

允许应用添加、移除或更改日历活动。

**权限级别**：normal

**授权方式**：user_grant

**ACL使能**：TRUE

**起始版本**：8

## ohos.permission.WRITE_CALL_LOG

允许应用添加、移除或更改通话记录。

**权限级别**：system_basic

**授权方式**：user_grant

**ACL使能**：TRUE

**起始版本**：8

## ohos.permission.WRITE_CONTACTS

允许应用添加、移除或更改联系人数据。

**权限级别**：system_basic

**授权方式**：user_grant

**ACL使能**：TRUE

**起始版本**：8

## ohos.permission.DISTRIBUTED_DATASYNC

允许不同设备间的数据交换。

**权限级别**：normal

**授权方式**：user_grant

**ACL使能**：TRUE

**起始版本**：7

## ohos.permission.MANAGE_VOICEMAIL

允许应用在语音信箱中留言。

**权限级别**：system_basic

**授权方式**：user_grant

**ACL使能**：TRUE

**起始版本**：8

## ohos.permission.LOCATION_IN_BACKGROUND

允许应用在后台运行时获取设备位置信息。

**权限级别**：normal

**授权方式**：user_grant

**ACL使能**：FALSE

**起始版本**：7

## ohos.permission.LOCATION

允许应用获取设备位置信息。

**申请条件**：使用API version 9以下版本的SDK开发的应用，可以直接申请此权限。使用API version 9及API version 9以上版本的SDK开发的应用，需要先申请权限[ohos.permission.APPROXIMATELY_LOCATION](#ohospermissionapproximately_location)，才可申请此权限。

**权限级别**：normal

**授权方式**：user_grant

**ACL使能**：TRUE

**起始版本**：7

## ohos.permission.APPROXIMATELY_LOCATION

允许应用获取设备模糊位置信息。

**申请条件**：仅供使用API version 9及API version 9以上版本的SDK开发的应用申请。

**权限级别**：normal

**授权方式**：user_grant

**ACL使能**：FALSE

**起始版本**：9

## ohos.permission.MEDIA_LOCATION

允许应用访问用户媒体文件中的地理位置信息。

**权限级别**：normal

**授权方式**：user_grant

**ACL使能**：TRUE

**起始版本**：7

## ohos.permission.CAMERA

允许应用使用相机拍摄照片和录制视频。

**权限级别**：normal

**授权方式**：user_grant

**ACL使能**：TRUE

**起始版本**：9

## ohos.permission.READ_MEDIA

允许应用读取用户外部存储中的媒体文件信息。

**权限级别**：normal

**授权方式**：user_grant

**ACL使能**：TRUE

**起始版本**：7

## ohos.permission.WRITE_MEDIA

允许应用读写用户外部存储中的媒体文件信息。

**权限级别**：normal

**授权方式**：user_grant

**ACL使能**：TRUE

**起始版本**：7

## ohos.permission.ACTIVITY_MOTION

允许应用读取用户当前的运动状态。

**权限级别**：normal

**授权方式**：user_grant

**ACL使能**：TRUE

**起始版本**：7

## ohos.permission.READ_HEALTH_DATA

允许应用读取用户的健康数据。

**权限级别**：normal

**授权方式**：user_grant

**ACL使能**：TRUE

**起始版本**：7

## ohos.permission.GET_DEFAULT_APPLICATION

允许应用查询默认应用。

**权限级别**：system_core

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：9

## ohos.permission.SET_DEFAULT_APPLICATION

允许应用设置、重置默认应用。

**权限级别**：system_core

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：9

## ohos.permission.MANAGE_DISPOSED_APP_STATUS

允许设置和查询应用的处置状态。

**权限级别**：system_core

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：9

## ohos.permission.ACCESS_IDS

允许应用查询设备的唯一标识符信息。

**权限级别**：system_core

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：9

## ohos.permission.DUMP

允许导出系统基础信息和SA服务信息。

**权限级别**：system_core

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：9

## ohos.permission.DISTRIBUTED_SOFTBUS_CENTER

允许不同设备之间进行组网处理。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：FALSE

**起始版本**：9

## ohos.permission.ACCESS_DLP_FILE

允许对DLP文件进行权限配置和管理。

**权限级别**：system_core

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：9

## ohos.permission.PROVISIONING_MESSAGE

允许激活超级设备管理器应用。

**权限级别**：system_core

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：9

## ohos.permission.ACCESS_SYSTEM_SETTINGS

允许应用接入或拉起系统设置界面。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：9

## ohos.permission.READ_IMAGEVIDEO

允许读取用户公共目录的图片或视频文件。

**权限级别**：system_basic

**授权方式**：user_grant

**ACL使能**：TRUE

**起始版本**：9

## ohos.permission.READ_AUDIO

允许读取用户公共目录的音频文件。

**权限级别**：system_basic

**授权方式**：user_grant

**ACL使能**：TRUE

**起始版本**：9

## ohos.permission.READ_DOCUMENT

允许读取用户公共目录的文档。

**权限级别**：system_basic

**授权方式**：user_grant

**ACL使能**：TRUE

**起始版本**：9

## ohos.permission.WRITE_IMAGEVIDEO

允许修改用户公共目录的图片或视频文件。

**权限级别**：system_basic

**授权方式**：user_grant

**ACL使能**：TRUE

**起始版本**：9

## ohos.permission.WRITE_AUDIO

允许修改用户公共目录的音频文件。

**权限级别**：system_basic

**授权方式**：user_grant

**ACL使能**：TRUE

**起始版本**：9

## ohos.permission.WRITE_DOCUMENT

允许修改用户公共目录的文档。

**权限级别**：system_basic

**授权方式**：user_grant

**ACL使能**：TRUE

**起始版本**：9

## ohos.permission.ABILITY_BACKGROUND_COMMUNICATION

允许应用将Ability组件在后台启动并与该Ability建立通信连接。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：9

## ohos.permission.securityguard.REPORT_SECURITY_INFO

允许应用上报风险数据至设备风险管理平台。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：9

## ohos.permission.securityguard.REQUEST_SECURITY_MODEL_RESULT

允许应用获取设备风险状态。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：9

## ohos.permission.securityguard.REQUEST_SECURITY_EVENT_INFO

允许应用获取风险详细数据。

**权限级别**：system_core

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：9

## ohos.permission.READ_ACCESSIBILITY_CONFIG

允许应用读取无障碍配置信息。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：FALSE

**起始版本**：9

## ohos.permission.WRITE_ACCESSIBILITY_CONFIG

允许应用设置无障碍配置信息。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：FALSE

**起始版本**：9

## ohos.permission.ACCESS_CERT_MANAGER_INTERNAL

允许应用进行证书及凭据的安装、卸载、启用、禁用等操作。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：9

## ohos.permission.ACCESS_CERT_MANAGER

允许应用进行查询证书及私有凭据等操作。

**权限级别**：normal

**授权方式**：system_grant

**ACL使能**：FALSE

**起始版本**：9

## ohos.permission.ACCESS_PUSH_SERVICE

允许应用访问推送服务的Ability。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：9

## ohos.permission.READ_APP_PUSH_DATA

允许推送服务读取应用中推送服务存储的数据。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：FALSE

**起始版本**：10

## ohos.permission.WRITE_APP_PUSH_DATA

允许推送服务往应用中写入数据。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：FALSE

**起始版本**：10

## ohos.permission.RECEIVER_STARTUP_COMPLETED

允许应用订阅开机广播。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：FALSE

**起始版本**：9

## ohos.permission.MANAGE_CAMERA_CONFIG

允许应用进行全局相机开关等操作。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：9

## ohos.permission.READ_WHOLE_CALENDAR

允许应用读取所有的日历信息。

**权限级别**：system_basic

**授权方式**：user_grant

**ACL使能**：TRUE

**起始版本**：9

## ohos.permission.WRITE_WHOLE_CALENDAR

允许应用添加、移除或更改所有的日历活动。

**权限级别**：system_basic

**授权方式**：user_grant

**ACL使能**：TRUE

**起始版本**：9

## ohos.permission.ENFORCE_USER_IDM

允许SA无token删除IAM子系统用户信息。

**权限级别**：system_core

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：9

## ohos.permission.ACCESS_AUTH_RESPOOL

允许SA注册执行器。

**权限级别**：system_core

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：9

## ohos.permission.MOUNT_UNMOUNT_MANAGER

允许应用对外卡进行挂载卸载操作。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：9

## ohos.permission.MOUNT_FORMAT_MANAGER

允许应用对外卡进行格式化操作。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：9

## ohos.permission.STORAGE_MANAGER

允许应用调用storage manager服务中对空间统计以及卷信息的查询接口。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：9

## ohos.permission.BACKUP

允许应用拥有备份恢复能力。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：9

## ohos.permission.CLOUDFILE_SYNC_MANAGER

允许应用获取端云同步管理能力。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：10

## ohos.permission.CLOUDFILE_SYNC

允许应用使用端云同步能力。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：10

## ohos.permission.FILE_ACCESS_MANAGER

允许文件管理类应用通过FAF框架访问公共数据文件。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：9

## ohos.permission.MANAGE_AUDIO_CONFIG

允许应用进行全局麦克风静音等操作。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：9

## ohos.permission.ACCESS_SERVICE_DM

允许系统应用获取分布式设备的认证组网能力。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：10+

## ohos.permission.APP_TRACKING_CONSENT

允许应用读取开放匿名设备标识符。

**权限级别**：normal

**授权方式**：user_grant

**ACL使能**：TRUE

**起始版本**：9

## ohos.permission.RUN_ANY_CODE

允许应用运行未签名的代码。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：10

## ohos.permission.PUBLISH_SYSTEM_COMMON_EVENT

允许应用发布系统公共事件。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：10

## ohos.permission.ACCESS_SCREEN_LOCK_INNER

允许应用使用锁屏服务的锁定屏幕、发送锁屏事件、系统事件回调功能。

**权限级别**：system_core

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：10

## ohos.permission.PRINT

允许应用获取打印框架的能力。

**权限级别**：normal

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：10

## ohos.permission.MANAGE_PRINT_JOB

允许应用获取管理打印任务的能力。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：10

## ohos.permission.CHANGE_OVERLAY_ENABLED_STATE

允许系统应用禁用使能overlay特性的应用。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：10

## ohos.permission.CONNECT_CELLULAR_CALL_SERVICE

允许系统服务访问蜂窝通话SA。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：FALSE

**起始版本**：10

## ohos.permission.CONNECT_IMS_SERVICE

允许系统服务访问IMS SA。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：FALSE

**起始版本**：10

## ohos.permission.ACCESS_SENSING_WITH_ULTRASOUND

允许应用使用超声波感知。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：FALSE

**起始版本**：10

## ohos.permission.INSTALL_ENTERPRISE_BUNDLE

允许应用安装、卸载其他企业InHouse应用。

**权限级别**：system_core

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：10

## ohos.permission.PROXY_AUTHORIZATION_URI

允许应用代理授权URI。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：10

## ohos.permission.GET_INSTALLED_BUNDLE_LIST

允许应用读取已安装应用列表。

**权限级别**：system_basic

**授权方式**：user_grant

**ACL使能**：TRUE

**起始版本**：10

## ohos.permission.MANAGE_DISTRIBUTED_ACCOUNTS

允许应用管理系统分布式帐号信息。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：9

## ohos.permission.GET_DISTRIBUTED_ACCOUNTS

允许应用查询系统分布式帐号信息。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：9

## ohos.permission.GET_LOCAL_ACCOUNTS

允许应用查询系统本地帐号信息。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：9

## ohos.permission.READ_HIVIEW_SYSTEM

允许应用访问hiview的数据。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：10

## ohos.permission.WRITE_HIVIEW_SYSTEM

允许应用修改hiview的数据。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：10

## ohos.permission.ACCESS_CAST_ENGINE_MIRROR

允许应用使用镜像投屏能力。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：10

## ohos.permission.ACCESS_CAST_ENGINE_STREAM

允许应用调用系统资源投射能力。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：10

## ohos.permission.CLOUDDATA_CONFIG

允许应用获取配置数据库端云信息能力。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：10

## ohos.permission.MANAGE_SENSOR

允许不直接使用传感器的应用打开和关闭传感器。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：10

## ohos.permission.DEVICE_STANDBY_EXEMPTION

允许应用在系统待机模式正常使用资源。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：10

## ohos.permission.RESTRICT_APPLICATION_ACTIVE

允许待机续航部件发布一个自定义的限网事件。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：FALSE

**起始版本**：10

## ohos.permission.UPLOAD_SESSION_MANAGER

允许应用管理上传任务会话。

**权限级别**：system_core

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：10

## ohos.permission.PREPARE_APP_TERMINATE

允许应用关闭前执行自定义的预关闭动作。

**权限级别**：normal

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：10

## ohos.permission.MANAGE_ECOLOGICAL_RULE

允许为管控服务设置场景值生成规则和配套的体验。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：10

## ohos.permission.GET_SCENE_CODE

允许应用获取指定应用当前的场景值。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：10

## ohos.permission.FILE_GUARD_MANAGER

允许应用进行公共目录扫描及设置文件扩展属性。

**权限级别**：system_core

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：10

## ohos.permission.SET_FILE_GUARD_POLICY

允许应用下发文件管控策略。

**权限级别**：system_core

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：10

## ohos.permission.securityguard.SET_MODEL_STATE

允许应用控制设备风险管理平台模型开关。

**权限级别**：system_core

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：10

## ohos.permission.hsdr.HSDR_ACCESS

允许应用访问安全检测与响应框架。

**权限级别**：normal

**授权方式**：system_grant

**ACL使能**：FALSE

**起始版本**：10

## ohos.permission.SUPPORT_USER_AUTH

允许应用与用户认证框架交互和注册扩展能力。

**权限级别**: system_basic

**授权方式**：system_grant

**ACL使能**：FALSE

**起始版本**：10

## ohos.permission.ACCESS_BUNDLE_DIR

允许应用访问其他应用安装目录。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：9

## ohos.permission.CAPTURE_VOICE_DOWNLINK_AUDIO

允许应用采集语音下行音频。

**权限级别**：system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：10

## ohos.permission.MANAGE_INTELLIGENT_VOICE

允许应用访问智能语音服务接口。

**权限级别**: system_basic

**授权方式**：system_grant

**ACL使能**：TRUE

## ohos.permission.INSTALL_ENTERPRISE_MDM_BUNDLE

允许在企业设备上安装企业MDM应用包。

**权限级别**：system_core

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：10

## ohos.permission.INSTALL_ENTERPRISE_NORMAL_BUNDLE

允许在企业设备上安装企业NORMAL应用包。

**权限级别**：system_core

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：10

## ohos.permission.INSTALL_SELF_BUNDLE

允许企业MDM应用在企业设备上自升级。

**权限级别**：system_core

**授权方式**：system_grant

**ACL使能**：TRUE

**起始版本**：10
