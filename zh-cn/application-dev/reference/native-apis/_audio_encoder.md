# AudioEncoder

## 概述

AudioEncoder模块提供用于音频编码的函数。该模块在部分设备上可能不支持，可以通过[CanIUse](../syscap.md)接口确认。

\@syscap SystemCapability.Multimedia.Media.AudioEncoder

**起始版本：**

9

## 汇总

### 文件

| 名称                                                              | 描述                                                                                                        |
| ----------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------- |
| [native_avcodec_audioencoder.h](native__avcodec__audioencoder_8h.md) | 声明用于音频编码的Native API。<br>**引用文件**：<multimedia/player_framework/native_avcodec_audioencoder.h><br>**库**：libnative_media_aenc.so |

### 函数

| 名称                                                                                                                                          | 描述                                                                             |
| --------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------- |
| \*[OHOS::Media::OH_AudioEncoder_CreateByMime](#oh_audioencoder_createbymime) (const char \*mime)                                                 | 根据MIME类型创建音频编码器实例，大多数场景下建议使用此方式。                     |
| \*[OHOS::Media::OH_AudioEncoder_CreateByName](#oh_audioencoder_createbyname) (const char \*name)                                                 | 通过音频编码器名称创建音频编码器实例，使用此接口的前提是知道编码器的确切名称。   |
| [OHOS::Media::OH_AudioEncoder_Destroy](#oh_audioencoder_destroy) (OH_AVCodec \*codec)                                                            | 清理编码器内部资源，销毁编码器实例。                                             |
| [OHOS::Media::OH_AudioEncoder_SetCallback](#oh_audioencoder_setcallback) (OH_AVCodec \*codec, OH_AVCodecAsyncCallback callback, void \*userData) | 设置异步回调函数，使您的应用程序可以响应音频编码器生成的事件。                   |
| [OHOS::Media::OH_AudioEncoder_Configure](#oh_audioencoder_configure) (OH_AVCodec \*codec, OH_AVFormat \*format)                                  | 要配置音频编码器，通常需要配置编码后的音轨的描述信息。                           |
| [OHOS::Media::OH_AudioEncoder_Prepare](#oh_audioencoder_prepare) (OH_AVCodec \*codec)                                                            | 准备编码器的内部资源，在调用此接口之前必须调用Configure接口。                    |
| [OHOS::Media::OH_AudioEncoder_Start](#oh_audioencoder_start) (OH_AVCodec \*codec)                                                                | Prepare成功后调用此接口启动编码器。                                              |
| [OHOS::Media::OH_AudioEncoder_Stop](#oh_audioencoder_stop) (OH_AVCodec \*codec)                                                                  | 停止编码器。                                                                     |
| [OHOS::Media::OH_AudioEncoder_Flush](#oh_audioencoder_flush) (OH_AVCodec \*codec)                                                                | 清除编码器中缓存的输入和输出数据。                                               |
| [OHOS::Media::OH_AudioEncoder_Reset](#oh_audioencoder_reset) (OH_AVCodec \*codec)                                                                | 重置编码器。                                                                     |
| \*[OHOS::Media::OH_AudioEncoder_GetOutputDescription](#oh_audioencoder_getoutputdescription) (OH_AVCodec \*codec)                                | 获取编码器输出数据的描述信息，详细信息请参见[OH_AVFormat](native__avformat_8h.md)。 |
| [OHOS::Media::OH_AudioEncoder_SetParameter](#oh_audioencoder_setparameter) (OH_AVCodec \*codec, OH_AVFormat \*format)                            | 配置编码器的动态参数。                                                           |
| [OHOS::Media::OH_AudioEncoder_PushInputData](#oh_audioencoder_pushinputdata) (OH_AVCodec \*codec, uint32_t index, OH_AVCodecBufferAttr attr)     | 将填充有数据的输入缓冲区提交给音频编码器。                                       |
| [OHOS::Media::OH_AudioEncoder_FreeOutputData](#oh_audioencoder_freeoutputdata) (OH_AVCodec \*codec, uint32_t index)                              | 将处理后的输出缓冲区返回给编码器。                                               |
| [OHOS::Media::OH_AudioEncoder_IsValid](#oh_audioencoder_isvalid) (OH_AVCodec \*codec, bool \*isValid)                                            | 检查当前编码器实例是否有效。                                                     |

## 函数说明

### OH_AudioEncoder_Configure()

```
OH_AVErrCode OHOS::Media::OH_AudioEncoder_Configure (OH_AVCodec * codec, OH_AVFormat * format )
```

**描述：**

要配置音频编码器，通常需要配置编码后的音轨的描述信息。

在调用Prepare之前，必须调用此接口。

\@syscap SystemCapability.Multimedia.Media.AudioEncoder

**参数：**

| 名称   | 描述                                                |
| ------ | --------------------------------------------------- |
| codec  | 指向OH_AVCodec实例的指针。                          |
| format | 指向OH_AVFormat的指针，给出要编码的音频轨道的描述。 |

**返回：**

如果执行成功，则返回AV_ERR_OK，否则返回特定错误代码，请参阅[OH_AVErrCode](_core.md#oh_averrcode)。

**起始版本：**

9

### OH_AudioEncoder_CreateByMime()

```
OH_AVCodec* OHOS::Media::OH_AudioEncoder_CreateByMime (const char * mime)
```

**描述：**

根据MIME类型创建音频编码器实例，大多数场景下建议使用此方式。

\@syscap SystemCapability.Multimedia.Media.AudioEncoder

**参数：**

| 名称 | 描述                                                    |
| ---- | ------------------------------------------------------- |
| mime | MIME类型描述字符串，请参阅**AVCODEC_MIME_TYPE**。 |

**返回：**

返回指向OH_AVCodec实例的指针。

**起始版本：**

9

### OH_AudioEncoder_CreateByName()

```
OH_AVCodec* OHOS::Media::OH_AudioEncoder_CreateByName (const char * name)
```

**描述：**

通过音频编码器名称创建音频编码器实例，使用此接口的前提是知道编码器的确切名称。

\@syscap SystemCapability.Multimedia.Media.AudioEncoder

**参数：**

| 名称 | 描述             |
| ---- | ---------------- |
| name | 音频编码器名称。 |

**返回：**

返回指向OH_AVCodec实例的指针。

**起始版本：**

9

### OH_AudioEncoder_Destroy()

```
OH_AVErrCode OHOS::Media::OH_AudioEncoder_Destroy (OH_AVCodec * codec)
```

**描述：**

清理编码器内部资源，销毁编码器实例。

\@syscap SystemCapability.Multimedia.Media.AudioEncoder

**参数：**

| 名称  | 描述                       |
| ----- | -------------------------- |
| codec | 指向OH_AVCodec实例的指针。 |

**返回：**

如果执行成功，则返回AV_ERR_OK，否则返回特定错误代码，请参阅[OH_AVErrCode](_core.md#oh_averrcode)。

**起始版本：**

9

### OH_AudioEncoder_Flush()

```
OH_AVErrCode OHOS::Media::OH_AudioEncoder_Flush (OH_AVCodec * codec)
```

**描述：**

清除编码器中缓存的输入和输出数据。

调用此接口后，以前通过异步回调上报的所有缓冲区 索引都将失效，请确保不要访问这些索引对应的缓冲区。

\@syscap SystemCapability.Multimedia.Media.AudioEncoder

**参数：**

| 名称  | 描述                       |
| ----- | -------------------------- |
| codec | 指向OH_AVCodec实例的指针。 |

**返回：**

如果执行成功，则返回AV_ERR_OK，否则返回特定错误代码，请参阅[OH_AVErrCode](_core.md#oh_averrcode)。

**起始版本：**

9

### OH_AudioEncoder_FreeOutputData()

```
OH_AVErrCode OHOS::Media::OH_AudioEncoder_FreeOutputData (OH_AVCodec * codec, uint32_t index )
```

**描述：**

将处理后的输出缓冲区返回给编码器。

\@syscap SystemCapability.Multimedia.Media.AudioEncoder

**参数：**

| 名称  | 描述                           |
| ----- | ------------------------------ |
| codec | 指向OH_AVCodec实例的指针。     |
| index | 输出缓冲区Buffer对应的索引值。 |

**返回：**

如果执行成功，则返回AV_ERR_OK，否则返回特定错误代码，请参阅[OH_AVErrCode](_core.md#oh_averrcode)。

**起始版本：**

9

### OH_AudioEncoder_GetOutputDescription()

```
OH_AVFormat* OHOS::Media::OH_AudioEncoder_GetOutputDescription (OH_AVCodec * codec)
```

**描述：**

获取编码器输出数据的描述信息，详细信息请参见[OH_AVFormat](native__avformat_8h.md)。

需要注意的是，返回值所指向的OH_AVFormat实例的生命周期需要调用者手动释放。

\@syscap SystemCapability.Multimedia.Media.AudioEncoder

**参数：**

| 名称  | 描述                       |
| ----- | -------------------------- |
| codec | 指向OH_AVCodec实例的指针。 |

**返回：**

返回OH_AVFormat句柄指针，生命周期将使用下一个GetOutputDescription 刷新，或使用OH_AVCodec销毁。

**起始版本：**

9

### OH_AudioEncoder_IsValid()

```
OH_AVErrCode OHOS::Media::OH_AudioEncoder_IsValid (OH_AVCodec * codec, bool * isValid )
```

**描述：**

检查当前编码器实例是否有效。

\@syscap SystemCapability.Multimedia.Media.AudioEncoder

**参数：**

| 名称    | 描述                                                              |
| ------- | ----------------------------------------------------------------- |
| codec   | 指向OH_AVCodec实例的指针。                                        |
| isValid | 指向布尔实例的指针，true：编码器实例有效，false：编码器实例无效。 |

**返回：**

如果执行成功，则返回AV_ERR_OK，否则返回特定错误代码，请参阅[OH_AVErrCode](_core.md#oh_averrcode)。

**起始版本：**

10

### OH_AudioEncoder_Prepare()

```
OH_AVErrCode OHOS::Media::OH_AudioEncoder_Prepare (OH_AVCodec * codec)
```

**描述：**

准备编码器的内部资源，在调用此接口之前必须调用Configure接口。

\@syscap SystemCapability.Multimedia.Media.AudioEncoder

**参数：**

| 名称  | 描述                       |
| ----- | -------------------------- |
| codec | 指向OH_AVCodec实例的指针。 |

**返回：**

如果执行成功，则返回AV_ERR_OK，否则返回特定错误代码，请参阅[OH_AVErrCode](_core.md#oh_averrcode)。

**起始版本：**

9

### OH_AudioEncoder_PushInputData()

```
OH_AVErrCode OHOS::Media::OH_AudioEncoder_PushInputData (OH_AVCodec * codec, uint32_t index, OH_AVCodecBufferAttr attr )
```

**描述：**

将填充有数据的输入缓冲区提交给音频编码器。

**OH_AVCodecOnNeedInputData**回调 将报告可用的输入缓冲区和相应的索引值。一旦具有指定索引的缓冲区提交到音频编码器，则无法再次访问此缓冲区， 直到再次收到**OH_AVCodecOnNeedInputData**回调，收到相同索引时此缓冲区才可使用。 此外，对于某些编码器，需要在开始时向编码器输入特定配置参数，以初始化编码器的编码过程。

\@syscap SystemCapability.Multimedia.Media.AudioEncoder

**参数：**

| 名称  | 描述                           |
| ----- | ------------------------------ |
| codec | 指向OH_AVCodec实例的指针。     |
| index | 输入缓冲区Buffer对应的索引值。 |
| attr  | 描述缓冲区中包含的数据的信息。 |

**返回：**

如果执行成功，则返回AV_ERR_OK，否则返回特定错误代码，请参阅[OH_AVErrCode](_core.md#oh_averrcode)。

**起始版本：**

9

### OH_AudioEncoder_Reset()

```
OH_AVErrCode OHOS::Media::OH_AudioEncoder_Reset (OH_AVCodec * codec)
```

**描述：**

重置编码器。如果要继续编码，需要再次调用Configure接口配置编码器实例。

\@syscap SystemCapability.Multimedia.Media.AudioEncoder

**参数：**

| 名称  | 描述                       |
| ----- | -------------------------- |
| codec | 指向OH_AVCodec实例的指针。 |

**返回：**

如果执行成功，则返回AV_ERR_OK，否则返回特定错误代码，请参阅[OH_AVErrCode](_core.md#oh_averrcode)。

### OH_AudioEncoder_SetCallback()

```
OH_AVErrCode OHOS::Media::OH_AudioEncoder_SetCallback (OH_AVCodec * codec, OH_AVCodecAsyncCallback callback, void * userData )
```

**描述：**

设置异步回调函数，使您的应用程序可以响应音频编码器生成的事件。

在调用Prepare之前，必须调用此接口。

\@syscap SystemCapability.Multimedia.Media.AudioEncoder

**参数：**

| 名称     | 描述                                                          |
| -------- | ------------------------------------------------------------- |
| codec    | 指向OH_AVCodec实例的指针。                                    |
| callback | 所有回调函数的集合，请参见**OH_AVCodecAsyncCallback**。 |
| userData | 用户特定数据。                                                |

**返回：**

如果执行成功，则返回AV_ERR_OK，否则返回特定错误代码，请参阅[OH_AVErrCode](_core.md#oh_averrcode)。

**起始版本：**

9

### OH_AudioEncoder_SetParameter()

```
OH_AVErrCode OHOS::Media::OH_AudioEncoder_SetParameter (OH_AVCodec * codec, OH_AVFormat * format )
```

**描述：**

配置编码器的动态参数。

注意，该接口必须在编码器启动后才能调用。另外，参数配置错误可能会导致编码失败。

\@syscap SystemCapability.Multimedia.Media.AudioEncoder

**参数：**

| 名称   | 描述                       |
| ------ | -------------------------- |
| codec  | 指向OH_AVCodec实例的指针。 |
| format | OH_AVFormat句柄指针。      |

**返回：**

如果执行成功，则返回AV_ERR_OK，否则返回特定错误代码，请参阅[OH_AVErrCode](_core.md#oh_averrcode)。

**起始版本：**

9

### OH_AudioEncoder_Start()

```
OH_AVErrCode OHOS::Media::OH_AudioEncoder_Start (OH_AVCodec * codec)
```

**描述：**

Prepare成功后调用此接口启动编码器。

启动后，编码器将开始上报OH_AVCodecOnNeedInputData事件。

\@syscap SystemCapability.Multimedia.Media.AudioEncoder

**参数：**

| 名称  | 描述                       |
| ----- | -------------------------- |
| codec | 指向OH_AVCodec实例的指针。 |

**返回：**

如果执行成功，则返回AV_ERR_OK，否则返回特定错误代码，请参阅[OH_AVErrCode](_core.md#oh_averrcode)。

**起始版本：**

9

### OH_AudioEncoder_Stop()

```
OH_AVErrCode OHOS::Media::OH_AudioEncoder_Stop (OH_AVCodec * codec)
```

**描述：**

停止编码器。停止后，您可以通过Start重新进入已启动状态。

\@syscap SystemCapability.Multimedia.Media.AudioEncoder

**参数：**

| 名称  | 描述                       |
| ----- | -------------------------- |
| codec | 指向OH_AVCodec实例的指针。 |

**返回：**

如果执行成功，则返回AV_ERR_OK，否则返回特定错误代码，请参阅[OH_AVErrCode](_core.md#oh_averrcode)。

**起始版本：**

9
