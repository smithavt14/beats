<template>
  <view class="beats__wrapper">
    <view>
      <text>Beats Page</text>
    </view>
    <view class="beats__callback" @tap="playBack" hover-class="beats__callback-active">START RECORDING CALLBACK</view>
    <view class="beats__callback" @tap="playMusic" hover-class="beats__callback-active">PLAY MUSIC</view>
    <view class="beats__callback" @tap="stopMusic" hover-class="beats__callback-active">STOP MUSIC</view>
    <view class="beats__callback" @tap="pauseMusic" hover-class="beats__callback-active">PAUSE MUSIC</view>
    <view class="beats__recorder" @tap="record"></view>
  </view>
</template>


<script>

export default {
  computed: {},

  data() {
    return {
      recording: '',
    };
  },

  methods: {
    record() {
      const recorderManager = wx.getRecorderManager();

      recorderManager.onStart(() => {
        console.log('recorder start');
      });
      recorderManager.onPause(() => {
        console.log('recorder pause');
      });
      recorderManager.onStop((res) => {
        console.log('recorder stop', res);
        this.recording = res.tempFilePath;
        console.log(this.recording);
      });
      recorderManager.onFrameRecorded((res) => {
        const frameBuffer = res;
        console.log('frameBuffer.byteLength', frameBuffer.byteLength);
      });
      const options = {
        duration: 5000,
        sampleRate: 44100,
        numberOfChannels: 1,
        encodeBitRate: 192000,
        format: 'aac',
        frameSize: 50,
      };
      recorderManager.start(options);
    },

    playBack() {
      const backgroundAudio = wx.getBackgroundAudioManager();
      backgroundAudio.title = 'Title';
      backgroundAudio.src = this.recording;
    },

    playMusic() {
      const backgroundAudio = wx.getBackgroundAudioManager();
      backgroundAudio.title = 'Title';
      backgroundAudio.src = 'http://mp3hdfm32.hala.jo:8132';
    },

    stopMusic() {
      const backgroundAudio = wx.getBackgroundAudioManager();
      backgroundAudio.stop();
    },

    pauseMusic() {
      const backgroundAudio = wx.getBackgroundAudioManager();
      backgroundAudio.pause();
    },
  },
};

</script>

<style>
@font-face {
    font-family: Marker;
    src: url(/src/style/fonts/PermanentMarker-Regular.ttf) format("ttf");
}

.beats__wrapper {
  background: linear-gradient(201.34deg, #0B191E 45.21%, #10110F 99.59%);
  height: 100vh;
  width: 100vw;
  color: white;
  font-family: Marker;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

.beats__recorder {
  margin: 0 auto;
  margin-bottom: 50px;
  height: 50px;
  width: 50px;
  border-radius: 50%;
  background-color: red;
  border: 3px solid white;
}

.beats__callback {
  width: 90vw;
  margin: 0 auto;
  height: 30px;
  border-radius: 50px;
  border: 1px solid white;
  text-align: center;
}

.beats__callback-active {
  background-color: white;
  color: black;
}
</style>
