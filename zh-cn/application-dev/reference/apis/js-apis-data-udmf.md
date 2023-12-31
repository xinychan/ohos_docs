# @ohos.data.UDMF（统一数据管理框架）

本模块提供数据统一管理的能力，包括对文本、图片等数据类型的标准化定义。通过调用对应数据类型的接口，应用程序可将各种数据封装为统一数据对象。

> **说明：**
>
> 本模块首批接口从API version 10开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。

## 导入模块

```js
import UDMF from '@ohos.data.UDMF';
```

## UnifiedDataType

[统一数据对象](#unifieddata)中各[数据记录](#unifiedrecord)的数据类型。

**系统能力：** SystemCapability.DistributedDataManager.UDMF.Core

| 名称                         | 值                            | 说明        |
|----------------------------|------------------------------|-----------|
| TEXT                       | 'Text'                       | 文本类型。     |
| PLAIN_TEXT                 | 'Text.PlainText'             | 纯文本类型。    |
| HYPERLINK                  | 'Text.Hyperlink'             | 超链接类型。    |
| HTML                       | 'Text.HTML'                  | 富文本类型。    |
| FILE                       | 'File'                       | 文件类型。     |
| IMAGE                      | 'File.Media.Image'           | 图片类型。     |
| VIDEO                      | 'File.Media.Video'           | 视频类型。     |
| AUDIO                      | 'File.Media.Audio'           | 音频类型。     |
| FOLDER                     | 'File.Folder'                | 文件夹类型。    |
| SYSTEM_DEFINED_RECORD      | 'SystemDefinedType'          | 系统服务数据类型。 |
| SYSTEM_DEFINED_FORM        | 'SystemDefinedType.Form'     | 卡片类型。     |
| SYSTEM_DEFINED_APP_ITEM    | 'SystemDefinedType.AppItem'  | 图标类型。     |
| SYSTEM_DEFINED_PIXEL_MAP   | 'SystemDefinedType.PixelMap' | 二进制图片类型。  |
| APPLICATION_DEFINED_RECORD | 'ApplicationDefinedType'     | 应用自定义类型。  |

## UnifiedData

表示UDMF统一数据对象，提供封装一组数据记录的方法。

**系统能力：** SystemCapability.DistributedDataManager.UDMF.Core

### constructor

constructor(record: UnifiedRecord)

用于创建带有一条数据记录的统一数据对象。

**系统能力：** SystemCapability.DistributedDataManager.UDMF.Core

**参数：**

| 参数名 | 类型                            | 必填 | 说明                                      |
| ------ | ------------------------------- | ---- |-----------------------------------------|
| record | [UnifiedRecord](#unifiedrecord) | 是   | 要添加到统一数据对象中的数据记录，该记录为UnifiedRecord子类对象。 |

**示例：**

```js
let text = new UDMF.PlainText();
text.textContent = 'this is textContent of text';
let unifiedData = new UDMF.UnifiedData(text);
```

### addRecord

addRecord(record: UnifiedRecord): void

在当前统一数据对象中添加一条数据记录。

**系统能力：** SystemCapability.DistributedDataManager.UDMF.Core

**参数：**

| 参数名 | 类型                            | 必填 | 说明                                          |
| ------ | ------------------------------- | ---- |---------------------------------------------|
| record | [UnifiedRecord](#unifiedrecord) | 是   | 要添加到统一数据对象中的数据记录，该记录为UnifiedRecord子类对象。|

**示例：**

```js
let text1 = new UDMF.PlainText();
text1.textContent = 'this is textContent of text1';
let unifiedData = new UDMF.UnifiedData(text1);

let text2 = new UDMF.PlainText();
text2.textContent = 'this is textContent of text2';
unifiedData.addRecord(text2);
```

### getRecords

getRecords(): Array\<UnifiedRecord\>

将当前统一数据对象中的所有数据记录取出。通过本接口取出的数据为UnifiedRecord类型，需通过[getType](#gettype)获取数据类型后转为子类再使用。

**系统能力** ：SystemCapability.DistributedDataManager.UDMF.Core

**返回值：**

| 类型                                     | 说明                      |
| ---------------------------------------- |-------------------------|
| Array\<[UnifiedRecord](#unifiedrecord)\> | 当前统一数据对象内所添加的记录。 |

**示例：**

```js
let text = new UDMF.PlainText();
text.textContent = 'this is textContent of text';
let unifiedData = new UDMF.UnifiedData(text);

let link = new UDMF.Hyperlink();
link.url = 'www.XXX.com';
unifiedData.addRecord(link);

let records = unifiedData.getRecords();
for (let i = 0; i < records.length; i++) {
  let record = records[i];
  if (record.getType() == UDMF.UnifiedDataType.PLAIN_TEXT) {
    let plainText = <UDMF.PlainText> (record);
    console.info(`textContent: ${plainText.textContent}`);
  } else if (record.getType() == UDMF.UnifiedDataType.HYPERLINK) {
    let hyperlink = <UDMF.Hyperlink> (record);
    console.info(`linkUrl: ${hyperlink.url}`);
  }
}
```

## Summary

描述某一统一数据对象的数据摘要，包括所含数据类型及大小，当前暂不支持。

**系统能力：** SystemCapability.DistributedDataManager.UDMF.Core

| 名称      | 类型                      | 可读 | 可写 | 说明                                                                                |
| --------- | ------------------------- | ---- | ---- |-----------------------------------------------------------------------------------|
| summary   | { [key: string]: number } | 是   | 否   | 是一个字典类型对象，key表示数据类型（见[UnifiedDataType](#unifieddatatype)），value为统一数据对象中该类型记录大小总和（单位：Byte）。 |
| totalSize | number                    | 是   | 否   | 统一数据对象内记录总大小（单位：Byte）。                                                                     |

## UnifiedRecord

对UDMF支持的数据内容的抽象定义，称为数据记录。一个统一数据对象内包含一条或多条数据记录，例如一条文本记录、一条图片记录、一条HTML记录等。

UnifiedRecord是一个抽象父类，无法保存具体数据内容，应用在使用时，不能将其添加到统一数据对象中，而应该创建带有数据内容的具体子类，如Text、Image等。

### getType

getType(): string

获取当前数据记录的类型。由于从统一数据对象中调用[getRecords](#getrecords)所取出的数据是UnifiedRecord对象，因此需要通过本接口查询此记录的具体类型，再将该UnifiedRecord对象转换为其子类，调用子类接口。

**系统能力** ：SystemCapability.DistributedDataManager.UDMF.Core

**返回值：**

| 类型   | 说明                                                   |
| ------ |------------------------------------------------------|
| string | 当前数据记录对应的具体数据类型，见[UnifiedDataType](#unifieddatatype)。|

**示例：**

```js
let text = new UDMF.PlainText();
text.textContent = 'this is textContent of text';
let unifiedData = new UDMF.UnifiedData(text);

let records = unifiedData.getRecords();
if (records[0].getType() == UDMF.UnifiedDataType.PLAIN_TEXT) {
    let plainText = <UDMF.PlainText> (records[0]);
    console.info(`textContent: ${plainText.textContent}`);
}
```

## Text

文本类型数据，是[UnifiedRecord](#unifiedrecord)的子类，也是文本类型数据的基类，用于描述文本类数据，推荐开发者优先使用Text的子类描述数据，如[PlainText](#plaintext)、[Hyperlink](#hyperlink)、[HTML](#html)等具体子类。

**系统能力**：SystemCapability.DistributedDataManager.UDMF.Core

| 名称    | 类型                      | 可读 | 可写 | 说明                                                                                                                                                  |
| ------- | ------------------------- | ---- | ---- |-----------------------------------------------------------------------------------------------------------------------------------------------------|
| details | { [key: string]: string } | 是   | 是   | 是一个字典类型对象，key和value都是string类型，用于描述文本内容。例如，可生成一个details内容为<br />{<br />"title":"标题",<br />"content":"内容"<br />}<br />的数据对象，用于描述一篇文章。非必填字段，默认值为空字典对象。 |

**示例：**

```js
let text = new UDMF.Text();
text.details = {
  title: 'MyTitle',
  content: 'this is content',
};
let unifiedData = new UDMF.UnifiedData(text);
```

## PlainText

纯文本类型数据，是[Text](#text)的子类，用于描述纯文本类数据。

**系统能力**：SystemCapability.DistributedDataManager.UDMF.Core

| 名称        | 类型   | 可读 | 可写 | 说明                    |
| ----------- | ------ | ---- | ---- |-----------------------|
| textContent | string | 是   | 是   | 纯文本内容。                |
| abstract    | string | 是   | 是   | 纯文本摘要，非必填字段，默认值为空字符串。 |

**示例：**

```js
let text = new UDMF.PlainText();
text.textContent = 'this is textContent';
text.abstract = 'this is abstract';
```

## Hyperlink

超链接类型数据，是[Text](#text)的子类，用于描述超链接类型数据。

**系统能力**：SystemCapability.DistributedDataManager.UDMF.Core

| 名称        | 类型   | 可读 | 可写 | 说明           |
| ----------- | ------ | ---- | ---- |--------------|
| url         | string | 是   | 是   | 链接url。       |
| description | string | 是   | 是   | 链接内容描述，非必填字段，默认值为空字符串。 |

**示例：**

```js
let link = new UDMF.Hyperlink();
link.url = 'www.XXX.com';
link.description = 'this is description';
```

## HTML

HTML类型数据，是[Text](#text)的子类，用于描述超文本标记语言数据。

**系统能力**：SystemCapability.DistributedDataManager.UDMF.Core

| 名称         | 类型   | 可读 | 可写 | 说明                    |
| ------------ | ------ | ---- | ---- |-----------------------|
| htmlContent  | string | 是   | 是   | html格式内容。             |
| plainContent | string | 是   | 是   | 去除html标签后的纯文本内容，非必填字段，默认值为空字符串。 |

**示例：**

```js
let html = new UDMF.HTML();
html.htmlContent = '<div><p>标题</p></div>';
html.plainContent = 'this is plainContent';
```

## File

File类型数据，是[UnifiedRecord](#unifiedrecord)的子类，也是文件类型数据的基类，用于描述文件类型数据，推荐开发者优先使用File的子类描述数据，如[Image](#image)、[Video](#video)、[Folder](#folder)等具体子类。

**系统能力**：SystemCapability.DistributedDataManager.UDMF.Core

| 名称      | 类型                        | 可读 | 可写 | 说明                                                                                                                                                   |
|---------|---------------------------| ---- | ---- |------------------------------------------------------------------------------------------------------------------------------------------------------|
| details | { [key: string]: string } | 是   | 是   | 是一个字典类型对象，key和value都是string类型，用于描述文件相关信息。例如，可生成一个details内容为<br />{<br />"name":"文件名",<br />"type":"文件类型"<br />}<br />的数据对象，用于描述一个文件。非必填字段，默认值为空字典对象。 |
| uri     | string                    | 是   | 是   | 文件数据uri。                                                                                                                                             |

**示例：**

```js
let file = new UDMF.File();
file.details = {
    name: 'test',
    type: 'txt',
};
file.uri = 'schema://com.samples.test/files/test.txt';
```

## Image

图片类型数据，是[File](#file)的子类，用于描述图片文件。

**系统能力**：SystemCapability.DistributedDataManager.UDMF.Core

| 名称     | 类型   | 可读 | 可写 | 说明       |
| -------- | ------ | ---- | ---- |----------|
| imageUri | string | 是   | 是   | 图片数据uri。 |

**示例：**

```js
let image = new UDMF.Image();
image.imageUri = 'schema://com.samples.test/files/test.jpg';
```

## Video

视频类型数据，是[File](#file)的子类，用于描述视频文件。

**系统能力**：SystemCapability.DistributedDataManager.UDMF.Core

| 名称     | 类型   | 可读 | 可写 | 说明       |
| -------- | ------ | ---- | ---- |----------|
| videoUri | string | 是   | 是   | 视频数据uri。 |

**示例：**

```js
let video = new UDMF.Video();
video.videoUri = 'schema://com.samples.test/files/test.mp4';
```

## Audio

音频类型数据，是[File](#file)的子类，用于描述音频文件。

**系统能力**：SystemCapability.DistributedDataManager.UDMF.Core

| 名称       | 类型     | 可读 | 可写 | 说明       |
|----------|--------|----|----|----------|
| audioUri | string | 是  | 是  | 音频数据uri。 |

**示例：**

```js
let audio = new UDMF.Audio();
audio.audioUri = 'schema://com.samples.test/files/test.mp3';
```

## Folder

文件夹类型数据，是[File](#file)的子类，用于描述文件夹。

**系统能力**：SystemCapability.DistributedDataManager.UDMF.Core

| 名称     | 类型   | 可读 | 可写 | 说明      |
| -------- | ------ | ---- | ---- |---------|
| folderUri | string | 是   | 是   | 文件夹uri。 |

**示例：**

```js
let folder = new UDMF.Folder();
folder.folderUri = 'schema://com.samples.test/files/folder/';
```

## SystemDefinedRecord

SystemDefinedRecord是[UnifiedRecord](#unifiedrecord)的子类，也是OpenHarmony系统特有数据类型的基类，用于描述仅在OpenHarmony系统范围内流通的特有数据类型，推荐开发者优先使用SystemDefinedRecord的子类描述数据，如[SystemDefinedForm](#systemdefinedform)、[SystemDefinedAppItem](#systemdefinedappitem)、[SystemDefinedPixelMap](#systemdefinedpixelmap)等具体子类。

**系统能力**：SystemCapability.DistributedDataManager.UDMF.Core

| 名称    | 类型                       | 可读 | 可写 | 说明                                                         |
| ------- |--------------------------| ---- | ---- | ------------------------------------------------------------ |
| details | { [key: string]: number \| string \| Uint8Array } | 是   | 是   | 是一个字典类型对象，key是string类型，value可以写入number（数值类型）、string（字符串类型）、Uint8Array（二进制字节数组）类型数据。非必填字段，默认值为空字典对象。|

**示例：**

```js
let sdr = new UDMF.SystemDefinedRecord();
let u8Array = new Uint8Array([1, 2, 3, 4, 5, 6, 7, 8, 9, 10]);
sdr.details = {
    title: 'recordTitle',
    version: 1,
    content: u8Array,
};
let unifiedData = new UDMF.UnifiedData(sdr);
```

## SystemDefinedForm

卡片类型数据，是[SystemDefinedRecord](#systemdefinedrecord)的子类。

**系统能力**：SystemCapability.DistributedDataManager.UDMF.Core

| 名称        | 类型   | 可读 | 可写 | 说明             |
| ----------- | ------ | ---- | ---- |----------------|
| formId      | number | 是   | 是   | 卡片id。          |
| formName    | string | 是   | 是   | 卡片名称。          |
| bundleName  | string | 是   | 是   | 卡片所属的bundle名。   |
| abilityName | string | 是   | 是   | 卡片对应的ability名。 |
| module      | string | 是   | 是   | 卡片所属的module名。   |

**示例：**

```js
let form = new UDMF.SystemDefinedForm();
form.formId = 123456;
form.formName = 'MyFormName';
form.bundleName = 'MyBundleName';
form.abilityName = 'MyAbilityName';
form.module = 'MyModule';
let u8Array = new Uint8Array([1, 2, 3, 4, 5, 6, 7, 8, 9, 10]);
form.details = {
  formKey1: 123,
  formKey2: 'formValue',
  formKey3: u8Array,
};
let unifiedData = new UDMF.UnifiedData(form);
```

## SystemDefinedAppItem

图标类型数据，是[SystemDefinedRecord](#systemdefinedrecord)的子类。

**系统能力**：SystemCapability.DistributedDataManager.UDMF.Core

| 名称        | 类型   | 可读 | 可写 | 说明              |
| ----------- | ------ | ---- | ---- |-----------------|
| appId       | string | 是   | 是   | 图标对应的应用id。      |
| appName     | string | 是   | 是   | 图标对应的应用名。       |
| appIconId   | string | 是   | 是   | 图标的图片id。        |
| appLabelId  | string | 是   | 是   | 图标名称对应的标签id。    |
| bundleName  | string | 是   | 是   | 图标对应的应用bundle名。 |
| abilityName | string | 是   | 是   | 图标对应的应用ability名。 |

**示例：**

```js
let appItem = new UDMF.SystemDefinedAppItem();
appItem.appId = 'MyAppId';
appItem.appName = 'MyAppName';
appItem.appIconId = 'MyAppIconId';
appItem.appLabelId = 'MyAppLabelId';
appItem.bundleName = 'MyBundleName';
appItem.abilityName = 'MyAbilityName';
let u8Array = new Uint8Array([1, 2, 3, 4, 5, 6, 7, 8, 9, 10]);
appItem.details = {
    appItemKey1: 123,
    appItemKey2: 'appItemValue',
    appItemKey3: u8Array,
};
let unifiedData = new UDMF.UnifiedData(appItem);
```

## SystemDefinedPixelMap

与系统侧定义的[PixelMap](js-apis-image.md#pixelmap7)数据类型对应的图片数据类型，是[SystemDefinedRecord](#systemdefinedrecord)的子类，仅保存PixelMap的二进制数据。

**系统能力**：SystemCapability.DistributedDataManager.UDMF.Core

| 名称    | 类型       | 可读 | 可写 | 说明                |
| ------- | ---------- | ---- | ---- |-------------------|
| rawData | Uint8Array | 是   | 是   | PixelMap对象的二进制数据。 |

**示例：**

```js
import image from '@ohos.multimedia.image'; // PixelMap类定义所在模块

const color = new ArrayBuffer(96); // 创建pixelmap对象
let opts = { editable: true, pixelFormat: 3, size: { height: 4, width: 6 } }
image.createPixelMap(color, opts, (error, pixelmap) => {
    if(error) {
        console.error('Failed to create pixelmap.');
    } else {
        console.info('Succeeded in creating pixelmap.');
        let arrayBuf = new ArrayBuffer(pixelmap.getPixelBytesNumber());
        pixelmap.readPixelsToBuffer(arrayBuf);
        let u8Array = new Uint8Array(arrayBuf);
        let sdpixel = new UDMF.SystemDefinedPixelMap();
        sdpixel.rawData = u8Array;
        let unifiedData = new UDMF.UnifiedData(sdpixel);
    }
})
```

## ApplicationDefinedRecord

ApplicationDefinedRecord是[UnifiedRecord](#unifiedrecord)的子类，也是应用自定义数据类型的基类，用于描述仅在应用生态内部流通的自定义数据类型，应用可基于此类进行自定义数据类型的扩展。

**系统能力**：SystemCapability.DistributedDataManager.UDMF.Core

| 名称                     | 类型         | 可读 | 可写 | 说明                                    |
|------------------------|------------| ---- | ---- |---------------------------------------|
| applicationDefinedType | string     | 是   | 是   | 应用自定义类型标识符，必须以'ApplicationDefined'开头。 |
| rawData                | Uint8Array | 是   | 是   | 应用自定义数据类型的二进制数据。                      |

**示例：**

```js
let record = new UDMF.ApplicationDefinedRecord();
let u8Array = new Uint8Array([1, 2, 3, 4, 5, 6, 7, 8, 9, 10]);
record.applicationDefinedType = 'ApplicationDefinedType';
record.rawData = u8Array;
let unifiedData = new UDMF.UnifiedData(record);
```

## Intention

UDMF已经支持的数据通路枚举类型。其主要用途是标识各种UDMF数据通路所面向的不同业务场景。

**系统能力：** SystemCapability.DistributedDataManager.UDMF.Core

| 名称       | 值         | 说明      |
|----------|-----------|---------|
| DATA_HUB | 'DataHub' | 公共数据通路。 |

## Options

UDMF提供的数据操作接口可选项，包含intention和key两个可选参数。无默认值，当对应接口不需要此参数时可不填，具体要求参照方法接口的参数说明。

**系统能力：** SystemCapability.DistributedDataManager.UDMF.Core


| 名称       | 类型                      | 可读 | 可写 | 必填 | 说明                                                                                                                                                                                                                                |
|-----------|-------------------------|----|----|----|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| intention | [Intention](#intention) | 是  | 是  | 否  | 表示数据操作相关的数据通路类型。                                                                                                                                                                                                                  |
| key       | string                  | 是  | 是  | 否  | UDMF中数据对象的唯一标识符，可通过[insertData](#udmfinsertdata)接口的返回值获取。<br>由udmf:/、intention、bundleName和groupId四部分组成，以'/'连接，比如：udmf://DataHub/com.ohos.test/0123456789。<br>其中udmf:/固定，DataHub为对应枚举的取值，com.ohos.test为包名，0123456789为随机生成的groupId。 |



## UDMF.insertData

insertData(options: Options, data: UnifiedData, callback: AsyncCallback&lt;string&gt;): void

将数据写入UDMF的公共数据通路中，并生成数据的唯一标识符，使用callback异步回调。

**系统能力：** SystemCapability.DistributedDataManager.UDMF.Core

**参数：**

| 参数名      | 类型                         | 必填 | 说明                           |
|----------|----------------------------|----|------------------------------|
| options  | [Options](#options)        | 是  | 配置项参数，仅需要intention的值。        |
| data     | [UnifiedData](#unifieddata) | 是  | 目标数据。                        |
| callback | AsyncCallback&lt;string&gt; | 是  | 回调函数，返回写入UDMF的数据的唯一标识符key的值。 |

**示例：**

```ts
import UDMF from '@ohos.data.UDMF';

let plainText = new UDMF.PlainText();
plainText.textContent = 'hello world!';
let unifiedData = new UDMF.UnifiedData(plainText);

let options = {
    intention: UDMF.Intention.DATA_HUB
}
try {
    UDMF.insertData(options, unifiedData, (err, data) => {
        if (err === undefined) {
            console.info(`Succeeded in inserting data. key = ${data}`);
        } else {
            console.error(`Failed to insert data. code is ${err.code},message is ${err.message} `);
        }
    });
} catch(e) {
    console.error(`Insert data throws an exception. code is ${e.code},message is ${e.message} `);
}

```

## UDMF.insertData

insertData(options: Options, data: UnifiedData): Promise&lt;string&gt;

将数据写入UDMF的公共数据通路中，并生成数据的唯一标识符，使用Promise异步回调。

**系统能力：** SystemCapability.DistributedDataManager.UDMF.Core

**参数：**

| 参数名     | 类型                          | 必填 | 说明                    |
|---------|-----------------------------|----|-----------------------|
| options | [Options](#options)         | 是  | 配置项参数，仅需要intention的值。 |
| data    | [UnifiedData](#unifieddata) | 是  | 目标数据。                 |

**返回值：**

| 类型                    | 说明                                |
|-----------------------|-----------------------------------|
| Promise&lt;string&gt; | Promise对象，返回写入UDMF的数据的唯一标识符key的值。 |

**示例：**

```ts
import UDMF from '@ohos.data.UDMF';

let plainText = new UDMF.PlainText();
plainText.textContent = 'hello world!';
let unifiedData = new UDMF.UnifiedData(plainText);

let options = {
    intention: UDMF.Intention.DATA_HUB
}
try {
    UDMF.insertData(options, unifiedData).then((data) => {
        console.info(`Succeeded in inserting data. key = ${data}`);
    }).catch((err) => {
        console.error(`Failed to insert data. code is ${err.code},message is ${err.message} `);
    });
} catch(e) {
    console.error(`Insert data throws an exception. code is ${e.code},message is ${e.message} `);
}
```

## UDMF.updateData

updateData(options: Options, data: UnifiedData, callback: AsyncCallback&lt;void&gt;): void

更新已写入UDMF的公共数据通路的数据，使用callback异步回调。

**系统能力：** SystemCapability.DistributedDataManager.UDMF.Core

**参数：**

| 参数名      | 类型                          | 必填 | 说明                                  |
|----------|-----------------------------|----|-------------------------------------|
| options  | [Options](#options)         | 是  | 配置项参数，仅需要key的值。                     |
| data     | [UnifiedData](#unifieddata) | 是  | 目标数据。                               |
| callback | AsyncCallback&lt;void&gt;   | 是  | 回调函数。当更新数据成功，err为undefined，否则为错误对象。 |

**示例：**

```ts
import UDMF from '@ohos.data.UDMF';

let plainText = new UDMF.PlainText();
plainText.textContent = 'hello world!';
let unifiedData = new UDMF.UnifiedData(plainText);

let options = {
    key: 'udmf://DataHub/com.ohos.test/0123456789'
};

try {
    UDMF.updateData(options, unifiedData, (err) => {
        if (err === undefined) {
            console.info('Succeeded in updating data.');
        } else {
            console.error(`Failed to update data. code is ${err.code},message is ${err.message} `);
        }
    });
} catch(e) {
    console.error(`Update data throws an exception. code is ${e.code},message is ${e.message} `);
}
```

## UDMF.updateData

updateData(options: Options, data: UnifiedData): Promise&lt;void&gt;

更新已写入UDMF的公共数据通路的数据，使用Promise异步回调。

**系统能力：** SystemCapability.DistributedDataManager.UDMF.Core

**参数：**

| 参数名     | 类型                          | 必填 | 说明              |
|---------|-----------------------------|----|-----------------|
| options | [Options](#options)         | 是  | 配置项参数，仅需要key的值。 |
| data    | [UnifiedData](#unifieddata) | 是  | 目标数据。           |

**返回值：**

| 类型                  | 说明                         |
|---------------------|----------------------------|
| Promise&lt;void&gt; | Promise对象。无返回结果的Promise对象。 |

**示例：**

```ts
import UDMF from '@ohos.data.UDMF';

let plainText = new UDMF.PlainText();
plainText.textContent = 'hello world!';
let unifiedData = new UDMF.UnifiedData(plainText);

let options = {
    key: 'udmf://DataHub/com.ohos.test/0123456789'
};

try {
    UDMF.updateData(options, unifiedData).then(() => {
        console.info('Succeeded in updating data.');
    }).catch((err) => {
        console.error(`Failed to update data. code is ${err.code},message is ${err.message} `);
    });
} catch(e) {
    console.error(`Update data throws an exception. code is ${e.code},message is ${e.message} `);
}
```

## UDMF.queryData

queryData(options: Options, callback: AsyncCallback&lt;Array&lt;UnifiedData&gt;&gt;): void

查询UDMF公共数据通路的数据，使用callback异步回调。

**系统能力：** SystemCapability.DistributedDataManager.UDMF.Core

**参数：**

| 参数名      | 类型                                                            | 必填 | 说明                                                                                                                                                               |
|----------|---------------------------------------------------------------|----|------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| options  | [Options](#options)                                           | 是  | 配置项参数，key和intention均为可选，根据传入的参数做相应的校验以返回不同的值。                                                                                                                    |
| callback | AsyncCallback&lt;Array&lt;[UnifiedData](#unifieddata)&gt;&gt; | 是  | 回调函数，返回查询到的所有数据。<br>如果options中填入的是key，则返回key对应的数据。<br>如果options中填入的是intention，则返回intention下所有数据。<br>如intention和key均填写了，取两者查询数据的交集，与options只填入key的获取结果一致；如没有交集报错。 |

**示例：**

```ts
import UDMF from '@ohos.data.UDMF';

let options = {
    intention: UDMF.Intention.DATA_HUB
};

try {
    UDMF.queryData(options, (err, data) => {
        if (err === undefined) {
            console.info(`Succeeded in querying data. size = ${data.length}`);
            for (let i = 0; i < data.length; i++) {
                let records = data[i].getRecords();
                for (let j = 0; j < records.length; j++) {
                    if (records[j].getType() === UDMF.UnifiedDataType.PLAIN_TEXT) {
                        let text = <UDMF.PlainText>(records[j]);
                        console.info(`${i + 1}.${text.textContent}`);
                    }
                }
            }
        } else {
            console.error(`Failed to query data. code is ${err.code},message is ${err.message} `);
        }
    });
} catch(e) {
    console.error(`Query data throws an exception. code is ${e.code},message is ${e.message} `);
}
```

## UDMF.queryData

queryData(options: Options): Promise&lt;Array&lt;UnifiedData&gt;&gt;

查询UDMF公共数据通路的数据，使用Promise异步回调。

**系统能力：** SystemCapability.DistributedDataManager.UDMF.Core

**参数：**

| 参数名     | 类型                  | 必填 | 说明                                            |
|---------|---------------------|----|-----------------------------------------------|
| options | [Options](#options) | 是  | 配置项参数，key和intention均为可选，根据传入的参数做相应的校验以返回不同的值。 |

**返回值：**

| 类型                                                      | 说明                                                                                                                                  |
|---------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------|
| Promise&lt;Array&lt;[UnifiedData](#unifieddata)&gt;&gt; | Promise对象，返回查询到的所有数据。<br>如果options中填入的是key，则返回key对应的数据。<br>如果options中填入的是intention，则返回intention下所有数据。<br>如intention和key均填写了，取两者查询数据的交集，与options只填入key的获取结果一致；如没有交集报错。 |

**示例：**

```ts
import UDMF from '@ohos.data.UDMF';

let options = {
    key: 'udmf://DataHub/com.ohos.test/0123456789'
};

try {
    UDMF.queryData(options).then((data) => {
        console.info(`Succeeded in querying data. size = ${data.length}`);
        for (let i = 0; i < data.length; i++) {
            let records = data[i].getRecords();
            for (let j = 0; j < records.length; j++) {
                if (records[j].getType() === UDMF.UnifiedDataType.PLAIN_TEXT) {
                    let text = <UDMF.PlainText>(records[j]);
                    console.info(`${i + 1}.${text.textContent}`);
                }
            }
        }
    }).catch((err) => {
        console.error(`Failed to query data. code is ${err.code},message is ${err.message} `);
    });
} catch(e) {
    console.error(`Query data throws an exception. code is ${e.code},message is ${e.message} `);
}
```

## UDMF.deleteData

deleteData(options: Options, callback: AsyncCallback&lt;Array&lt;UnifiedData&gt;&gt;): void

删除UDMF公共数据通路的数据，返回删除的数据集，使用callback异步回调。

**系统能力：** SystemCapability.DistributedDataManager.UDMF.Core

**参数：**

| 参数名      | 类型                                                            | 必填 | 说明                                                                                                                                                                                     |
|----------|---------------------------------------------------------------|----|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| options  | [Options](#options)                                           | 是  | 配置项参数，key和intention均为可选，根据传入的参数做相应的校验以返回不同的值。                                                                                                                                          |
| callback | AsyncCallback&lt;Array&lt;[UnifiedData](#unifieddata)&gt;&gt; | 是  | 回调函数，返回删除的所有数据。<br>如果options中填入的是key，则删除key对应的数据并返回该数据。<br>如果options中填入的是intention，则删除intention下所有数据并返回删除的数据。<br>如intention和key均填写了，取两者数据的交集进行删除，并返回删除的数据，与options只填入key的结果一致；如没有交集报错。 |

**示例：**

```ts
import UDMF from '@ohos.data.UDMF';

let options = {
    intention: UDMF.Intention.DATA_HUB
};

try {
    UDMF.deleteData(options, (err, data) => {
        if (err === undefined) {
            console.info(`Succeeded in deleting data. size = ${data.length}`);
            for (let i = 0; i < data.length; i++) {
                let records = data[i].getRecords();
                for (let j = 0; j < records.length; j++) {
                    if (records[j].getType() === UDMF.UnifiedDataType.PLAIN_TEXT) {
                        let text = <UDMF.PlainText>(records[j]);
                        console.info(`${i + 1}.${text.textContent}`);
                    }
                }
            }
        } else {
            console.error(`Failed to delete data. code is ${err.code},message is ${err.message} `);
        }
    });
} catch(e) {
    console.error(`Delete data throws an exception. code is ${e.code},message is ${e.message} `);
}
```

## UDMF.deleteData

deleteData(options: Options): Promise&lt;Array&lt;UnifiedData&gt;&gt;

删除UDMF公共数据通路的数据，返回删除的数据集，使用Promise异步回调。

**系统能力：** SystemCapability.DistributedDataManager.UDMF.Core

**参数：**

| 参数名     | 类型                  | 必填 | 说明     |
|---------|---------------------|----|--------|
| options | [Options](#options) | 是  | 配置项参数，key和intention均为可选，根据传入的参数做相应的校验以返回不同的值。 |

**返回值：**

| 类型                                                      | 说明                                                                                                                                                          |
|---------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Promise&lt;Array&lt;[UnifiedData](#unifieddata)&gt;&gt; | Promise对象，返回删除的所有数据。<br>如果options中填入的是key，则删除key对应的数据并返回该数据。<br>如果options中填入的是intention，则删除intention下所有数据并返回删除的数据。<br>如intention和key均填写了，取两者数据的交集进行删除，并返回删除的数据，与options只填入key的结果一致；如没有交集报错。 |

**示例：**

```ts
import UDMF from '@ohos.data.UDMF';

let options = {
    key: 'udmf://DataHub/com.ohos.test/0123456789'
};

try {
    UDMF.deleteData(options).then((data) => {
        console.info(`Succeeded in deleting data. size = ${data.length}`);
        for (let i = 0; i < data.length; i++) {
            let records = data[i].getRecords();
            for (let j = 0; j < records.length; j++) {
                if (records[j].getType() === UDMF.UnifiedDataType.PLAIN_TEXT) {
                    let text = <UDMF.PlainText>(records[j]);
                    console.info(`${i + 1}.${text.textContent}`);
                }
            }
        }
    }).catch((err) => {
        console.error(`Failed to delete data. code is ${err.code},message is ${err.message} `);
    });
} catch(e) {
    console.error(`Delete data throws an exception. code is ${e.code},message is ${e.message} `);
}
```