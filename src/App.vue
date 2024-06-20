<script setup>
import { ref, onMounted } from "vue";
import ChildComp from "./components/ChildComp.vue";
import JSConfetti from 'js-confetti'

const confetti = new JSConfetti()

function showConfetti() {
  confetti.addConfetti()
}

const pElem = ref(null);
const changedText = ref("");
const res = ref("No response yet");

const changeText = () => {
  pElem.value.textContent = changedText.value;
  changedText.value = " ";
};

onMounted(() => {
  pElem.value.style.color = "red";
  pElem.value.style.fontSize = "50px";
});
</script>

<template>
  <center>
    <p ref="pElem">Hello World</p>
    <input type="text" v-model="changedText" />
    <button @click="changeText">Change Text</button>
    <ChildComp :msg="changedText" @response="(msg) => (res = msg)">
      <p>Respone from parent to child</p>
    </ChildComp>
    <p>Response: {{ res }}</p>
    <button @click="showConfetti">Show Confetti</button>
  </center>
</template>
