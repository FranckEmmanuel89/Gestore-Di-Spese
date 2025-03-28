<script setup>
import img from "../assets/img.png";

const props = defineProps({
  total: {
    type: Number,
    required: true,
  },
});
</script>

<template>
  <div class="balance-container">
    <div class="balance-container-data">
      <p class="saldo-txt">Il tuo saldo</p>
      <transition mode="out-in">
        <p :key="total" class="saldo">{{ total }} €</p>
      </transition>
    </div>
    <img :src="img" alt="img" />
  </div>
</template>

<style scoped>
.v-enter-active,
.v-leave-active {
  transition: opacity 0.3s ease;
}

.v-enter-from,
.v-leave-to {
  opacity: 0;
}

.balance-container {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

img {
  width: 40px;
  margin-right: 20px;
  transition: transform 1s ease-in-out;
}

img:hover {
  transform: rotate(360deg);
}

.balance-container-data {
  padding: 20px;
  max-width: 780px;
  height: 90px;
  border-bottom-right-radius: 10px;
  border-bottom-left-radius: 10px;
}

.saldo-txt {
  color: rgb(218, 214, 214);
  font-size: 20px;
}

.saldo {
  color: white;
  font-size: 25px;
}
</style>
