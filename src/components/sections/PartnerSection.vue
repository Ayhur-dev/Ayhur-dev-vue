<!-- src/components/sections/PartnerSection.vue -->

<template>
  <section id="partner" class="bg-brand-dark">
    <!-- Bangkok full-bleed band with fading image slideshow -->
    <div class="relative h-72 overflow-hidden flex items-center justify-center">
      <!-- Slideshow images.
       Each image is stacked absolutely in the same spot.
       Only the active one has opacity-100, others are opacity-0.
       The transition-opacity duration-1000 gives a slow 1s fade. -->
      <div
        v-for="(img, idx) in slideshowImages"
        :key="idx"
        class="absolute inset-0 transition-opacity duration-1000"
        :class="activeSlide === idx ? 'opacity-100' : 'opacity-0'"
      >
        <img
          :src="img"
          :alt="`Bangkok slide ${idx + 1}`"
          class="w-full h-full object-cover"
        />
      </div>

      <!-- Edge fading effect.
       Four absolutely positioned divs, one on each edge.
       Each fades from bg-brand-dark to transparent inward,
       blending the image seamlessly into the dark background.
       The gradient goes FROM the dark color TO transparent. -->

      <!-- Left fade -->
      <div
        class="absolute inset-y-0 left-0 w-48 z-10"
        style="background: linear-gradient(to right, #1a1a1a, transparent)"
      ></div>

      <!-- Right fade -->
      <div
        class="absolute inset-y-0 right-0 w-48 z-10"
        style="background: linear-gradient(to left, #1a1a1a, transparent)"
      ></div>

      <!-- Top fade -->
      <div
        class="absolute inset-x-0 top-0 h-16 z-10"
        style="background: linear-gradient(to bottom, #1a1a1a, transparent)"
      ></div>

      <!-- Bottom fade -->
      <div
        class="absolute inset-x-0 bottom-0 h-16 z-10"
        style="background: linear-gradient(to top, #1a1a1a, transparent)"
      ></div>

      <!-- Bangkok text sits on top of everything via z-20 -->
      <div class="relative z-20 text-center">
        <p
          class="font-display text-5xl lg:text-7xl text-brand-yellow tracking-[0.5em]"
        >
          BANGKOK
        </p>
        <p class="text-brand-yellow/50 font-bold text-xs uppercase tracking-[0.4em] mt-2">
          Our Global Headquarters
        </p>
      </div>
    </div>

    <!-- Partner CTA -->
    <div class="py-24">
      <div
        class="max-w-7xl mx-auto px-4 sm:px-8 grid lg:grid-cols-2 gap-16 items-center"
      >
        <div class="relative flex items-center justify-center">
          <div
            class="absolute -left-4 -bottom-4 w-48 h-48 bg-brand-yellow/10 rounded-sm"
          ></div>

          <img
            src="https://images.unsplash.com/photo-1542291026-7eec264c27ff?w=600&auto=format&fit=crop"
            alt="Jin Zhen Lian Partner Display"
            class="relative z-10 w-full max-w-md object-contain drop-shadow-2xl"
          />
        </div>

        <div>
          <p
            class="text-xs uppercase tracking-[0.4em] text-brand-yellow font-semibold mb-4"
          >
            Business Opportunity
          </p>

          <h2
            class="font-display text-5xl lg:text-6xl text-white tracking-wider mb-6"
          >
            BECOME A<br />JIN ZHEN LIAN<br />PARTNER
          </h2>

          <p class="text-sm text-white/60 leading-relaxed mb-10 max-w-sm">
            Join our super-family. Enjoy a stable and profitable business with
            full support and partnership opportunities around the world. We
            provide everything you need to succeed.
          </p>

          <ul class="space-y-3 mb-10">
            <li
              v-for="benefit in benefits"
              :key="benefit"
              class="flex items-center gap-3 text-sm text-white/70"
            >
              <span
                class="w-2 h-2 rounded-full bg-brand-yellow shrink-0"
              ></span>
              {{ benefit }}
            </li>
          </ul>

          <div class="flex gap-4 flex-wrap">
            <a
              href="#contact"
              class="bg-brand-yellow text-brand-dark font-semibold text-sm px-8 py-3 uppercase tracking-widest hover:bg-yellow-400 transition-colors duration-200"
            >
              Contact Us
            </a>

            <a
              href="#products"
              class="border-2 border-white/30 text-white font-semibold text-sm px-8 py-3 uppercase tracking-widest hover:border-brand-yellow hover:text-brand-yellow transition-colors duration-200"
            >
              View More
            </a>
          </div>
        </div>
      </div>
    </div>

    <!-- Certifications Section -->
    <div id="certifications" class="py-15">
      <div class="max-w-7xl mx-auto px-4 sm:px-8">
        <div class="text-center mb-16">
          <h2
            class="font-display text-3xl lg:text-4xl text-white tracking-widest"
          >
            CERTIFICATIONS
          </h2>

          <div class="w-16 h-0.5 bg-brand-yellow mx-auto mt-4"></div>
        </div>

        <div
          class="flex flex-wrap items-center justify-center gap-12 md:gap-16"
        >
          <div
            v-for="cert in certs"
            :key="cert.label"
            class="flex flex-col items-center gap-4 group"
          >
            <div
              class="w-36 h-36 group-hover:border-brand-yellow/50 transition-all duration-300 flex items-center justify-center p-4"
            >
              <img
                :src="cert.logo"
                :alt="cert.label"
                class="w-full h-full object-contain filter brightness-90 group-hover:brightness-110 transition-all duration-300"
              />
            </div>

            <p
              class="text-xs uppercase tracking-[0.3em] text-white/40 font-semibold group-hover:text-brand-yellow transition-colors duration-300"
            >
              {{ cert.label }}
            </p>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
