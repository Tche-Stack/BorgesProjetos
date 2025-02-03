<script setup lang="ts">
  import { ref } from 'vue'
  import type { ContactForm,Service } from '../types'

  const emit = defineEmits(['submit'])
  const props = defineProps<{ services: Service[] }>()

  const form = ref<ContactForm>({
    name: '',
    email: '',
    phone: '',
    service: '',
    message: ''
  })

  const handleSubmit = () => {
    emit('submit',form.value)
    form.value = {
      name: '',
      email: '',
      phone: '',
      service: '',
      message: ''
    }
  }
</script>

<template>
  <section class="py-24 bg-(--neutral-100) relative overflow-hidden">
    <!-- Padrão de bolinhas à esquerda -->
    <div class="absolute left-0 top-0 h-full w-64 opacity-10 dots-pattern"></div>

    <!-- Padrão de bolinhas à direita -->
    <div class="absolute right-0 top-0 h-full w-64 opacity-10 dots-pattern"></div>

    <div class="relative max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <!-- Seção de Título -->
      <div class="text-center mb-16">
        <h2 class="text-4xl font-bold text-(--neutral-800) mb-4">Entre em Contato</h2>
        <p class="text-xl text-(--neutral-600) max-w-2xl mx-auto">
          Estamos prontos para transformar seu projeto em realidade. Entre em contato e faça parte da nossa história de sucesso.
        </p>
      </div>

      <div class="grid lg:grid-cols-5 gap-12">
        <!-- Informações de Contato -->
        <div class="lg:col-span-2 space-y-8">
          <div class="bg-(--neutral-50) rounded-xl shadow-lg p-8">
            <h3 class="text-2xl font-semibold text-(--neutral-800) mb-6">Informações de Contato</h3>
            
            <div class="space-y-6">
              <div class="flex items-start space-x-4">
                <div class="bg-(--primary-500) p-3 rounded-lg">
                  <svg class="w-6 h-6 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 5a2 2 0 012-2h3.28a1 1 0 01.948.684l1.498 4.493a1 1 0 01-.502 1.21l-2.257 1.13a11.042 11.042 0 005.516 5.516l1.13-2.257a1 1 0 011.21-.502l4.493 1.498a1 1 0 01.684.949V19a2 2 0 01-2 2h-1C9.716 21 3 14.284 3 6V5z" />
                  </svg>
                </div>
                <div>
                  <h4 class="text-lg font-medium text-(--neutral-800)">Telefone</h4>
                  <p class="text-(--neutral-600)">(11) 99999-9999</p>
                </div>
              </div>

              <div class="flex items-start space-x-4">
                <div class="bg-(--primary-500) p-3 rounded-lg">
                  <svg class="w-6 h-6 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 8l7.89 5.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z" />
                  </svg>
                </div>
                <div>
                  <h4 class="text-lg font-medium text-(--neutral-800)">Email</h4>
                  <p class="text-(--neutral-600)">contato@empresa.com</p>
                </div>
              </div>

              <div class="flex items-start space-x-4">
                <div class="bg-(--primary-500) p-3 rounded-lg">
                  <svg class="w-6 h-6 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17.657 16.657L13.414 20.9a1.998 1.998 0 01-2.827 0l-4.244-4.243a8 8 0 1111.314 0z" />
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 11a3 3 0 11-6 0 3 3 0 016 0z" />
                  </svg>
                </div>
                <div>
                  <h4 class="text-lg font-medium text-(--neutral-800)">Endereço</h4>
                  <p class="text-(--neutral-600)">Rua Example, 123 - São Paulo, SP</p>
                </div>
              </div>
            </div>
          </div>
        </div>

        <!-- Formulário -->
        <div class="lg:col-span-3">
          <div class="bg-(--neutral-50) rounded-xl shadow-lg p-8">
            <form @submit.prevent="handleSubmit" class="space-y-6">
              <div class="grid md:grid-cols-2 gap-6">
                <div class="space-y-2">
                  <label class="text-sm font-medium text-(--neutral-800)">Nome</label>
                  <input 
                    v-model="form.name" 
                    type="text" 
                    class="w-full p-3 rounded-lg border border-(--neutral-200) focus:ring-(--primary-500) focus:border-transparent bg-(--neutral-50)"
                  >
                </div>
                <div class="space-y-2">
                  <label class="text-sm font-medium text-(--neutral-800)">Email</label>
                  <input 
                    v-model="form.email" 
                    type="email" 
                    class="w-full p-3 rounded-lg border border-(--neutral-200) focus:ring-(--primary-500) focus:border-transparent bg-(--neutral-50)"
                  >
                </div>
                <div class="space-y-2">
                  <label class="text-sm font-medium text-(--neutral-800)">Telefone</label>
                  <input 
                    v-model="form.phone" 
                    type="tel" 
                    class="w-full p-3 rounded-lg border border-(--neutral-200) focus:ring-(--primary-500) focus:border-transparent bg-(--neutral-50)"
                  >
                </div>
                <div class="space-y-2">
                  <label class="text-sm font-medium text-(--neutral-800)">Serviço</label>
                  <select 
                    v-model="form.service"
                    class="w-full p-3 rounded-lg border border-(--neutral-200) focus:ring-(--primary-500) focus:border-transparent bg-(--neutral-50)"
                  >
                    <option value="">Selecione um serviço</option>
                    <option 
                      v-for="service in services" 
                      :key="service.title" 
                      :value="service.title"
                    >
                      {{ service.title }}
                    </option>
                  </select>
                </div>
              </div>

              <div class="space-y-2">
                <label class="text-sm font-medium text-(--neutral-800)">Mensagem</label>
                <textarea 
                  v-model="form.message" 
                  rows="4"
                  class="w-full p-3 rounded-lg border border-(--neutral-200) focus:ring-(--primary-500) focus:border-transparent bg-(--neutral-50)"
                ></textarea>
              </div>

              <button 
                type="submit" 
                class="w-full bg-(--accent-500) text-(--neutral-50) px-8 py-4 rounded-lg hover:bg-(--accent-600) transition-colors text-lg font-medium"
              >
                Enviar Mensagem
              </button>
            </form>
          </div>
        </div>
      </div>
    </div>

    <!-- Gradientes para suavizar as bordas -->
    <div class="absolute left-0 top-0 h-full w-24 bg-gradient-to-r from-(--neutral-100) to-transparent pointer-events-none"></div>
    <div class="absolute right-0 top-0 h-full w-24 bg-gradient-to-l from-(--neutral-100) to-transparent pointer-events-none"></div>
  </section>
</template>

<style scoped>
.focus\:ring-2:focus {
  box-shadow: 0 0 0 2px rgba(178, 34, 34, 0.2);
}

.dots-pattern {
  background-image: url('data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMjAiIGhlaWdodD0iMjAiIHZpZXdCb3g9IjAgMCAyMCAyMCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KPGNpcmNsZSBjeD0iMTAiIGN5PSIxMCIgcj0iMiIgZmlsbD0iI2RjMjYyNiIvPgo8L3N2Zz4=');
  background-repeat: repeat;
}
</style>