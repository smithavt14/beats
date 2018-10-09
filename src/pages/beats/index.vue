<script>
import musicPlayer from '@/components/musicPlayer';

export default {
  computed: {},

  components: {
    musicPlayer,
  },

  data() {
    return {
      fakeMusicData: [
        { name: 'MicMasterK', songImg: 'https://images.pexels.com/photos/1238980/pexels-photo-1238980.jpeg?auto=compress&cs=tinysrgb&dpr=2&h=650&w=940', songLink: '' },
        { name: 'Fiesty Meatballs', songImg: 'https://images.pexels.com/photos/462442/pexels-photo-462442.jpeg?auto=compress&cs=tinysrgb&dpr=2&h=650&w=940', songLink: '' },
        { name: 'Mr. Operator', songImg: 'https://images.pexels.com/photos/802195/pexels-photo-802195.jpeg?auto=compress&cs=tinysrgb&dpr=2&h=650&w=940', songLink: '' },
      ],
    };
  },

  methods: {

    startRecording() {
      const recorderManager = wx.getRecorderManager();

      recorderManager.onStart(() => {
        console.log('recorder start');
      });

      const options = {
        duration: 10000,
        sampleRate: 44100,
        numberOfChannels: 1,
        encodeBitRate: 192000,
        format: 'aac',
        frameSize: 50,
      };
      recorderManager.start(options);
    },

    stopRecording() {
      const recorderManager = wx.getRecorderManager();
      recorderManager.onStop((res) => {
        console.log('recorder stop', res);
        this.recording = res.tempFilePath;
        console.log(this.recording);
      });
      recorderManager.stop();
    },

    playRecording() {
      const backgroundAudio = wx.getBackgroundAudioManager();
      backgroundAudio.title = 'Title';
      backgroundAudio.src = this.recording;
    },

    playMusic() {
      const backgroundAudio = wx.getBackgroundAudioManager();
      backgroundAudio.title = 'Title';
      backgroundAudio.src = 'http://ws.stream.qqmusic.qq.com/M500001VfvsJ21xFqb.mp3?guid=ffffffff82def4af4b12b3cd9337d5e7&uin=346897220&vkey=6292F51E1E384E06DCBDC9AB7C49FD713D632D313AC4858BACB8DDD29067D3C601481D36E62053BF8DFEAF74C0A5CCFADD6471160CAF3E6A&fromtag=46';
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

<template>
  <view class="beats__wrapper">
    <musicPlayer :musicData="fakeMusicData" class="beats__music-player"></musicPlayer>
    <view class="beats__recorder" @touchstart="startRecording" @touchend="stopRecording" hover-class="beats__recorder-active"></view>
  </view>
</template>

<style>

.beats__wrapper {
  background: linear-gradient(201.34deg, #0B191E 45.21%, #10110F 99.59%);
  height: 100vh;
  width: 100vw;
  color: white;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  align-items: center;
}

.beats__music-player {
  margin-top: 20px;
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

.beats__recorder-active {
  animation-name: recorder;
  animation-duration: 0.5s;
  box-shadow: 0 0 30px white;
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

@keyframes recorder {
  from {
    box-shadow: none;
  }

  to {
    box-shadow: 0 0 20px white;
  }
}



</style>
