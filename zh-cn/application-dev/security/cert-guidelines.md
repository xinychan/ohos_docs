# 证书开发指导

> **说明**
>
> 本开发指导基于API version 9，OH SDK版本3.2.9及以上，适用于JS语言开发

## 使用证书操作

**场景说明**

使用证书操作中，典型的场景有：

1. 解析X509证书数据生成证书对象。
2. 获取证书信息，比如：证书版本、证书序列号等。
3. 获取证书对象的序列化数据。
4. 获取证书公钥。
5. 证书验签。
6. 校验证书有效期。

**接口及参数说明**

详细接口说明可参考[API参考](../reference/apis/js-apis-cert.md)。

以上场景涉及的常用接口如下表所示：

| 实例名          | 接口名                                                       | 描述                                         |
| --------------- | ------------------------------------------------------------ | -------------------------------------------- |
| cryptoCert | createX509Cert(inStream : EncodingBlob, callback : AsyncCallback\<X509Cert>) : void | 使用callback方式解析X509证书数据生成证书对象 |
| cryptoCert | createX509Cert(inStream : EncodingBlob) : Promise\<X509Cert>  | 使用promise方式解析X509证书数据生成证书对象  |
| X509Cert        | verify(key : cryptoFramework.PubKey, callback : AsyncCallback\<void>) : void  | 使用callback方式进行证书验签                 |
| X509Cert        | verify(key : cryptoFramework.PubKey) : Promise\<void>                         | 使用promise方式进行证书验签                  |
| X509Cert        | getEncoded(callback : AsyncCallback\<EncodingBlob>) : void    | 使用callback方式获取证书序列化数据           |
| X509Cert        | getEncoded() : Promise\<EncodingBlob>                         | 使用promise方式获取证书序列化数据            |
| X509Cert        | getPublicKey() : cryptoFramework.PubKey                       | 获取证书公钥                               |
| X509Cert        | checkValidityWithDate(date: string) : void                   | 校验证书有效期                              |
| X509Cert        | getVersion() : number                                        | 获取证书版本                                 |
| X509Cert        | getSerialNumber() : number                                   | 获取证书序列号                               |
| X509Cert        | getIssuerName() : DataBlob                                   | 获取证书颁发者名称                           |
| X509Cert        | getSubjectName() : DataBlob                                  | 获取证书主体名称                             |
| X509Cert        | getNotBeforeTime() : string                                  | 获取证书有效期起始时间                       |
| X509Cert        | getNotAfterTime() : string                                   | 获取证书有效期截至时间                       |
| X509Cert        | getSignature() : DataBlob                                    | 获取证书签名                                 |
| X509Cert        | getSignatureAlgName() : string                               | 获取证书签名算法名称                         |
| X509Cert        | getSignatureAlgOid() : string                                | 获取证书签名算法OID                          |
| X509Cert        | getSignatureAlgParams() : DataBlob                           | 获取证书签名算法参数                         |
| X509Cert        | getKeyUsage() : DataBlob                                     | 获取证书秘钥用途                             |
| X509Cert        | getExtKeyUsage() : DataArray                                 | 获取证书扩展秘钥用途                         |
| X509Cert        | getBasicConstraints() : number                               | 获取证书基本约束                             |
| X509Cert        | getSubjectAltNames() : DataArray                             | 获取证书主体可选名称                         |
| X509Cert        | getIssuerAltNames() : DataArray                              | 获取证书颁发者可选名称                       |
| X509Cert        | getItem(itemType: CertItemType) : DataBlob<sup>10+</sup>          | 获取X509证书对应的字段                       |
**开发步骤**

示例：解析X509证书数据生成证书对象，并调用对象方法（包含场景1-6）

