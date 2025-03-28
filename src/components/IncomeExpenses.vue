<script setup>
const props = defineProps({
  entrate: {
    type: Number,
    required: true,
  },

  uscite: {
    type: Number,
    required: true,
  },
});
</script>

<template>
  <div class="container-entrate-uscite">
    <div class="entrate-container">
      <span>ENTRATE</span>
      <transition mode="out-in">
        <span :key="entrate" class="entrate">+{{ entrate }} €</span>
      </transition>
    </div>
    <div class="uscite-container">
      <span>USCITE</span>
      <transition mode="out-in">
        <span :key="uscite" class="uscite">{{ uscite }} €</span>
      </transition>
    </div>
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

.container-entrate-uscite {
  display: flex;
  margin-left: 20px;
  margin-right: 20px;
  margin-bottom: 10px;
  border-radius: 10px;
  align-items: center;
  justify-content: center;
  height: 70px;
  max-width: 780px;
  background: #ececec;
  box-shadow: 5px 5px 26px #d3d3d3, -5px -5px 26px #ededed;
}

.entrate-container,
.uscite-container {
  display: flex;
  font-weight: 600;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  border-collapse: collapse;
  width: 180px;
  height: 60px;
  transition: background-color 0.3s ease-in-out, transform 0.3s ease-in-out;
}

.entrate-container {
  border-right: 1px solid rgb(148, 147, 147);
  background: #d3d2d253;
  border-top-left-radius: 10px;
  border-bottom-left-radius: 10px;
}

.entrate-container:hover,
.uscite-container:hover {
  background-color: white;
}

.uscite-container {
  border-left: 1px solid rgb(148, 147, 147);
  background: #d3d2d253;
  border-top-right-radius: 10px;
  border-bottom-right-radius: 10px;
}

.entrate {
  color: green;
  margin-top: 5px;
}
.uscite {
  color: red;
  margin-top: 5px;
}
</style>
