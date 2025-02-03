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

const slogan = "Segurança e confiabilidade na projeção do seu futuro"
const description = "Soluções completas em prevenção de incêndios"
const buttonText = "Solicitar Orçamento"
</script>

<template>
  <section class="relative min-h-screen">
    <!-- Background Image with Overlay -->
    <div class="absolute inset-0 bg-[url('@/assets/poa.webp')] bg-cover bg-center">
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
              {{ slogan }}
            </h2>
            <p class="text-lg md:text-xl text-(--neutral-100) mb-4 md:mb-10">
              {{ description }}
            </p>
            <button class="w-full md:w-auto bg-(--neutral-50) text-(--primary-500) px-6 md:px-10 py-3 md:py-4 rounded-lg hover:bg-(--neutral-100) transition-colors text-base md:text-lg font-semibold mb-4 md:mb-0">
              {{ buttonText }}
            </button>
          </div>

        </div>
      </div>

      <!-- Highlights Box -->
      <div class="hidden md:block md:absolute md:w-[450px] md:right-8 md:bottom-8">
        <div class="bg-(--primary-500) bg-opacity-95 backdrop-blur-sm rounded-lg shadow-2xl overflow-hidden">
          <div class="relative h-[220px]">
            <TransitionGroup 
              :name="`slide-${slideDirection}`"
              tag="div"
              class="h-full"
            >
              <div 
                v-for="(highlight, index) in companyHighlights" 
                :key="highlight.title"
                v-show="currentSlide === index"
                class="absolute inset-0 pt-6 px-8"
              >
                <h4 class="text-2xl font-bold text-(--neutral-50) mb-3">
                  {{ highlight.title }}
                </h4>
                <p class="text-lg text-(--neutral-100) mb-3">
                  {{ highlight.description }}
                </p>
                <p class="text-xl font-semibold text-(--neutral-50)">
                  {{ highlight.stats }}
                </p>
              </div>
            </TransitionGroup>

            <!-- Indicadores de slide em um container separado -->
            <div class="absolute bottom-0 left-0 right-0 h-14 flex items-center justify-center bg-black/10">
              <div class="flex space-x-3">
                <button
                  v-for="(_, index) in companyHighlights"
                  :key="index"
                  @click="changeSlide(index)"
                  class="w-3 h-3 rounded-full transition-colors"
                  :class="currentSlide === index ? 'bg-(--neutral-50)' : 'bg-black/40'"
                />
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
/* Configuração base para todas as transições */
.slide-right-enter-active,
.slide-right-leave-active,
.slide-left-enter-active,
.slide-left-leave-active {
  transition: all 0.5s cubic-bezier(0.4, 0, 0.2, 1);
  position: absolute;
  width: 100%;
  height: 100%;
}

/* Slide para direita */
.slide-right-enter-from {
  opacity: 0;
  transform: translateX(50%);
}

.slide-right-leave-to {
  opacity: 0;
  transform: translateX(-50%);
}

/* Slide para esquerda */
.slide-left-enter-from {
  opacity: 0;
  transform: translateX(-50%);
}

.slide-left-leave-to {
  opacity: 0;
  transform: translateX(50%);
}

/* Estado normal */
.slide-right-enter-to,
.slide-right-leave-from,
.slide-left-enter-to,
.slide-left-leave-from {
  opacity: 1;
  transform: translateX(0);
}

/* Ajuste para o container dos slides */
.h-full > div {
  position: relative;
  height: 100%;
  overflow: hidden;
}

/* Ajuste para cada slide */
.absolute {
  backface-visibility: hidden;
  -webkit-backface-visibility: hidden;
}

.backdrop-blur-sm {
  backdrop-filter: blur(8px);
}
</style>