```javascript
import cryptoCert from '@ohos.security.cert';
import cryptoFramework from '@ohos.security.cryptoFramework';

// 证书数据，此处仅示例，业务需根据场景自行设置
let certData = "-----BEGIN CERTIFICATE-----\n"
+ "MIID/jCCAuagAwIBAgIBATANBgkqhkiG9w0BAQsFADCBjDELMAkGA1UEBhMCQ04x\n"
+ "ETAPBgNVBAgMCHNoYW5naGFpMQ8wDQYDVQQHDAZodWF3ZWkxFTATBgNVBAoMDHd3\n"
+ "dy50ZXN0LmNvbTENMAsGA1UECwwEdGVzdDEVMBMGA1UEAwwMd3d3LnRlc3QuY29t\n"
+ "MRwwGgYJKoZIhvcNAQkBFg10ZXN0QHRlc3QuY29tMB4XDTIyMDgyOTA2NTUwM1oX\n"
+ "DTIzMDgyOTA2NTUwM1owezELMAkGA1UEBhMCQ04xETAPBgNVBAgMCHNoYW5naGFp\n"
+ "MRUwEwYDVQQKDAx3d3cudGVzdC5jb20xDTALBgNVBAsMBHRlc3QxFTATBgNVBAMM\n"
+ "DHd3dy50ZXN0LmNvbTEcMBoGCSqGSIb3DQEJARYNdGVzdEB0ZXN0LmNvbTCCASIw\n"
+ "DQYJKoZIhvcNAQEBBQADggEPADCCAQoCggEBAJmY9T4SzXXwKvfMvnvMWY7TqUJK\n"
+ "jnWf2Puv0YUQ2fdvyoKQ2LQXdtzoUL53j587oI+IXelOr7dg020zPyun0cmZHZ4y\n"
+ "l/qAcrWbDjZeEGcbbb5UtQtn1WOEnv8pkXluO355mbZQUKK9L3gFWseXJKGbIXw0\n"
+ "NRpaJZzqvPor4m3a5pmJKPHOlivUdYfLaKSkNj3DlaFzCWKV82k5ee6gzVyETtG+\n"
+ "XN+vq8qLybT+fIFsLNMmAHzRxlqz3NiH7yh+1/p/Knvf8bkkRVR2btH51RyX2RSu\n"
+ "DjPM0/VRL8fxDSDeWBq+Gvn/E6AbOVMmkx63tcyWHhklCSaZtyz7kq39TQMCAwEA\n"
+ "AaN7MHkwCQYDVR0TBAIwADAsBglghkgBhvhCAQ0EHxYdT3BlblNTTCBHZW5lcmF0\n"
+ "ZWQgQ2VydGlmaWNhdGUwHQYDVR0OBBYEFFiFDysfADQCzRZCOSPupQxFicwzMB8G\n"
+ "A1UdIwQYMBaAFNYQRQiPsG8HefOTsmsVhaVjY7IPMA0GCSqGSIb3DQEBCwUAA4IB\n"
+ "AQAeppxf6sKQJxJQXKPTT3xHKaskidNwDBbOSIvnVvWXicZXDs+1sF6tUaRgvPxL\n"
+ "OL58+P2Jy0tfSwj2WhqQRGe9MvQ5iFHcdelZc0ciW6EQ0VDHIaDAQc2nQzej/79w\n"
+ "UE7BJJV3b9n1be2iCsuodKO14pOkMb84WcIxng+8SD+MiFqV5BPO1QyKGdO1PE1b\n"
+ "+evjyTpFSTgZf2Mw3fGtu5hfEXyHw1lnsFY2MlSwiRlAym/gm4aXy+4H6LyXKd56\n"
+ "UYQ6fituD0ziaw3RI6liyIe7aENHCkZf6bAvMRhk4QiU4xu6emwX8Qt1bT7RthP0\n"
+ "1Vsro0IOeXT9WAcqEtQUegsi\n"
+ "-----END CERTIFICATE-----\n";

// string转Uint8Array
function stringToUint8Array(str) {
    var arr = [];
    for (var i = 0, j = str.length; i < j; i++) {
        arr.push(str.charCodeAt(i));
    }
    return new Uint8Array(arr);
}

// 证书示例
function certSample() {
    let encodingBlob = {
        // 将string类型证书数据转为Uint8Array
        data: stringToUint8Array(certData),
        // 证书格式：支持PEM和DER，此例中对应PEM
        encodingFormat: cryptoCert.EncodingFormat.FORMAT_PEM
    };

    // 创建证书对象
    cryptoCert.createX509Cert(encodingBlob, function (err, x509Cert) {
        if (err != null) {
            // 创建证书对象失败
            console.log("createX509Cert failed, errCode: " + err.code + ", errMsg: " + err.message);
            return;
        }
        // 创建证书对象成功
        console.log("createX509Cert success");

        // 获取证书版本
        let version = x509Cert.getVersion();
        
        // 获取证书对象的序列化数据
        x509Cert.getEncoded(function (err, data) {
            if (err != null) {
                // 获取序列化数据失败
                console.log("getEncoded failed, errCode: " + err.code + ", errMsg: " + err.message);
            } else {
                // 获取序列化数据成功
                console.log("getEncoded success");
            }
        });

        // 业务需通过上级证书对象或本证书对象(自签名)的getPublicKey接口获取公钥对象，此处省略
        let pubKey = null;
        try {
            pubKey = x509Cert.getPublicKey();
        } catch (error) {
            console.log("getPublicKey failed, errCode: " + error.code + ", errMsg: " + error.message);
        }

        // 证书验签
        x509Cert.verify(pubKey, function (err, data) {
            if (err == null) {
                // 验签成功
                console.log("verify success");
            } else {
                // 验签失败
                console.log("verify failed, errCode: " + err.code + ", errMsg: " + err.message);
            }
        });

        // 时间字符串
        let date = "20220830000001Z";
        
        // 校验证书有效期
        try {
            x509Cert.checkValidityWithDate(date);
        } catch (error) {
            console.log("checkValidityWithDate failed, errCode: " + error.code + ", errMsg: " + error.message);
        }
    });
}
```

