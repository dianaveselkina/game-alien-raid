<template>
  <div class="game__wrapper">
    <AlienDiv @click="removeAlienDiv()" v-if="alienVisibility"></AlienDiv>
    <RulesDiv v-if="!divVisibility"></RulesDiv>
    <Button
      v-if="!btnVisibility"
      @click="removeRules(), deleteBtn(), emersionAlien()"
    ></Button>
    <MonsterDiv></MonsterDiv>
  </div>
</template>
<script>
import Button from '@/components/Button.vue';
import AlienDiv from '@/components/AlienDiv.vue';
import RulesDiv from '@/components/RulesDiv.vue';
import MonsterDiv from '@/components/MonsterDiv.vue';
export default {
  components: {
    Button,
    RulesDiv,
    AlienDiv,
    // MonsterDiv,
  },
  data() {
    return {
      divVisibility: false,
      btnVisibility: false,
      alienVisibility: false,
    };
  },
  methods: {
    removeRules() {
      this.divVisibility = true;
    },
    deleteBtn() {
      this.btnVisibility = true;
    },
    emersionAlien() {
      this.alienVisibility = true;
    },
    removeAlienDiv() {
      this.alienVisibility = false;
    },
  },
};
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
