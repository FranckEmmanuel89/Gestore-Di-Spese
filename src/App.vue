<script setup>
import { ref, computed } from "vue";
import Login from "./components/Login.vue";
import HeaderApp from "./components/HeaderApp.vue";
import Balance from "./components/Balance.vue";
import IncomeExpenses from "./components/IncomeExpenses.vue";
import History from "./components/History.vue";
import NewTransaction from "./components/NewTransaction.vue";
import { useToast } from "vue-toastification";

const toast = useToast();

const transazioni = ref([]);

const total = computed(() => {
  return transazioni.value.reduce((acc, transazione) => {
    return acc + transazione.prezzo;
  }, 0);
});

const entrate = computed(() => {
  return transazioni.value
    .filter((transazione) => transazione.prezzo > 0)
    .reduce((acc, transazione) => {
      return acc + transazione.prezzo;
    }, 0)
    .toFixed(2);
});

const uscite = computed(() => {
  return transazioni.value
    .filter((transazione) => transazione.prezzo < 0)
    .reduce((acc, transazione) => {
      return acc + transazione.prezzo;
    }, 0)
    .toFixed(2);
});

const handletransactionDeleted = (id) => {
  transazioni.value = transazioni.value.filter(
    (transazione) => transazione.id !== id
  );
  toast.success("Operazione cancellata");
};

const handleEntrateSubmitted = (entrateData) => {
  transazioni.value.push({
    id: entrateData.id,
    text: entrateData.text,
    prezzo: entrateData.prezzo,
    date: entrateData.date,
  });

  toast.success("Entrata aggiunta");
};

const handleUscitesubnitted = (usciteData) => {
  transazioni.value.push({
    id: usciteData.id,
    text: usciteData.text,
    prezzo: usciteData.prezzo,
    date: usciteData.date,
  });

  toast.success("Uscita aggiunta");
};

const utente = ref({});

const handleLoginSubmitted = (loginData) => {
  utente.value = {
    nome: loginData.nome,
    cognome: loginData.cognome,
  };
};


</script>

<template>
  <div class="container">
    <div class="container-data">
      <div class="header-balance-container">
        <HeaderApp :utente="utente" />
        <Balance :total="+total" />
      </div>
      <IncomeExpenses :entrate="+entrate" :uscite="+uscite" />
      <History :transazioni="transazioni" @transazioneDeleted="handletransactionDeleted"/>
      <new-transaction @entrateSubmitted="handleEntrateSubmitted" @uscitesubmitted="handleUscitesubnitted"/>
      <Login @loginSubmitted="handleLoginSubmitted" />
    </div>
  </div>
</template>

<style scoped>
.container {
  display: flex;
  align-items: center;
  padding: 10px;
  justify-content: center;
  width: 100%;
  background: whitesmoke;
  margin-bottom: 20px;
}

.container-data {
  width: 800px;
}

.header-balance-container {
  margin-left: 20px;
  margin-right: 20px;
  margin-top: 10px;
  margin-bottom: 50px;
  max-width: 770px;
  border-radius: 10px;
  background: rgb(2, 0, 36);
  background: linear-gradient(
    167deg,
    rgba(2, 0, 36, 1) 0%,
    rgba(9, 9, 121, 1) 47%,
    rgba(0, 0, 0, 1) 100%
  );
}
</style>