## 使用证书扩展域段操作

> **说明**
>
> 本场景基于API version 10，OH SDK版本4.0.9及以上，适用于JS语言开发

**场景说明**

使用证书扩展域段操作中，典型的场景有：

1. 解析证书扩展域段数据生成证书扩展域段对象。
2. 获取证书扩展域段信息，比如：证书扩展域段对象标识符列表，根据对象标识符获取具体数据等。
3. 校验证书是否为CA证书。

**接口及参数说明**

详细接口说明可参考[API参考](../reference/apis/js-apis-cert.md)。

以上场景涉及的常用接口如下表所示：

| 实例名        | 接口名                                                       | 描述                                   |
| ------------- | ------------------------------------------------------------ | -------------------------------------- |
| cryptoCert    | createCertExtension(inStream : EncodingBlob, callback : AsyncCallback) : void | 使用callback方式创建证书扩展域段的对象 |
| cryptoCert    | createCertExtension(inStream : EncodingBlob) : Promise       | 使用promise方式创建证书扩展域段的对象  |
| CertExtension | getEncoded() : EncodingBlob                                  | 获取证书扩展域段序列化数据             |
| CertExtension | getOidList(valueType : ExtensionOidType) : DataArray         | 获取证书扩展域段对象标识符列表         |
| CertExtension | getEntry(valueType: ExtensionEntryType, oid : DataBlob) : DataBlob | 获取证书扩展域段对象信息               |
| CertExtension | checkCA() : number                                           | 校验证书是否为CA证书                   |

**开发步骤**

示例：解析X509证书扩展域段数据生成证书扩展域段对象，并调用对象方法（包含场景1-3）

