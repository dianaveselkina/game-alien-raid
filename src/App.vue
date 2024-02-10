<template>
  <div class="game__wrapper">
    <AlienDiv></AlienDiv>
    <RulesDiv></RulesDiv>
    <Button></Button>
  </div>
</template>
<script>
import Button from '@/components/Button.vue';
import AlienDiv from '@/components/AlienDiv.vue';
import RulesDiv from '@/components/RulesDiv.vue';
export default {
  components: {
    Button,
    RulesDiv,
  },
};
// function decreaseTime() {
//   if (time === 0) {
//     finishGame();
//   } else {
//     let current = --time;
//     if (current < 10) {
//       current = `0${current}`;
//     }
//     setTime(current);
//   }
// }
</script>
<style>
.game__wrapper {
  max-width: 900px;
  height: 900px;
  margin: 2rem auto;
  background-image: url(./img/scenery.png);
  background-repeat: no-repeat;
  background-size: cover;
  border-radius: 3rem;
  display: flex;
  flex-direction: column;
  justify-content: flex-start;

  align-items: center;
}
</style>
