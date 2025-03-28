<script setup>
import { ref } from "vue";

const nomeInput = ref("");
const cognomeInput = ref("");
const msgErrorText = ref("");
const showLogin = ref(true);

const emit = defineEmits(["loginSubmitted"]);

const onSubmit = () => {
  if (nomeInput.value === "" || cognomeInput.value === "") {
    return (msgErrorText.value = "Entrambi i campi devono essere compilati.");
  }

  const loginData = {
    nome: nomeInput.value,
    cognome: cognomeInput.value,
  };

  emit("loginSubmitted", loginData);

  showLogin.value = false;
};
</script>

<template>
  <div v-if="showLogin" class="container">
    <div class="login-container">
      <p class="welcome-txt">BENVENUTO</p>
      <p class="login-details-txt">
        Per favore, inserisci i tuoi dati di accesso
      </p>
      <input
        v-model.trim="nomeInput"
        id="nomeInput"
        type="text"
        placeholder="Nome..."
      />
      <input
        v-model.trim="cognomeInput"
        id="cognomeInput"
        type="text"
        placeholder="Cognome..."
      />
      <button @click="onSubmit">Login</button>
      <p class="msg-error">{{ msgErrorText }}</p>
    </div>
  </div>
</template>

<style scoped>
.container {
  width: 100%;
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  background: whitesmoke;
  position: fixed;
  top: 0;
  left: 0;
  z-index: 10;
}

.login-container {
  width: 350px;
  height: 300px;
  border-radius: 5px;
  align-items: center;
  justify-content: center;
  padding: 20px;
  display: flex;
  flex-direction: column;
  background: white;
  box-shadow: 5px 5px 12px #8f8f8f, -5px -5px 12px #ffffff;
}

input {
  padding: 10px;
  margin-bottom: 10px;
  width: 280px;
  border: none;
  background: #eae7e7;
  outline-color: rgb(179, 179, 175);
}

.welcome-txt {
  margin-bottom: 10px;
  font-weight: bold;
}

.login-details-txt {
  margin-bottom: 30px;
  font-size: 14px;
}

button {
  width: 280px;
  padding: 10px;
  border: none;
  background: linear-gradient(
    167deg,
    rgba(2, 0, 36, 1) 0%,
    rgba(9, 9, 121, 1) 47%,
    rgba(0, 0, 0, 1) 100%
  );
  color: white;
  cursor: pointer;
  background-size: 200% 200%;
  transition: background-position 0.5s ease-in-out, transform 0.3s ease,
    box-shadow 0.3s ease;
}

button:hover {
  background-position: 100% 100%;
  transform: translateY(-1px);
  box-shadow: 0 8px 20px rgba(0, 0, 0, 0.6);
}

.msg-error {
  color: red;
  font-size: 13px;
  margin-top: 10px;
}
</style>
