<script setup lang="ts">
import Header from "./components/layout/Header.vue";
import Hero from "./components/sections/Hero.vue";
import Features from "./components/sections/Features.vue";
import Pricing from "./components/sections/Pricing.vue";
import Footer from "./components/layout/Footer.vue";
import Faq from "./components/sections/Faq.vue";
import Testimonial from "./components/sections/Testimonial.vue";
</script>

<template>
  <main class="overflow-hidden">
    <Header />
    <Hero />
    <Features />
    <Pricing />
    <Faq />
    <Testimonial />
    <Footer />
  </main>
</template>
