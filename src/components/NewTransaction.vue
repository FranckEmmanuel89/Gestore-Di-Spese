<script setup>
import { ref } from "vue";
import { useToast } from "vue-toastification";

const text = ref("");
const prezzo = ref();

const emit = defineEmits(["entrateSubmitted", "uscitesubmitted"]);

const toast = useToast();

const onSubmitEntrate = () => {
  if (!text.value || !prezzo.value) {
    toast.error("Compila entrambi i campi.");
    return;
  }
  const entrateData = {
    id: Math.floor(Math.random() * 1000000),
    text: text.value,
    date: new Date(),
    prezzo: parseFloat(prezzo.value),
  };
  emit("entrateSubmitted", entrateData);
  text.value = "";
  prezzo.value = "";
};

const onSubmitUscite = () => {
  if (!text.value || !prezzo.value) {
    toast.error("Compila entrambi i campi.");
    return;
  }
  const valeurNegative = -1 * Number(prezzo.value);

  const usciteData = {
    id: Math.floor(Math.random() * 1000000),
    text: text.value,
    date: new Date(),
    prezzo: parseFloat(valeurNegative),
  };
  emit("uscitesubmitted", usciteData);
  text.value = "";
  prezzo.value = "";

  text.value = "";
  prezzo.value = "";
};
</script>

<template>
  <div class="container-nuova-transazione">
    <div>
      <p class="container-transazione-txt">
        Aggiungi una nuova entrata / uscita
      </p>
    </div>
    <div>
      <form id="form" @submit.prevent>
        <div class="input-comun-container">
          <div class="input-text-container">
            <label for="text">Testo</label>
            <input
              v-model="text"
              type="text"
              name="text"
              id="text"
              placeholder="Entrata o uscita..."
            />
          </div>
          <div class="input-prezzo-container">
            <label for="prezzo"> Prezzo</label>
            <input
              v-model="prezzo"
              type="number"
              name="prezzo"
              id="prezzo"
              placeholder="Prezzo..."
            />
          </div>
        </div>
        <div class="btn-container">
          <button
            type="button"
            @click="onSubmitEntrate"
            class="aggiungi-entrata-btn"
          >
            Aggiungi Entrata
          </button>
          <button
            type="button"
            @click="onSubmitUscite"
            class="aggiungi-uscita-btn"
          >
            Aggiungi Uscita
          </button>
        </div>
      </form>
    </div>
  </div>
</template>

<style scoped>
.container-nuova-transazione {
  color: white;
  max-width: 780px;
  margin-left: 20px;
  margin-right: 20px;
  padding-left: 20px;
  padding-right: 20px;
  padding-top: 1px;
  border-radius: 10px;
  padding-bottom: 20px;
  background: linear-gradient(
    167deg,
    rgba(2, 0, 36, 1) 0%,
    rgba(9, 9, 121, 1) 47%,
    rgba(0, 0, 0, 1) 100%
  );
}
.input-comun-container {
  width: 100%;
  max-width: 730px;
  display: flex;
  gap: 10px;
  margin-bottom: 8px;
}

.input-text-container,
.input-prezzo-container {
  display: flex;
  align-items: center;
  justify-content: space-between;
  max-width: 780px;
  gap: 10px;
}

.container-transazione-txt {
  margin-top: 20px;
  margin-bottom: 10px;
  font-weight: bold;
  font-size: 17px;
}

.btn-container {
  width: 100%;
  max-width: 720px;
  display: flex;
  flex-direction: column;
  gap: 10px;
  margin: 0 auto;
}

form {
  max-width: 780px;
}

#text {
  width: 100%;
  padding: 8px;
  outline-color: wheat;
  margin-top: 5px;
  margin-bottom: 5px;
}

#prezzo {
  width: 100%;
  padding: 8px;
  outline-color: wheat;
  margin-top: 5px;
  margin-bottom: 5px;
}

.agguingi-container,
.input-comun-container div,
.btn-container button {
  width: 100%;
  padding-top: 10px;
  padding-bottom: 10px;
}

.aggiungi-entrata-btn {
  background: rgb(6, 67, 172);
  color: white;
  height: 35px;
  font-weight: bold;
  border: none;
  cursor: pointer;
  transition: background-color 0.3s ease, transform 0.3s ease;
}

.aggiungi-uscita-btn {
  background: whitesmoke;
  height: 35px;
  font-weight: bold;
  border: none;
  cursor: pointer;
  transition: background-color 0.3s ease, transform 0.3s ease;
}

.aggiungi-entrata-btn:hover {
  background-color: rgb(39, 103, 213);
  transform: translateY(-2px);
}

.aggiungi-uscita-btn:hover {
  background-color: rgb(194, 192, 192);
  transform: translateY(-2px);
}

@media (max-width: 768px) {
  .btn-container {
    max-width: 100%;
    align-items: center;
  }

  .input-comun-container {
    flex-direction: column;
    justify-content: end;
    margin-bottom: 10px;
  }

  .input-text-container,
  .input-prezzo-container {
    display: flex;
    flex-direction: column;
    align-items: start;
    justify-content: center;
    max-width: 100%;
    gap: 2px;
  }

  .input-prezzo-container {
    margin-top: -20px;
  }

  #prezzo,
  #text {
    width: 100%;
    border: 2px solid black;
  }
}
</style>
