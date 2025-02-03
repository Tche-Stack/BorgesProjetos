<script setup lang="ts">
  import {type Service} from '../types'

  defineProps<{
    services: Service[]
  }>()
</script>

<template>
  <section class="py-16 bg-(--neutral-100) relative overflow-hidden">
    <!-- Padrão de bolinhas à esquerda -->
    <div class="absolute left-0 top-0 h-full w-64 opacity-10 dots-pattern"></div>

    <!-- Padrão de bolinhas à direita -->
    <div class="absolute right-0 top-0 h-full w-64 opacity-10 dots-pattern"></div>

    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 relative">
      <h3 class="text-3xl font-bold text-center mb-12 text-(--neutral-800)">Nossos Serviços</h3>
      
      <div class="grid md:grid-cols-3 border-2 border-(--neutral-300) rounded-lg overflow-hidden">
        <div 
          v-for="(service, index) in services" 
          :key="service.title" 
          class="p-6 relative group hover:bg-(--neutral-200) transition-colors"
          :class="{
            'border-r-2 border-(--neutral-300)': (index + 1) % 3 !== 0,
            'border-b-2 border-(--neutral-300)': index < services.length - 3
          }"
        >
          <div class="text-(--primary-500) text-4xl mb-4">
            <i :class="service.icon"></i>
          </div>
          <h4 class="text-xl font-semibold text-(--neutral-800) mb-2">{{ service.title }}</h4>
          <p class="text-(--neutral-600)">{{ service.description }}</p>
        </div>
      </div>
    </div>

    <!-- Gradientes para suavizar as bordas -->
    <div class="absolute left-0 top-0 h-full w-24 bg-gradient-to-r from-(--neutral-100) to-transparent pointer-events-none"></div>
    <div class="absolute right-0 top-0 h-full w-24 bg-gradient-to-l from-(--neutral-100) to-transparent pointer-events-none"></div>
  </section>
</template>

<style scoped>
.group:hover {
  z-index: 10;
}

.dots-pattern {
  background-image: url('data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMjAiIGhlaWdodD0iMjAiIHZpZXdCb3g9IjAgMCAyMCAyMCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KPGNpcmNsZSBjeD0iMTAiIGN5PSIxMCIgcj0iMiIgZmlsbD0iI2RjMjYyNiIvPgo8L3N2Zz4=');
  background-repeat: repeat;
}
</style>

