<script setup lang="ts">
import Navbar from "../components/Navbar.vue";
import HeroSection from "../components/HeroSection.vue"
import ServicesSection from "../components/ServicesSection.vue";
import ClientsSection from "../components/ClientsSection.vue";
import ContactSection from "../components/ContactSection.vue";
import FooterSection from "../components/FooterSection.vue";

import { services } from '../data/services'
import { clients } from '../data/clients'
import type { Link, ContactForm } from './../types'

const links: Link[] = [
  {name: 'Inicio', href: '/'},
  {name: 'Serviços', href: '/about'},
  {name: 'Clientes', href: '/clients'},
  {name: 'Contato', href: '/contact'}
]

const handleFormSubmit = (formData: ContactForm) => {
  console.log('Form submitted', formData)
  alert('Formulário enviado com sucesso!')
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