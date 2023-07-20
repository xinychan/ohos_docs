# 系统相册资源使用指导

photoAccessHelper仅提供开发者对收藏夹、视频相册、截屏和录屏相册进行相关操作。

> **说明：**
>
> 在进行功能开发前，请开发者查阅[相册管理模块开发概述](photoAccessHelper-overview.md)，了解如何获取相册管理模块实例和如何申请相册管理模块功能开发相关权限。
> 文档中使用到mgr的地方默认为使用相册管理模块开发概述中获取的对象，如未添加此段代码报mgr未定义的错误请自行添加。

为了保证应用的运行效率，大部分photoAccessHelper调用都是异步的，对于异步调用的API均提供了callback和Promise两种方式，以下示例均采用Promise函数，更多方式可以查阅[API参考](../reference/apis/js-apis-photoAccessHelper.md)。
如无特别说明，文档中涉及的待获取的资源均视为已经预置且在数据库中存在相应数据。如出现按照示例代码执行出现获取资源为空的情况请确认文件是否已预置，数据库中是否存在该文件的数据。

## 收藏夹

收藏夹属于系统相册，对图片或视频设置收藏时会自动将其加入到收藏夹中，取消收藏则会从收藏夹中移除。

### 获取收藏夹对象

通过[getAlbums](../reference/apis/js-apis-photoAccessHelper.md#getalbums)接口获取收藏夹对象。

**前提条件：**

- 获取相册管理模块photoAccessHelper实例。
- 申请相册管理模块权限'ohos.permission.READ_IMAGEVIDEO'。

**开发步骤：**

1. 设置获取收藏夹的参数为photoAccessHelper.AlbumType.SYSTEM和photoAccessHelper.AlbumSubtype.FAVORITE。
2. 调用getAlbums接口获取收藏夹对象。

```ts
try {
  let fetchResult = await phAccessHelper.getAlbums(photoAccessHelper.AlbumType.SYSTEM, photoAccessHelper.AlbumSubtype.FAVORITE);
  let album = await fetchResult.getFirstObject();
  console.info('get favorite Album successfully, albumUri: ' + album.albumUri);
  fetchResult.close();
} catch (err) {
  console.error('get favorite Album failed with err: ' + err);
}
```

### 收藏图片和视频

通过[favorite](../reference/apis/js-apis-photoAccessHelper.md#favorite)接口将图片或者视频设置收藏。

**前提条件：**

- 获取相册管理模块photoAccessHelper实例。
- 申请相册管理模块权限'ohos.permission.READ_IMAGEVIDEO'和'ohos.permission.WRITE_IMAGEVIDEO'。

下面将以收藏一张图片为例。

**开发步骤：**

1. [获取指定媒体资源](photoAccessHelper-resource-guidelines.md#获取指定媒体资源)。
2. isFavorite参数设置为true，表示将会设置为收藏。
3. 调用FileAsset.favorite接口设置收藏。

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

let predicates = new dataSharePredicates.DataSharePredicates();
predicates.equalTo(photoAccessHelper.ImageVideoKey.DISPLAY_NAME, 'test.jpg');
let fetchOptions = {
  fetchColumns: [],
  predicates: predicates
};

try {
  let photoFetchResult = await phAccessHelper.getAssets(fetchOptions);
  let fileAsset = await photoFetchResult.getFirstObject();
  console.info('getAssets fileAsset.displayName : ' + fileAsset.displayName);
  let isFavorite = true;
  await fileAsset.favorite(isFavorite);
} catch (err) {
  console.error('favorite failed with err: ' + err);
}
```

### 获取收藏夹中的图片和视频

先[获取收藏夹对象](#获取收藏夹对象)。然后调用[Album.getAssets](../reference/apis/js-apis-photoAccessHelper.md#getassets-2)接口获取收藏夹中的资源。

**前提条件：**

- 获取相册管理模块photoAccessHelper实例。
- 申请相册管理模块权限'ohos.permission.READ_IMAGEVIDEO'。

下面以获取收藏夹中的一张图片为例。

**开发步骤：**

1. [获取收藏夹对象](#获取收藏夹对象)。
2. 建立图片检索条件，用于获取图片。
3. 调用Album.getAssets接口获取图片资源。
4. 调用[FetchResult.getFirstObject](../reference/apis/js-apis-photoAccessHelper.md#getfirstobject)接口获取第一张图片。

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

let predicates = new dataSharePredicates.DataSharePredicates();
let fetchOptions = {
  fetchColumns: [],
  predicates: predicates
};

try {
  let albumFetchResult = await phAccessHelper.getAlbums(photoAccessHelper.AlbumType.SYSTEM, photoAccessHelper.AlbumSubtype.FAVORITE);
  let album = await albumFetchResult.getFirstObject();
  console.info('get favorite Album successfully, albumUri: ' + album.albumUri);

  let photoFetchResult = await album.getAssets(fetchOptions);
  let fileAsset = await photoFetchResult.getFirstObject();
  console.info('favorite album getAssets successfully, albumName: ' + fileAsset.displayName);
  photoFetchResult.close();
  albumFetchResult.close();
} catch (err) {
  console.error('favorite failed with err: ' + err);
}
```

### 取消收藏图片或视频

通过[favorite](../reference/apis/js-apis-photoAccessHelper.md#favorite)接口将图片或者视频取消收藏。

**前提条件：**

- 获取相册管理模块photoAccessHelper实例。
- 申请相册管理模块权限'ohos.permission.READ_IMAGEVIDEO'和'ohos.permission.WRITE_IMAGEVIDEO'。

下面以将一张图片取消收藏为例。

**开发步骤：**

1. [获取收藏夹中的图片和视频](#获取收藏夹中的图片和视频)。
2. isFavorite参数设置为false。
3. 调用FileAsset.favorite接口设置收藏。


```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

let predicates = new dataSharePredicates.DataSharePredicates();
let fetchOptions = {
  fetchColumns: [],
  predicates: predicates
};

try {
  let albumFetchResult = await phAccessHelper.getAlbums(photoAccessHelper.AlbumType.SYSTEM, photoAccessHelper.AlbumSubtype.FAVORITE);
  let album = await albumFetchResult.getFirstObject();
  console.info('get favorite Album successfully, albumUri: ' + album.albumUri);

  let photoFetchResult = await album.getAssets(fetchOptions);
  let fileAsset = await photoFetchResult.getFirstObject();
  console.info('favorite album getAssets successfully, albumName: ' + fileAsset.displayName);
  let isFavorite = false;
  await fileAsset.favorite(isFavorite);
  photoFetchResult.close();
  albumFetchResult.close();
} catch (err) {
  console.error('favorite failed with err: ' + err);
}
```

## 视频相册

视频相册属于系统相册，用户文件中属于视频类型的媒体文件会自动加入到视频相册中。

### 获取视频相册对象

通过[getAlbums](../reference/apis/js-apis-photoAccessHelper.md#getalbums)接口获取视频相册对象。

**前提条件：**

- 获取相册管理模块photoAccessHelper实例。
- 申请相册管理模块权限'ohos.permission.READ_IMAGEVIDEO'。

**开发步骤：**

1. 设置获取视频相册的参数为photoAccessHelper.AlbumType.SYSTEM和photoAccessHelper.AlbumSubtype.VIDEO。
2. 调用getAlbums接口获取视频相册。

```ts
try {
  let fetchResult = await phAccessHelper.getAlbums(photoAccessHelper.AlbumType.SYSTEM, photoAccessHelper.AlbumSubtype.VIDEO);
  let album = await fetchResult.getFirstObject();
  console.info('get video Album successfully, albumUri: ' + album.albumUri);
  fetchResult.close();
} catch (err) {
  console.error('get video Album failed with err: ' + err);
}
```

### 获取视频相册中的视频

先[获取视频相册对象](#获取视频相册对象)。然后调用[Album.getAssets](../reference/apis/js-apis-photoAccessHelper.md#getassets-2)接口获取视频相册对象中的视频资源。

**前提条件：**

- 获取相册管理模块photoAccessHelper实例。
- 申请相册管理模块权限'ohos.permission.READ_IMAGEVIDEO'。

下面以获取视频相册中的一个视频为例。

**开发步骤：**

1. 先[获取视频相册对象](#获取视频相册对象)。
2. 建立视频检索条件，用于获取视频。
3. 调用Album.getAssets接口获取视频资源。
4. 调用[FetchResult.getFirstObject](../reference/apis/js-apis-photoAccessHelper.md#getfirstobject)接口获取第一个视频。

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

let predicates = new dataSharePredicates.DataSharePredicates();
let fetchOptions = {
  fetchColumns: [],
  predicates: predicates
};

try {
  let albumFetchResult = await phAccessHelper.getAlbums(photoAccessHelper.AlbumType.SYSTEM, photoAccessHelper.AlbumSubtype.VIDEO);
  let album = await albumFetchResult.getFirstObject();
  console.info('get video Album successfully, albumUri: ' + album.albumUri);

  let videoFetchResult = await album.getAssets(fetchOptions);
  let fileAsset = await videoFetchResult.getFirstObject();
  console.info('video album getAssets successfully, albumName: ' + fileAsset.displayName);
  videoFetchResult.close();
  albumFetchResult.close();
} catch (err) {
  console.error('video failed with err: ' + err);
}
```

## 截屏和录屏相册

截屏和录屏相册属于系统相册，用户文件中属于截屏和录屏的媒体文件会自动加入到截屏和录屏相册中。

### 获取截屏和录屏相册对象

通过[getAlbums](../reference/apis/js-apis-photoAccessHelper.md#getalbums)接口获取截屏和录屏相册。

**前提条件：**

- 获取相册管理模块photoAccessHelper实例。
- 申请相册管理模块权限'ohos.permission.READ_IMAGEVIDEO'。

**开发步骤：**

1. 设置获取截屏和录屏相册的参数为photoAccessHelper.AlbumType.SYSTEM和photoAccessHelper.AlbumSubtype.SCREENSHOT。
2. 调用getAlbums接口获取截屏和录屏相册。

```ts
try {
  let fetchResult = await phAccessHelper.getAlbums(photoAccessHelper.AlbumType.SYSTEM, photoAccessHelper.AlbumSubtype.SCREENSHOT);
  let album = await fetchResult.getFirstObject();
  console.info('get screenshot Album successfully, albumUri: ' + album.albumUri);
  fetchResult.close();
} catch (err) {
  console.error('get screenshot Album failed with err: ' + err);
}
```

### 获取截屏和录屏相册中的媒体资源

先[获取截屏和录屏相册对象](#获取截屏和录屏相册对象)。然后调用[Album.getAssets](../reference/apis/js-apis-photoAccessHelper.md#getassets-2)接口获取截屏和录屏相册对象中的媒体资源。

**前提条件：**

- 获取相册管理模块photoAccessHelper实例。
- 申请相册管理模块权限'ohos.permission.READ_IMAGEVIDEO'。

下面以获取截屏和录屏相册中的一个媒体资源为例。

**开发步骤：**

1. 先[获取截屏和录屏相册对象](#获取截屏和录屏相册对象)。
2. 建立检索条件，用于获取媒体资源。
3. 调用Album.getAssets接口获取媒体资源。
4. 调用[FetchResult.getFirstObject](../reference/apis/js-apis-photoAccessHelper.md#getfirstobject)接口获取第一个媒体资源。

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

let predicates = new dataSharePredicates.DataSharePredicates();
let fetchOptions = {
  fetchColumns: [],
  predicates: predicates
};

try {
  let albumFetchResult = await phAccessHelper.getAlbums(photoAccessHelper.AlbumType.SYSTEM, photoAccessHelper.AlbumSubtype.SCREENSHOT);
  let album = await albumFetchResult.getFirstObject();
  console.info('get screenshot album successfully, albumUri: ' + album.albumUri);

  let screenshotFetchResult = await album.getAssets(fetchOptions);
  let fileAsset = await screenshotFetchResult.getFirstObject();
  console.info('screenshot album getAssets successfully, albumName: ' + fileAsset.displayName);
  screenshotFetchResult.close();
  albumFetchResult.close();
} catch (err) {
  console.error('screenshot album failed with err: ' + err);
}
```
