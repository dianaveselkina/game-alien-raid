<template>
  <div class="timer">
    <div id="timer">{{ counter }}</div>
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

      // this.counter = 'Время вышло...';
    },
  },
  mounted() {
    this.countDown();
  },
};
</script>
<style>
.timer {
  width: 100px;
  height: 100px;
  font-size: 52px;
  color: rgb(181, 182, 33);
}
</style>
