# @ohos.file.photoAccessHelper (相册管理模块)

该模块提供相册管理模块能力，包括创建相册以及访问、修改相册中的媒体数据信息等。

> **说明：**
>
> - 本模块首批接口从API version 10开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。


## 导入模块

```ts
import photoAccessHelper from '@ohos.file.photoAccessHelper';
```

## photoAccessHelper.getPhotoAccessHelper

getPhotoAccessHelper(context: Context): PhotoAccessHelper

获取相册管理模块模块的实例，用于访问和修改相册中的媒体文件。

**模型约束**： 此接口仅可在Stage模型下使用。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**需要权限**：ohos.permission.READ_IMAGEVIDEO

**参数：**

| 参数名  | 类型    | 必填 | 说明                       |
| ------- | ------- | ---- | -------------------------- |
| context | [Context](js-apis-inner-app-context.md) | 是   | 传入Ability实例的Context。 |

**返回值：**

| 类型                            | 说明    |
| ----------------------------- | :---- |
| [PhotoAccessHelper](#photoaccesshelper) | 相册管理模块模块的实例。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcodes/errorcode-universal.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 401   | if parameter is invalid.         |

**示例：**

```ts
//此处获取的phAccessHelper实例为全局对象，后续使用到phAccessHelper的地方默认为使用此处获取的对象，如未添加此段代码报phAccessHelper未定义的错误请自行添加
const context = getContext(this);
let phAccessHelper = photoAccessHelper.getPhotoAccessHelper(context);
```

## PhotoAccessHelper

### getAssets

getAssets(options: FetchOptions, callback: AsyncCallback&lt;FetchResult&lt;PhotoAsset&gt;&gt;): void;

获取图片和视频资源，使用callback方式返回结果。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**需要权限**：ohos.permission.READ_IMAGEVIDEO

**参数：**

| 参数名   | 类型                     | 必填 | 说明                      |
| -------- | ------------------------ | ---- | ------------------------- |
| options  | [FetchOptions](#fetchoptions)        | 是   | 图片和视频检索选项。              |
| callback |  AsyncCallback&lt;[FetchResult](#fetchresult)&lt;[PhotoAsset](#photoasset)&gt;&gt; | 是   | callback返回图片和视频检索结果集。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcodes/errorcode-universal.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 401   | if type options is not FetchOptions.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('getAssets');
  let predicates = new dataSharePredicates.DataSharePredicates();
  let fetchOptions = {
    fetchColumns: [],
    predicates: predicates
  };

  phAccessHelper.getAssets(fetchOptions, async (err, fetchResult) => {
    if (fetchResult != undefined) {
      console.info('fetchResult success');
      let photoAsset = await fetchResult.getFirstObject();
      if (photoAsset != undefined) {
        console.info('photoAsset.displayName : ' + photoAsset.displayName);
      }
    } else {
      console.error('fetchResult fail' + err);
    }
  });
}
```

### getAssets

getAssets(options: FetchOptions): Promise&lt;FetchResult&lt;PhotoAsset&gt;&gt;;

获取图片和视频资源，使用Promise方式返回结果。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**需要权限**：ohos.permission.READ_IMAGEVIDEO

**参数：**

| 参数名  | 类型                | 必填 | 说明             |
| ------- | ------------------- | ---- | ---------------- |
| options | [FetchOptions](#fetchoptions)   | 是   | 图片和视频检索选项。     |

**返回值：**

| 类型                        | 说明           |
| --------------------------- | -------------- |
| Promise&lt;[FetchResult](#fetchresult)&lt;[PhotoAsset](#photoasset)&gt;&gt; | Promise对象，返回图片和视频数据结果集。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcodes/errorcode-universal.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 401   | if type options is not FetchOptions.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('getAssets');
  let predicates = new dataSharePredicates.DataSharePredicates();
  let fetchOptions = {
    fetchColumns: [],
    predicates: predicates
  };
  try {
    let fetchResult = await phAccessHelper.getAssets(fetchOptions);
    if (fetchResult != undefined) {
      console.info('fetchResult success');
      let photoAsset = await fetchResult.getFirstObject();
      if (photoAsset != undefined) {
        console.info('photoAsset.displayName :' + photoAsset.displayName);
      }
    }
  } catch (err) {
    console.error('getAssets failed, message = ', err);
  }
}
```

### createAsset

createAsset(displayName: string, callback: AsyncCallback&lt;PhotoAsset&gt;): void;

指定待创建的图片或者视频的文件名，创建图片或视频资源，使用callback方式返回结果。

**系统接口**：此接口为系统接口。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**需要权限**：ohos.permission.WRITE_IMAGEVIDEO

**参数：**

| 参数名   | 类型                     | 必填 | 说明                      |
| -------- | ------------------------ | ---- | ------------------------- |
| displayName  | string        | 是   | 创建的图片或者视频文件名。              |
| callback |  AsyncCallback&lt;[PhotoAsset](#photoasset)&gt; | 是   | callback返回创建的图片和视频结果。 |

**错误码：**

接口抛出错误码的详细介绍请参见[文件管理错误码](../errorcodes/errorcode-filemanagement.md)和[通用错误码](../errorcodes/errorcode-universal.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 202   | Called by non-system application.         |
| 401   | if type displayName is not string.         |
| 14000001   | if type of displayName is invalid.         |

**示例：**

```ts
async function example() {
  console.info('createAssetDemo');
  let testFileName = 'testFile' + Date.now() + '.jpg';
  phAccessHelper.createAsset(testFileName, (err, photoAsset) => {
    if (photoAsset != undefined) {
      console.info('createAsset file displayName' + photoAsset.displayName);
      console.info('createAsset successfully');
    } else {
      console.error('createAsset failed, message = ', err);
    }
  });
}
```

### createAsset

createAsset(displayName: string): Promise&lt;PhotoAsset&gt;;

指定待创建的图片或者视频的文件名，创建图片或视频资源，使用Promise方式返回结果。

**系统接口**：此接口为系统接口。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**需要权限**：ohos.permission.WRITE_IMAGEVIDEO

**参数：**

| 参数名   | 类型                     | 必填 | 说明                      |
| -------- | ------------------------ | ---- | ------------------------- |
| displayName  | string        | 是   | 创建的图片或者视频文件名。              |

**返回值：**

| 类型                        | 说明           |
| --------------------------- | -------------- |
| Promise&lt;[PhotoAsset](#photoasset)&gt; | Promise对象，返回创建的图片和视频结果。 |

**错误码：**

接口抛出错误码的详细介绍请参见[文件管理错误码](../errorcodes/errorcode-filemanagement.md)和[通用错误码](../errorcodes/errorcode-universal.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 202   | Called by non-system application.         |
| 401   | if type displayName or albumUri is not string.         |
| 14000001   | if type of displayName is invalid.         |

**示例：**

```ts
async function example() {
  console.info('createAssetDemo');
  try {
    let testFileName = 'testFile' + Date.now() + '.jpg';
    let photoAsset = await phAccessHelper.createAsset(testFileName);
    console.info('createAsset file displayName' + photoAsset.displayName);
    console.info('createAsset successfully');
  } catch (err) {
    console.error('createAsset failed, message = ', err);
  }
}
```

### createAsset

createAsset(displayName: string, options: PhotoCreateOptions, callback: AsyncCallback&lt;PhotoAsset&gt;): void;

指定待创建的图片或者视频的文件名和创建选项，创建图片或视频资源，使用callback方式返回结果。

**系统接口**：此接口为系统接口。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**需要权限**：ohos.permission.WRITE_IMAGEVIDEO

**参数：**

| 参数名   | 类型                     | 必填 | 说明                      |
| -------- | ------------------------ | ---- | ------------------------- |
| displayName  | string        | 是   | 创建的图片或者视频文件名。              |
| options  | [PhotoCreateOptions](#photocreateoptions)        | 是   | 图片或视频的创建选项。              |
| callback |  AsyncCallback&lt;[PhotoAsset](#photoasset)&gt; | 是   | callback返回创建的图片和视频结果。 |

**错误码：**

接口抛出错误码的详细介绍请参见[文件管理错误码](../errorcodes/errorcode-filemanagement.md)和[通用错误码](../errorcodes/errorcode-universal.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 202   | Called by non-system application.         |
| 401   | if type displayName is not string.         |
| 14000001   | if type displayName invalid.         |

**示例：**

```ts
async function example() {
  console.info('createAssetDemo');
  let testFileName = 'testFile' + Date.now() + '.jpg';
  let createOption = {
    subtype: photoAccessHelper.PhotoSubtype.DEFAULT
  }
  phAccessHelper.createAsset(testFileName, createOption, (err, photoAsset) => {
    if (photoAsset != undefined) {
      console.info('createAsset file displayName' + photoAsset.displayName);
      console.info('createAsset successfully');
    } else {
      console.error('createAsset failed, message = ', err);
    }
  });
}
```

### createAsset

createAsset(displayName: string, options: PhotoCreateOptions): Promise&lt;PhotoAsset&gt;;

指定待创建的图片或者视频的文件名和创建选项，创建图片或视频资源，使用Promise方式返回结果。

**系统接口**：此接口为系统接口。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**需要权限**：ohos.permission.WRITE_IMAGEVIDEO

**参数：**

| 参数名   | 类型                     | 必填 | 说明                      |
| -------- | ------------------------ | ---- | ------------------------- |
| displayName  | string        | 是   | 创建的图片或者视频文件名。              |
| options  |  [PhotoCreateOptions](#photocreateoptions)       | 是   | 图片或视频的创建选项。              |

**返回值：**

| 类型                        | 说明           |
| --------------------------- | -------------- |
| Promise&lt;[PhotoAsset](#photoasset)&gt; | Promise对象，返回创建的图片和视频结果。 |

**错误码：**

接口抛出错误码的详细介绍请参见[文件管理错误码](../errorcodes/errorcode-filemanagement.md)和[通用错误码](../errorcodes/errorcode-universal.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 202   | Called by non-system application.         |  
| 401   | if type displayName is not string.         |
| 14000001   | if type of displayName is invalid.         |

**示例：**

```ts
async function example() {
  console.info('createAssetDemo');
  try {
    let testFileName = 'testFile' + Date.now() + '.jpg';
    let createOption = {
      subtype: photoAccessHelper.PhotoSubtype.DEFAULT
    }
    let photoAsset = await phAccessHelper.createAsset(testFileName, createOption);
    console.info('createAsset file displayName' + photoAsset.displayName);
    console.info('createAsset successfully');
  } catch (err) {
    console.error('createAsset failed, message = ', err);
  }
}
```

### createAsset

createAsset(photoType: PhotoType, extension: string, options: CreateOptions, callback: AsyncCallback&lt;string&gt;): void;

指定待创建的文件类型、后缀和创建选项，创建图片或视频资源，使用callback方式返回结果。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**需要权限**：ohos.permission.WRITE_IMAGEVIDEO

**参数：**

| 参数名   | 类型                     | 必填 | 说明                      |
| -------- | ------------------------ | ---- | ------------------------- |
| photoType  | [PhotoType](#phototype)        | 是   | 创建的文件类型，IMAGE或者VIDEO类型。              |
| extension  | string        | 是   | 文件名后缀参数，例如：'jpg'。              |
| options  | [CreateOptions](#createoptions)        | 是   | 创建选项，例如{title: 'testPhoto'}。              |
| callback |  AsyncCallback&lt;string&gt; | 是   | callback返回创建的图片和视频的uri。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcodes/errorcode-universal.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 401   | if type createOption is wrong.         |

**示例：**

```ts
async function example() {
  console.info('createAssetDemo');
  let photoType = photoAccessHelper.PhotoType.IMAGE;
  let extension = 'jpg';
  let options = {
    title: 'testPhoto'
  }
  phAccessHelper.createAsset(photoType, extension, options, (err, photoAsset) => {
    if (photoAsset != undefined) {
      console.info('createAsset file displayName' + photoAsset.displayName);
      console.info('createAsset successfully');
    } else {
      console.error('createAsset failed, message = ', err);
    }
  });
}
```

### createAsset

createAsset(photoType: PhotoType, extension: string, callback: AsyncCallback&lt;string&gt;): void;

指定待创建的文件类型和后缀，创建图片或视频资源，使用callback方式返回结果。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**需要权限**：ohos.permission.WRITE_IMAGEVIDEO

**参数：**

| 参数名   | 类型                     | 必填 | 说明                      |
| -------- | ------------------------ | ---- | ------------------------- |
| photoType  | [PhotoType](#phototype)        | 是   | 创建的文件类型，IMAGE或者VIDEO类型。              |
| extension  | string        | 是   | 文件名后缀参数，例如：'jpg'。              |
| callback |  AsyncCallback&lt;string&gt; | 是   | callback返回创建的图片和视频的uri。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcodes/errorcode-universal.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 401   | if type createOption is wrong.         |

**示例：**

```ts
async function example() {
  console.info('createAssetDemo');
  let photoType = photoAccessHelper.PhotoType.IMAGE;
  let extension = 'jpg';
  phAccessHelper.createAsset(photoType, extension, (err, photoAsset) => {
    if (photoAsset != undefined) {
      console.info('createAsset file displayName' + photoAsset.displayName);
      console.info('createAsset successfully');
    } else {
      console.error('createAsset failed, message = ', err);
    }
  });
}
```

### createAsset

createAsset(photoType: PhotoType, extension: string, options?: CreateOptions): Promise&lt;string&gt;;

指定待创建的文件类型、后缀和创建选项，创建图片或视频资源，使用Promise方式返回结果。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**需要权限**：ohos.permission.WRITE_IMAGEVIDEO

**参数：**

| 参数名   | 类型                     | 必填 | 说明                      |
| -------- | ------------------------ | ---- | ------------------------- |
| photoType  | [PhotoType](#phototype)        | 是   | 创建的文件类型，IMAGE或者VIDEO类型。              |
| extension  | string        | 是   | 文件名后缀参数，例如：'jpg'。              |
| options  | [CreateOptions](#createoptions)        | 否   | 创建选项，例如{title: 'testPhoto'}。              |

**返回值：**

| 类型                        | 说明           |
| --------------------------- | -------------- |
| Promise&lt;string&gt; | Promise对象，返回创建的图片和视频的uri。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcodes/errorcode-universal.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 401   | if type createOption is wrong.         |

**示例：**

```ts
async function example() {
  console.info('createAssetDemo');
  try {
    let photoType = photoAccessHelper.PhotoType.IMAGE;
    let extension = 'jpg';
    let options = {
      title: 'testPhoto'
    }
    let photoAsset = await phAccessHelper.createAsset(photoType,extension, options);
    console.info('createAsset file displayName' + photoAsset.displayName);
    console.info('createAsset successfully');
  } catch (err) {
    console.error('createAsset failed, message = ', err);
  }
}
```

### createAlbum

createAlbum(name: string, callback: AsyncCallback&lt;Album&gt;): void;

创建相册，使用callback方式返回结果。

待创建的相册名参数规格为：
- 相册名字符串长度为1~255。
- 不允许出现的非法英文字符，包括：<br> . .. \ / : * ? " ' ` < > | { } [ ]
- 英文字符大小写不敏感。
- 相册名不允许重名。

**系统接口**：此接口为系统接口。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**需要权限**：ohos.permission.WRITE_IMAGEVIDEO

**参数：**

| 参数名   | 类型                     | 必填 | 说明                      |
| -------- | ------------------------ | ---- | ------------------------- |
| name  | string         | 是   | 待创建相册的相册名。              |
| callback |  AsyncCallback&lt;[Album](#album)&gt; | 是   | callback返回创建的相册实例。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcodes/errorcode-universal.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 202   | Called by non-system application.         |
| 401   | if parameter is invalid.         |

**示例：**

```ts
async function example() {
  console.info('createAlbumDemo');
  let albumName = 'newAlbumName' + new Date().getTime();
  phAccessHelper.createAlbum(albumName, (err, album) => {
    if (err) {
      console.error('createAlbumCallback failed with err: ' + err);
      return;
    }
    console.info('createAlbumCallback successfully, album: ' + album.albumName + ' album uri: ' + album.albumUri);
  });
}
```

### createAlbum

createAlbum(name: string): Promise&lt;Album&gt;;

创建相册，使用Promise方式返回结果。

待创建的相册名参数规格为：
- 相册名字符串长度为1~255。
- 不允许出现的非法英文字符，包括：<br> . .. \ / : * ? " ' ` < > | { } [ ]
- 英文字符大小写不敏感。
- 相册名不允许重名。

**系统接口**：此接口为系统接口。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**需要权限**：ohos.permission.WRITE_IMAGEVIDEO

**参数：**

| 参数名   | 类型                     | 必填 | 说明                      |
| -------- | ------------------------ | ---- | ------------------------- |
| name  | string         | 是   | 待创建相册的相册名。              |

**返回值：**

| 类型                        | 说明           |
| --------------------------- | -------------- |
| Promise&lt;[Album](#album)&gt; | Promise对象，返回创建的相册实例。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcodes/errorcode-universal.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 202   | Called by non-system application.         |
| 401   | if parameter is invalid.         |

**示例：**

```ts
async function example() {
  console.info('createAlbumDemo');
  let albumName = 'newAlbumName' + new Date().getTime();
  phAccessHelper.createAlbum(albumName).then((album) => {
    console.info('createAlbumPromise successfully, album: ' + album.albumName + ' album uri: ' + album.albumUri);
  }).catch((err) => {
    console.error('createAlbumPromise failed with err: ' + err);
  });
}
```

### deleteAlbums

deleteAlbums(albums: Array&lt;Album&gt;, callback: AsyncCallback&lt;void&gt;): void;

删除相册，使用callback方式返回结果。

删除相册前需先确保相册存在，只能删除用户相册。

**系统接口**：此接口为系统接口。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**需要权限**：ohos.permission.WRITE_IMAGEVIDEO

**参数：**

| 参数名   | 类型                     | 必填 | 说明                      |
| -------- | ------------------------ | ---- | ------------------------- |
| albums  | Array&lt;[Album](#album)&gt;         | 是   | 待删除相册的数组。              |
| callback |  AsyncCallback&lt;void&gt; | 是   | callback返回void。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcodes/errorcode-universal.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 202   | Called by non-system application.         |
| 401   | if parameter is invalid.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  // 示例代码为删除相册名为newAlbumName的相册。
  console.info('deleteAlbumsDemo');
  let predicates = new dataSharePredicates.DataSharePredicates();
  predicates.equalTo('album_name', 'newAlbumName');
  let fetchOptions = {
    fetchColumns: [],
    predicates: predicates
  };
  let fetchResult = await phAccessHelper.getAlbums(photoAccessHelper.AlbumType.USER, photoAccessHelper.AlbumSubtype.USER_GENERIC, fetchOptions);
  let album = await fetchResult.getFirstObject();
  phAccessHelper.deleteAlbums([album], (err) => {
    if (err) {
      console.error('deletePhotoAlbumsCallback failed with err: ' + err);
      return;
    }
    console.info('deletePhotoAlbumsCallback successfully');
  });
  fetchResult.close();
}
```

### deleteAlbums

deleteAlbums(albums: Array&lt;Album&gt;): Promise&lt;void&gt;;

删除相册，使用Promise方式返回结果。

删除相册前需先确保相册存在，只能删除用户相册。

**系统接口**：此接口为系统接口。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**需要权限**：ohos.permission.WRITE_IMAGEVIDEO

**参数：**

| 参数名   | 类型                     | 必填 | 说明                      |
| -------- | ------------------------ | ---- | ------------------------- |
| albums  |  Array&lt;[Album](#album)&gt;          | 是   | 待删除相册的数组。              |

**返回值：**

| 类型                        | 说明           |
| --------------------------- | -------------- |
| Promise&lt;void&gt; | Promise对象，返回void。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcodes/errorcode-universal.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 202   | Called by non-system application.         |
| 401   | if parameter is invalid.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  // 示例代码为删除相册名为newAlbumName的相册。
  console.info('deleteAlbumsDemo');
  let predicates = new dataSharePredicates.DataSharePredicates();
  predicates.equalTo('album_name', 'newAlbumName');
  let fetchOptions = {
    fetchColumns: [],
    predicates: predicates
  };
  let fetchResult = await phAccessHelper.getAlbums(photoAccessHelper.AlbumType.USER, photoAccessHelper.AlbumSubtype.USER_GENERIC, fetchOptions);
  let album = await fetchResult.getFirstObject();
  phAccessHelper.deleteAlbums([album]).then(() => {
    console.info('deletePhotoAlbumsPromise successfully');
    }).catch((err) => {
      console.error('deletePhotoAlbumsPromise failed with err: ' + err);
  });
  fetchResult.close();
}
```

### getAlbums

getAlbums(type: AlbumType, subtype: AlbumSubtype, options: FetchOptions, callback: AsyncCallback&lt;FetchResult&lt;Album&gt;&gt;): void;

根据检索选项和相册类型获取相册，使用callback方式返回结果。

获取相册前需先保证相册存在。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**需要权限**：ohos.permission.READ_IMAGEVIDEO

**参数：**

| 参数名   | 类型                     | 必填 | 说明                      |
| -------- | ------------------------ | ---- | ------------------------- |
| type  | [AlbumType](#albumtype)         | 是   | 相册类型。              |
| subtype  | [AlbumSubtype](#albumsubtype)         | 是   | 相册子类型。              |
| options  | [FetchOptions](#fetchoptions)         | 是   |  检索选项。              |
| callback |  AsyncCallback&lt;[FetchResult](#fetchresult)&lt;[Album](#album)&gt;&gt; | 是   | callback返回获取相册的结果集。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcodes/errorcode-universal.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 401   | if type options is not FetchOption.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  // 示例代码中为获取相册名为newAlbumName的相册。
  console.info('getAlbumsDemo');
  let predicates = new dataSharePredicates.DataSharePredicates();
  predicates.equalTo('album_name', 'newAlbumName');
  let fetchOptions = {
    fetchColumns: [],
    predicates: predicates
  };
  phAccessHelper.getAlbums(photoAccessHelper.AlbumType.USER, photoAccessHelper.AlbumSubtype.USER_GENERIC, fetchOptions, async (err, fetchResult) => {
    if (err) {
      console.error('getAlbumsCallback failed with err: ' + err);
      return;
    }
    if (fetchResult == undefined) {
      console.error('getAlbumsCallback fetchResult is undefined');
      return;
    }
    let album = await fetchResult.getFirstObject();
    console.info('getAlbumsCallback successfully, albumName: ' + album.albumName);
    fetchResult.close();
  });
}
```

### getAlbums

getAlbums(type: AlbumType, subtype: AlbumSubtype, callback: AsyncCallback&lt;FetchResult&lt;Album&gt;&gt;): void;

根据相册类型获取相册，使用callback方式返回结果。

获取相册前需先保证相册存在。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**需要权限**：ohos.permission.READ_IMAGEVIDEO

**参数：**

| 参数名   | 类型                     | 必填 | 说明                      |
| -------- | ------------------------ | ---- | ------------------------- |
| type  | [AlbumType](#albumtype)         | 是   | 相册类型。              |
| subtype  | [AlbumSubtype](#albumsubtype)         | 是   | 相册子类型。              |
| callback |  AsyncCallback&lt;[FetchResult](#fetchresult)&lt;[Album](#album)&gt;&gt; | 是   | callback返回获取相册的结果集。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcodes/errorcode-universal.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 401   | if type options is not FetchOption.         |

**示例：**

```ts
async function example() {
  // 示例代码中为获取统相册VIDEO，默认已预置。
  console.info('getAlbumsDemo');
  phAccessHelper.getAlbums(photoAccessHelper.AlbumType.SYSTEM, photoAccessHelper.AlbumSubtype.VIDEO, async (err, fetchResult) => {
    if (err) {
      console.error('getAlbumsCallback failed with err: ' + err);
      return;
    }
    if (fetchResult == undefined) {
      console.error('getAlbumsCallback fetchResult is undefined');
      return;
    }
    let album = await fetchResult.getFirstObject();
    console.info('getAlbumsCallback successfully, albumUri: ' + album.albumUri);
    fetchResult.close();
  });
}
```

### getAlbums

getAlbums(type: AlbumType, subtype: AlbumSubtype, options?: FetchOptions): Promise&lt;FetchResult&lt;Album&gt;&gt;;

根据检索选项和相册类型获取相册，使用Promise方式返回结果。

获取相册前需先保证相册存在。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**需要权限**：ohos.permission.READ_IMAGEVIDEO

**参数：**

| 参数名   | 类型                     | 必填 | 说明                      |
| -------- | ------------------------ | ---- | ------------------------- |
| type  | [AlbumType](#albumtype)         | 是   | 相册类型。              |
| subtype  | [AlbumSubtype](#albumsubtype)         | 是   | 相册子类型。              |
| options  | [FetchOptions](#fetchoptions)         | 否   |  检索选项，不填时默认根据相册类型检索。              |

**返回值：**

| 类型                        | 说明           |
| --------------------------- | -------------- |
| Promise&lt;[FetchResult](#fetchresult)&lt;[Album](#album)&gt;&gt; | Promise对象，返回获取相册的结果集。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcodes/errorcode-universal.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 401   | if type options is not FetchOption.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  // 示例代码中为获取相册名为newAlbumName的相册。
  console.info('getAlbumsDemo');
  let predicates = new dataSharePredicates.DataSharePredicates();
  predicates.equalTo('album_name', 'newAlbumName');
  let fetchOptions = {
    fetchColumns: [],
    predicates: predicates
  };
  phAccessHelper.getAlbums(photoAccessHelper.AlbumType.USER, photoAccessHelper.AlbumSubtype.USER_GENERIC, fetchOptions).then( async (fetchResult) => {
    if (fetchResult == undefined) {
      console.error('getAlbumsPromise fetchResult is undefined');
      return;
    }
    let album = await fetchResult.getFirstObject();
    console.info('getAlbumsPromise successfully, albumName: ' + album.albumName);
    fetchResult.close();
  }).catch((err) => {
    console.error('getAlbumsPromise failed with err: ' + err);
  });
}
```

### deleteAssets

deleteAssets(uriList: Array&lt;string&gt;, callback: AsyncCallback&lt;void&gt;): void;

删除媒体文件，删除的文件进入到回收站，使用callback方式返回结果。

**系统接口**：此接口为系统接口。

**需要权限**：ohos.permission.WRITE_IMAGEVIDEO

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名   | 类型                      | 必填 | 说明       |
| -------- | ------------------------- | ---- | ---------- |
| uriList | Array&lt;string&gt; | 是   | 待删除的媒体文件uri数组。 |
| callback | AsyncCallback&lt;void&gt; | 是   | callback返回void。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcodes/errorcode-universal.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 202   | Called by non-system application.         |
| 401   | if parameter is invalid.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('deleteAssetDemo');
  let predicates = new dataSharePredicates.DataSharePredicates();
  let fetchOptions = {
    fetchColumns: [],
    predicates: predicates
  };
  try {
    const fetchResult = await phAccessHelper.getAssets(fetchOptions);
    var asset = await fetchResult.getFirstObject();
  } catch (err) {
    console.info('fetch failed, message =', err);
  }

  if (asset == undefined) {
    console.error('asset not exist');
    return;
  }
  phAccessHelper.deleteAssets([asset.uri], (err) => {
    if (err == undefined) {
      console.info('deleteAssets successfully');
    } else {
      console.error('deleteAssets failed with error: ' + err);
    }
  });
}
```

### deleteAssets

deleteAssets(uriList: Array&lt;string&gt;): Promise&lt;void&gt;;

删除媒体文件，删除的文件进入到回收站，使用Promise方式返回结果。

**系统接口**：此接口为系统接口。

**需要权限**：ohos.permission.WRITE_IMAGEVIDEO

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名   | 类型                      | 必填 | 说明       |
| -------- | ------------------------- | ---- | ---------- |
| uriList | Array&lt;string&gt; | 是   | 待删除的媒体文件uri数组。 |

**返回值：**

| 类型                                    | 说明              |
| --------------------------------------- | ----------------- |
| Promise&lt;void&gt;| Promise对象，返回void。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcodes/errorcode-universal.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 202   | Called by non-system application.         |
| 401   | if parameter is invalid.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('deleteDemo');
  let predicates = new dataSharePredicates.DataSharePredicates();
  let fetchOptions = {
    fetchColumns: [],
    predicates: predicates
  };
  try {
    const fetchResult = await phAccessHelper.getAssets(fetchOptions);
    var asset = await fetchResult.getFirstObject();
  } catch (err) {
    console.info('fetch failed, message =', err);
  }

  if (asset == undefined) {
    console.error('asset not exist');
    return;
  }
  try {
    await phAccessHelper.deleteAssets([asset.uri]);
    console.info('deleteAssets successfully');
  } catch (err) {
    console.error('deleteAssets failed with error: ' + err);
  }
}
```

### registerChange

registerChange(uri: string, forChildUris: boolean, callback: Callback&lt;ChangeData&gt;) : void

注册对指定uri的监听，使用callback方式返回异步结果。

**需要权限**：ohos.permission.READ_IMAGEVIDEO

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名    | 类型                                        | 必填 | 说明                                                         |
| --------- | ------------------------------------------- | ---- | ------------------------------------------------------------ |
| uri       | string                                      | 是   | PhotoAsset的uri, Album的uri或[DefaultChangeUri](#defaultchangeuri)的值。 |
| forChildUris | boolean                                     | 是   | 是否模糊监听，uri为相册uri时，forChildUris为true能监听到相册中文件的变化，如果是false只能监听相册本身变化。uri为photoAsset时，forChildUris为true、false没有区别，uri为DefaultChangeUri时，forChildUris必须为true，如果为false将找不到该uri，收不到任何消息。 |
| callback  | Callback&lt;[ChangeData](#changedata)&gt; | 是   | 返回要监听的[ChangeData](#changedata)。注：uri可以注册多个不同的callback监听，[unRegisterChange](#unregisterchange)可以关闭该uri所有监听，也可以关闭指定callback的监听。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcodes/errorcode-universal.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 401   | if parameter is invalid.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('registerChangeDemo');
  let predicates = new dataSharePredicates.DataSharePredicates();
  let fetchOptions = {
    fetchColumns: [],
    predicates: predicates
  };
  let fetchResult = await phAccessHelper.getAssets(fetchOptions);
  let photoAsset = await fetchResult.getFirstObject();
  if (photoAsset != undefined) {
    console.info('photoAsset.displayName : ' + photoAsset.displayName);
  }
  let onCallback1 = (changeData) => {
      console.info('onCallback1 success, changData: ' + JSON.stringify(changeData));
    //file had changed, do something
  }
  let onCallback2 = (changeData) => {
      console.info('onCallback2 success, changData: ' + JSON.stringify(changeData));
    //file had changed, do something
  }
  // 注册onCallback1监听
  phAccessHelper.registerChange(photoAsset.uri, false, onCallback1); 
  // 注册onCallback2监听
  phAccessHelper.registerChange(photoAsset.uri, false, onCallback2);

  photoAsset.favorite(true, (err) => {
    if (err == undefined) {
      console.info('favorite successfully');
    } else {
      console.error('favorite failed with error:' + err);
    }
  });
}
```

### unRegisterChange

unRegisterChange(uri: string, callback?: Callback&lt;ChangeData&gt;): void

取消指定uri的监听，一个uri可以注册多个监听，存在多个callback监听时，可以取消指定注册的callback的监听；不指定callback时取消该uri的所有监听。

**需要权限**：ohos.permission.READ_IMAGEVIDEO

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名   | 类型                                        | 必填 | 说明                                                         |
| -------- | ------------------------------------------- | ---- | ------------------------------------------------------------ |
| uri      | string                                      | 是   | PhotoAsset的uri, Album的uri或[DefaultChangeUri](#defaultchangeuri)的值。 |
| callback | Callback&lt;[ChangeData](#changedata)&gt; | 否   | 取消[registerChange](#registerchange)注册时的callback的监听，不填时，取消该uri的所有监听。注：off指定注册的callback后不会进入此回调。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcodes/errorcode-universal.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 401   | if parameter is invalid.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('offDemo');
  let predicates = new dataSharePredicates.DataSharePredicates();
  let fetchOptions = {
    fetchColumns: [],
    predicates: predicates
  };
  let fetchResult = await phAccessHelper.getAssets(fetchOptions);
  let photoAsset = await fetchResult.getFirstObject();
  if (photoAsset != undefined) {
    console.info('photoAsset.displayName : ' + photoAsset.displayName);
  }
  let onCallback1 = (changeData) => {
    console.info('onCallback1 on');
  }
  let onCallback2 = (changeData) => {
    console.info('onCallback2 on');
  }
  // 注册onCallback1监听
  phAccessHelper.registerChange(photoAsset.uri, false, onCallback1);
  // 注册onCallback2监听
  phAccessHelper.registerChange(photoAsset.uri, false, onCallback2);
  // 关闭onCallback1监听，onCallback2 继续监听
  phAccessHelper.unRegisterChange(photoAsset.uri, onCallback1);
  photoAsset.favorite(true, (err) => {
    if (err == undefined) {
      console.info('favorite successfully');
    } else {
      console.error('favorite failed with error:' + err);
    }
  });
}
```

### createDeleteRequest

createDeleteRequest(uriList: Array&lt;string&gt;, callback: AsyncCallback&lt;void&gt;): void;

创建一个弹出框来删除照片，删除的文件进入到回收站，使用callback方式返回结果。

**需要权限**：ohos.permission.WRITE_IMAGEVIDEO

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名   | 类型                      | 必填 | 说明       |
| -------- | ------------------------- | ---- | ---------- |
| uriList | Array&lt;string&gt; | 是   | 待删除的媒体文件uri数组。 |
| callback | AsyncCallback&lt;void&gt; | 是   | callback返回void。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcodes/errorcode-universal.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 401   | if parameter is invalid.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('createDeleteRequestDemo');
  let predicates = new dataSharePredicates.DataSharePredicates();
  let fetchOptions = {
    fetchColumns: [],
    predicates: predicates
  };
  try {
    const fetchResult = await phAccessHelper.getAssets(fetchOptions);
    var asset = await fetchResult.getFirstObject();
  } catch (err) {
    console.info('fetch failed, message =', err);
  }

  if (asset == undefined) {
    console.error('asset not exist');
    return;
  }
  phAccessHelper.createDeleteRequest([asset.uri], (err) => {
    if (err == undefined) {
      console.info('createDeleteRequest successfully');
    } else {
      console.error('createDeleteRequest failed with error: ' + err);
    }
  });
}
```

### createDeleteRequest

createDeleteRequest(uriList: Array&lt;string&gt;): Promise&lt;void&gt;;

创建一个弹出框来删除照片，删除的文件进入到回收站，使用Promise方式返回结果。

**需要权限**：ohos.permission.WRITE_IMAGEVIDEO

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名   | 类型                      | 必填 | 说明       |
| -------- | ------------------------- | ---- | ---------- |
| uriList | Array&lt;string&gt; | 是   | 待删除的媒体文件uri数组。 |

**返回值：**

| 类型                                    | 说明              |
| --------------------------------------- | ----------------- |
| Promise&lt;void&gt;| Promise对象，返回void。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcodes/errorcode-universal.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 401   | if parameter is invalid.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('createDeleteRequestDemo');
  let predicates = new dataSharePredicates.DataSharePredicates();
  let fetchOptions = {
    fetchColumns: [],
    predicates: predicates
  };
  try {
    const fetchResult = await phAccessHelper.getAssets(fetchOptions);
    var asset = await fetchResult.getFirstObject();
  } catch (err) {
    console.info('fetch failed, message =', err);
  }

  if (asset == undefined) {
    console.error('asset not exist');
    return;
  }
  try {
    await phAccessHelper.createDeleteRequest([asset.uri]);
    console.info('createDeleteRequest successfully');
  } catch (err) {
    console.error('createDeleteRequest failed with error: ' + err);
  }
}
```

### release

release(callback: AsyncCallback&lt;void&gt;): void

释放PhotoAccessHelper实例。
当后续不需要使用PhotoAccessHelper实例中的方法时调用。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名   | 类型                      | 必填 | 说明                 |
| -------- | ------------------------- | ---- | -------------------- |
| callback | AsyncCallback&lt;void&gt; | 是   | 回调表示成功还是失败。 |

**错误码：**

接口抛出错误码的详细介绍请参见[文件管理错误码](../errorcodes/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 13900042    | Unknown error.         |

**示例：**

```ts
async function example() {
  console.info('releaseDemo');
  phAccessHelper.release((err) => {
    if (err != undefined) {
      console.error('release failed. message = ', err);
    } else {
      console.info('release ok.');
    }
  });
}
```

### release

release(): Promise&lt;void&gt;

释放PhotoAccessHelper实例。
当后续不需要使用PhotoAccessHelper 实例中的方法时调用。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**返回值：**

| 类型                | 说明                              |
| ------------------- | --------------------------------- |
| Promise&lt;void&gt; | Promise对象，返回void。 |

**错误码：**

接口抛出错误码的详细介绍请参见[文件管理错误码](../errorcodes/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 13900042    | Unknown error.         |

**示例：**

```ts
async function example() {
  console.info('releaseDemo');
  try {
    await phAccessHelper.release();
    console.info('release ok.');
  } catch (err) {
    console.error('release failed. message = ', err);
  }
}
```

## PhotoAsset

提供封装文件属性的方法。

### 属性

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

| 名称                      | 类型                     | 可读 | 可写 | 说明                                                   |
| ------------------------- | ------------------------ | ---- | ---- | ------------------------------------------------------ |
| uri                       | string                   | 是   | 否   | 文件资源uri（如：file://media/image/2）。         |
| photoType   | [PhotoType](#phototype) | 是   | 否   | 媒体文件类型                                               |
| displayName               | string                   | 是   | 否   | 显示文件名，包含后缀名。                                 |

### get

get(member: string): MemberType;

获取PhotoAsset成员参数。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名      | 类型                        | 必填   | 说明    |
| -------- | ------------------------- | ---- | ----- |
| member | string | 是    | 成员参数名称，在get时，除了uri、photoType和displayName三个属性之外，其他的属性都需要在fetchColumns中填入需要get的[PhotoKeys](#photokeys)，例如：get title属性fetchColumns: ['title']。 |

**返回值：**

| 类型                | 说明                              |
| ------------------- | --------------------------------- |
| [MemberType](#membertype) | 获取PhotoAsset成员参数的值。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcodes/errorcode-universal.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 401    | if parameter is invalid.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('photoAssetGetDemo');
  try {
    let predicates = new dataSharePredicates.DataSharePredicates();
    let fetchOption = {
      fetchColumns: ['title'],
      predicates: predicates
    };
    let fetchResult = await phAccessHelper.getAssets(fetchOption);
    let photoAsset = await fetchResult.getFirstObject();
    let title = photoAccessHelper.PhotoKeys.TITLE;
    let photoAssetTitle = photoAsset.get(title.toString());
    console.info('photoAsset Get photoAssetTitle = ', photoAssetTitle);
  } catch (err) {
    console.error('release failed. message = ', err);
  }
}
```

### set

set(member: string, value: string): void;

设置PhotoAsset成员参数。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名      | 类型                        | 必填   | 说明    |
| -------- | ------------------------- | ---- | ----- |
| member | string | 是    | 成员参数名称例如：[PhotoKeys](#photokeys).TITLE。 |
| value | string | 是    | 设置成员参数名称，只能修改[PhotoKeys](#photokeys).TITLE的值。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcodes/errorcode-universal.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 401    | if parameter is invalid.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('photoAssetSetDemo');
  try {
    let predicates = new dataSharePredicates.DataSharePredicates();
    let fetchOption = {
      fetchColumns: ['title'],
      predicates: predicates
    };
    let fetchResult = await phAccessHelper.getAssets(fetchOption);
    let photoAsset = await fetchResult.getFirstObject();
    let title = photoAccessHelper.PhotoKeys.TITLE.toString();
    photoAsset.set(title, 'newTitle');
  } catch (err) {
    console.error('release failed. message = ', err);
  }
}
```

### commitModify

commitModify(callback: AsyncCallback&lt;void&gt;): void

修改文件的元数据，使用callback方式返回异步结果。

**需要权限**：ohos.permission.WRITE_IMAGEVIDEO

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名      | 类型                        | 必填   | 说明    |
| -------- | ------------------------- | ---- | ----- |
| callback | AsyncCallback&lt;void&gt; | 是    | callback返回void。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcodes/errorcode-universal.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 401    | if values to commit is invalid.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('commitModifyDemo');
  let predicates = new dataSharePredicates.DataSharePredicates();
  let fetchOption = {
    fetchColumns: ['title'],
    predicates: predicates
  };
  let fetchResult = await phAccessHelper.getAssets(fetchOption);
  let photoAsset = await fetchResult.getFirstObject();
  let title = photoAccessHelper.PhotoKeys.TITLE.toString();
  let photoAssetTitle = photoAsset.get(title);
  console.info('photoAsset get photoAssetTitle = ', photoAssetTitle);
  photoAsset.set(title, 'newTitle2');
  photoAsset.commitModify((err) => {
    if (err == undefined) {
      let newPhotoAssetTitle = photoAsset.get(title);
      console.info('photoAsset get newPhotoAssetTitle = ', newPhotoAssetTitle);
    } else {
      console.error('commitModify failed, message =', err);
    }
  });
}
```

### commitModify

commitModify(): Promise&lt;void&gt;

修改文件的元数据，使用promise方式返回异步结果。

**需要权限**：ohos.permission.WRITE_IMAGEVIDEO

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**返回值：**

| 类型                  | 说明         |
| ------------------- | ---------- |
| Promise&lt;void&gt; | Promise对象，返回void。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcodes/errorcode-universal.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 401    | if values to commit is invalid.         |

**示例：**  

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('commitModifyDemo');
  let predicates = new dataSharePredicates.DataSharePredicates();
  let fetchOption = {
    fetchColumns: ['title'],
    predicates: predicates
  };
  let fetchResult = await phAccessHelper.getAssets(fetchOption);
  let photoAsset = await fetchResult.getFirstObject();
  let title = photoAccessHelper.PhotoKeys.TITLE.toString();
  let photoAssetTitle = photoAsset.get(title);
  console.info('photoAsset get photoAssetTitle = ', photoAssetTitle);
  photoAsset.set(title, 'newTitle3');
  try {
    await photoAsset.commitModify();
    let newPhotoAssetTitle = photoAsset.get(title);
    console.info('photoAsset get newPhotoAssetTitle = ', newPhotoAssetTitle);
  } catch (err) {
    console.error('release failed. message = ', err);
  }
}
```

### open

open(mode: string, callback: AsyncCallback&lt;number&gt;): void

打开当前文件，使用callback方式返回异步结果。

**注意**：当前写操作是互斥的操作，写操作完成后需要调用close进行释放。

**系统接口**：此接口为系统接口。

**需要权限**：ohos.permission.READ_IMAGEVIDEO 或 ohos.permission.WRITE_IMAGEVIDEO

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名      | 类型                          | 必填   | 说明                                  |
| -------- | --------------------------- | ---- | ----------------------------------- |
| mode     | string                      | 是    | 打开文件方式，如：'r'（只读）, 'w'（只写）, 'rw'（读写）。 |
| callback | AsyncCallback&lt;number&gt; | 是    | callback返回文件描述符。                            |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcodes/errorcode-universal.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 202   | Called by non-system application.         |
| 401   | if parameter is invalid.         |

**示例：**

```ts
async function example() {
  console.info('openDemo');
   let testFileName = 'testFile' + Date.now() + '.jpg';
  const photoAsset = await phAccessHelper.createAsset(testFileName);
  photoAsset.open('rw', (err, fd) => {
    if (fd != undefined) {
      console.info('File fd' + fd);
      photoAsset.close(fd);
    } else {
      console.error('File err' + err);
    }
  });
}
```

### open

open(mode: string): Promise&lt;number&gt;

打开当前文件，使用promise方式返回异步结果。

**注意**：当前写操作是互斥的操作，写操作完成后需要调用close进行释放。

**系统接口**：此接口为系统接口。

**需要权限**：ohos.permission.READ_IMAGEVIDEO 或 ohos.permission.WRITE_IMAGEVIDEO

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名  | 类型     | 必填   | 说明                                  |
| ---- | ------ | ---- | ----------------------------------- |
| mode | string | 是    | 打开文件方式，如：'r'（只读）, 'w'（只写）, 'rw'（读写）。 |

**返回值：**

| 类型                    | 说明            |
| --------------------- | ------------- |
| Promise&lt;number&gt; | Promise对象，返回文件描述符。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcodes/errorcode-universal.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 202   | Called by non-system application.         |
| 401   | if parameter is invalid.         |

**示例：**

```ts
async function example() {
  console.info('openDemo');
  try {
    let testFileName = 'testFile' + Date.now() + '.jpg';
    const photoAsset = await phAccessHelper.createAsset(testFileName);
    let fd = await photoAsset.open('rw');
    if (fd != undefined) {
      console.info('File fd' + fd);
      photoAsset.close(fd);
    } else {
      console.error(' open File fail');
    }
  } catch (err) {
    console.error('open Demo err' + err);
  }
}
```

### getReadOnlyFd

getReadOnlyFd(callback: AsyncCallback&lt;number&gt;): void

以只读方式打开当前文件，使用callback方式返回异步结果。

**注意**：读操作完成后需要调用close进行释放。

**需要权限**：ohos.permission.READ_IMAGEVIDEO

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名      | 类型                          | 必填   | 说明                                  |
| -------- | --------------------------- | ---- | ----------------------------------- |
| callback | AsyncCallback&lt;number&gt; | 是    | callback返回文件描述符。                            |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcodes/errorcode-universal.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 401   | if parameter is invalid.         |

**示例：**

```ts
async function example() {
  console.info('getReadOnlyFdDemo');
   let testFileName = 'testFile' + Date.now() + '.jpg';
  const photoAsset = await phAccessHelper.createAsset(testFileName);
  photoAsset.getReadOnlyFd((err, fd) => {
    if (fd != undefined) {
      console.info('File fd' + fd);
      photoAsset.close(fd);
    } else {
      console.error('File err' + err);
    }
  });
}
```

### getReadOnlyFd

getReadOnlyFd(): Promise&lt;number&gt;

以只读方式打开当前文件，使用promise方式返回异步结果。

**注意**：读操作完成后需要调用close进行释放。

**需要权限**：ohos.permission.READ_IMAGEVIDEO

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**返回值：**

| 类型                    | 说明            |
| --------------------- | ------------- |
| Promise&lt;number&gt; | Promise对象，返回文件描述符。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcodes/errorcode-universal.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 401   | if parameter is invalid.         |

**示例：**

```ts
async function example() {
  console.info('getReadOnlyFdDemo');
  try {
    let testFileName = 'testFile' + Date.now() + '.jpg';
    const photoAsset = await phAccessHelper.createAsset(testFileName);
    let fd = await photoAsset.getReadOnlyFd();
    if (fd != undefined) {
      console.info('File fd' + fd);
      photoAsset.close(fd);
    } else {
      console.error(' open File fail');
    }
  } catch (err) {
    console.error('open Demo err' + err);
  }
}
```

### close

close(fd: number, callback: AsyncCallback&lt;void&gt;): void

关闭当前文件，使用callback方式返回异步结果。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名      | 类型                        | 必填   | 说明    |
| -------- | ------------------------- | ---- | ----- |
| fd       | number                    | 是    | 文件描述符。 |
| callback | AsyncCallback&lt;void&gt; | 是    | callback返回void。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcodes/errorcode-universal.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 401   | if parameter is invalid.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('closeDemo');
  try {
    let predicates = new dataSharePredicates.DataSharePredicates();
    let fetchOption = {
      fetchColumns: [],
      predicates: predicates
    };
    let fetchResult = await phAccessHelper.getAssets(fetchOption);
    const photoAsset = await fetchResult.getFirstObject();
    let fd = await photoAsset.open('rw');
    console.info('file fd', fd);
    photoAsset.close(fd, (err) => {
      if (err == undefined) {
        console.info('asset close succeed.');
      } else {
        console.error('close failed, message = ' + err);
      }
    });
  } catch (err) {
    console.error('close failed, message = ' + err);
  }
}
```

### close

close(fd: number): Promise&lt;void&gt;

关闭当前文件，使用promise方式返回异步结果。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名  | 类型     | 必填   | 说明    |
| ---- | ------ | ---- | ----- |
| fd   | number | 是    | 文件描述符。 |

**返回值：**

| 类型                  | 说明         |
| ------------------- | ---------- |
| Promise&lt;void&gt; | Promise对象，返回void。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcodes/errorcode-universal.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 401   | if parameter is invalid.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('closeDemo');
  try {
    let predicates = new dataSharePredicates.DataSharePredicates();
    let fetchOption = {
      fetchColumns: [],
      predicates: predicates
    };
    let fetchResult = await phAccessHelper.getAssets(fetchOption);
    const asset = await fetchResult.getFirstObject();
    let fd = await asset.open('rw');
    console.info('file fd', fd);
    await asset.close(fd);
    console.info('asset close succeed.');
  } catch (err) {
    console.error('close failed, message = ' + err);
  }
}
```

### getThumbnail

getThumbnail(callback: AsyncCallback&lt;image.PixelMap&gt;): void

获取文件的缩略图，使用callback方式返回异步结果。

**需要权限**：ohos.permission.READ_IMAGEVIDEO

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名      | 类型                                  | 必填   | 说明               |
| -------- | ----------------------------------- | ---- | ---------------- |
| callback | AsyncCallback&lt;[image.PixelMap](js-apis-image.md#pixelmap7)&gt; | 是    | callback返回缩略图的PixelMap。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcodes/errorcode-universal.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 401   | if parameter is invalid.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('getThumbnailDemo');
  let predicates = new dataSharePredicates.DataSharePredicates();
  let fetchOption = {
    fetchColumns: [],
    predicates: predicates
  };
  let fetchResult = await phAccessHelper.getAssets(fetchOption);
  const asset = await fetchResult.getFirstObject();
  console.info('asset displayName = ', asset.displayName);
  asset.getThumbnail((err, pixelMap) => {
    if (err == undefined) {
      console.info('getThumbnail successful ' + pixelMap);
    } else {
      console.error('getThumbnail fail', err);
    }
  });
}
```

### getThumbnail

getThumbnail(size: image.Size, callback: AsyncCallback&lt;image.PixelMap&gt;): void

获取文件的缩略图，传入缩略图尺寸，使用callback方式返回异步结果。

**需要权限**：ohos.permission.READ_IMAGEVIDEO

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名      | 类型                                  | 必填   | 说明               |
| -------- | ----------------------------------- | ---- | ---------------- |
| size     | [image.Size](js-apis-image.md#size) | 是    | 缩略图尺寸。            |
| callback | AsyncCallback&lt;[image.PixelMap](js-apis-image.md#pixelmap7)&gt; | 是    | callback返回缩略图的PixelMap。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcodes/errorcode-universal.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 401   | if parameter is invalid.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('getThumbnailDemo');
  let predicates = new dataSharePredicates.DataSharePredicates();
  let fetchOption = {
    fetchColumns: [],
    predicates: predicates
  };
  let size = { width: 720, height: 720 };
  let fetchResult = await phAccessHelper.getAssets(fetchOption);
  const asset = await fetchResult.getFirstObject();
  console.info('asset displayName = ', asset.displayName);
  asset.getThumbnail(size, (err, pixelMap) => {
    if (err == undefined) {
      console.info('getThumbnail successful ' + pixelMap);
    } else {
      console.error('getThumbnail fail', err);
    }
  });
}
```

### getThumbnail

getThumbnail(size?: image.Size): Promise&lt;image.PixelMap&gt;

获取文件的缩略图，传入缩略图尺寸，使用promise方式返回异步结果。

**需要权限**：ohos.permission.READ_IMAGEVIDEO

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名  | 类型             | 必填   | 说明    |
| ---- | -------------- | ---- | ----- |
| size | [image.Size](js-apis-image.md#size) | 否    | 缩略图尺寸。 |

**返回值：**

| 类型                            | 说明                    |
| ----------------------------- | --------------------- |
| Promise&lt;[image.PixelMap](js-apis-image.md#pixelmap7)&gt; | Promise对象，返回缩略图的PixelMap。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcodes/errorcode-universal.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 401   | if parameter is invalid.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('getThumbnailDemo');
  let predicates = new dataSharePredicates.DataSharePredicates();
  let fetchOption = {
    fetchColumns: [],
    predicates: predicates
  };
  let size = { width: 720, height: 720 };
  let fetchResult = await phAccessHelper.getAssets(fetchOption);
  const asset = await fetchResult.getFirstObject();
  console.info('asset displayName = ', asset.displayName);
  asset.getThumbnail(size).then((pixelMap) => {
    console.info('getThumbnail successful ' + pixelMap);
  }).catch((err) => {
    console.error('getThumbnail fail' + err);
  });
}
```

### setFavorite

setFavorite(favoriteState: boolean, callback: AsyncCallback&lt;void&gt;): void

将文件设置为收藏文件，使用callback方式返回异步结果。

**系统接口**：此接口为系统接口。

**需要权限**：ohos.permission.WRITE_IMAGEVIDEO

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名        | 类型                        | 必填   | 说明                                 |
| ---------- | ------------------------- | ---- | ---------------------------------- |
| favoriteState | boolean                   | 是    | 是否设置为收藏文件， true：设置为收藏文件，false：取消收藏。 |
| callback   | AsyncCallback&lt;void&gt; | 是    | callback返回void。                              |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcodes/errorcode-universal.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 202   | Called by non-system application.         |
| 401   | if parameter is invalid.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('setFavoriteDemo');
  let predicates = new dataSharePredicates.DataSharePredicates();
  let fetchOption = {
    fetchColumns: [],
    predicates: predicates
  };
  let fetchResult = await phAccessHelper.getAssets(fetchOption);
  const asset = await fetchResult.getFirstObject();
  asset.setFavorite(true, (err) => {
    if (err == undefined) {
      console.info('favorite successfully');
    } else {
      console.error('favorite failed with error:' + err);
    }
  });
}
```

### setFavorite

setFavorite(favoriteState: boolean): Promise&lt;void&gt;

将文件设置为收藏文件，使用promise方式返回异步结果。

**系统接口**：此接口为系统接口。

**需要权限**：ohos.permission.WRITE_IMAGEVIDEO

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名        | 类型      | 必填   | 说明                                 |
| ---------- | ------- | ---- | ---------------------------------- |
| favoriteState | boolean | 是    | 是否设置为收藏文件， true：设置为收藏文件，false：取消收藏。 |

**返回值：**

| 类型                  | 说明         |
| ------------------- | ---------- |
| Promise&lt;void&gt; | Promise对象，返回void。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcodes/errorcode-universal.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 202   | Called by non-system application.         |
| 401   | if parameter is invalid.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('setFavoriteDemo');
  let predicates = new dataSharePredicates.DataSharePredicates();
  let fetchOption = {
    fetchColumns: [],
    predicates: predicates
  };
  let fetchResult = await phAccessHelper.getAssets(fetchOption);
  const asset = await fetchResult.getFirstObject();
  asset.setFavorite(true).then(function () {
    console.info('setFavorite successfully');
  }).catch(function (err) {
    console.error('setFavorite failed with error:' + err);
  });
}
```

### setHidden

setHidden(hiddenState: boolean, callback: AsyncCallback&lt;void&gt;): void

将文件设置为隐私文件，使用callback方式返回异步结果。

隐私文件存在隐私相册中，用户通过隐私相册去获取隐私文件后可以通过设置hiddenState为false来从隐私相册中移除。

**系统接口**：此接口为系统接口。

**需要权限**：ohos.permission.WRITE_IMAGEVIDEO

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名        | 类型                        | 必填   | 说明                                 |
| ---------- | ------------------------- | ---- | ---------------------------------- |
| hiddenState | boolean                   | 是    | 是否设置为隐藏文件，true:将文件资产放入隐藏相册;false:从隐藏相册中恢复。 |
| callback   | AsyncCallback&lt;void&gt; | 是    | callback返回void。                              |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcodes/errorcode-universal.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 202   | Called by non-system application.         |
| 401   | if parameter is invalid.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('setHiddenDemo');
  let predicates = new dataSharePredicates.DataSharePredicates();
  let fetchOption = {
    fetchColumns: [],
    predicates: predicates
  };
  let fetchResult = await phAccessHelper.getAssets(fetchOption);
  const asset = await fetchResult.getFirstObject();
  asset.setHidden(true, (err) => {
    if (err == undefined) {
      console.info('setHidden successfully');
    } else {
      console.error('setHidden failed with error:' + err);
    }
  });
}
```

### setHidden

setHidden(hiddenState: boolean): Promise&lt;void&gt;

将文件设置为隐私文件，使用promise方式返回异步结果。

隐私文件存在隐私相册中，用户通过隐私相册去获取隐私文件后可以通过设置hiddenState为false来从隐私相册中移除。

**系统接口**：此接口为系统接口。

**需要权限**：ohos.permission.WRITE_IMAGEVIDEO

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名        | 类型      | 必填   | 说明                                 |
| ---------- | ------- | ---- | ---------------------------------- |
| hiddenState | boolean | 是    | 是否设置为隐藏文件，true:将文件资产放入隐藏相册;false:从隐藏相册中恢复。 |

**返回值：**

| 类型                  | 说明         |
| ------------------- | ---------- |
| Promise&lt;void&gt; | Promise对象，返回void。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcodes/errorcode-universal.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 202   | Called by non-system application.         |
| 401   | if parameter is invalid.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  // 示例代码为将文件从隐藏相册中恢复，需要先在隐藏相册预置资源
  console.info('setHiddenDemo');
  let predicates = new dataSharePredicates.DataSharePredicates();
  let fetchOption = {
    fetchColumns: [],
    predicates: predicates
  };
  let albumList = await phAccessHelper.getAlbums(photoAccessHelper.AlbumType.SYSTEM, photoAccessHelper.AlbumSubtype.HIDDEN);
  const album = await albumList.getFirstObject();
  let fetchResult = await album.getAssets(fetchOption);
  const asset = await fetchResult.getFirstObject();
  asset.setHidden(false).then(() => {
    console.info('setHidden successfully');
  }).catch((err) => {
    console.error('setHidden failed with error:' + err);
  });
}
```

## FetchResult

文件检索结果集。

### getCount

getCount(): number

获取文件检索结果中的文件总数。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**返回值：**

| 类型     | 说明       |
| ------ | -------- |
| number | 检索到的文件总数。 |

**错误码：**

接口抛出错误码的详细介绍请参见[文件管理错误码](../errorcodes/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 13900042   | Unknown error.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('getCountDemo');
  let predicates = new dataSharePredicates.DataSharePredicates();
  let fetchOption = {
    fetchColumns: [],
    predicates: predicates
  };
  let fetchResult = await phAccessHelper.getAssets(fetchOption);
  const fetchCount = fetchResult.getCount();
  console.info('fetchCount = ', fetchCount);
}
```

### isAfterLast

isAfterLast(): boolean

检查结果集是否指向最后一行。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**返回值：**

| 类型      | 说明                                 |
| ------- | ---------------------------------- |
| boolean | 当读到最后一条记录后，后续没有记录返回true，否则返回false。 |

**错误码：**

接口抛出错误码的详细介绍请参见[文件管理错误码](../errorcodes/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 13900042   | Unknown error.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  let predicates = new dataSharePredicates.DataSharePredicates();
  let fetchOption = {
    fetchColumns: [],
    predicates: predicates
  };
  let fetchResult = await phAccessHelper.getAssets(fetchOption);
  const fetchCount = fetchResult.getCount();
  console.info('count:' + fetchCount);
  let photoAsset = await fetchResult.getLastObject();
  if (fetchResult.isAfterLast()) {
    console.info('photoAsset isAfterLast displayName = ', photoAsset.displayName);
  } else {
    console.info('photoAsset  not isAfterLast ');
  }
}
```

### close

close(): void

释放FetchFileResult实例并使其失效。无法调用其他方法。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**错误码：**

接口抛出错误码的详细介绍请参见[文件管理错误码](../errorcodes/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 13900042   | Unknown error.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('fetchResultCloseDemo');
  let predicates = new dataSharePredicates.DataSharePredicates();
  let fetchOption = {
    fetchColumns: [],
    predicates: predicates
  };
  try {
    let fetchResult = await phAccessHelper.getAssets(fetchOption);
    fetchResult.close();
    console.info('close succeed.');
  } catch (err) {
    console.error('close fail. message = ' + err);
  }
}
```

### getFirstObject

getFirstObject(callback: AsyncCallback&lt;T&gt;): void

获取文件检索结果中的第一个文件资产。此方法使用callback形式返回结果。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名   | 类型                                          | 必填 | 说明                                        |
| -------- | --------------------------------------------- | ---- | ------------------------------------------- |
| callback | AsyncCallback&lt;T&gt; | 是   | 异步获取结果集中的第一个完成后的回调。 |

**错误码：**

接口抛出错误码的详细介绍请参见[文件管理错误码](../errorcodes/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 13900042   | Unknown error.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('getFirstObjectDemo');
  let predicates = new dataSharePredicates.DataSharePredicates();
  let fetchOption = {
    fetchColumns: [],
    predicates: predicates
  };
  let fetchResult = await phAccessHelper.getAssets(fetchOption);
  fetchResult.getFirstObject((err, photoAsset) => {
    if (photoAsset != undefined) {
      console.info('photoAsset displayName: ', photoAsset.displayName);
    } else {
      console.error('photoAsset failed with err:' + err);
    }
  });
}
```

### getFirstObject

getFirstObject(): Promise&lt;T&gt;

获取文件检索结果中的第一个文件资产。此方法使用promise方式来异步返回。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**返回值：**

| 类型                                    | 说明                       |
| --------------------------------------- | -------------------------- |
| Promise&lt;T&gt; | Promise对象，返回结果集中第一个对象。 |

**错误码：**

接口抛出错误码的详细介绍请参见[文件管理错误码](../errorcodes/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 13900042   | Unknown error.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('getFirstObjectDemo');
  let predicates = new dataSharePredicates.DataSharePredicates();
  let fetchOption = {
    fetchColumns: [],
    predicates: predicates
  };
  let fetchResult = await phAccessHelper.getAssets(fetchOption);
  let photoAsset = await fetchResult.getFirstObject();
  console.info('photoAsset displayName: ', photoAsset.displayName);
}
```

### getNextObject

 getNextObject(callback: AsyncCallback&lt;T&gt;): void

获取文件检索结果中的下一个文件资产。此方法使用callback形式返回结果。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名    | 类型                                          | 必填 | 说明                                      |
| --------- | --------------------------------------------- | ---- | ----------------------------------------- |
| callbacke | AsyncCallback&lt;T&gt; | 是   | 异步返回结果集中下一个之后的回调。 |

**错误码：**

接口抛出错误码的详细介绍请参见[文件管理错误码](../errorcodes/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 13900042   | Unknown error.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('getNextObjectDemo');
  let predicates = new dataSharePredicates.DataSharePredicates();
  let fetchOption = {
    fetchColumns: [],
    predicates: predicates
  };
  let fetchResult = await phAccessHelper.getAssets(fetchOption);
  await fetchResult.getFirstObject();
  if (fetchResult.isAfterLast()) {
    fetchResult.getNextObject((err, photoAsset) => {
      if (photoAsset != undefined) {
        console.info('photoAsset displayName: ', photoAsset.displayName);
      } else {
        console.error('photoAsset failed with err: ' + err);
      }
    });
  }
}
```

### getNextObject

 getNextObject(): Promise&lt;T&gt;

获取文件检索结果中的下一个文件资产。此方法使用promise方式来异步返回。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**返回值：**

| 类型                                    | 说明              |
| --------------------------------------- | ----------------- |
| Promise&lt;T&gt; | Promise对象，返回结果集中下一个对象。 |

**错误码：**

接口抛出错误码的详细介绍请参见[文件管理错误码](../errorcodes/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 13900042   | Unknown error.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('getNextObjectDemo');
  let predicates = new dataSharePredicates.DataSharePredicates();
  let fetchOption = {
    fetchColumns: [],
    predicates: predicates
  };
  let fetchResult = await phAccessHelper.getAssets(fetchOption);
  await fetchResult.getFirstObject();
  if (fetchResult.isAfterLast()) {
    let photoAsset = await fetchResult.getNextObject();
    console.info('photoAsset displayName: ', photoAsset.displayName);
  }
}
```

### getLastObject

getLastObject(callback: AsyncCallback&lt;T&gt;): void

获取文件检索结果中的最后一个文件资产。此方法使用callback回调来返回。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名   | 类型                                          | 必填 | 说明                        |
| -------- | --------------------------------------------- | ---- | --------------------------- |
| callback | AsyncCallback&lt;T&gt; | 是   | 异步返回结果集中最后一个的回调。 |

**错误码：**

接口抛出错误码的详细介绍请参见[文件管理错误码](../errorcodes/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 13900042   | Unknown error.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('getLastObjectDemo');
  let predicates = new dataSharePredicates.DataSharePredicates();
  let fetchOption = {
    fetchColumns: [],
    predicates: predicates
  };
  let fetchResult = await phAccessHelper.getAssets(fetchOption);
  fetchResult.getLastObject((err, photoAsset) => {
    if (photoAsset != undefined) {
      console.info('photoAsset displayName: ', photoAsset.displayName);
    } else {
      console.error('photoAsset failed with err: ' + err);
    }
  });
}
```

### getLastObject

getLastObject(): Promise&lt;T&gt;

获取文件检索结果中的最后一个文件资产。此方法使用Promise方式来返回。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**返回值：**

| 类型                                    | 说明              |
| --------------------------------------- | ----------------- |
| Promise&lt;T&gt; | Promise对象，返回结果集中最后一个对象。 |

**错误码：**

接口抛出错误码的详细介绍请参见[文件管理错误码](../errorcodes/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 13900042   | Unknown error.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('getLastObjectDemo');
  let predicates = new dataSharePredicates.DataSharePredicates();
  let fetchOption = {
    fetchColumns: [],
    predicates: predicates
  };
  let fetchResult = await phAccessHelper.getAssets(fetchOption);
  let photoAsset = await fetchResult.getLastObject();
  console.info('photoAsset displayName: ', photoAsset.displayName);
}
```

### getObjectByPosition

getObjectByPosition(index: number, callback: AsyncCallback&lt;T&gt;): void

获取文件检索结果中具有指定索引的文件资产。此方法使用callback来返回。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名       | 类型                                       | 必填   | 说明                 |
| -------- | ---------------------------------------- | ---- | ------------------ |
| index    | number                                   | 是    | 要获取的文件的索引，从0开始。     |
| callback | AsyncCallback&lt;T&gt; | 是    | 异步返回指定索引的文件资产的回调。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcodes/errorcode-universal.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 401    | if type index is not number.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('getObjectByPositionDemo');
  let predicates = new dataSharePredicates.DataSharePredicates();
  let fetchOption = {
    fetchColumns: [],
    predicates: predicates
  };
  let fetchResult = await phAccessHelper.getAssets(fetchOption);
  fetchResult.getObjectByPosition(0, (err, photoAsset) => {
    if (photoAsset != undefined) {
      console.info('photoAsset displayName: ', photoAsset.displayName);
    } else {
      console.error('photoAsset failed with err: ' + err);
    }
  });
}
```

### getObjectByPosition

getObjectByPosition(index: number): Promise&lt;T&gt;

获取文件检索结果中具有指定索引的文件资产。此方法使用Promise形式返回文件Asset。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名    | 类型     | 必填   | 说明             |
| ----- | ------ | ---- | -------------- |
| index | number | 是    | 要获取的文件的索引，从0开始。 |

**返回值：**

| 类型                                    | 说明              |
| --------------------------------------- | ----------------- |
| Promise&lt;T&gt; | Promise对象，返回结果集中指定索引的一个对象。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcodes/errorcode-universal.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 401   | if type index is not number.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('getObjectByPositionDemo');
  let predicates = new dataSharePredicates.DataSharePredicates();
  let fetchOption = {
    fetchColumns: [],
    predicates: predicates
  };
  let fetchResult = await phAccessHelper.getAssets(fetchOption);
  let photoAsset = await fetchResult.getObjectByPosition(0);
  console.info('photoAsset displayName: ', photoAsset.displayName);
}
```

### getAllObjects

getAllObjects(callback: AsyncCallback&lt;Array&lt;T&gt;&gt;): void

获取文件检索结果中的所有文件资产。此方法使用callback形式返回结果。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名   | 类型                                          | 必填 | 说明                                        |
| -------- | --------------------------------------------- | ---- | ------------------------------------------- |
| callback | AsyncCallback&lt;Array&lt;T&gt;&gt; | 是   | 异步获取结果集中的所有文件资产完成后的回调。 |

**错误码：**

接口抛出错误码的详细介绍请参见[文件管理错误码](../errorcodes/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 13900042    | Unknown error.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('getAllObjectDemo');
  let predicates = new dataSharePredicates.DataSharePredicates();
  let fetchOption = {
    fetchColumns: [],
    predicates: predicates
  };
  let fetchResult = await phAccessHelper.getAssets(fetchOption);
  fetchResult.getAllObjects((err, photoAssetList) => {
    if (photoAssetList != undefined) {
      console.info('photoAssetList length: ', photoAssetList.length);
    } else {
      console.error('photoAssetList failed with err:' + err);
    }
  });
}
```

### getAllObjects

getAllObjects(): Promise&lt;Array&lt;T&gt;&gt;

获取文件检索结果中的所有文件资产。此方法使用promise方式来异步返回。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**返回值：**

| 类型                                    | 说明                       |
| --------------------------------------- | -------------------------- |
| Promise&lt;Array&lt;T&gt;&gt; | Promise对象，返回结果集中所有文件资产数组。 |

**错误码：**

接口抛出错误码的详细介绍请参见[文件管理错误码](../errorcodes/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 13900042    | Unknown error.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('getAllObjectDemo');
  let predicates = new dataSharePredicates.DataSharePredicates();
  let fetchOption = {
    fetchColumns: [],
    predicates: predicates
  };
  let fetchResult = await phAccessHelper.getAssets(fetchOption);
  let photoAssetList = await fetchResult.getAllObjects();
  console.info('photoAssetList length: ', photoAssetList.length);
}
```

## Album

实体相册

### 属性

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

| 名称           | 类型    | 可读   | 可写  | 说明   |
| ------------ | ------ | ---- | ---- | ------- |
| albumType | [AlbumType]( #albumtype) | 是    | 否    | 相册类型。    |
| albumSubtype | [AlbumSubtype]( #albumsubtype) | 是    | 否   | 相册子类型。    |
| albumName | string | 是    | 用户相册可写，预置相册不可写   | 相册名称。    |
| albumUri | string | 是    | 否    | 相册Uri。   |
| count | number | 是    | 否    |  相册中文件数量。 |
| coverUri | string | 是    | 否    | 封面文件Uri。 |

### getAssets

getAssets(options: FetchOptions, callback: AsyncCallback&lt;FetchResult&lt;PhotoAsset&gt;&gt;): void;

获取相册中的文件。该方法使用callback形式来返回文件。

**需要权限**：ohos.permission.READ_IMAGEVIDEO

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名   | 类型                      | 必填 | 说明       |
| -------- | ------------------------- | ---- | ---------- |
| options | [FetchOptions](#fetchoptions) | 是   | 检索选项。 |
| callback | AsyncCallback&lt;[FetchResult](#fetchresult)&lt;[PhotoAsset](#photoasset)&gt;&gt; | 是   | callback返回图片和视频数据结果集。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcodes/errorcode-universal.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 401   | if type options is not FetchOptions.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('albumGetPhotoAssetsDemoCallback');

  let predicates = new dataSharePredicates.DataSharePredicates();
  let albumFetchOptions = {
    predicates: predicates
  };
  let fetchOption = {
    fetchColumns: [],
    predicates: predicates
  };
  const albumList = await phAccessHelper.getAlbums(albumFetchOptions);
  const album = await albumList.getFirstObject();
  album.getAssets(fetchOption, (err, albumFetchResult) => {
    if (albumFetchResult != undefined) {
      console.info('album getAssets successfully, getCount: ' + albumFetchResult.getCount());
    } else {
      console.error('album getAssets failed with error: ' + err);
    }
  });
}
```

### getAssets

getAssets(options: FetchOptions): Promise&lt;FetchResult&lt;PhotoAsset&gt;&gt;;

获取相册中的文件。该方法使用Promise来返回文件。

**需要权限**：ohos.permission.READ_IMAGEVIDEO

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名   | 类型                      | 必填 | 说明       |
| -------- | ------------------------- | ---- | ---------- |
| options | [FetchOptions](#fetchoptions) | 是   | 检索选项。 |

**返回值：**

| 类型                                    | 说明              |
| --------------------------------------- | ----------------- |
| Promise&lt;[FetchResult](#fetchresult)&lt;[PhotoAsset](#photoasset)&gt;&gt; | Promise对象，返回图片和视频数据结果集。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcodes/errorcode-universal.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 401   | if type options is not FetchOptions.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('albumGetPhotoAssetsDemoPromise');

  let predicates = new dataSharePredicates.DataSharePredicates();
  let albumFetchOptions = {
    predicates: predicates
  };
  let fetchOption = {
    fetchColumns: [],
    predicates: predicates
  };
  const albumList = await phAccessHelper.getAlbums(albumFetchOptions);
  const album = await albumList.getFirstObject();
  album.getAssets(fetchOption).then((albumFetchResult) => {
    console.info('album getPhotoAssets successfully, getCount: ' + albumFetchResult.getCount());
  }).catch((err) => {
    console.error('album getPhotoAssets failed with error: ' + err);
  });
}
```

### commitModify

commitModify(callback: AsyncCallback&lt;void&gt;): void;

更新相册属性修改到数据库中。该方法使用callback形式来返回结果。

**需要权限**：ohos.permission.WRITE_IMAGEVIDEO

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名   | 类型                      | 必填 | 说明       |
| -------- | ------------------------- | ---- | ---------- |
| callback | AsyncCallback&lt;void&gt; | 是   | callback返回void。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcodes/errorcode-universal.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 401   | if value to modify is invalid.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('albumCommitModifyDemo');
  let predicates = new dataSharePredicates.DataSharePredicates();
  let albumFetchOptions = {
    predicates: predicates
  };
  const albumList = await phAccessHelper.getAlbums(albumFetchOptions);
  const album = await albumList.getFirstObject();
  album.albumName = 'hello';
  album.commitModify((err) => {
    if (err != undefined) {
      console.error('commitModify failed with error: ' + err);
    } else {
      console.info('commitModify successfully');
    }
  });
}
```

### commitModify

commitModify(): Promise&lt;void&gt;;

更新相册属性修改到数据库中。该方法使用Promise来返回结果。

**需要权限**：ohos.permission.WRITE_IMAGEVIDEO

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**返回值：**

| 类型                  | 说明           |
| ------------------- | ------------ |
| Promise&lt;void&gt; | Promise对象，返回void。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcodes/errorcode-universal.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 401   | if value to modify is invalid.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('albumCommitModifyDemo');
  let predicates = new dataSharePredicates.DataSharePredicates();
  let albumFetchOptions = {
    predicates: predicates
  };
  const albumList = await phAccessHelper.getAlbums(albumFetchOptions);
  const album = await albumList.getFirstObject();
  album.albumName = 'hello';
  album.commitModify().then(() => {
    console.info('commitModify successfully');
  }).catch((err) => {
    console.error('commitModify failed with error: ' + err);
  });
}
```

### addAssets

addAssets(assets: Array&lt;PhotoAsset&gt;, callback: AsyncCallback&lt;void&gt;): void;

往相册中添加图片或者视频，需要先预置相册和文件资源。该方法使用callback形式来返回结果。

**需要权限**：ohos.permission.WRITE_IMAGEVIDEO

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名   | 类型                      | 必填 | 说明       |
| -------- | ------------------------- | ---- | ---------- |
| assets | Array&lt;[PhotoAsset](#photoasset)&gt; | 是   | 待添加到相册中的图片或视频数组。 |
| callback | AsyncCallback&lt;void&gt; | 是   | callback返回void。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcodes/errorcode-universal.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 401   | if PhotoAssets is invalid.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  try {
    console.info('addAssetsDemoCallback');
    let predicates = new dataSharePredicates.DataSharePredicates();
    let fetchOption = {
      fetchColumns: [],
      predicates: predicates
    };
    let albumFetchResult = await phAccessHelper.getAlbums(photoAccessHelper.AlbumType.USER, photoAccessHelper.AlbumSubtype.USER_GENERIC);
    let album = await albumFetchResult.getFirstObject();
    let fetchResult = await phAccessHelper.getAssets(fetchOption);
    let asset = await fetchResult.getFirstObject();
    album.addAssets([asset], (err) => {
      if (err === undefined) {
        console.info('album addAssets successfully');
      } else {
        console.error('album addAssets failed with error: ' + err);
      }
    });
  } catch (err) {
    console.error('addAssetsDemoCallback failed with error: ' + err);
  }
}
```

### addAssets

addAssets(assets: Array&lt;PhotoAsset&gt;): Promise&lt;void&gt;;

往相册中添加图片或者视频，需要先预置相册和文件资源。该方法使用Promise来返回结果。

**需要权限**：ohos.permission.WRITE_IMAGEVIDEO

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名   | 类型                      | 必填 | 说明       |
| -------- | ------------------------- | ---- | ---------- |
| assets | Array&lt;[PhotoAsset](#photoasset)&gt; | 是   | 待添加到相册中的图片或视频数组。 |

**返回值：**

| 类型                                    | 说明              |
| --------------------------------------- | ----------------- |
|Promise&lt;void&gt; | Promise对象，返回void。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcodes/errorcode-universal.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 401   | if PhotoAssets is invalid.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  try {
    console.info('addAssetsDemoPromise');
    let predicates = new dataSharePredicates.DataSharePredicates();
    let fetchOption = {
      fetchColumns: [],
      predicates: predicates
    };
    let albumFetchResult = await phAccessHelper.getAlbums(photoAccessHelper.AlbumType.USER, photoAccessHelper.AlbumSubtype.USER_GENERIC);
    let album = await albumFetchResult.getFirstObject();
    let fetchResult = await phAccessHelper.getAssets(fetchOption);
    let asset = await fetchResult.getFirstObject();
    album.addAssets([asset]).then(() => {
      console.info('album addAssets successfully');
    }).catch((err) => {
      console.error('album addAssets failed with error: ' + err);
    });
  } catch (err) {
    console.error('addAssetsDemoPromise failed with error: ' + err);
  }
}
```

### removeAssets

removeAssets(assets: Array&lt;PhotoAsset&gt;, callback: AsyncCallback&lt;void&gt;): void;

从相册中移除图片或者视频，需要先预置相册和文件资源。该方法使用callback形式来返回结果。

**需要权限**：ohos.permission.WRITE_IMAGEVIDEO

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名   | 类型                      | 必填 | 说明       |
| -------- | ------------------------- | ---- | ---------- |
| assets | Array&lt;[PhotoAsset](#photoasset)&gt; | 是   | 相册中待移除的图片或视频数组。 |
| callback | AsyncCallback&lt;void&gt; | 是   | callback返回void。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcodes/errorcode-universal.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 401   | if PhotoAssets is invalid.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  try {
    console.info('removeAssetsDemoCallback');
    let predicates = new dataSharePredicates.DataSharePredicates();
    let fetchOption = {
      fetchColumns: [],
      predicates: predicates
    };
    let albumFetchResult = await phAccessHelper.getAlbums(photoAccessHelper.AlbumType.USER, photoAccessHelper.AlbumSubtype.USER_GENERIC);
    let album = await albumFetchResult.getFirstObject();
    let fetchResult = await album.getAssets(fetchOption);
    let asset = await fetchResult.getFirstObject();
    album.removeAssets([asset], (err) => {
      if (err === undefined) {
        console.info('album removeAssets successfully');
      } else {
        console.error('album removeAssets failed with error: ' + err);
      }
    });
  } catch (err) {
    console.error('removeAssetsDemoCallback failed with error: ' + err);
  }
}
```

### removeAssets

removeAssets(assets: Array&lt;PhotoAsset&gt;): Promise&lt;void&gt;;

从相册中移除图片或者视频，需要先预置相册和文件资源。该方法使用Promise来返回结果。

**需要权限**：ohos.permission.WRITE_IMAGEVIDEO

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名   | 类型                      | 必填 | 说明       |
| -------- | ------------------------- | ---- | ---------- |
| assets | Array&lt;[PhotoAsset](#photoasset)&gt; | 是   | 相册中待移除的图片或视频数组。 |

**返回值：**

| 类型                                    | 说明              |
| --------------------------------------- | ----------------- |
|Promise&lt;void&gt; | Promise对象，返回void。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcodes/errorcode-universal.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 401   | if PhotoAssets is invalid.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  try {
    console.info('removeAssetsDemoPromise');
    let predicates = new dataSharePredicates.DataSharePredicates();
    let fetchOption = {
      fetchColumns: [],
      predicates: predicates
    };
    let albumFetchResult = await phAccessHelper.getAlbums(photoAccessHelper.AlbumType.USER, photoAccessHelper.AlbumSubtype.USER_GENERIC);
    let album = await albumFetchResult.getFirstObject();
    let fetchResult = await album.getAssets(fetchOption);
    let asset = await fetchResult.getFirstObject();
    album.removeAssets([asset]).then(() => {
      console.info('album removeAssets successfully');
    }).catch((err) => {
      console.error('album removeAssets failed with error: ' + err);
    });
  } catch (err) {
    console.error('removeAssetsDemoPromise failed with error: ' + err);
  }
}
```

### recoverAssets

recoverAssets(assets: Array&lt;PhotoAsset&gt;, callback: AsyncCallback&lt;void&gt;): void;

从回收站中恢复图片或者视频，需要先在回收站中预置文件资源。该方法使用callback形式来返回结果。

**系统接口**：此接口为系统接口。

**需要权限**：ohos.permission.WRITE_IMAGEVIDEO

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名   | 类型                      | 必填 | 说明       |
| -------- | ------------------------- | ---- | ---------- |
| assets | Array&lt;[PhotoAsset](#photoasset)&gt; | 是   | 回收站中待恢复图片或者视频数组。 |
| callback | AsyncCallback&lt;void&gt; | 是   | callback返回void。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcodes/errorcode-universal.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 202   | Called by non-system application.                |
| 401   |  if PhotoAssets is invalid.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  try {
    console.info('recoverAssetsDemoCallback');
    let predicates = new dataSharePredicates.DataSharePredicates();
    let fetchOption = {
      fetchColumns: [],
      predicates: predicates
    };
    let albumFetchResult = await phAccessHelper.getAlbums(photoAccessHelper.AlbumType.SYSTEM, photoAccessHelper.AlbumSubtype.TRASH);
    let album = await albumFetchResult.getFirstObject();
    let fetchResult = await album.getAssets(fetchOption);
    let asset = await fetchResult.getFirstObject();
    album.recoverAssets([asset], (err) => {
      if (err === undefined) {
        console.info('album recoverAssets successfully');
      } else {
        console.error('album recoverAssets failed with error: ' + err);
      }
    });
  } catch (err) {
    console.error('recoverAssetsDemoCallback failed with error: ' + err);
  }
}
```

### recoverAssets

recoverAssets(assets: Array&lt;PhotoAsset&gt;): Promise&lt;void&gt;;

从回收站中恢复图片或者视频，需要先在回收站中预置文件资源。该方法使用Promise来返回结果。

**系统接口**：此接口为系统接口。

**需要权限**：ohos.permission.WRITE_IMAGEVIDEO

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名   | 类型                      | 必填 | 说明       |
| -------- | ------------------------- | ---- | ---------- |
| assets | Array&lt;[PhotoAsset](#photoasset)&gt; | 是   | 回收站中待恢复图片或者视频数组。 |

**返回值：**

| 类型                                    | 说明              |
| --------------------------------------- | ----------------- |
|Promise&lt;void&gt; | Promise对象，返回void。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcodes/errorcode-universal.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 202   | Called by non-system application.                |
| 401   |  if PhotoAssets is invalid.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  try {
    console.info('recoverAssetsDemoPromise');
    let predicates = new dataSharePredicates.DataSharePredicates();
    let fetchOption = {
      fetchColumns: [],
      predicates: predicates
    };
    let albumFetchResult = await phAccessHelper.getAlbums(photoAccessHelper.AlbumType.SYSTEM, photoAccessHelper.AlbumSubtype.TRASH);
    let album = await albumFetchResult.getFirstObject();
    let fetchResult = await album.getAssets(fetchOption);
    let asset = await fetchResult.getFirstObject();
    album.recoverAssets([asset]).then(() => {
      console.info('album recoverAssets successfully');
    }).catch((err) => {
      console.error('album recoverAssets failed with error: ' + err);
    });
  } catch (err) {
    console.error('recoverAssetsDemoPromise failed with error: ' + err);
  }
}
```

### deleteAssets

deleteAssets(assets: Array&lt;PhotoAsset&gt;, callback: AsyncCallback&lt;void&gt;): void;

从回收站中彻底删除图片或者视频，需要先在回收站中预置文件资源。该方法使用callback形式来返回结果。

**注意**：此操作不可逆，执行此操作后文件资源将彻底删除，请谨慎操作。

**系统接口**：此接口为系统接口。

**需要权限**：ohos.permission.WRITE_IMAGEVIDEO

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名   | 类型                      | 必填 | 说明       |
| -------- | ------------------------- | ---- | ---------- |
| assets | Array&lt;[PhotoAsset](#photoasset)&gt; | 是   | 回收站中待彻底删除图片或者视频数组。 |
| callback | AsyncCallback&lt;void&gt; | 是   | callback返回void。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcodes/errorcode-universal.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 202   | Called by non-system application.                |
| 401   | if PhotoAssets is invalid.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  try {
    console.info('deleteAssetsDemoCallback');
    let predicates = new dataSharePredicates.DataSharePredicates();
    let fetchOption = {
      fetchColumns: [],
      predicates: predicates
    };
    let albumFetchResult = await phAccessHelper.getAlbums(photoAccessHelper.AlbumType.SYSTEM, photoAccessHelper.AlbumSubtype.TRASH);
    let album = await albumFetchResult.getFirstObject();
    let fetchResult = await album.getAssets(fetchOption);
    let asset = await fetchResult.getFirstObject();
    album.deleteAssets([asset], (err) => {
      if (err === undefined) {
        console.info('album deleteAssets successfully');
      } else {
        console.error('album deleteAssets failed with error: ' + err);
      }
    });
  } catch (err) {
    console.error('deleteAssetsDemoCallback failed with error: ' + err);
  }
}
```

### deleteAssets

deleteAssets(assets: Array&lt;PhotoAsset&gt;): Promise&lt;void&gt;;

从回收站中彻底删除图片或者视频，需要先在回收站中预置文件资源。该方法使用Promise来返回结果。

**注意**：此操作不可逆，执行此操作后文件资源将彻底删除，请谨慎操作。

**系统接口**：此接口为系统接口。

**需要权限**：ohos.permission.WRITE_IMAGEVIDEO

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名   | 类型                      | 必填 | 说明       |
| -------- | ------------------------- | ---- | ---------- |
| assets | Array&lt;[PhotoAsset](#photoasset)&gt; | 是   | 回收站中待彻底删除图片或者视频数组。 |

**返回值：**

| 类型                                    | 说明              |
| --------------------------------------- | ----------------- |
|Promise&lt;void&gt; | Promise对象，返回void。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcodes/errorcode-universal.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 202   | Called by non-system application.                |
| 401   | if PhotoAssets is invalid.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  try {
    console.info('deleteAssetsDemoPromise');
    let predicates = new dataSharePredicates.DataSharePredicates();
    let fetchOption = {
      fetchColumns: [],
      predicates: predicates
    };
    let albumFetchResult = await phAccessHelper.getAlbums(photoAccessHelper.AlbumType.SYSTEM, photoAccessHelper.AlbumSubtype.TRASH);
    let album = await albumFetchResult.getFirstObject();
    let fetchResult = await album.getAssets(fetchOption);
    let asset = await fetchResult.getFirstObject();
    album.deleteAssets([asset]).then(() => {
      console.info('album deleteAssets successfully');
    }).catch((err) => {
      console.error('album deleteAssets failed with error: ' + err);
    });
  } catch (err) {
    console.error('deleteAssetsDemoPromise failed with error: ' + err);
  }
}
```

## MemberType

成员类型。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

| 名称  |  类型 |  可读  |  可写  |  说明  |
| ----- |  ---- |  ---- |  ---- |  ---- |
| number |  number | 是 | 是 | number类型。 |
| string |  string | 是 | 是 | string类型。|
| boolean |  boolean | 是 | 是 | boolean类型。 |

## PhotoType

枚举，媒体文件类型。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

| 名称  |  值 |  说明 |
| ----- |  ---- |  ---- |
| IMAGE |  1 |  图片。 |
| VIDEO |  2 |  视频。 |

## PhotoSubtype

枚举，不同[PhotoAsset](#photoasset)的类型。

**系统接口**：此接口为系统接口。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

| 名称  |  值 |  说明 |
| ----- |  ---- |  ---- |
| DEFAULT |  0 |  默认照片类型。 |
| SCREENSHOT |  1 |  截屏录屏文件类型。 |

## PositionType

枚举，文件位置，表示文件在本地或云端。

**系统接口**：此接口为系统接口。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

| 名称  |  值 |  说明 |
| ----- |  ---- |  ---- |
| LOCAL |  1 << 0 |  文件只存在于本端设备。 |
| CLOUD |  1 << 1 |  文件只存在于云端。 |

## AlbumType

枚举，相册类型，表示是用户相册还是系统预置相册。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

| 名称  |  值 |  说明 |
| ----- |  ---- |  ---- |
| USER |  0 |  用户相册。 |
| SYSTEM |  1024 |  系统预置相册。 |

## AlbumSubtype

枚举，相册子类型，表示具体的相册类型。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

| 名称  |  值 |  说明 |
| ----- |  ---- |  ---- |
| USER_GENERIC |  1 |  用户相册。 |
| FAVORITE |  1025 |  收藏夹。 |
| VIDEO |  1026 |  视频相册。 |
| HIDDEN |  1027 |  隐藏相册。**系统接口**：此接口为系统接口。 |
| TRASH |  1028 |  回收站。**系统接口**：此接口为系统接口。 |
| SCREENSHOT |  1029 |  截屏和录屏相册。**系统接口**：此接口为系统接口。 |
| CAMERA |  1030 |  相机拍摄的照片和视频相册。**系统接口**：此接口为系统接口。 |
| ANY |  2147483647 |  任意相册。 |

## PhotoKeys

枚举，图片和视频文件关键信息。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

| 名称          | 值              | 说明                                                       |
| ------------- | ------------------- | ---------------------------------------------------------- |
| URI           | 'uri'                 | 文件uri。                                                   |
| PHOTO_TYPE    | 'media_type'           | 媒体文件类型。                                              |
| DISPLAY_NAME  | 'display_name'        | 显示名字。                                                   |
| SIZE          | 'size'                | 文件大小。                                                   |
| DATE_ADDED    | 'date_added'          | 添加日期（添加文件时间距1970年1月1日的秒数值）。             |
| DATE_MODIFIED | 'date_modified'       | 修改日期（修改文件时间距1970年1月1日的秒数值，修改文件名不会改变此值，当文件内容发生修改时才会更新）。 |
| DURATION      | 'duration'            | 持续时间（单位：毫秒）。                                    |
| WIDTH         | 'width'               | 图片宽度（单位：像素）。                                    |
| HEIGHT        | 'height'              | 图片高度（单位：像素）。                                      |
| DATE_TAKEN    | 'date_taken'          | 拍摄日期（文件拍照时间距1970年1月1日的秒数值）。                |
| ORIENTATION   | 'orientation'         | 图片文件的方向。                                             |
| FAVORITE      | 'is_favorite'            | 收藏。                                                    |
| TITLE         | 'title'               | 文件标题。                                                   |
| POSITION  | 'position'            | 文件位置类型。**系统接口**：此接口为系统接口。                               |
| DATE_TRASHED  | 'date_trashed'  | 删除日期（删除文件时间距1970年1月1日的秒数值）。**系统接口**：此接口为系统接口。                 |
| HIDDEN  | 'hidden'            | 文件的隐藏状态。**系统接口**：此接口为系统接口。                               |

## AlbumKeys

枚举，相册关键信息。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

| 名称          | 值              | 说明                                                       |
| ------------- | ------------------- | ---------------------------------------------------------- |
| URI           | 'uri'                 | 相册uri。                                                   |
| ALBUM_NAME    | 'album_name'          | 相册名字。                                                   |

## PhotoCreateOptions

图片或视频的创建选项。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

| 名称                   | 类型                | 必填 | 说明                                              |
| ---------------------- | ------------------- | ---- | ------------------------------------------------ |
| subtype           | [PhotoSubtype](#photosubtype) | 否  | 图片或者视频的子类型。**系统接口**：此接口为系统接口。  |

## CreateOptions

图片或视频的创建选项。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

| 名称                   | 类型                | 必填 | 说明                                              |
| ---------------------- | ------------------- | ---- | ------------------------------------------------ |
| title           | string | 否  | 图片或者视频的标题。  |

## FetchOptions

检索条件。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

| 名称                   | 类型                | 可读 | 可写 | 说明                                              |
| ---------------------- | ------------------- | ---- |---- | ------------------------------------------------ |
| fetchColumns           | Array&lt;string&gt; | 是   | 是   | 检索条件，指定列名查询，如果该参数为空时默认查询uri、name、photoType（具体字段名称以检索对象定义为准）。示例：<br />fetchColumns: ['uri', 'title']。 |
| predicates           | [dataSharePredicates.DataSharePredicates](js-apis-data-dataSharePredicates.md) | 是   | 是   | 谓词查询，显示过滤条件。 |

## ChangeData

监听器回调函数的值。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

| 名称    | 类型                        | 可读 | 可写 | 说明                                                         |
| ------- | --------------------------- | ---- | ---- | ------------------------------------------------------------ |
| type    | [NotifyType](#notifytype) | 是   | 否   | ChangeData的通知类型。                                       |
| uris    | Array&lt;string&gt;         | 是   | 否   | 相同[NotifyType](#notifytype)的所有uri，可以是PhotoAsset或Album。 |
| extraUris | Array&lt;string&gt;         | 是   | 否   | 相册中变动文件的uri数组。                                    |

## NotifyType

枚举，通知事件的类型。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

| 名称                      | 值   | 说明                             |
| ------------------------- | ---- | -------------------------------- |
| NOTIFY_ADD                | 0    | 添加文件集或相册通知的类型。     |
| NOTIFY_UPDATE             | 1    | 文件集或相册的更新通知类型。     |
| NOTIFY_REMOVE             | 2    | 删除文件集或相册的通知类型。     |
| NOTIFY_ALBUM_ADD_ASSET    | 3    | 在相册中添加的文件集的通知类型。 |
| NOTIFY_ALBUM_REMOVE_ASSET | 4    | 在相册中删除的文件集的通知类型。 |

## DefaultChangeUri

枚举，DefaultChangeUri子类型。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

| 名称              | 值                      | 说明                                                         |
| ----------------- | ----------------------- | ------------------------------------------------------------ |
| DEFAULT_PHOTO_URI | 'file://media/Photo'      | 默认PhotoAsset的Uri，与forSubUri{true}一起使用，将接收所有PhotoAsset的更改通知。 |
| DEFAULT_ALBUM_URI | 'file://media/PhotoAlbum' | 默认相册的Uri，与forSubUri{true}一起使用，将接收所有相册的更改通知。 |
