# 网络连接管理

## 简介

网络连接管理提供管理网络一些基础能力，包括WiFi/蜂窝/Ethernet等多网络连接优先级管理、网络质量评估、订阅默认/指定网络连接状态变化、查询网络连接信息、DNS解析等功能。

> **说明：**
> 为了保证应用的运行效率，大部分API调用都是异步的，对于异步调用的API均提供了callback和Promise两种方式，以下示例均采用callback函数，更多方式可以查阅[API参考](../reference/apis/js-apis-net-connection.md)。

## 基本概念

- 网络生产者：数据网络的提供方，比如WiFi、蜂窝、Ethernet等。
- 网络消费者：数据网络的使用方，比如应用或系统服务。
- 网络探测：检测网络有效性，避免将网络从可用网络切换到不可用网络。内容包括绑定网络探测、DNS探测、HTTP探测及HTTPS探测。
- 网络优选：处理多网络共存时选择最优网络。在网络状态、网络信息及评分发生变化时被触发。

## 约束

- 开发语言：C++ JS
- 系统：linux内核
- 本模块首批接口从API version 8开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。

## 场景介绍

网络连接管理的典型场景有：

- 接收指定网络的状态变化通知
- 获取所有注册的网络
- 根据数据网络查询网络的连接信息
- 使用对应网络解析域名，获取所有IP

以下分别介绍具体开发方式。

## 接口说明

完整的JS API说明以及实例代码请参考：[网络连接管理](../reference/apis/js-apis-net-connection.md)。

| 类型 | 接口 | 功能说明 |
| ---- | ---- | ---- |
| ohos.net.connection | function getDefaultNet(callback: AsyncCallback\<NetHandle>): void; |获取一个含有默认网络的netId的NetHandle对象，使用callback回调 |
| ohos.net.connection | function getGlobalHttpProxy<sup>10+</sup>(callback: AsyncCallback\<HttpProxy>): void;| 获取网络的全局代理设置，使用callback回调 |
| ohos.net.connection | function setGlobalHttpProxy<sup>10+</sup>(httpProxy: HttpProxy, callback: AsyncCallback\<void>): void;| 设置网络全局Http代理配置信息，使用callback回调 |
| ohos.net.connection | function getAppNet<sup>9+</sup>(callback: AsyncCallback\<NetHandle>): void;| 获取一个App绑定的包含了网络netId的NetHandle对象，使用callback回调 |
| ohos.net.connection | function setAppNet<sup>9+</sup>(netHandle: NetHandle, callback: AsyncCallback\<void>): void;| 绑定App到指定网络，绑定后的App只能通过指定网络访问外网。使用callback回调 |
| ohos.net.connection | function getDefaultNetSync<sup>9+</sup>(): NetHandle; |使用同步方法获取默认激活的数据网络。可以使用getNetCapabilities去获取网络的类型、拥有的能力等信息。|
| ohos.net.connection | function hasDefaultNet(callback: AsyncCallback\<boolean>): void; |查询是否有默认网络，使用callback回调 |
| ohos.net.connection | function getAllNets(callback: AsyncCallback\<Array\<NetHandle>>): void;| 获取所处于连接状态的网络的MetHandle对象列表，使用callback回调 |
| ohos.net.connection | function getConnectionProperties(netHandle: NetHandle, callback: AsyncCallback\<ConnectionProperties>): void; |查询默认网络的链路信息，使用callback回调 |
| ohos.net.connection | function getNetCapabilities(netHandle: NetHandle, callback: AsyncCallback\<NetCapabilities>): void; |查询默认网络的能力集信息，使用callback回调 |
| ohos.net.connection | function isDefaultNetMetered<sup>9+</sup>(callback: AsyncCallback\<boolean>): void; |检查当前网络上的数据流量使用是否被计量，使用callback方式作为异步方法 |
| ohos.net.connection | function reportNetConnected(netHandle: NetHandle, callback: AsyncCallback\<void>): void;| 向网络管理报告网络处于可用状态，调用此接口说明应用程序认为网络的可用性（ohos.net.connection.NetCap.NET_CAPABILITY_VAILDATED）与网络管理不一致。使用callback回调 |
| ohos.net.connection | function reportNetDisconnected(netHandle: NetHandle, callback: AsyncCallback\<void>): void;| 向网络管理报告网络处于不可用状态，调用此接口说明应用程序认为网络的可用性（ohos.net.connection.NetCap.NET_CAPABILITY_VAILDATED）与网络管理不一致。使用callback回调 |
| ohos.net.connection | function getAddressesByName(host: string, callback: AsyncCallback\<Array\<NetAddress>>): void; |使用对应网络解析域名，获取所有IP，使用callback回调 |
| ohos.net.connection | function enableAirplaneMode(callback: AsyncCallback\<void>): void; | 设置网络为飞行模式，使用callback回调 |
| ohos.net.connection | function disableAirplaneMode(callback: AsyncCallback\<void>): void;| 关闭网络飞行模式，使用callback回调 |
| ohos.net.connection | function createNetConnection(netSpecifier?: NetSpecifier, timeout?: number): NetConnection; | 返回一个NetConnection对象，netSpecifier指定关注的网络的各项特征，timeout是超时时间(单位是毫秒)，netSpecifier是timeout的必要条件，两者都没有则表示关注默认网络 |
| ohos.net.connection.NetHandle | bindSocket(socketParam: TCPSocket \| UDPSocket, callback: AsyncCallback\<void>): void; | 将TCPSocket或UDPSockett绑定到当前网络，使用callback回调 |
| ohos.net.connection.NetHandle | getAddressesByName(host: string, callback: AsyncCallback\<Array\<NetAddress>>): void; |使用默认网络解析域名，获取所有IP，使用callback回调 |
| ohos.net.connection.NetHandle | getAddressByName(host: string, callback: AsyncCallback\<NetAddress>): void; |使用对应网络解析域名，获取一个IP，调用callbac |
| ohos.net.connection.NetConnection | on(type: 'netAvailable', callback: Callback\<NetHandle>): void; |监听收到网络可用的事件 |
| ohos.net.connection.NetConnection | on(type: 'netCapabilitiesChange', callback: Callback\<{ netHandle: NetHandle, netCap: NetCapabilities }>): void; |监听网络能力变化的事件 |
| ohos.net.connection.NetConnection | on(type: 'netConnectionPropertiesChange', callback: Callback\<{ netHandle: NetHandle, connectionProperties: ConnectionProperties }>): void; |监听网络连接信息变化的事件 |
| ohos.net.connection.NetConnection | on(type: 'netBlockStatusChange', callback: Callback<{ netHandle: NetHandle, blocked: boolean }>): void; |订阅网络阻塞状态事件，使用callback方式作为异步方法 |
| ohos.net.connection.NetConnection | on(type: 'netLost', callback: Callback\<NetHandle>): void; |监听网络丢失的事件 |
| ohos.net.connection.NetConnection | on(type: 'netUnavailable', callback: Callback\<void>): void; |监听网络不可用的事件 |
| ohos.net.connection.NetConnection | register(callback: AsyncCallback\<void>): void; |注册默认网络或者createNetConnection中指定的网络的监听 |
| ohos.net.connection.NetConnection | unregister(callback: AsyncCallback\<void>): void; |注销默认网络或者createNetConnection中指定的网络的监听 |

