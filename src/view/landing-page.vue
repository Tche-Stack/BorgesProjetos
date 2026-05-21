<script setup lang="ts">
import HeroSection from "../components/HeroSection.vue"
import ServicesSection from "../components/ServicesSection.vue";
import ClientsSection from "../components/ClientsSection.vue";
import ContactSection from "../components/ContactSection.vue";
import FooterSection from "../components/FooterSection.vue";

import { services } from '../data/services'
import { clients } from '../data/clients'
import { businessInfo } from '../data/businessInfo'
import type { ContactForm } from './../types'

const handleFormSubmit = (formData: ContactForm) => {
  const lines = [
    'Olá! Vim pelo site da Borges Projetos.',
    '',
    `*Nome:* ${formData.name}`,
    `*Email:* ${formData.email}`,
    `*Telefone:* ${formData.phone}`,
    `*Serviço de interesse:* ${formData.service || 'não informado'}`,
    '',
    '*Mensagem:*',
    formData.message || '(sem mensagem)'
  ]
  const text = encodeURIComponent(lines.join('\n'))
  window.open(`https://wa.me/${businessInfo.phoneE164}?text=${text}`, '_blank')
}
</script>

<template>
  <div class="min-h-screen bg-gray-50">
    <HeroSection/>
    <ServicesSection :services="services"/>
    <ClientsSection :clients="clients"/>
    <ContactSection :services="services" @submit="handleFormSubmit"/>
    <FooterSection/>
  </div>
</template>