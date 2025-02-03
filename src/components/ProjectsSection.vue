<script setup lang="ts">
import type { Project } from '../types'

defineProps<{
  projects: Project[]
}>()
</script>

<template>
  <section class="py-16 bg-gray-100">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <h3 class="text-3xl font-bold text-center mb-12 text-gray-900">Projetos Recentes</h3>
      <div class="grid md:grid-cols-2 lg:grid-cols-3 gap-6">
        <div v-for="project in projects" :key="project.title" class="relative group overflow-hidden rounded-lg">
          <img :src="project.image" :alt="project.title" class="w-full h-64 object-cover transform group-hover:scale-105 transition-transform">
          <div class="absolute inset-0 bg-black bg-opacity-40 flex items-end p-4 opacity-0 group-hover:opacity-100 transition-opacity">
            <div>
              <h4 class="text-white text-lg font-semibold">{{ project.title }}</h4>
              <p class="text-gray-200">{{ project.location }}</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