```javascript
import cryptoCert from '@ohos.security.cert';

// 证书扩展域段数据，此处仅示例，业务需根据场景自行设置
let certData = new Uint8Array([
  0x30, 0x40, 0x30, 0x0F, 0x06, 0x03, 0x55, 0x1D, 
  0x13, 0x01, 0x01, 0xFF, 0x04, 0x05, 0x30, 0x03,
  0x01, 0x01, 0xFF, 0x30, 0x0E, 0x06, 0x03, 0x55, 
  0x1D, 0x0F, 0x01, 0x01, 0xFF, 0x04, 0x04, 0x03,
  0x02, 0x01, 0xC6, 0x30, 0x1D, 0x06, 0x03, 0x55, 
  0x1D, 0x0E, 0x04, 0x16, 0x04, 0x14, 0xE0, 0x8C,
  0x9B, 0xDB, 0x25, 0x49, 0xB3, 0xF1, 0x7C, 0x86, 
  0xD6, 0xB2, 0x42, 0x87, 0x0B, 0xD0, 0x6B, 0xA0,
  0xD9, 0xE4
]);

// string转Uint8Array
function stringToUint8Array(str) {
  var arr = [];
  for (var i = 0, j = str.length; i < j; i++) {
    arr.push(str.charCodeAt(i));
  }
  return new Uint8Array(arr);
}

// 证书扩展域段示例
function certExtensionSample() {
  let encodingBlob = {
    data: certData,
    // 证书扩展域段格式：当前仅支持DER格式
    encodingFormat: cryptoCert.EncodingFormat.FORMAT_DER
  };

  // 创建证书扩展域段对象
  cryptoCert.createCertExtension(encodingBlob, function (err, certExtension) {
    if (err != null) {
      // 创建证书扩展域段对象失败
      console.log("createCertExtension failed, errCode: " + err.code + ", errMsg: " + err.message);
      return;
    }
    // 创建证书扩展域段对象成功
    console.log("createCertExtension success");
    
    try {
      // 获取证书扩展域段对象的序列化数据
      let encodedData = certExtension.getEncoded();
      
      // 获取证书扩展域段对象的对象标识符列表
      let oidList = certExtension.getOidList(cryptoCert.ExtensionOidType.EXTENSION_OID_TYPE_ALL);
      
      // 根据对象标识符获取证书扩展域段信息
      let oidData = "2.5.29.14";
      let oid = {
        data: stringToUint8Array(oidData),
      }
      let entry = certExtension.getEntry(cryptoCert.ExtensionEntryType.EXTENSION_ENTRY_TYPE_ENTRY, oid);
        
      // 校验证书是否为CA证书
      let pathLen = certExtension.checkCA();
    } catch (err) {
      console.log("operation failed: " + JSON.stringify(err));
    }
  });
}
```

## 使用证书吊销列表操作

**场景说明**

使用证书吊销列表操作中，典型的场景有：

1. 解析X509证书吊销列表数据生成吊销列表对象。
2. 获取证书吊销列表信息，比如：证书吊销列表版本、证书吊销列表类型等。
3. 获取证书吊销列表对象的序列化数据。
4. 检查证书是否被吊销。
5. 证书吊销列表验签。
6. 获取被吊销证书。

**接口及参数说明**

详细接口说明可参考[API参考](../reference/apis/js-apis-cert.md)。

以上场景涉及的常用接口如下表所示：

| 实例名          | 接口名                                                       | 描述                                                         |
| --------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| cryptoCert | createX509Crl(inStream : EncodingBlob, callback : AsyncCallback\<X509Crl>) : void | 使用callback方式解析X509证书吊销列表数据生成证书吊销列表对象 |
| cryptoCert | createX509Crl(inStream : EncodingBlob) : Promise\<X509Crl>    | 使用promise方式解析X509证书吊销列表数据生成证书吊销列表对象  |
| X509Crl         | isRevoked(cert : X509Cert) : boolean                     |  检查证书是否被吊销                            |
| X509Crl         | getType() : string                                           | 获取证书吊销列表类型                                        |
| X509Crl         | getEncoded(callback : AsyncCallback\<EncodingBlob>) : void    | 使用callback方式获取证书吊销列表序列化数据                   |
| X509Crl         | getEncoded() : Promise\<EncodingBlob>                         | 使用promise方式获取证书吊销列表序列化数据                    |
| X509Crl         | verify(key : cryptoFramework.PubKey, callback : AsyncCallback\<void>) : void  | 使用callback方式进行证书吊销列表验签        |
| X509Crl         | verify(key : cryptoFramework.PubKey) : Promise\<void>                         | 使用Promise方式进行证书吊销列表验签         |
| X509Crl         | getVersion() : number                                        | 获取证书吊销列表版本                                        |
| X509Crl         | getIssuerName() : DataBlob                                   | 获取证书吊销列表颁发者名称                                   |
| X509Crl         | getLastUpdate() : string                                     | 获取证书吊销列表lastUpdate日期                               |
| X509Crl         | getNextUpdate() : string                                     | 获取证书吊销列表nextUpdate日期                               |
| X509Crl         | getRevokedCert(serialNumber : number) : X509CrlEntry         | 通过序列号获取证书吊销列表中的被吊销证书                       |
| X509Crl         | getRevokedCertWithCert(cert : X509Cert) : X509CrlEntry         | 通过X509证书获取证书吊销列表中的被吊销证书                   |
| X509Crl         | getRevokedCerts(callback : AsyncCallback\<Array\<X509CrlEntry>>) : void | 使用callback方式获取证书吊销列表的所有被吊销证书    |
| X509Crl         | getRevokedCerts() : Promise\<Array\<X509CrlEntry>>             | 使用Promise方式获取证书吊销列表的所有被吊销证书              |
| X509Crl         | getTbsInfo() : DataBlob                                      | 获取证书吊销列表的tbsCertList                                |
| X509Crl         | getSignature() : DataBlob                                    | 获取证书吊销列表的签名                                       |
| X509Crl         | getSignatureAlgName() : string                               | 获取证书吊销列表的签名算法名称                                |
| X509Crl         | getSignatureAlgOid() : string                                | 获取证书吊销列表的签名算法OID                                 |
| X509Crl         | getSignatureAlgParams() : DataBlob                           | 获取证书吊销列表的签名算法参数                                |

