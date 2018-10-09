<script>
export default {
  props: ['musicData'],

  data() {
    return {
      message: 'Alex',
    };
  },
};
</script>

<template>
  <div class="music_player__wrapper">
    <div :style="musicData[0].songImg" class="music_player__album-art"></div>
  </div>
</template>

<style>
.music_player__wrapper {
  height: 75vh;
  width: 75vw;
  background: black;
  color: white;
  border-radius: 5px;
}

.music_player__album-art {
  height: 50vh;
  width: 100%;
  background-size: cover;
}
</style>
