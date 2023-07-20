# HTTP数据请求

## 场景介绍

应用通过HTTP发起一个数据请求，支持常见的GET、POST、OPTIONS、HEAD、PUT、DELETE、TRACE、CONNECT方法。

## 接口说明

HTTP数据请求功能主要由http模块提供。

使用该功能需要申请ohos.permission.INTERNET权限。

权限申请请参考[访问控制（权限）开发指导](../security/accesstoken-guidelines.md)。

涉及的接口如下表，具体的接口说明请参考[API文档](../reference/apis/js-apis-http.md)。

| 接口名                                    | 功能描述                            |
| ----------------------------------------- | ----------------------------------- |
| createHttp()                              | 创建一个http请求。                  |
| request()                                 | 根据URL地址，发起HTTP网络请求。     |
| request2()<sup>10+</sup>                  | 根据URL地址，发起HTTP网络请求并返回流式响应|
| destroy()                                 | 中断请求任务。                      |
| on(type: 'headersReceive')                | 订阅HTTP Response Header 事件。     |
| off(type: 'headersReceive')               | 取消订阅HTTP Response Header 事件。 |
| once\('headersReceive'\)<sup>8+</sup>     | 订阅HTTP Response Header 事件，但是只触发一次。|
| on\('dataReceive'\)<sup>10+</sup>         | 订阅HTTP流式响应数据接收事件。      |
| off\('dataReceive'\)<sup>10+</sup>        | 取消订阅HTTP流式响应数据接收事件。  |
| on\('dataEnd'\)<sup>10+</sup>             | 订阅HTTP流式响应数据接收完毕事件。  |
| off\('dataEnd'\)<sup>10+</sup>            | 取消订阅HTTP流式响应数据接收完毕事件。 |
| on\('dataProgress'\)<sup>10+</sup>        | 订阅HTTP流式响应数据接收进度事件。  |
| off\('dataProgress'\)<sup>10+</sup>       | 取消订阅HTTP流式响应数据接收进度事件。 |

## request接口开发步骤

1. 从@ohos.net.http.d.ts中导入http命名空间。
2. 调用createHttp()方法，创建一个HttpRequest对象。
3. 调用该对象的on()方法，订阅http响应头事件，此接口会比request请求先返回。可以根据业务需要订阅此消息。
4. 调用该对象的request()方法，传入http请求的url地址和可选参数，发起网络请求。
5. 按照实际业务需要，解析返回结果。
6. 调用该对象的off()方法，取消订阅http响应头事件。
7. 当该请求使用完毕时，调用destroy()方法主动销毁。

```js
// 引入包名
import http from '@ohos.net.http';

// 每一个httpRequest对应一个HTTP请求任务，不可复用
let httpRequest = http.createHttp();
// 用于订阅HTTP响应头，此接口会比request请求先返回。可以根据业务需要订阅此消息
// 从API 8开始，使用on('headersReceive', Callback)替代on('headerReceive', AsyncCallback)。 8+
httpRequest.on('headersReceive', (header) => {
  console.info('header: ' + JSON.stringify(header));
});
httpRequest.request(
  // 填写HTTP请求的URL地址，可以带参数也可以不带参数。URL地址需要开发者自定义。请求的参数可以在extraData中指定"EXAMPLE_URL",
  {
    method: http.RequestMethod.POST, // 可选，默认为http.RequestMethod.GET
    // 开发者根据自身业务需要添加header字段
    header: {
      'Content-Type': 'application/json'
    },
    // 当使用POST请求时此字段用于传递内容
    extraData: {
      "data": "data to send",
    },
    expectDataType: http.HttpDataType.STRING, // 可选，指定返回数据的类型
    usingCache: true, // 可选，默认为true
    priority: 1, // 可选，默认为1
    connectTimeout: 60000, // 可选，默认为60000ms
    readTimeout: 60000, // 可选，默认为60000ms
    usingProtocol: http.HttpProtocol.HTTP1_1, // 可选，协议类型默认值由系统自动指定
    usingProxy: false, //可选，默认不使用网络代理，自API 10开始支持该属性
  }, (err, data) => {
    if (!err) {
      // data.result为HTTP响应内容，可根据业务需要进行解析
      console.info('Result:' + JSON.stringify(data.result));
      console.info('code:' + JSON.stringify(data.responseCode));
      // data.header为HTTP响应头，可根据业务需要进行解析
      console.info('header:' + JSON.stringify(data.header));
      console.info('cookies:' + JSON.stringify(data.cookies)); // 8+
      // 当该请求使用完毕时，调用destroy方法主动销毁
      httpRequest.destroy();
    } else {
      console.info('error:' + JSON.stringify(err));
      // 取消订阅HTTP响应头事件
      httpRequest.off('headersReceive');
      // 当该请求使用完毕时，调用destroy方法主动销毁
      httpRequest.destroy();
    }
  }
);
```

