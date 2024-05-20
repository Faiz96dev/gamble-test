<template>
  <div class="card-container">
    <div
      v-for="(card, index) in cards"
      :key="index"
      class="card-wrapper"
      :class="{ lifted: liftedCard === index }"
    >
      <div class="card" :class="{ flipped: flippedCard === index }">
        <div class="card-inner">
          <div class="card-front">Front</div>
          <div class="card-back">Back</div>
        </div>
      </div>
    </div>
  </div>
  <button @click="flipAndLiftCard">Flip Middle Card</button>
  <button @click="reset">Reset</button>
</template>

<script lang="ts" setup>
import { ref } from "vue";

const cards = ref([1, 2, 3]);
const flippedCard = ref<number | null>(null);
const liftedCard = ref<number | null>(null);

const reset = () => {
  cards.value = [1, 2, 3];
  flippedCard.value = null;
  liftedCard.value = null;
};
const flipAndLiftCard = () => {
  flippedCard.value = 1;
  setTimeout(() => {
    liftedCard.value = 1;
  }, 800);
};
</script>

<style scoped>
.card-container {
  display: flex;
  justify-content: center;
  align-items: flex-end;
  position: relative;
  height: 200px;
}

.card-wrapper {
  margin: 10px;
  border-radius: 5px;
  position: relative;
  transition: transform 0.8s ease-in-out;
}

.card {
  width: 100px;
  height: 150px;
  perspective: 1000px;
}

.card-inner {
  width: 100%;
  height: 100%;
  transform-style: preserve-3d;
  position: relative;
  transition: transform 0.8s ease-in-out;
}

.card.flipped .card-inner {
  transform: rotateY(180deg);
}

.card-wrapper.lifted {
  transform: translateY(-170px);
}

.card-front,
.card-back {
  width: 100%;
  height: 100%;
  position: absolute;
  border-radius: 2px;
  backface-visibility: hidden;
}

.card-front {
  background-color: #fff;
  color: black;
  display: flex;
  align-items: center;
  justify-content: center;
}

.card-back {
  background-color: #007bff;
  color: white;
  transform: rotateY(180deg);
  display: flex;
  align-items: center;
  justify-content: center;
}

button {
  margin: 20px;
}

@media (max-width: 600px) {
  .card {
    width: 80px;
    height: 120px;
  }

  button {
    font-size: 14px;
  }
}
</style>
