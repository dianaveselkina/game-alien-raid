<template>
  <div class="game__wrapper">
    <Button></Button>
  </div>
</template>
<script>
import Button from '@/components/Button.vue';
export default {
  components: {
    Button,
  },
};
</script>
<style>
.game__wrapper {
  max-width: 900px;
  height: 900px;
  margin: 2rem auto;
  background-color: coral;
  border-radius: 15px;
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
