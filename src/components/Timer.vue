<template>
  <div class="timer">
    <p>{{ counter }}</p>
  </div>
</template>
<script>
export default {
  data() {
    return {
      counter: 60,
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
      //   this.$router.push({ path: '/2'})
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
