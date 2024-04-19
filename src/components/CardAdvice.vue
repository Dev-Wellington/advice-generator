<script setup>
import "../assets/global.css";
import { ref, onMounted, onUnmounted, watchEffect } from "vue";
const adviceNumber = ref("");
const adviceContent = ref("");
const imgSrc = ref("");
const windowWidth = ref(window.innerWidth);

const btnRequest = async () => {
  const r = await fetch("https://api.adviceslip.com/advice");
  const d = await r.json();
  adviceNumber.value = d.slip.id;
  adviceContent.value = d.slip.advice;
};
</script>

<template>
  <div class="card">
    <h1>ADVICE #{{ adviceNumber }}</h1>
    <p>"{{ adviceContent }}"</p>
    <picture>
      <source
        srcset="../assets/images/pattern-divider-mobile.svg"
        media="(max-width: 768px)"
      />

      <source
        srcset="../assets/images/pattern-divider-desktop.svg"
        media="(min-width: 769px)"
      />

      <img src="../assets/images/pattern-divider.svg" alt="Pattern divider" />
    </picture>
    <div>
      <button @click="btnRequest()">
        <img src="../assets/images/icon-dice.svg" alt="" />
      </button>
    </div>
  </div>
</template>

<style scoped>
h1 {
  font-size: 14px;
  color: var(--neon-green);
  font-weight: 400;
  letter-spacing: 4px;
}
p {
  color: var(--light-cyan);
  font-size: var(--quote-size);
  word-wrap: wrap;
  text-align: center;
}
.card {
  padding: 50px 25px 0 25px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-between;
  background-color: var(--dark-grayish-blue);
  border-radius: 25px;
  gap: 25px;
  font-family: var(--font-family);
  max-width: 530px;
  max-height: 345px;
  box-shadow: 10px 10px 15px 0px rgba(0,0,0,0.3)
}

button {
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: var(--neon-green);
  border: none;
  border-radius: 50%;
  width: 75px;
  height: 75px;
  cursor: pointer;
}
button {
  position: relative;
  z-index: 2;
  top: 25px;
}
@media (max-width: 426px) {
  .card {
    padding: 25px 25px 0 25px;
    max-width: 90%;
    max-height: 345px;
  }
  button{
    top:10px;
  }
}
@media (max-width:321px){
    .card{
        height: 50%;
    }
   h1{
    font-size: 12px;
   }
   p{
    font-size: 28px;
   }
    button{
        position: relative;
       top: 15px;
    }
   
}
</style>