## request2接口开发步骤

1. 从@ohos.net.http.d.ts中导入http命名空间。
2. 调用createHttp()方法，创建一个HttpRequest对象。
3. 调用该对象的on()方法，可以根据业务需要订阅HTTP响应头事件、HTTP流式响应数据接收事件、HTTP流式响应数据接收进度事件和HTTP流式响应数据接收完毕事件。
4. 调用该对象的request2()方法，传入http请求的url地址和可选参数，发起网络请求。
5. 按照实际业务需要，可以解析返回的响应码。
6. 调用该对象的off()方法，取消订阅相应事件。
7. 当该请求使用完毕时，调用destroy()方法主动销毁。

```js
// 引入包名
import http from '@ohos.net.http'

// 每一个httpRequest对应一个HTTP请求任务，不可复用
let httpRequest = http.createHttp();
// 用于订阅HTTP响应头事件
httpRequest.on('headersReceive', (header) => {
  console.info('header: ' + JSON.stringify(header));
});
// 用于订阅HTTP流式响应数据接收事件
let res = '';
httpRequest.on('dataReceive', (data) => {
  res += data;
  console.info('res: ' + res);
});
// 用于订阅HTTP流式响应数据接收完毕事件
httpRequest.on('dataEnd', () => {
  console.info('No more data in response, data receive end');
});
// 用于订阅HTTP流式响应数据接收进度事件
httpRequest.on('dataProgress', (data) => {
  console.log("dataProgress receiveSize:" + data.receiveSize + ", totalSize:" + data.totalSize);
});

httpRequest.request2(
  // 填写HTTP请求的URL地址，可以带参数也可以不带参数。URL地址需要开发者自定义。请求的参数可以在extraData中指定
  "EXAMPLE_URL",
  {
    method: http.RequestMethod.POST, // 可选，默认为http.RequestMethod.GET
    // 开发者根据自身业务需要添加header字段
    header: {
      'Content-Type': 'application/json'
    },
    // 当使用POST请求时此字段用于传递内容
    extraData: {
      "data": "data to send",
    },
    expectDataType: http.HttpDataType.STRING, // 可选，指定返回数据的类型
    usingCache: true, // 可选，默认为true
    priority: 1, // 可选，默认为1
    connectTimeout: 60000, // 可选，默认为60000ms
    readTimeout: 60000, // 可选，默认为60000ms。若传输的数据较大，需要较长的时间，建议增大该参数以保证数据传输正常终止
    usingProtocol: http.HttpProtocol.HTTP1_1, // 可选，协议类型默认值由系统自动指定
  }, (err, data) => {
    console.info('error:' + JSON.stringify(err));
    console.info('ResponseCode :' + JSON.stringify(data));
    // 取消订阅HTTP响应头事件
    httpRequest.off('headersReceive');
    // 取消订阅HTTP流式响应数据接收事件
    httpRequest.off('dataReceive');
    // 取消订阅HTTP流式响应数据接收进度事件
    httpRequest.off('dataProgress');
    // 取消订阅HTTP流式响应数据接收完毕事件
    httpRequest.off('dataEnd');
    // 当该请求使用完毕时，调用destroy方法主动销毁
    httpRequest.destroy();
  }
);
```

## 相关实例

针对HTTP数据请求，有以下相关实例可供参考：

- [`Http:`数据请求（ArkTS）（API9））](https://gitee.com/openharmony/applications_app_samples/tree/master/code/BasicFeature/Connectivity/Http)