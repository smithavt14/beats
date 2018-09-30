<template>
  <view class="home__wrapper">
    <view class="home__title">
      <text>Shanghai Beats</text>
    </view>
    <view class="home__enter-btn" hover-class="home__active-btn" @tap="navigateToBeats">
      <text>Enter</text>
    </view>
  </view>
</template>

<script>

export default {

  data() {
    return {
      name: 'Alex',
      userInfo: {
        name: 'Alex',
        height: '180 meters',
      },
    };
  },

  components: {},

  methods: {
    navigateToBeats() {
      wx.navigateTo({
        url: '../beats/main',
      });
      console.log('Hello there.');
    },
  },

};

</script>

<style>
.home__wrapper {
  background-image: url('https://images.pexels.com/photos/894156/pexels-photo-894156.jpeg?auto=compress&cs=tinysrgb&dpr=2&h=650&w=940');
  background-size: cover;
  height: 100vh;
  width: 100vw;
  align-items: center;
  display: flex;
  flex-direction: column;
}

.home__title {
  color: white;
  font-size: 40px;
  padding-top: 50px;
  text-shadow: 1px 1px 1px gray;
}

.home__enter-btn {
  color: #808080;
  font-size: 30px;
  text-shadow: 1px 1px 1px gray;
  width: 200rpx;
  width:200rpx;
  margin-top:40px;
  text-align: center;
}

.home__active-btn {
  color: white;
}

</style>
