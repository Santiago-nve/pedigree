<template>
  <div v-if="started" class="screensaver" :style="{ backgroundColor: backgroundColor }">
    <img :src="logo"
      :style="{ transform: `translate(${x}px, ${y}px)`, filter: `hue-rotate(${logoRotateColor}deg)`, width: `${width}px`, height: `${height}px` }">
  </div>
</template>

<script>
export default {
  data() {
    return {
      x: 0,
      y: 0,
      velocity: 0.5,
      width: 200,
      height: 100,
      backgroundColor: '#000',
      logoRotateColor: 0,
      started: false,
      logo: require('../../assets/DVD_logo.svg'),
      signX: 1,
      signY: 1
    };
  },
  mounted() {
    this.startScreenSaverTimeout();
  },
  methods: {
    startLogo(time) {
      let prevX = this.x;
      let prevY = this.y;
      this.x = Math.abs(window.innerWidth - this.width - (time * this.velocity) % (2 * (window.innerWidth - this.width)));
      this.y = Math.abs(window.innerHeight - this.height - (time * this.velocity) % (2 * (window.innerHeight - this.height)));
      if (Math.sign(prevX - this.x) != this.signX || Math.sign(prevY - this.y) != this.signY) {
        this.updateColor();
      }
      this.signX = Math.sign(prevX - this.x);
      this.signY = Math.sign(prevY - this.y);
      if (this.started) {
        requestAnimationFrame(this.startLogo);
      }
    },
    updateColor() {
      this.backgroundColor = this.generateRandomColor();
      this.logoRotateColor = Math.floor(Math.random() * 360);
    },
    generateRandomColor() {
      return '#' + Math.floor(Math.random() * 16777215).toString(16);
    },
    startScreenSaverTimeout() {
      let timer;
      window.addEventListener('mousemove', () => {
        clearTimeout(timer);
        this.started = false;
        timer = setTimeout(() => {
          this.started = true;
          this.startLogo();
        }, 60000);
      });
    }
  }
};
</script>

<style scoped lang="less">
.screensaver {
  position: absolute;
  width: 100%;
  height: 100%;
  top: 0;
  left: 0;
  overflow: hidden;
}
</style>
