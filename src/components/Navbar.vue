<script setup lang="ts">
import  { type Link } from '../types'

defineProps<{
  links: Link[]
}>()
</script>

<template>
  <nav class="fixed w-full bg-white shadow-sm z-50">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <div class="flex justify-between h-16">
        <div class="flex items-center">
          <h1 class="text-2xl font-bold text-blue-900">Construtora<span class="text-blue-600">Plus</span></h1>
        </div>
        <div class="hidden md:flex items-center space-x-8">
          <a v-for="link in links" :key="link.name" :href="link.href" class="text-gray-700 hover:text-blue-600">
            {{ link.name }}
          </a>
        </div>
      </div>
    </div>
  </nav>
</template>

