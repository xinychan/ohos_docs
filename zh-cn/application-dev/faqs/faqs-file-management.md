# 文件管理开发常见问题

## 如何获取系统截屏图片的保存路径

适用于OpenHarmony 3.2 Beta5  API 9

**解决措施**

截图图片保存路径：/storage/media/100/local/files/Pictures/Screenshots/

## 如何修改设备中文件目录为可读写权限

适用于OpenHarmony 3.2 Beta5  API 9

**问题现象**

使用hdc命令向设备上发送文件时，报错：权限不足。

**解决措施**

输入命令 hdc shell mount -o remount,rw /，正确执行无提示信息。

## 如何实现文件不存在则创建文件

适用于：OpenHarmony 3.2 版本  API 9

**解决措施**

可以通过调用函数fs.open来实现，open\(path: string, mode?: number\)，指定第二个参数mode为fs.OpenMode.CREATE，表示若文件不存在，则创建文件。

## 如何解决文件的中文乱码问题

适用于：OpenHarmony 3.2 版本  API 9

**解决措施**

读取文件内容的buffer数据后，通过@ohos.util的TextDecoder对文件内容进行解码。

```
let filePath = getContext(this).filesDir + "/test0.txt";
let stream = fs.createStreamSync(filePath, "r+");
let buffer = new ArrayBuffer(4096)
let readOut = stream.readSync(buffer);
let textDecoder = util.TextDecoder.create('utf-8', { ignoreBOM: true })
let readString = textDecoder.decodeWithStream(new Uint8Array(buffer), { stream: false });
console.log("读取的文件内容：" + readString);
```

## “datashare://”路径使用fs.open可以打开，但使用fs.copyFile会报错

适用于：OpenHarmony 3.2 版本  API 9

**解决措施**

copyfile不支持uri，可以先使用open接口打开datashare uri后，拿到fd后再调用copyfile接口。

```
let file = fs.openSync("datashare://...")
fs.copyFile(file.fd, 'dstPath', 0).then(() => {
  console.info('copyFile success')
}).catch((err) => {
  console.info("copy file failed with error message: " + err.message + ", error code: " + err.code);
})
```

## 如何修改沙箱路径下json文件的指定内容

适用于：OpenHarmony 3.2 版本  API 9

**解决措施**

可以通过以下步骤来完成：

1、使用fs.openSyn获取json文件的fd。

```
import fs from '@ohos.file.fs';  
let sanFile = fs.open(basePath, fs.OpenMode.READ_WRITE | fs.OpenMode.CREATE);
let fd = sanFile.fd;
```

2、通过fs.readSync读取json文件内容。

```
let content = fs.readSync(basePath);
```

3、修改内容。

```
obj.name = 'new name';
```

4、重新写入json文件。

```
fs.writeSync(file.fd, JSON.stringify(obj));
```

fs的具体使用可以参考：[@ohos.file.fs](../reference/apis/js-apis-file-fs.md)

## 通过fileAccess模块获取的文件路径对应的实际路径是什么

适用于：OpenHarmony 3.2 版本 API 9 Stage模型

**解决措施**

此类文件是保存在/storage/media/100/local/files目录下，具体位置与文件类型和来源有关。知道文件名时，可在此目录下通过如下命令查找：find . -name \[filename\]

[应用文件上传下载](../file-management/app-file-upload-download.md)
