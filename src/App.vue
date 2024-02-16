<template>
  <div class="game__wrapper">
    <div v-if="timerVisibility" class="timer">
      <div>{{ counter }}</div>
    </div>
    <!-- <Timer v-if="timerVisibility"></Timer> -->
    <AlienDiv
      @click="removeAlienDiv(), addAlienTwoDiv(), addAlienThreeDiv()"
      v-if="alienVisibility"
    ></AlienDiv>
    <AlienTwoDiv
      @click="removeAlienTwoDiv()"
      v-if="alienTwoVisibility"
    ></AlienTwoDiv>
    <AlienThreeDiv
      @click="removeAlienThreeDiv()"
      v-if="alienThreeVisibility"
    ></AlienThreeDiv>
    <RulesDiv v-if="!divVisibility"></RulesDiv>
    <Button
      v-if="!btnVisibility"
      @click="removeRules(), deleteBtn(), emersionAlien(), addTimer()"
    ></Button>

    <MonsterDiv v-if="monsterVisibility"></MonsterDiv>
  </div>
</template>
<script>
import Button from '@/components/Button.vue';
import AlienDiv from '@/components/AlienDiv.vue';
import RulesDiv from '@/components/RulesDiv.vue';
import AlienTwoDiv from '@/components/AlienTwoDiv.vue';
import MonsterDiv from '@/components/MonsterDiv.vue';
import AlienThreeDiv from '@/components/AlienThreeDiv.vue';
export default {
  components: {
    Button,
    RulesDiv,
    AlienDiv,
    AlienTwoDiv,
    AlienThreeDiv,
    MonsterDiv,
  },

  data() {
    return {
      counter: 10,
      divVisibility: false,
      btnVisibility: false,
      alienVisibility: false,
      alienTwoVisibility: false,
      alienThreeVisibility: false,
      timerVisibility: false,
      monsterVisibility: false,
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
    addAlienTwoDiv() {
      this.alienTwoVisibility = true;
    },
    removeAlienTwoDiv() {
      this.alienTwoVisibility = false;
    },
    addAlienThreeDiv() {
      this.alienThreeVisibility = true;
    },
    removeAlienThreeDiv() {
      this.alienThreeVisibility = false;
    },
    addTimer() {
      this.timerVisibility = true;
    },

    countDown() {
      if (this.counter) {
        return setTimeout(() => {
          --this.counter;
          this.countDown();
        }, 1000);
      }
      this.monsterVisibility = true;
      this.counter = 'Время вышло... Ты провалил миссию!';
    },
  },

  mounted() {
    this.countDown();
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
.timer {
  z-index: 4;
  display: inline-block;
  text-align: center;
  margin-top: 40px;
  width: 700px;
  height: 100px;
  font-size: 52px;
  color: #664017;
}
</style>
