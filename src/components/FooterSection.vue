<script setup lang="ts">
import { businessInfo } from '../data/businessInfo'

const currentYear = new Date().getFullYear()
</script>

<template>
  <footer class="bg-(--secondary-500) text-(--neutral-50) py-12">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <div class="grid md:grid-cols-3 gap-8">
        <div>
          <h4 class="text-xl font-bold mb-4">{{ businessInfo.name }}</h4>
          <p class="text-(--neutral-100)">
            {{ businessInfo.description }}. Soluções completas em prevenção de incêndios para toda a região metropolitana de Porto Alegre.
          </p>
        </div>

        <div>
          <h4 class="text-xl font-bold mb-4">Contato</h4>
          <ul class="space-y-2 text-(--neutral-100)">
            <li>{{ businessInfo.phone }}</li>
            <li>{{ businessInfo.email }}</li>
          </ul>
        </div>

        <div>
          <h4 class="text-xl font-bold mb-4">Endereço</h4>
          <p class="text-(--neutral-100)">
            {{ businessInfo.address }}
          </p>
        </div>
      </div>

      <div class="border-t border-(--neutral-100/20) mt-12 pt-8 text-center">
        <p class="text-(--neutral-100)">
          © {{ currentYear }} {{ businessInfo.name }}. Todos os direitos reservados.
        </p>
      </div>
    </div>
  </footer>
</template>

<style scoped>

</style>