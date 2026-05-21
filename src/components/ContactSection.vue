<script setup lang="ts">
  import { ref } from 'vue'
  import type { ContactForm,Service } from '../types'
  import { contactInfo } from '../data/contactInfo'

  const emit = defineEmits(['submit'])
  defineProps<{ services: Service[] }>()

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
  <section id="contato" class="py-24 bg-(--neutral-100) relative overflow-hidden scroll-mt-20">
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
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" :d="contactInfo.phone.icon" />
                  </svg>
                </div>
                <div>
                  <h4 class="text-lg font-medium text-(--neutral-800)">{{ contactInfo.phone.label }}</h4>
                  <p class="text-(--neutral-600)">{{ contactInfo.phone.number }}</p>
                </div>
              </div>

              <div class="flex items-start space-x-4">
                <div class="bg-(--primary-500) p-3 rounded-lg">
                  <svg class="w-6 h-6 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" :d="contactInfo.email.icon" />
                  </svg>
                </div>
                <div>
                  <h4 class="text-lg font-medium text-(--neutral-800)">{{ contactInfo.email.label }}</h4>
                  <p class="text-(--neutral-600)">{{ contactInfo.email.address }}</p>
                </div>
              </div>

              <div class="flex items-start space-x-4">
                <div class="bg-(--primary-500) p-3 rounded-lg">
                  <svg class="w-6 h-6 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" :d="contactInfo.address.icon" />
                  </svg>
                </div>
                <div>
                  <h4 class="text-lg font-medium text-(--neutral-800)">{{ contactInfo.address.label }}</h4>
                  <p class="text-(--neutral-600)">{{ contactInfo.address.text }}</p>
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
                class="w-full bg-(--accent-500) text-(--neutral-50) px-8 py-4 rounded-lg hover:bg-(--accent-600) transition-colors text-lg font-medium flex items-center justify-center gap-3"
              >
                <svg class="w-5 h-5" fill="currentColor" viewBox="0 0 24 24">
                  <path d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.967 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51-.173-.008-.371-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347m-5.421 7.403h-.004a9.87 9.87 0 01-5.031-1.378l-.361-.214-3.741.982.998-3.648-.235-.374a9.86 9.86 0 01-1.51-5.26c.001-5.45 4.436-9.884 9.888-9.884 2.64 0 5.122 1.03 6.988 2.898a9.825 9.825 0 012.893 6.994c-.003 5.45-4.437 9.884-9.885 9.884m8.413-18.297A11.815 11.815 0 0012.05 0C5.495 0 .16 5.335.157 11.892c0 2.096.547 4.142 1.588 5.945L.057 24l6.305-1.654a11.882 11.882 0 005.683 1.448h.005c6.554 0 11.89-5.335 11.893-11.893a11.821 11.821 0 00-3.48-8.413z" />
                </svg>
                Enviar via WhatsApp
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