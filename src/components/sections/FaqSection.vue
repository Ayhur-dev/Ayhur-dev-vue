<!-- src/components/sections/FaqSection.vue -->

<template>
  <section id="faq" class="bg-brand-yellow py-24">
    <div class="max-w-7xl mx-auto px-4 sm:px-8">
      <div class="grid lg:grid-cols-2 gap-6 items-start">
        <!-- Left: heading + product image -->
        <div class="flex flex-col justify-between h-full">
          <h2
            class="font-display text-6xl lg:text-7xl text-brand-dark tracking-wide leading-none mb-12"
          >
            FREQUENTLY<br />ASKED<br />QUESTIONS
          </h2>

          <!-- Product/fruit image.
               Replace src with your own imported asset when ready.
               object-contain keeps the full image visible. -->
          <div class="w-full max-w-md">
            <img
              :src="durianImg"
              alt="Durian fruit"
              class="mr-20 w-full object-contain drop-shadow-xl"
            />
          </div>
        </div>

        <!-- Right: tabs + accordion -->
        <div>
          <!-- Tab buttons.
               Active tab: black background, white bold text.
               Inactive: white background, gray text. -->
          <div class="flex gap-3 mb-10 flex-wrap">
            <button
              v-for="tab in tabs"
              :key="tab"
              @click="switchTab(tab)"
              :class="
                activeTab === tab
                  ? 'bg-brand-dark text-white'
                  : 'bg-white text-gray-400 hover:text-gray-600'
              "
              class="px-6 py-3 lg:text-lg text-xs rounded-lg font-bold uppercase tracking-widest transition-all duration-200"
            >
              {{ tab }}
            </button>
          </div>

          <!-- FAQ accordion.
               Each question has a bold black title, a +/- toggle,
               and a bottom border divider. The answer fades in
               using max-height transition. -->
          <div class="space-y-0">
            <div
              v-for="(faq, idx) in activeFaqs"
              :key="idx"
              class="border-b border-brand-dark/20"
            >
              <!-- Question row -->
              <button
                @click="openIdx = openIdx === idx ? -1 : idx"
                class="w-full flex items-start justify-between py-5 text-left gap-6 group"
              >
                <span
                  class="text-sm font-bold text-brand-dark leading-snug group-hover:text-brand-dark/70 transition-colors"
                >
                  {{ faq.q }}
                </span>

                <!-- + / − icon -->
                <span
                  class="text-brand-dark text-2xl leading-none shrink-0 mt-0.5 font-light"
                >
                  {{ openIdx === idx ? "−" : "+" }}
                </span>
              </button>

              <!-- Answer body -->
              <div
                class="overflow-hidden transition-all duration-300 text-sm text-brand-dark/60 leading-relaxed"
                :style="
                  openIdx === idx
                    ? 'max-height: 300px; padding-bottom: 20px'
                    : 'max-height: 0'
                "
              >
                {{ faq.a }}
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
import { ref, computed } from "vue";

import durianImg from "@/assets/Best-Dragon-Fruit-Varieties-Feature.png";

interface Faq {
  q: string;
  a: string;
}

const faqData: Record<string, Faq[]> = {
  Product: [
    {
      q: "What are the products made of, and do they contain any dairy, sugar, or food additives?",
      a: "Our products contain no dairy, sugar, or food additives. They are made from 100% Eastern Monthong durian with natural ingredients only.",
    },
    {
      q: "What is the difference between the Durian Sorbet Bar and the Classic Vanilla Stick?",
      a: "The Sorbet Bar is lighter and fruit-forward, made with fresh durian pulp and cane sugar. The Classic Vanilla Stick is richer and creamier, with a milk and cream base.",
    },
    {
      q: "Are the products vegan?",
      a: "The Durian Sorbet Bar is fully vegan. The Classic Vanilla Stick contains dairy and is not suitable for vegans.",
    },
    {
      q: "How should I store the products?",
      a: "Keep all products frozen at -18°C or below. Consume within 30 minutes of removing from the freezer for the best experience.",
    },
    {
      q: "What are the health benefits of eating durian?",
      a: "Durian is rich in vitamins C and B, dietary fibre, potassium, and antioxidants. It provides natural energy and supports immune health.",
    },
  ],
  Partnerships: [
    {
      q: "How do I become a distributor or partner?",
      a: "Contact us through our partnership form and our team will reach out within 3 business days to discuss opportunities in your region.",
    },
    {
      q: "What support do partners receive?",
      a: "Partners receive full marketing support, product training, POS materials, and a dedicated account manager.",
    },
    {
      q: "Are exclusive territories available?",
      a: "Yes, exclusive distribution rights are available in select markets. Contact our team for current availability.",
    },
    {
      q: "What is the minimum order quantity for partners?",
      a: "MOQ varies by product and market. Please contact us directly for specific requirements for your region.",
    },
  ],
  Support: [
    {
      q: "Do you ship internationally?",
      a: "Yes, we ship worldwide with full cold-chain logistics to ensure product integrity during transit.",
    },
    {
      q: "How is the cold chain maintained during shipping?",
      a: "We use certified frozen logistics partners with temperature-controlled containers throughout the entire journey.",
    },
    {
      q: "What should I do if my order arrives damaged?",
      a: "Please contact us within 24 hours of receiving your order with photos of the damage and we will arrange a replacement.",
    },
    {
      q: "How can I track my order?",
      a: "Once your order is dispatched, you will receive a tracking number via email to monitor your shipment in real time.",
    },
  ],
};

const tabs = Object.keys(faqData);
const activeTab = ref<string>("Product");
const openIdx = ref<number>(0); // first question open by default like the screenshot

// When switching tabs, reset the open accordion to the first item
function switchTab(tab: string): void {
  activeTab.value = tab;
  openIdx.value = 0;
}

const activeFaqs = computed<Faq[]>(() => faqData[activeTab.value]);
</script>