**开发步骤**

示例：解析X509证书吊销列表数据生成证书吊销列表对象，并调用对象方法（包含场景1-6）

```javascript
import cryptoCert from '@ohos.security.cert';
import cryptoFramework from '@ohos.security.cryptoFramework';

// 证书吊销列表数据，此处仅示例，业务需根据场景自行设置
let crlData = "-----BEGIN X509 CRL-----\n"
+ "MIIBijB0AgEBMA0GCSqGSIb3DQEBCwUAMBMxETAPBgNVBAMMCHJvb3QtY2ExFw0y\n"
+ "MDA2MTkxNjE1NDhaFw0yMDA3MTkxNjE1NDhaMBwwGgIJAMsozRATnap1Fw0yMDA2\n"
+ "MTkxNjEyMDdaoA8wDTALBgNVHRQEBAICEAIwDQYJKoZIhvcNAQELBQADggEBACPs\n"
+ "9gQB+djaXPHHRmAItebZpD3iJ/e36Dxr6aMVkn9FkI8OVpUI4RNcCrywyCZHQJte\n"
+ "995bbPjP7f1sZstOTZS0fDPgJ5SPAxkKOQB+SQnBFrlZSsxoUNU60gRqd2imR0Rn\n"
+ "1r09rP69F6E4yPc9biEld+llLGgoImP3zPOVDD6fbfcvVkjStY3bssVEQ/vjp4a3\n"
+ "/I12U7ZnSe3jaKqaQBoVJppkTFOIOq7IOxf5/IkMPmvRHDeC2IzDMzcUxym0dkny\n"
+ "EowHrjzo0bZVqpHMA2YgKZuwTpVLHk9GeBEK2hVkIoPVISkmiU4HFg0S6z68C5yd\n"
+ "DrAA7hErVgXhtURLbAI=\n"
+ "-----END X509 CRL-----\n";

// string转Uint8Array
function stringToUint8Array(str) {
    var arr = [];
    for (var i = 0, j = str.length; i < j; i++) {
        arr.push(str.charCodeAt(i));
    }
    return new Uint8Array(arr);
}

// 证书吊销列表示例
function crlSample() {
    let encodingBlob = {
        // 将string类型证书吊销列表数据转为Uint8Array
        data: stringToUint8Array(crlData),
        // 证书吊销列表格式：支持PEM和DER，此例中对应PEM
        encodingFormat: cryptoCert.EncodingFormat.FORMAT_PEM
    };

    // 创建证书吊销列表对象
    cryptoCert.createX509Crl(encodingBlob, function (err, x509Crl) {
        if (err != null) {
            // 创建证书吊销列表对象失败
            console.log("createX509Crl failed, errCode: " + err.code + ", errMsg: " + err.message);
            return;
        }
        // 创建证书吊销列表对象成功
        console.log("createX509Crl success");

        // 获取证书吊销列表版本
        let version = x509Crl.getVersion();
        
        // 获取证书吊销列表对象的序列化数据
        x509Crl.getEncoded(function (err, data) {
            if (err != null) {
                // 获取序列化数据失败
                console.log("getEncoded failed, errCode: " + err.code + ", errMsg: " + err.message);
            } else {
                // 获取序列化数据成功
                console.log("getEncoded success");
            }
        });

        // 业务需通过cryptoFramework的createX509Cert生成X509Cert证书对象，此处省略
        let x509Cert = null;
        // 检查证书是否被吊销
        try {
            let revokedFlag = x509Crl.isRevoked(x509Cert);
        } catch (error) {
           console.log("isRevoked failed, errCode: " + error.code + ", errMsg: " + error.message);
        }

        // 业务需通过将public key二进制数据输入 @ohos.security.cryptoFramework的convertKey接口获取PubKey对象，此处省略
        let pubKey = null;
        
        // 证书吊销列表验签
        x509Crl.verify(pubKey, function (err, data) {
            if (err == null) {
                // 验签成功
                console.log("verify success");
            } else {
                // 验签失败
                console.log("verify failed, errCode: " + err.code + ", errMsg: " + err.message);
            }
        });

        // 证书序列号，业务需自行设置
        let serialNumber = 1000;

        // 获取被吊销证书对象
        try {
            let entry = x509Crl.getRevokedCert(serialNumber);
        } catch (error) {
           console.log("getRevokedCert failed, errCode: " + error.code + ", errMsg: " + error.message);
        }
    });
}
```

