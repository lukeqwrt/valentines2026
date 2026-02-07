<script setup>
import { ref } from 'vue'

const message = ref('')
const showFlowers = ref(false)
const yes = ref(false)

const noStyle = ref({
  transform: 'translate(0, 0)'
})

const flowerTypes = ['🌹', '🌷', '🌸', '💐', '🌺']
const flowers = Array.from({ length: 50 })

const sayYes = () => {
  showFlowers.value = true
  yes.value = true
  message.value = `
💖 Yay!! 💖
Thank you for being my Valentine 🥰
I can’t wait to spend this special day with you 🌹
  `
}
let escaping = false

const moveNo = (event) => {
  if (escaping) return
  escaping = true

  const button = event.target
  const rect = button.getBoundingClientRect()

  const mouseX = event.clientX
  const mouseY = event.clientY

  const buttonX = rect.left + rect.width / 2
  const buttonY = rect.top + rect.height / 2

  const diffX = buttonX - mouseX
  const diffY = buttonY - mouseY

  const distance = 180
  const angle = Math.atan2(diffY, diffX)

  const x = Math.cos(angle) * distance
  const y = Math.sin(angle) * distance

  noStyle.value = {
    transform: `translate(${x}px, ${y}px)`
  }

  setTimeout(() => {
    escaping = false
  }, 300)
}


</script>

<template>
  <div class="wrapper">
    <div v-if="showFlowers" class="flower-container">
      <span
        v-for="(f, i) in flowers"
        :key="i"
        class="flower"
        :style="{
          left: Math.random() * 100 + '%',
          animationDelay: Math.random() * 2 + 's',
          animationDuration: 4 + Math.random() * 4 + 's'
        }"
      >
        {{ flowerTypes[Math.floor(Math.random() * flowerTypes.length)] }}
      </span>
    </div>

    <div v-if="!yes" class="card">
      <h1>💌 Hey my Aira</h1>

      <p class="question">
        I was wondering…<br />
        <strong>Will you be my Valentine? 💖</strong>
      </p>

      <div class="buttons">
        <button class="yes" @click="sayYes">Yes 💕</button>
        <button
          class="no"
          :style="noStyle"
          @mousemove="moveNo"
        >
          No 🙈
        </button>

      </div>

      <p v-if="message" class="message">
        {{ message }}
      </p>
    </div>
    <div v-else>
      <img src="/public/dudu-bubu-dancing-so-cute.gif" alt="">
    </div>
  </div>
</template>

<style>

*,html,body{
  padding: 0;
  margin: 0;
}
.wrapper {
  height: 100vh;
  background: linear-gradient(135deg, #ffafbd, #ffc3a0);
  display: flex;
  justify-content: center;
  align-items: center;
  font-family: 'Poppins', sans-serif;
  overflow: hidden;
  padding: 20px;
}

.flower-container {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  pointer-events: none;
  z-index: 1;
}

.flower {
  position: absolute;
  top: -50px;
  font-size: 30px;
  animation-name: fall;
  animation-timing-function: linear;
  animation-iteration-count: infinite;
}

@keyframes fall {
  to {
    transform: translateY(110vh) rotate(360deg);
  }
}

.card {
  background: white;
  padding: 35px 25px;
  border-radius: 25px;
  text-align: center;
  width: 90%;
  max-width: 400px;
  box-shadow: 0 15px 30px rgba(0, 0, 0, 0.2);
  z-index: 2;
  animation: pop 0.6s ease;
}

@keyframes pop {
  from {
    transform: scale(0.8);
    opacity: 0;
  }
  to {
    transform: scale(1);
    opacity: 1;
  }
}

h1 {
  color: #ff4d6d;
}

.question {
  font-size: 18px;
  color: #555;
  margin-top: 10px;
}

.buttons {
  margin-top: 25px;
}

button {
  padding: 12px 26px;
  font-size: 16px;
  border: none;
  border-radius: 30px;
  cursor: pointer;
  margin: 10px;
  transition: 0.3s ease;
}

.yes {
  background-color: #ff4d6d;
  color: white;
}

.yes:hover {
  transform: scale(1.1);
}

.no {
  background-color: #eee;
  position: relative;
}

.message {
  margin-top: 25px;
  font-size: 18px;
  color: #ff4d6d;
  font-weight: 600;
  white-space: pre-line;
}
</style>
