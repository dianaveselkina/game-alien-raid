<template>
  <div class="game__wrapper">
    <div v-if="timerVisibility" class="timer">
      <div><span v-if="spanVisibility">0:</span>{{ counter }}</div>
    </div>

    <div v-if="alienFiveVisibility">
      <div
        class="alien"
        v-for="alien in aliens"
        :class="`alien-${alien.id}`"
        :key="alien.id"
        @click="removeAlienFiveDiv(alien)"
      ></div>
    </div>
    <AlienDiv
      @click="removeAlienDiv(), addAlienTwoDiv(), addAlienThreeDiv()"
      v-if="alienVisibility"
    ></AlienDiv>
    <AlienTwoDiv
      @click="removeAlienTwoDiv()"
      v-if="alienTwoVisibility"
    ></AlienTwoDiv>
    <AlienThreeDiv
      @click="removeAlienThreeDiv(), addAlienFiveDiv()"
      v-if="alienThreeVisibility"
    ></AlienThreeDiv>
    <RulesDiv v-if="!divVisibility"></RulesDiv>
    <Button
      v-if="!btnVisibility"
      @click="
        countDown(), removeRules(), deleteBtn(), emersionAlien(), addTimer()
      "
    ></Button>
    <div>
      <transition name="monster">
        <MonsterDiv v-if="monsterVisibility"></MonsterDiv
      ></transition>
    </div>
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
      aliens: [
        { id: 1 },
        { id: 2 },
        { id: 3 },
        { id: 4 },
        { id: 5 },
        { id: 6 },
        { id: 7 },
      ],
      counter: 9,
      divVisibility: false,
      btnVisibility: false,
      alienVisibility: false,
      alienTwoVisibility: false,
      alienThreeVisibility: false,
      alienFiveVisibility: false,
      timerVisibility: false,
      monsterVisibility: false,
      spanVisibility: true,
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
    addAlienFiveDiv() {
      this.alienFiveVisibility = true;
    },
    removeAlienFiveDiv(alien) {
      this.aliens = this.aliens.filter((a) => a.id !== alien.id);
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
      this.spanVisibility = false;
      this.alienFiveVisibility = false;
      this.alienVisibility = false;
      this.alienTwoVisibility = false;
      this.alienThreeVisibility = false;
      this.monsterVisibility = true;
      this.counter = 'Время вышло... Ты провалил миссию!';
    },
  },
};
</script>
<style>
.game__wrapper {
  position: relative;
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
.alien {
  position: absolute;
  cursor: pointer;
  background-image: url(./img/alien.png);
  background-repeat: no-repeat;
  background-size: cover;
  width: 50px;
  height: 66px;
}
.alien-1 {
  top: 300px;
  right: 600px;
  transform: rotate(-125deg);
  opacity: 0.33;
}
.alien-2 {
  top: 800px;
  right: 800px;
  transform: rotate(121deg);
  opacity: 0.3;
}
.alien-3 {
  top: 450px;
  right: 300px;
  transform: rotate(-170deg);
  opacity: 0.25;
}
.alien-4 {
  top: 650px;
  right: 200px;
  transform: rotate(-25deg);
  opacity: 0.2;
}
.alien-5 {
  top: 250px;
  right: 400px;
  transform: rotate(65deg);
  opacity: 0.15;
}
.alien-6 {
  top: 175px;
  right: 840px;
  transform: rotate(65deg);
  opacity: 0.45;
}
.alien-7 {
  top: 290px;
  right: 100px;
  transform: rotate(65deg);
  opacity: 0.65;
}
.monster-enter-active {
  transition: all 3s ease-out;
}

.monster-enter-to {
  transform: scale(4);
  opacity: 1;
}
</style>