## 使用证书链校验器操作

**场景说明**

使用证书链校验器操作中，典型的场景：证书链校验。

**接口及参数说明**

详细接口说明可参考[API参考](../reference/apis/js-apis-cert.md)。

以上场景涉及的常用接口如下表所示：

| 实例名             | 接口名                                                       | 描述                             |
| ------------------ | ------------------------------------------------------------ | -------------------------------- |
| cryptoCert | createCertChainValidator(algorithm :string) : CertChainValidator | 使用指定算法生成证书链校验器对象 |
| CertChainValidator | validate(certChain : CertChainData, callback : AsyncCallback\<void>) : void | 使用callback方式校验证书链   |
| CertChainValidator | validate(certChain : CertChainData) : Promise\<void>          | 使用promise方式校验证书链        |
| CertChainValidator | algorithm : string                                           | 证书链校验器算法名称             |

**开发步骤**

示例：创建证书链校验器对象，并对证书链数据进行校验（场景1）

```javascript
import cryptoCert from '@ohos.security.cert';

// 一级证书数据，此处仅示例，业务需自行设置真实数据
let caCertData = "-----BEGIN CERTIFICATE-----\n"
+ "...\n"
+ "...\n"
+ "...\n"
+ "-----END CERTIFICATE-----\n";

// 二级证书数据，此处仅示例，业务需自行设置真实数据
let secondCaCertData = "-----BEGIN CERTIFICATE-----\n"
+ "...\n"
+ "...\n"
+ "...\n"
+ "-----END CERTIFICATE-----\n";

// string转Uint8Array
function stringToUint8Array(str) {
    var arr = [];
    for (var i = 0, j = str.length; i < j; i++) {
        arr.push(str.charCodeAt(i));
    }
    return new Uint8Array(arr);
}

// 证书链校验器示例：此示例中以校验二级证书链为例，业务需根据场景自行修改
function certChainValidatorSample() {
    // 证书链校验器算法，当前仅支持PKIX
    let algorithm = "PKIX";
    
    // 创建证书链校验器对象
    let validator = cryptoCert.createCertChainValidator(algorithm);
    
    // 一级证书数据
    let uint8ArrayOfCaCertData = stringToUint8Array(caCertData);
    
    // 一级证书数据长度
    let uint8ArrayOfCaCertDataLen = new Uint8Array(new Uint16Array([uint8ArrayOfCaCertData.byteLength]).buffer);
    
    // 二级证书数据
    let uint8ArrayOf2ndCaCertData = stringToUint8Array(secondCaCertData);
    
    // 二级证书数据长度
    let uint8ArrayOf2ndCaCertDataLen = new Uint8Array(new Uint16Array([uint8ArrayOf2ndCaCertData.byteLength]).buffer);
    
    // 证书链二进制数据：二级证书数据长度+二级证书数据+一级证书数据长度+一级证书数据（L-V格式）
    let encodingData = new Uint8Array(uint8ArrayOf2ndCaCertDataLen.length + uint8ArrayOf2ndCaCertData.length +
                                     uint8ArrayOfCaCertDataLen.length + uint8ArrayOfCaCertData.length);
    for (var i = 0; i < uint8ArrayOf2ndCaCertDataLen.length; i++) {
        encodingData[i] = uint8ArrayOf2ndCaCertDataLen[i];
    }
    for (var i = 0; i < uint8ArrayOf2ndCaCertData.length; i++) {
        encodingData[uint8ArrayOf2ndCaCertDataLen.length + i] = uint8ArrayOf2ndCaCertData[i];
    }
    for (var i = 0; i < uint8ArrayOfCaCertDataLen.length; i++) {
        encodingData[uint8ArrayOf2ndCaCertDataLen.length + uint8ArrayOf2ndCaCertData.length + i] = uint8ArrayOfCaCertDataLen[i];
    }
    for (var i = 0; i < uint8ArrayOfCaCertData.length; i++) {
        encodingData[uint8ArrayOf2ndCaCertDataLen.length + uint8ArrayOf2ndCaCertData.length +
                     uint8ArrayOfCaCertDataLen.length + i] = uint8ArrayOfCaCertData[i];
    }
    
    let certChainData = {
        // Uint8Array类型：L-V格式(证书数据长度-证书数据)
        data: encodingData,
        // 证书数量，此示例中为2
        count: 2,
        // 证书格式：支持PEM和DER，此例中对应PEM
        encodingFormat: cryptoCert.EncodingFormat.FORMAT_PEM
    };
    
    // 校验证书链
    validator.validate(certChainData, function (err, data) {
        if (err != null) {
            // 证书链校验失败
            console.log("validate failed, errCode: " + err.code + ", errMsg: " + err.message);
        } else {
            // 证书链校验成功
            console.log("validate success");
        }
	});
}
```

