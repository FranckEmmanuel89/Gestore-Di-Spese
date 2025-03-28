<script setup>
const props = defineProps({
  utente: {
    type: Object,
    required: true,
  },
});
</script>

<template>
  <div class="header">
    <div class="benvenuto-txt">
      <span>Benvenuto !</span>
    </div>
    <div class="nome-container">
      <span>{{ utente.nome }}</span>
      <span>{{ utente.cognome }}</span>
    </div>
  </div>
</template>

<style scoped>
.header {
  display: flex;
  align-items: center;
  max-width: 780px;
  padding: 30px 20px 10px 20px;
  height: 70px;
  /* background: rgb(165, 110, 233);; */
  border-top-right-radius: 10px;
  border-top-left-radius: 10px;
  margin-top: 20px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  color: white;
}

.benvenuto-txt {
  font-size: 22px;
  color: rgb(248, 237, 215);
}

.nome-container {
  display: flex;
  flex-direction: column;
  text-align: end;
  gap: 5px;
  font-size: 20px;
  color: rgb(248, 237, 215);
}

@media screen and (max-width: 576px) {
  .benvenuto-txt {
    font-size: 19px;
  }
  .nome-container {
    font-size: 15px;
  }
}
</style>
