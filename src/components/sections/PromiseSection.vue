<!-- src/components/sections/WhySection.vue -->

<template>
  <section id="why" class="py-24 bg-brand-yellow">
    <div
      class="max-w-7xl mx-auto px-4 sm:px-8 grid lg:grid-cols-2 gap-16 items-center"
    >
      <!-- Left: image that fades when active reason changes.
           The key trick is the v-show + fade-image class.
           Each image is stacked in the same spot using absolute
           positioning, and only the active one is visible. -->
      <div class="relative aspect-square overflow-hidden rounded-sm">
        <div
          v-for="reason in reasons"
          :key="reason.num"
          class="absolute inset-0 transition-opacity duration-700"
          :class="activeNum === reason.num ? 'opacity-100' : 'opacity-0'"
        >
          <!-- If you have real images, replace this div with:
               <img :src="reason.image" class="w-full h-full object-cover" /> -->
          <img
            :src="reason.image"
            :alt="reason.title"
            class="w-full h-full object-cover"
          />
        </div>
      </div>

      <!-- Right: numbered circles + active reason content -->
      <div>
        <p
          class="text-xs uppercase tracking-[0.4em] text-brand-dark/50 font-semibold mb-3"
        >
          The Difference
        </p>
        <h2
          class="font-display text-5xl lg:text-6xl text-brand-dark tracking-wider mb-10"
        >
          WHY EASTERN<br />MONTHONG?
        </h2>

        <!-- Numbered circle tabs.
             Clicking a circle sets activeNum to that reason's number.
             The active circle gets a filled dark background. -->
        <div class="flex gap-4 mb-10">
          <button
            v-for="reason in reasons"
            :key="reason.num"
            @click="activeNum = reason.num"
            :class="
              activeNum === reason.num
                ? 'bg-brand-dark text-brand-yellow'
                : 'bg-transparent text-brand-dark border-2 border-brand-dark hover:bg-brand-dark/10'
            "
            class="w-12 h-12 rounded-full flex items-center justify-center font-display text-xl transition-all duration-300"
          >
            {{ reason.num }}
          </button>
        </div>

        <!-- Active reason content.
             transition-all + opacity gives a smooth fade when
             switching between reasons. We use a key on the div
             so Vue re-renders it (and replays the animation)
             every time activeNum changes. -->
        <transition name="fade" mode="out-in">
          <div :key="activeNum" class="space-y-3">
            <h4 class="font-display text-3xl tracking-wider text-brand-dark">
              {{ activeReason.title }}
            </h4>
            <p class="text-sm text-brand-dark/60 leading-relaxed max-w-sm">
              {{ activeReason.desc }}
            </p>
          </div>
        </transition>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
import { ref, computed } from "vue";

import img1 from "@/assets/easter_1.png";
import img2 from "@/assets/easter_2.png";
import img3 from "@/assets/easter_mb_3.png";

interface Reason {
  num: string;
  title: string;
  desc: string;
  image: string;
}

const reasons: Reason[] = [
  {
    num: "1",
    title: "Ideal Growing Conditions",
    desc: "The Eastern Monthong grows in the dry climate and mineral-rich soil of Rayong, Chanthaburi, and Trat provinces, giving the variety its distinct flavor profile.",
    image: img1,
  },
  {
    num: "2",
    title: "Finest Monthong Variety",
    desc: 'Monthong, meaning "Golden Pillow", is prized for its mild, sweet flavour and creamy, thick flesh above all other varieties.',
    image: img2,
  },
  {
    num: "3",
    title: "Sustainable Harvesting",
    desc: "Hand-picked at peak ripeness to ensure maximum flavour and nutritional value in every single piece we produce.",
    image: img3,
  },
];

const activeNum = ref<string>("1");

const activeReason = computed<Reason>(
  () => reasons.find((r) => r.num === activeNum.value)!,
);
</script>

<style scoped>
/* Vue's built-in <transition> component looks for these
   class names automatically when name="fade" is set.
   
   fade-enter-active / fade-leave-active — duration of the animation
   fade-enter-from  — starting state when element enters
   fade-leave-to    — ending state when element leaves */

.fade-enter-active,
.fade-leave-active {
  transition:
    opacity 0.4s ease,
    transform 0.4s ease;
}

.fade-enter-from {
  opacity: 0;
  transform: translateY(10px);
}

.fade-leave-to {
  opacity: 0;
  transform: translateY(-10px);
}
</style>