## 接收指定网络的状态变化通知

1. 从@ohos.net.connection.d.ts中导入connection命名空间。

2. 调用createNetConnection方法，指定网络能力、网络类型和超时时间（可选，如不传入代表默认网络；创建不同于默认网络时可通过指定这些参数完成），创建一个NetConnection对象。

3. 调用该对象的on()方法，传入type和callback，订阅关心的事件。

4. 调用该对象的register()方法，订阅指定网络状态变化的通知。

5. 当网络可用时，会收到netAvailable事件的回调；当网络不可用时，会收到netUnavailable事件的回调。

6. 当不使用该网络时，可以调用该对象的unregister()方法，取消订阅。

```js
// 引入包名
import connection from '@ohos.net.connection'

let netCap = {
  // 假设当前默认网络是WiFi，需要创建蜂窝网络连接，可指定网络类型为蜂窝网
  bearerTypes: [connection.NetBearType.BEARER_CELLULAR],
  // 指定网络能力为Internet
  networkCap: [connection.NetCap.NET_CAPABILITY_INTERNET],
};
let netSpec = {
  netCapabilities: netCap,
};

// 指定超时时间为10s(默认值为0)
let timeout = 10 * 1000;

// 创建NetConnection对象
let conn = connection.createNetConnection(netSpec, timeout);

// 订阅事件，如果当前指定网络可用，通过on_netAvailable通知用户
conn.on('netAvailable', (data => {
  console.log("net is available, netId is " + data.netId);
}));

// 订阅事件，如果当前指定网络不可用，通过on_netUnavailable通知用户
conn.on('netUnavailable', (data => {
  console.log("net is unavailable, netId is " + data.netId);
}));

// 订阅指定网络状态变化的通知
conn.register((err, data) => {
});

// 当不使用该网络时，可以调用该对象的unregister()方法，取消订阅
conn.unregister((err, data) => {
});
```

## 获取所有注册的网络

### 开发步骤

