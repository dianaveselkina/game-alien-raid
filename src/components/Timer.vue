<template>
  <div class="timer">
    <div>{{ counter }}</div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      counter: 10,
    };
  },
  methods: {
    countDown() {
      if (this.counter) {
        return setTimeout(() => {
          --this.counter;
          this.countDown();
        }, 1000);
      }

      // this.counter = 'Время вышло... Ты провалил миссию!';
    },
  },
  mounted() {
    this.countDown();
  },
};
</script>
<style>
.timer {
  z-index: 4;
  display: inline-block;
  text-align: center;
  margin-top: 40px;
  width: 346px;
  height: 100px;
  font-size: 52px;
  color: #664017;
}
</style>