## 使用被吊销证书操作

**场景说明**

使用被吊销证书操作中，典型的场景有：

1. 获取被吊销证书对象。
2. 获取被吊销证书信息，比如：序列号、证书颁发者、证书吊销日期。
3. 获取被吊销证书对象的序列化数据。

**接口及参数说明**

详细接口说明可参考[API参考](../reference/apis/js-apis-cert.md)。

以上场景涉及的常用接口如下表所示：

| 实例名       | 接口名                                                      | 描述                                      |
| ------------ | ----------------------------------------------------------- | ---------------------------------------- |
| X509CrlEntry | getEncoded(callback : AsyncCallback\<EncodingBlob>) : void;  | 使用callback方式获取被吊销证书的序列化数据 |
| X509CrlEntry | getEncoded() : Promise\<EncodingBlob>;                       | 使用promise方式获取被吊销证书的序列化数据  |
| X509CrlEntry | getSerialNumber() : number;                                  | 获取被吊销证书的序列号                    |
| X509CrlEntry | getCertIssuer() : DataBlob;                                  | 获取被吊销证书颁发者                     |
| X509CrlEntry | getRevocationDate() : string;                                | 获取被吊销证书的吊销日期                  |

**开发步骤**

示例：获取被吊销证书对象，并调用对象方法（包含场景1-3）

```javascript
import cryptoCert from '@ohos.security.cert';

// 被吊销证书示例
function crlEntrySample() {
    // 业务需自行通过cryptoFramework的createX509Crl接口创建X509Crl对象，此处省略
    let x509Crl = null;
    
    // 获取被吊销证书对象，业务需根据场景调用X509Crl的接口获取，此示例使用getRevokedCert获取
    let serialNumber = 1000;
    let crlEntry = null;
    try {
        crlEntry = x509Crl.getRevokedCert(serialNumber);
    } catch (error) {
        console.log("getRevokedCert failed, errCode: " + error.code + ", errMsg: " + error.message);
    }

    // 获取被吊销证书的序列号
    serialNumber = crlEntry.getSerialNumber();
    
    // 获取被吊销证书的吊销日期
    try {
        crlEntry.getRevocationDate();
    } catch (error) {
        console.log("getRevocationDate failed, errCode: " + error.code + ", errMsg: " + error.message);
    }

    // 获取被吊销证书对象的序列化数据
    crlEntry.getEncoded(function (err, data) {
        if (err != null) {
            // 获取序列化数据失败
            console.log("getEncoded failed, errCode: " + err.code + ", errMsg: " + err.message);
        } else {
            // 获取序列化数据成功
            console.log("getEncoded success");
        }
    });
}
```
