# 短信服务

## 场景介绍

短信服务模块提供了管理短信的一些基础能力，包括创建、发送短信，获取、设置发送短信的默认SIM卡槽ID，获取、设置短信服务中心地址，以及检查当前设备是否具备短信发送和接收能力等。

## 基本概念

- 短信服务

  即SMS（Short Messaging Service），是一种存储和转发服务。用户的移动电话可以通过它进行相互收发短信，内容以文本、数字或二进制非文本数据为主。发送方的信息通过短信服务中心进行储存并转发给接收方。

- 短信服务中心

  即SMSC（Short Message Service Center），负责在基站和移动设备间中继、储存或转发短消息。移动设备到短信服务中心的协议能传输来自移动设备或朝向移动设备的短消息，协议内容遵从GMS 03.40协议。

- 协议数据单元

  即PDU（Protocol Data Unit），PDU模式收发短信可以使用3种编码：7-bit、8-bit和UCS-2编码。7-bit编码用于发送普通的ASCII字符，8-bit编码通常用于发送数据短信，UCS-2编码用于发送Unicode字符。

## 约束与限制

1. 仅支持在标准系统上运行。
2. 需授予发送短信权限且插入SIM卡才可成功发送短信。


## 接口说明

> **说明：**
> 为了保证应用的运行效率，大部分API调用都是异步的，对于异步调用的API均提供了callback和Promise两种方式，以下示例均采用callback函数，更多方式可以查阅[API参考](../reference/apis/js-apis-sms.md)。

| 接口名                                                       | 描述                                                    |
| ------------------------------------------------------------ | ------------------------------------------------------- |
| createMessage(pdu: Array\<number>, specification: string, callback: AsyncCallback\<ShortMessage>): void | 基于协议数据单元（PDU）和指定的SMS协议创建SMS消息实例。 |
| sendMessage(options: SendMessageOptions): void               | 发送文本或数据SMS消息。                                                      |
| getDefaultSmsSlotId(callback: AsyncCallback\<number>): void   | 获取用于发送短信的默认SIM卡。                                                |
| setSmscAddr(slotId: number, smscAddr: string, callback: AsyncCallback\<void>): void | 根据指定的插槽ID设置短信服务中心的地址。                |
| getSmscAddr(slotId: number, callback: AsyncCallback\<string>): void | 根据指定的插槽ID获取短信服务中心地址。                                  |


## 开发步骤

1. 声明接口调用所需要的权限：
   - 如果是想发送短信，则调用sendMessage接口，需要配置ohos.permission.SEND_MESSAGES权限，权限级别为system_basic。
   - 如果是想设置短信服务中心地址，则调用setSmscAddr接口，需要配置ohos.permission.SET_TELEPHONY_STATE权限，权限级别为system_basic。
   - 如果是想获取短信服务中心地址，则调用getSmscAddr接口，需要配置ohos.permission.GET_TELEPHONY_STATE权限，权限级别为system_basic。
   在申请权限前，请保证符合[权限使用的基本原则](../security/accesstoken-overview.md#权限使用的基本原则)。然后参考[配置文件权限声明指导文档](../security/accesstoken-guidelines.md#配置文件权限声明)声明对应权限。

2. import需要的模块。

3. 基于协议数据单元（PDU）和指定的SMS协议创建SMS消息实例。

4. 发送SMS消息。

   ```js
    // import需要的模块
    import sms from '@ohos.telephony.sms'
   
    export default class SmsModel {
        async createMessage() {
            const specification = '3gpp'
            const pdu = [0x08, 0x91] // 以数组的形式显示协议数据单元（PDU），类型为number
            const shortMessage = await sms.createMessage(pdu, specification)
            Logger.info(`${TAG}, createMessageCallback: shortMessage = ${JSON.stringify(shortMessage)}`)
            return shortMessage
        }
   
        sendMessage(slotId, content, destinationHost, serviceCenter, destinationPort, handleSend, handleDelivery) {
            Logger.info(`${TAG}, sendMessage start ${slotId} ${content} ${destinationHost} ${serviceCenter} ${destinationPort}`)
            const options =
            {
                slotId: slotId,
                content: content,
                destinationHost: destinationHost,
                serviceCenter: serviceCenter,
                destinationPort: destinationPort,
                sendCallback(err, data) {
                    Logger.info(`${TAG}, sendCallback: data = ${JSON.stringify(data)} err = ${JSON.stringify(err)}`)
                    handleSend(err, data)
                },
                deliveryCallback(err, data) {
                    Logger.info(`${TAG}, deliveryCallback: data = ${JSON.stringify(data)} err = ${JSON.stringify(err)}`)
                    handleDelivery(err, data)
                }
            }
            // 发送SMS消息
            sms.sendMessage(options)
            Logger.info(`${TAG}, sendMessage end`)
        }
   
        // 获取用于发送短信的默认SIM卡
        async getDefaultSmsSlotId() {
            const defaultSmsSlotId = await sms.getDefaultSmsSlotId()
            Logger.info(`${TAG}, getDefaultSmsSlotId: defaultSmsSlotId = ${defaultSmsSlotId}`)
            return defaultSmsSlotId
        }
   
        // 根据指定的插槽ID设置短信服务中心的地址
        async setSmscAddr(slotId, smscAddr) {
            const serviceCenter = await sms.setSmscAddr(slotId, smscAddr)
            Logger.info(`${TAG}, setSmscAddr: serviceCenter = ${JSON.stringify(serviceCenter)}`)
            return serviceCenter
        }
   
        // 根据指定的插槽ID获取短信服务中心地址
        async getSmscAddr(slotId) {
            const serviceCenter = await sms.getSmscAddr(slotId)
            Logger.info(`${TAG}, getSmscAddr: serviceCenter = ${JSON.stringify(serviceCenter)}`)
            return serviceCenter
        }
    }
   ```


## 相关实例

针对短信的使用，有以下相关实例可供参考：
- [短信服务](https://gitee.com/openharmony/applications_app_samples/tree/master/code/BasicFeature/Telephony/Message)