1. 从@ohos.net.connection.d.ts中导入connection命名空间。

2. 调用getAllNets方法，获取所有处于连接状态的网络列表。

```js
// 引入包名
import connection from '@ohos.net.connection'

// 获取所有处于连接状态的网络列表
connection.getAllNets((err, data) => {
  console.log(JSON.stringify(err));
  console.log(JSON.stringify(data));
  if (data) {
    this.netList = data;
  }
})
```

## 根据数据网络查询网络的能力信息及连接信息

### 开发步骤

1. 从@ohos.net.connection.d.ts中导入connection命名空间。

2. 通过调用getDefaultNet方法，获取默认的数据网络(NetHandle)；或者通过调用getAllNets方法，获取所有处于连接状态的网络列表(Array\<NetHandle>)。

3. 调用getNetCapabilities方法，获取NetHandle对应网络的能力信息。能力信息包含了网络类型(蜂窝网络、Wi-Fi网络、以太网网络等)、网络具体能力等网络信息。

4. 调用getConnectionProperties方法，获取NetHandle对应网络的连接信息。

```js
// 引入包名
import connection from '@ohos.net.connection'

// 调用getDefaultNet方法，获取默认的数据网络(NetHandle)
connection.getDefaultNet((err, data) => {
  console.log(JSON.stringify(err));
  console.log(JSON.stringify(data));
  if (data) {
    this.netHandle = data;
  }
})

// 获取netHandle对应网络的能力信息。能力信息包含了网络类型、网络具体能力等网络信息
connection.getNetCapabilities(this.netHandle, (err, data) => {
  console.log(JSON.stringify(err));

  // 获取网络类型(bearerTypes)
  for (let item of data.bearerTypes) {
    if (item == 0) {
      // 蜂窝网
      console.log(JSON.stringify("BEARER_CELLULAR"));
    } else if (item == 1) {
      // Wi-Fi网络
      console.log(JSON.stringify("BEARER_WIFI"));
    } else if (item == 3) {
      // 以太网网络
      console.log(JSON.stringify("BEARER_ETHERNET"));
    }
  }

  // 获取网络具体能力(networkCap)
  for (let item of data.networkCap) {
    if (item == 0) {
      // 表示网络可以访问运营商的MMSC（Multimedia Message Service，多媒体短信服务）发送和接收彩信
      console.log(JSON.stringify("NET_CAPABILITY_MMS"));
    } else if (item == 11) {
      // 表示网络流量未被计费
      console.log(JSON.stringify("NET_CAPABILITY_NOT_METERED"));
    } else if (item == 12) {
      // 表示该网络应具有访问Internet的能力，该能力由网络提供者设置
      console.log(JSON.stringify("NET_CAPABILITY_INTERNET"));
    } else if (item == 15) {
      // 表示网络不使用VPN（Virtual Private Network，虚拟专用网络）
      console.log(JSON.stringify("NET_CAPABILITY_NOT_VPN"));
    } else if (item == 16) {
      // 表示该网络访问Internet的能力被网络管理成功验证，该能力由网络管理模块设置
      console.log(JSON.stringify("NET_CAPABILITY_VALIDATED"));
    }
  }
})

// 获取netHandle对应网络的连接信息。连接信息包含了链路信息、路由信息等
connection.getConnectionProperties(this.netHandle, (err, data) => {
  console.log(JSON.stringify(err));
  console.log(JSON.stringify(data));
})

// 调用getAllNets,获取所有处于连接状态的网络列表(Array<NetHandle>)
connection.getAllNets((err, data) => {
  console.log(JSON.stringify(err));
  console.log(JSON.stringify(data));
  if (data) {
    this.netList = data;
  }
})

for (let item of this.netList) {
  // 循环获取网络列表每个netHandle对应网络的能力信息
  connection.getNetCapabilities(item, (err, data) => {
    console.log(JSON.stringify(err));
    console.log(JSON.stringify(data));
  })

  // 循环获取网络列表每个netHandle对应的网络的连接信息
  connection.getConnectionProperties(item, (err, data) => {
    console.log(JSON.stringify(err));
    console.log(JSON.stringify(data));
  })
}
```

## 使用对应网络解析域名，获取所有IP

### 开发步骤

1. 从@ohos.net.connection.d.ts中导入connection命名空间。

2. 调用getAddressesByName方法，使用默认网络解析主机名以获取所有IP地址。

```js
    // 引入包名
import connection from '@ohos.net.connection'

// 使用默认网络解析主机名以获取所有IP地址
connection.getAddressesByName(this.host, (err, data) => {
  console.log(JSON.stringify(err));
  console.log(JSON.stringify(data));
})
```
