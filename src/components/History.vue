<script setup>
const props = defineProps({
  transazioni: {
    type: Array,
    required: true,
  },
});

const emit = defineEmits(["transazioneDeleted"]);

const deleteTransazione = (id) => {
  emit("transazioneDeleted", id);
};
</script>

<template>
  <div class="container-storico">
    <div class="storico-txt-container">
      <p class="storico-txt">Storico dei movimenti</p>
      <hr />
    </div>
    <div class="movimenti">
      <TransitionGroup name="fade" tag="div">
        <div
          v-for="transazione in transazioni"
          :key="transazione.id"
          :class="transazione.prezzo > 0 ? 'plus' : 'minus'"
          class="contanier-movimento"
        >
          <button title="cancella" @click="deleteTransazione(transazione.id)">
            x
          </button>
          <p class="movimento-txt">{{ transazione.text }}</p>
          <p class="data">{{ transazione.date.toLocaleDateString("it-EU") }}</p>
          <p :class="transazione.prezzo > 0 ? 'plus-prezzo' : 'minus-prezzo'">
            {{ transazione.prezzo }} €
          </p>
        </div>
      </TransitionGroup>
    </div>
  </div>
</template>

<style scoped>
.fade-enter-from,
.fade-leave-to {
  opacity: 0;
  transform: translatex(-20px) scale(0.95);
}

.fade-enter-to,
.fade-leave-from {
  opacity: 1;
  transform: translatex(10px) scale(1);
}

.fade-enter-active,
.fade-leave-active {
  transition: all 0.4s ease-in-out;
}

.container-storico {
  margin-left: 20px;
  margin-right: 20px;
  margin-bottom: 10px;
  max-width: 780px;
  padding: 20px;
  background: #e2e2e2;
  border-radius: 10px;
}

.storico-txt-container {
  margin-bottom: 20px;
}

.storico-txt {
  margin-bottom: 5px;
  font-size: 17px;
  font-weight: bold;
}

hr {
  height: 2px;
  background: #d8d6d6;
}

.movimenti {
  display: flex;
  flex-direction: column;
  gap: 7px;
}

.contanier-movimento {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-bottom: 7px;
  padding: 18px;
  height: 40px;
  border-radius: 2px;
  background: white;
  box-shadow: 5px 5px 10px #8e8e8e, -5px -5px 10px #ffffff;
  transition: transform 0.3s ease;
}

.contanier-movimento:hover {
  transform: translateY(-2px);
}

.minus {
  border-right: 5px solid red;
}

.plus {
  border-right: 5px solid green;
}

.minus-prezzo {
  color: red;
  width: 190px;
  text-align: end;
}

.plus-prezzo {
  color: green;
  width: 190px;
  text-align: end;
}

button {
  position: absolute;
  border-radius: 2px;
  left: 10;
  margin-left: -28px;
  width: 18px;
  background: #000;
  color: white;
  cursor: pointer;
  border: none;
  opacity: 0;
  transition: opacity 0.5s ease-in-out, background-color 0.3s;
}

button:hover {
  background-color: red;
}

.contanier-movimento:hover button {
  opacity: 1;
}

.data {
  font-size: 12px;
  background: #d6fff3;
  border-radius: 5px;
  padding: 5px;
  width: 100px;
  text-align: center;
}

.movimento-txt {
  font-size: 14px;
  padding: 5px;
  width: 200px;
}

@media screen and (max-width: 576px) {
  .data {
    width: 70px;
  }

  .movimento-txt {
    width: 120px;
  }

  .minus-prezzo {
    width: 110px;
    font-size: 14px;
  }

  .plus-prezzo {
    width: 110px;
    font-size: 14px;
  }

  .contanier-movimento {
    padding-left: 5px;
    padding-right: 5px;
    height: 50px;
  }
}
</style>