import ghpLogo from "@/assets/cer_1.png";
import gmpLogo from "@/assets/cer_2.png";
import haccpLogo from "@/assets/cer_3.png";
import fdaLogo from "@/assets/cer_4.png";

import { ref, onMounted, onUnmounted } from "vue";

// Add your Bangkok city images here.
// Using Unsplash Bangkok photos as placeholders —
// swap these for your own imported assets when ready.
const slideshowImages: string[] = [
  "https://images.unsplash.com/photo-1508009603885-50cf7c579365?w=1200&auto=format&fit=crop",
  "https://images.unsplash.com/photo-1559592413-7cec4d0cae2b?w=1200&auto=format&fit=crop",
  "https://images.unsplash.com/photo-1563492065599-3520f775eeed?w=1200&auto=format&fit=crop",
];

// activeSlide tracks which image is currently visible.
// Starts at 0 so the first image shows immediately.
const activeSlide = ref<number>(0);

// We store the interval ID so we can clear it when the
// component is unmounted — prevents memory leaks.
let slideInterval: ReturnType<typeof setInterval>;

onMounted(() => {
  // Every 5000ms (5s), advance to the next slide.
  // The modulo (%) wraps back to 0 after the last image.
  slideInterval = setInterval(() => {
    activeSlide.value = (activeSlide.value + 1) % slideshowImages.length;
  }, 5000);
});

onUnmounted(() => {
  // Clean up the interval when the component is destroyed.
  clearInterval(slideInterval);
});

const benefits: string[] = [
  "Full marketing and branding support",
  "Dedicated account management",
  "Exclusive territory rights available",
  "Product training and POS materials",
];

interface Cert {
  label: string;
  logo: string;
}

const certs: Cert[] = [
  { label: "GHP", logo: ghpLogo },
  { label: "GMP", logo: gmpLogo },
  { label: "HACCP", logo: haccpLogo },
  { label: "FDA Thailand", logo: fdaLogo },
];
</script>
