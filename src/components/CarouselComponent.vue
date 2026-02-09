<script setup>
import { onMounted, ref } from 'vue'

const load = ref(false)
const currentIndex = ref(0)

const images = [
  'transition-image/image-1.jpeg',
  'transition-image/image-2.jpeg',
  'transition-image/image-3.jpeg',
  'transition-image/image-4.jpeg',
  'transition-image/image-5.jpeg',
  'transition-image/image-6.jpeg',
  'transition-image/image-7.jpeg',
  'transition-image/image-8.jpeg',
]

onMounted(() => {
  setTimeout(() => {
    load.value = true

    setInterval(() => {
      currentIndex.value =
        (currentIndex.value + 1) % images.length
    }, 3000) // change image every 3s
  }, 3000) // initial delay
})
</script>
<template>
    <div v-if="load" class="carousel-main">
      <transition name="fade" mode="out-in" appear="">
        <img
          :key="currentIndex"
          :src="images[currentIndex]"
          class="carousel-img"
          alt="carousel image"
        />
      </transition>
    </div>
  </template>
  

<style>

.carousel-main {    
  position: absolute;
  width: 300px;
  height: 400px;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}

.carousel-img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  border-radius: 12px;
  border: 8px solid #ff4d6d; /* Pinkish red */
    border-radius: 20px;       /* Rounded corners for a soft look */
    padding: 5px;              /* Space between image and border */
    box-shadow: 0 0 15px rgba(255, 77, 109, 0.6); /* Soft pink glow */
}

/* Fade animation */
.fade-enter-active,
.fade-leave-active {
  transition: opacity 1s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}

</style>