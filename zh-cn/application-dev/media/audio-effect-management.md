# 音效管理

音效管理主要包括播放实例音效管理和全局音效查询两部分，播放实例音效管理主要包括查询和设置当前音频播放流的音效模式，全局音效查询支持查询ContentType和StreamUsage对应场景支持的音效模式。

## 播放实例音效管理

主要包括查询和设置当前音频播放流的音效模式，音效模式包括EFFECT_NONE关闭音效模式和EFFECT_DEFAULT默认音效模式。默认音效模式会根据创建音频流的ContentType和StreamUsage自动加载对应场景的音效。

### 获取播放实例

管理播放实例音效的接口是getAudioEffectMode()查询当前音频播放流的音效模式和setAudioEffectMode(mode: AudioEffectMode)设置当前音频播放流的音效模式，在使用之前，需要使用createAudioRenderer(options: AudioRendererOptions)先创建音频播放流AudioRenderer实例。

1. 步骤一：导入音频接口。

  ```js
  import audio from '@ohos.multimedia.audio';
  ```

2. 步骤二：配置音频渲染参数并创建AudioRenderer实例，音频渲染参数的详细信息可以查看[AudioRendererOptions](../reference/apis/js-apis-audio.md#audiorendereroptions8)，创建AudioRenderer实例时会默认挂载EFFECT_DEFAULT模式音效。

  ```js
  let audioStreamInfo = {
    samplingRate: audio.AudioSamplingRate.SAMPLE_RATE_44100,
    channels: audio.AudioChannel.CHANNEL_1,
    sampleFormat: audio.AudioSampleFormat.SAMPLE_FORMAT_S16LE,
    encodingType: audio.AudioEncodingType.ENCODING_TYPE_RAW
  };

  let audioRendererInfo = {
    content: audio.ContentType.CONTENT_TYPE_SPEECH,
    usage: audio.StreamUsage.STREAM_USAGE_VOICE_COMMUNICATION,
    rendererFlags: 0
  };

  let audioRendererOptions = {
    streamInfo: audioStreamInfo,
    rendererInfo: audioRendererInfo
  };

  audio.createAudioRenderer(audioRendererOptions, (err, data) => {
    if (err) {
      console.error(`Invoke createAudioRenderer failed, code is ${err.code}, message is ${err.message}`);
      return;
    } else {
      console.info('Invoke createAudioRenderer succeeded.');
      let audioRenderer = data;
    }
  });
  ```

### 查询当前播放实例的音效模式

  ```js
  audioRenderer.getAudioEffectMode((err, effectmode) => {
    if (err) {
      console.error(`Failed to get params, code is ${err.code}, message is ${err.message}`);
      return;    
    } else {
      console.info(`getAudioEffectMode: ${effectmode}`);
    }
  });
  ```

### 设置当前播放实例的音效模式

关闭系统音效：

  ```js
  audioRenderer.setAudioEffectMode(audio.AudioEffectMode.EFFECT_NONE, (err) => {
    if (err) {
      console.error(`Failed to set params, code is ${err.code}, message is ${err.message}`);
      return;
    } else {
      console.info('Callback invoked to indicate a successful audio effect mode setting.');
    }
  });
  ```

开启系统音效默认模式：

  ```js
  audioRenderer.setAudioEffectMode(audio.AudioEffectMode.EFFECT_DEFAULT, (err) => {
    if (err) {
      console.error(`Failed to set params, code is ${err.code}, message is ${err.message}`);
      return;
    } else {
      console.info('Callback invoked to indicate a successful audio effect mode setting.');
    }
  });
  ```

## 全局查询音效模式

主要包括全局音效查询相应StreamUsage对应场景的音效模式。
对于播放音频类的应用，开发者需要关注该应用的音频流使用什么音效模式并做出相应的操作，比如音乐App播放时，应选择音乐场景下的模式。在使用查询接口前，开发者需要使用getStreamManager()创建一个AudioStreamManager音频流管理实例。

### 获取音频流管理接口

1.创建AudioStreamManager实例。在使用AudioStreamManager的API前，需要使用getStreamManager()创建一个AudioStreamManager实例。

   ```js
   import audio from '@ohos.multimedia.audio';
   let audioManager = audio.getAudioManager();
   let audioStreamManager = audioManager.getStreamManager();
   ```

### 查询对应场景的音效模式

  ```js
  audioStreamManager.getAudioEffectInfoArray(audio.StreamUsage.STREAM_USAGE_MEDIA, async (err, audioEffectInfoArray) => {
    if (err) {
      console.error('Failed to get effect info array');
      return;    
    } else {
      console.info(`getAudioEffectInfoArray: ${audioEffectInfoArray}`);
    }
  });
  ```
