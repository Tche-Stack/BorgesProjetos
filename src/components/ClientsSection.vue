<script setup lang="ts">
import { type Client } from '../types'
import { ref, computed } from 'vue'

const props = defineProps<{
  clients: Client[]
}>()

// Duplicar clientes o suficiente para cobrir a largura da tela
const duplicatedClients = computed(() => {
  // Duplicar 4 vezes para garantir cobertura suficiente
  return [...props.clients, ...props.clients, ...props.clients, ...props.clients]
})
const isAnimationPaused = ref(false)
</script>

<template>
  <section class="py-16 bg-(--neutral-800) overflow-hidden relative">
    <div class="relative max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <h3 class="text-3xl font-bold text-center mb-12 text-(--neutral-50)">Nossos Clientes</h3>
      
      <div class="relative py-12">
        <!-- Gradientes para suavizar as bordas do carrossel -->
        <div class="absolute left-0 top-8 bottom-8 w-32 bg-gradient-to-r from-(--neutral-800) via-(--neutral-800/80) to-transparent z-10"></div>
        <div class="absolute right-0 top-8 bottom-8 w-32 bg-gradient-to-l from-(--neutral-800) via-(--neutral-800/80) to-transparent z-10"></div>

        <div 
          class="flex overflow-hidden py-8"
          @mouseenter="isAnimationPaused = true"
          @mouseleave="isAnimationPaused = false"
        >
          <!-- Primeiro conjunto -->
          <div 
            class="flex animate-scroll px-4"
            :class="{ 'pause-animation': isAnimationPaused }"
            :style="`animation-duration: ${props.clients.length * 10}s`"
          >
            <div 
              v-for="(client, index) in duplicatedClients" 
              :key="`${client.name}-${index}`"
              class="flex-shrink-0 w-80 mx-4 bg-(--primary-500) rounded-lg overflow-hidden transform transition-all duration-300 hover:scale-105 shadow-lg hover:shadow-xl"
            >
              <div class="p-6">
                <div class="flex items-center mb-4">
                  <img 
                    :src="client.logo" 
                    :alt="client.name" 
                    class="w-16 h-16 object-cover rounded-full bg-(--neutral-100)"
                  >
                  <div class="ml-4">
                    <h4 class="text-xl font-semibold text-(--neutral-50)">{{ client.name }}</h4>
                    <p class="text-(--neutral-100)">{{ client.industry }}</p>
                  </div>
                </div>
                <p class="text-(--neutral-100)">{{ client.description }}</p>
              </div>
            </div>
          </div>

          <!-- Clone do primeiro conjunto -->
          <div 
            class="flex animate-scroll px-4"
            :class="{ 'pause-animation': isAnimationPaused }"
            :style="`animation-duration: ${props.clients.length * 10}s`"
            aria-hidden="true"
          >
            <div 
              v-for="(client, index) in duplicatedClients" 
              :key="`clone-${client.name}-${index}`"
              class="flex-shrink-0 w-80 mx-4 bg-(--primary-500) rounded-lg overflow-hidden transform transition-all duration-300 hover:scale-105 shadow-lg hover:shadow-xl"
            >
              <div class="p-6">
                <div class="flex items-center mb-4">
                  <img 
                    :src="client.logo" 
                    :alt="client.name" 
                    class="w-16 h-16 object-cover rounded-full bg-(--neutral-100)"
                  >
                  <div class="ml-4">
                    <h4 class="text-xl font-semibold text-(--neutral-50)">{{ client.name }}</h4>
                    <p class="text-(--neutral-100)">{{ client.industry }}</p>
                  </div>
                </div>
                <p class="text-(--neutral-100)">{{ client.description }}</p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
@keyframes scroll {
  0% {
    transform: translateX(0);
  }
  100% {
    transform: translateX(-50%);
  }
}

.animate-scroll {
  animation: scroll linear infinite;
  position: relative;
  z-index: 1;
}

.pause-animation {
  animation-play-state: paused;
}
</style> 