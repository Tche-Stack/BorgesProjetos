<script setup lang="ts">
import { ref, onMounted } from 'vue'
import { companyHighlights } from '../data/companyHighlights'

const currentSlide = ref(0)
const slideDirection = ref('right')

const changeSlide = (newIndex: number) => {
  slideDirection.value = newIndex > currentSlide.value ? 'right' : 'left'
  currentSlide.value = newIndex
}

onMounted(() => {
  setInterval(() => {
    slideDirection.value = 'right'
    currentSlide.value = (currentSlide.value + 1) % companyHighlights.length
  }, 4000)
})
</script>

<template>
  <section class="relative min-h-screen">
    <!-- Background Image with Overlay -->
    <div class="absolute inset-0 bg-[url('https://images.unsplash.com/photo-1600585154526-990dced4db0d')] bg-cover bg-center">
      <div class="absolute inset-0 bg-black/50"></div>
    </div>

    <!-- Colored Side Bar -->
    <div class="absolute left-0 top-0 bottom-0 w-1/4 bg-(--primary-500) bg-opacity-95 hidden md:block"></div>

    <!-- Content Wrapper -->
    <div class="relative min-h-screen">
      <!-- Main Content -->
      <div class="flex flex-col md:block">
        <div class="relative md:absolute px-6 pt-28 md:p-0 md:left-1/4 md:transform md:-translate-x-1/2 md:top-1/2 md:-translate-y-1/2 max-w-2xl">
          <div class="bg-black/70 backdrop-blur-sm p-8 rounded-lg">
            <h2 class="text-3xl md:text-5xl font-bold text-(--neutral-50) mb-4 md:mb-6">
              Construindo o Futuro com Excelência
            </h2>
            <p class="text-lg md:text-xl text-(--neutral-100) mb-4 md:mb-10">
              Soluções completas em engenharia civil e construção sustentável
            </p>
            <button class="w-full md:w-auto bg-(--neutral-50) text-(--primary-500) px-6 md:px-10 py-3 md:py-4 rounded-lg hover:bg-(--neutral-100) transition-colors text-base md:text-lg font-semibold mb-4 md:mb-0">
              Solicitar Orçamento
            </button>
          </div>
        </div>
      </div>

      <!-- Highlights Box -->
      <div class="hidden md:block md:absolute md:w-[450px] md:right-8 md:bottom-8">
        <div class="bg-(--primary-500) bg-opacity-95 backdrop-blur-sm rounded-lg shadow-2xl overflow-hidden">
          <!-- ... resto do código do highlights box ... -->
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
/* Slide para direita */
.slide-right-enter-active,
.slide-right-leave-active,
.slide-left-enter-active,
.slide-left-leave-active {
  transition: all 0.5s ease-in-out;
  position: absolute;
  width: 100%;
  height: 100%;
}

.slide-right-enter-from {
  opacity: 0;
  transform: translateX(100%);
}

.slide-right-leave-to {
  opacity: 0;
  transform: translateX(-100%);
}

/* Slide para esquerda */
.slide-left-enter-from {
  opacity: 0;
  transform: translateX(-100%);
}

.slide-left-leave-to {
  opacity: 0;
  transform: translateX(100%);
}

/* Estado normal */
.slide-right-enter-to,
.slide-right-leave-from,
.slide-left-enter-to,
.slide-left-leave-from {
  opacity: 1;
  transform: translateX(0);
}

/* Adicionando estilos para garantir posicionamento correto */
.h-full > div {
  position: relative;
  height: 100%;
}

.backdrop-blur-sm {
  backdrop-filter: blur(8px);
}
</style>