<!-- src/App.vue -->

<template>
  <div>
    <NavBar />

    <main>
      <HeroSection />
      <VideoSection />
      <ProductsSection />
      <PromiseSection />
     
      <PartnerSection />
      <FaqSection />
      <ContactSection />
    </main>
  </div>
</template>

<script setup lang="ts">
// We import each section component so Vue knows what
// <HeroSection />, <NavBar /> etc. mean in the template above.
// With <script setup>, imported components are automatically
// available in the template — no need to register them manually.

import NavBar from "./components/NavBar.vue";
import HeroSection from "./components/sections/HeroSection.vue";
import VideoSection from "./components/sections/VideoSection.vue";
import ProductsSection from "./components/sections/ProductsSection.vue";
import PromiseSection from "./components/sections/PromiseSection.vue";
import PartnerSection from "./components/sections/PartnerSection.vue";
import FaqSection from "./components/sections/FaqSection.vue";
import ContactSection from "./components/sections/ContactSection.vue";
</script>
