<script setup lang="ts">
import { ref, computed } from 'vue'

import logodark from '../assets/Logo-dark.svg'
import logolight from '../assets/Logo-light.svg'
import { businessInfo } from '../data/businessInfo'

const navItems = ref([
  { name: 'Home', path: '/' },
  { name: 'About', path: '/about' },
  { name: 'Services', path: '/services' },
  { name: 'Contact', path: '/contact' }
])

const isMenuOpen = ref(false)

const closeMenu = () => {
  isMenuOpen.value = false
}

const whatsappLink = computed(() => {
  const phoneNumber = businessInfo.phone.replace(/\D/g, '')
  return `https://wa.me/${phoneNumber}`
})
</script>


<template>
  <header class="bg-black/70 backdrop-blur-sm fixed w-full top-0 left-0 shadow-lg">

    <div class="container mx-auto px-4">
      <div class="flex items-center h-20 justify-between">
        <!-- Logo -->
        <div class="flex-shrink-0 w-48">
          <img :src='logodark' alt="Logo" class="h-12 w-48 object-contain" />
        </div>

        <!-- Desktop Navigation -->
        <div class="hidden md:flex items-center space-x-8">
          <nav>
            <div class="flex space-x-8">
              <a v-for="item in navItems" :key="item.name" :href="item.path"
                class="text-(--neutral-50) hover:text-(--primary-500) px-3 py-2 rounded-md text-base font-medium transition-colors">
                {{ item.name }}
              </a>
            </div>
          </nav>

          <a :href="whatsappLink" target="_blank"
            class="bg-(--primary-500) hover:bg-(--primary-600) text-(--neutral-50) px-6 py-3 rounded-md flex items-center space-x-2 text-base transition-colors">
            <svg class="w-5 h-5" fill="currentColor" viewBox="0 0 24 24">
              <path
                d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.967 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51-.173-.008-.371-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347m-5.421 7.403h-.004a9.87 9.87 0 01-5.031-1.378l-.361-.214-3.741.982.998-3.648-.235-.374a9.86 9.86 0 01-1.51-5.26c.001-5.45 4.436-9.884 9.888-9.884 2.64 0 5.122 1.03 6.988 2.898a9.825 9.825 0 012.893 6.994c-.003 5.45-4.437 9.884-9.885 9.884m8.413-18.297A11.815 11.815 0 0012.05 0C5.495 0 .16 5.335.157 11.892c0 2.096.547 4.142 1.588 5.945L.057 24l6.305-1.654a11.882 11.882 0 005.683 1.448h.005c6.554 0 11.89-5.335 11.893-11.893a11.821 11.821 0 00-3.48-8.413z" />
            </svg>
            <span>WhatsApp</span>
          </a>
        </div>

        <!-- Mobile Menu Button -->
        <button @click="isMenuOpen = !isMenuOpen"
          class="block md:hidden p-2 rounded-lg hover:bg-gray-100 transition-colors">
          <svg class="w-6 h-6 text-gray-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path v-if="!isMenuOpen" stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
              d="M4 6h16M4 12h16M4 18h16" />
            <path v-else stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
          </svg>
        </button>
      </div>
    </div>

    <!-- Mobile Menu Overlay -->
    <div v-show="isMenuOpen" class="fixed inset-0 bg-black bg-opacity-50 md:hidden" @click="closeMenu"></div>

    <!-- Mobile Menu Sidebar -->
    <div :class="[
      'fixed right-0 top-0 bottom-0 w-64 bg-white transform transition-transform duration-300 ease-in-out md:hidden',
      isMenuOpen ? 'translate-x-0' : 'translate-x-full'
    ]">
      <div class="flex flex-col h-full">
        <div class="p-4 border-b">
          <img :src='logolight' alt="Logo" class="h-8 w-32 object-contain" />
        </div>

        <nav class="flex-1 px-4 py-6 space-y-4">
          <a v-for="item in navItems" :key="item.name" :href="item.path" @click="closeMenu"
            class="block py-3 text-gray-700 hover:text-indigo-600 text-lg font-medium border-b border-gray-100">
            {{ item.name }}
          </a>
        </nav>

        <div class="p-4 border-t">
          <a :href="whatsappLink" target="_blank"
            class="w-full bg-green-500 hover:bg-green-600 text-white px-4 py-3 rounded-lg flex items-center justify-center space-x-2">
            <svg class="w-5 h-5" fill="currentColor" viewBox="0 0 24 24">
              <path
                d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.967 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51-.173-.008-.371-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347m-5.421 7.403h-.004a9.87 9.87 0 01-5.031-1.378l-.361-.214-3.741.982.998-3.648-.235-.374a9.86 9.86 0 01-1.51-5.26c.001-5.45 4.436-9.884 9.888-9.884 2.64 0 5.122 1.03 6.988 2.898a9.825 9.825 0 012.893 6.994c-.003 5.45-4.437 9.884-9.885 9.884m8.413-18.297A11.815 11.815 0 0012.05 0C5.495 0 .16 5.335.157 11.892c0 2.096.547 4.142 1.588 5.945L.057 24l6.305-1.654a11.882 11.882 0 005.683 1.448h.005c6.554 0 11.89-5.335 11.893-11.893a11.821 11.821 0 00-3.48-8.413z" />
            </svg>
            <span>WhatsApp</span>
          </a>
        </div>
      </div>
    </div>
  </header>
</template>

<style scoped>
header {
  z-index: 50;
}

.backdrop-blur-sm {
  backdrop-filter: blur(8px);
}
</style>
