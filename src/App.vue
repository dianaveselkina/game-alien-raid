<template>
  <div class="game__wrapper">
    <div v-if="timerVisibility" class="timer">
      <div><span v-if="spanVisibility">0:</span>{{ counter }}</div>
    </div>
    <div v-if="alienVisibility">
      <div
        class="alien"
        v-for="(alien, i) in aliens"
        :style="{
          top: top + 'px',
          right: right + 'px',
          opacity: opacity,
          rotate: rotate + 'deg',
          scale: scale,
        }"
        :key="alien.id"
        @click="
          (count += 1),
            aliens.splice(i, 1),
            getRandomTop(),
            getRandomRight(),
            getOpacity(),
            getRotate(),
            getScale()
        "
      ></div>
    </div>
    <RulesDiv v-if="!divVisibility"></RulesDiv>
    <transition name="btn">
      <MyButton
        class="game__start"
        v-if="!btnVisibility"
        @click="countDown(), removeRules(), deleteBtn(), addTimer(), addAlien()"
        >Начать игру</MyButton
      >
    </transition>

    <div>
      <CupDiv v-if="cupVisibility"></CupDiv>
    </div>
    <div>
      <transition name="monster">
        <MonsterDiv v-if="monsterVisibility"></MonsterDiv
      ></transition>
    </div>
    <MyButton
      class="game__restart"
      v-show="btnRestartVisibility"
      @click="
        methodRefreshPage();
        deleteBtnRestart();
      "
      >Попробовать еще раз</MyButton
    >
  </div>
</template>
<script>
import MyButton from '@/components/MyButton.vue';
import RulesDiv from '@/components/RulesDiv.vue';
import MonsterDiv from '@/components/MonsterDiv.vue';
import CupDiv from '@/components/CupDiv.vue';

export default {
  components: {
    MyButton,
    RulesDiv,
    MonsterDiv,
    CupDiv,
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
        { id: 8 },
        { id: 9 },
        { id: 10 },
        { id: 11 },
        { id: 12 },
      ],
      scale: 1,
      rotate: 0,
      top: 450,
      right: 413,
      count: 0,
      counter: 10,
      divVisibility: false,
      btnVisibility: false,
      timerVisibility: false,
      monsterVisibility: false,
      spanVisibility: true,
      cupVisibility: false,
      btnRestartVisibility: false,
      alienVisibility: false,
    };
  },
  methods: {
    getRandomTop() {
      this.top = Math.round(Math.random() * (800 - 150) + 150);
    },
    getRandomRight() {
      this.right = Math.round(Math.random() * (800 - 100) + 100);
    },
    getOpacity() {
      this.opacity = Math.random().toFixed(2);
    },
    getRotate() {
      this.rotate = Math.random().toFixed(2) * 100;
    },
    getScale() {
      this.scale = Math.round(Math.random() * (100 - 60) + 60) * 0.01;
    },
    removeRules() {
      this.divVisibility = true;
    },
    deleteBtn() {
      this.btnVisibility = true;
    },
    deleteBtnRestart() {
      this.btnRestartVisibility = false;
    },
    addTimer() {
      this.timerVisibility = true;
    },
    addAlien() {
      this.alienVisibility = true;
    },

    methodRefreshPage() {
      location.reload();
    },
    countDown() {
      if (this.counter) {
        return setTimeout(() => {
          --this.counter;
          this.countDown();
        }, 1000);
      }
      this.spanVisibility = false;
      setTimeout(() => {
        this.btnRestartVisibility = true;
      }, '1500');
      this.alienVisibility = false;
      this.count > 11
        ? (this.monsterVisibility = false)
        : (this.monsterVisibility = true);
      this.count > 11
        ? (this.cupVisibility = true)
        : (this.cupVisibility = false);
      this.count > 11
        ? (this.counter = 'Ты герой! Ты спас планету!')
        : (this.counter = 'Время вышло... Ты провалил миссию!');
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
  width: 75px;
  height: 99px;
}

.game__restart {
  margin-top: 4rem;
  padding: 1rem;
  border-radius: 1rem;
  cursor: pointer;
  background-color: rgba(181, 182, 33, 0.7);
  border: 4px solid #413e15;
  font-size: 3rem;
  color: #664017;
}
.game__restart:hover {
  box-shadow: 0 0 14px 14px rgba(65, 62, 21, 1.6);
}
.monster-enter-active {
  transition: all 1s ease-out;
}

.monster-enter-to {
  transform: scale(8);
  opacity: 1;
}
.btn-leave-active {
  transition: all 1s;
}
.btn-leave-to {
  transform: translateY(-250px);
  opacity: 0;
}
</style>
