<!-- src/components/sections/ProductsSection.vue -->

<template>
  <section id="products" class="py-24 bg-brand-dark">
    <div class="max-w-7xl mx-auto px-4 sm:px-8">

      <!-- Section heading -->
      <div class="text-center mb-16">
        <p class="text-xs uppercase tracking-[0.4em] text-brand-yellow font-semibold mb-2">
          What We Offer
        </p>
        <h2 class="font-display text-5xl lg:text-6xl text-white tracking-wider">
          OUR PRODUCTS
        </h2>
      </div>

      <!-- Product cards grid -->
      <div class="grid md:grid-cols-2 gap-8">
        <div
          v-for="product in products"
          :key="product.name"
          class="border border-yellow/10 hover:border-brand-yellow/50 hover:-translate-y-1 transition-all duration-300 overflow-hidden group bg-white/5"
        >

          <!-- Product image area -->
          <div class="bg-white/5 h-64 flex items-center justify-center relative overflow-hidden">
            <img
              :src="product.image"
              :alt="product.name"
              class="w-48 h-48 object-contain group-hover:scale-105 transition-transform duration-500"
            />

            <!-- Certification badges -->
            <div class="absolute top-4 left-4 flex gap-2 flex-wrap">
              <span
                v-for="badge in product.badges"
                :key="badge"
                class="bg-brand-yellow text-brand-dark text-[10px] font-semibold uppercase tracking-wider px-2 py-1"
              >
                {{ badge }}
              </span>
            </div>
          </div>

          <!-- Product text content -->
          <div class="p-6">
            <h3 class="font-display text-3xl tracking-wider text-white mb-2">
              {{ product.name }}
            </h3>
            <p class="text-sm text-white/50 leading-relaxed mb-4">
              {{ product.desc }}
            </p>

            <!-- Accordion -->
            <div class="border-t border-white/10 pt-4 space-y-1">
              <div
                v-for="(faq, idx) in product.faqs"
                :key="idx"
                class="border-b border-white/10"
              >
                <button
                  @click="toggle(product.name, idx)"
                  class="w-full flex items-center justify-between py-3 text-sm font-semibold uppercase tracking-wider text-left text-white/70 hover:text-brand-yellow transition-colors"
                >
                  {{ faq.q }}
                  <span class="text-brand-yellow text-xl leading-none ml-4 shrink-0">
                    {{ openIndex[product.name] === idx ? "−" : "+" }}
                  </span>
                </button>

                <div
                  class="overflow-hidden transition-all duration-300 text-sm text-white/40 leading-relaxed"
                  :style="openIndex[product.name] === idx
                    ? 'max-height: 200px; padding-bottom: 12px'
                    : 'max-height: 0'"
                >
                  {{ faq.a }}
                </div>
              </div>
            </div>
          </div>

        </div>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
import { reactive } from "vue";

import durianStick from "@/assets/classic_vanilla-stick-1200x1200-2.png";
import durianSorbet from "@/assets/mock-up-ice-cream-cone-11917984.png";
import durianStick2 from "@/assets/newone.png";
import durianStick3 from "@/assets/Vanilla_Ice_Cream.png";

interface Faq {
  q: string;
  a: string;
}

interface Product {
  name: string;
  image: string;
  desc: string;
  badges: string[];
  faqs: Faq[];
}

const products: Product[] = [
  {
    name: "CLASSIC VANILLA STICK",
    image: durianStick,
    desc: "A smooth, creamy chocolate popsicle crafted for pure indulgence. Rich cocoa flavor meets refreshing chill in every bite, delivering the perfect balance of sweetness and satisfaction.",
    badges: ["Halal", "Premium Cocoa", "Creamy"],
    faqs: [
      {
        q: "Ingredients",
        a: "Fresh milk, premium cocoa powder, cream, sugar, natural vanilla flavor, stabilizer (plant-based).",
      },
      {
        q: "Nutritional Facts (Per 100g Approx.)",
        a: "Calories: 180 kcal, total fat: 10g, saturated fat: 6g, cholesterol: 30mg, sodium: 50mg, total carbohydrates: 20g, sugars: 18g, protein: 3g.",
      },
      {
        q: "How to Store",
        a: "Keep frozen at -18°C or below. Consume within 30 minutes of removing from freezer for best taste.",
      },
    ],
  },
  {
    name: "CONE CREAM & STRAWBERRY",
    image: durianSorbet,
    desc: "A delightful fusion of smooth cream and refreshing strawberry sorbet, perfectly nestled in a crispy cone. Light, vibrant, and irresistibly delicious.",
    badges: ["Halal", "Real Strawberry", "Creamy", "Crispy Cone"],
    faqs: [
      {
        q: "Ingredients",
        a: "Strawberry sorbet, Dairy cream, Sugar, Natural strawberry flavor, Stabilizer (plant-based), Cone (wheat flour, sugar, vegetable oil, salt).",
      },
      {
        q: "Nutritional Facts (Per 100g Approx.)",
        a: "Calories: 165 kcal, total fat: 8g, saturated fat: 5g, cholesterol: 25mg, sodium: 40mg, total carbohydrates: 18g, sugars: 16g, protein: 2g.",
      },
      {
        q: "How to Enjoy",
        a: "Best enjoyed straight from the freezer.",
      },
    ],
  },
  {
    name: "VANILLA ICE CREAM",
    image: durianStick3,
    desc: "A smooth, creamy vanilla ice cream crafted for pure indulgence. Rich vanilla flavor meets refreshing chill in every bite.",
    badges: ["Halal", "Premium Cocoa", "Creamy"],
    faqs: [
      {
        q: "Ingredients",
        a: "Fresh milk, premium cocoa powder, cream, sugar, natural vanilla flavor, stabilizer (plant-based).",
      },
      {
        q: "Nutritional Facts (Per 100g Approx.)",
        a: "Calories: 180 kcal, total fat: 10g, saturated fat: 6g, cholesterol: 30mg, sodium: 50mg, total carbohydrates: 20g, sugars: 18g, protein: 3g.",
      },
      {
        q: "How to Store",
        a: "Keep frozen at -18°C or below. Consume within 30 minutes of removing from freezer for best taste.",
      },
    ],
  },
  {
    name: "BLACKBERRY ICE CREAM",
    image: durianStick2,
    desc: "Indulge in the rich, fruity goodness of our Blackberry Ice Cream — a smooth, creamy delight made with real blackberry flavor and crafted for pure refreshment.",
    badges: ["Halal", "Premium Cocoa", "Creamy"],
    faqs: [
      {
        q: "Ingredients",
        a: "Fresh Blackberry Puree, Dairy cream, Sugar, Natural blackberry flavor, Stabilizer (plant-based).",
      },
      {
        q: "Nutritional Facts (Per Serving Approx.)",
        a: "Calories: 180 kcal, total fat: 8g, sodium: 45mg, carbohydrates: 24g, sugars: 20g, protein: 3g.",
      },
      {
        q: "How to Store",
        a: "Keep frozen at −18°C or below.",
      },
    ],
  },
];

const openIndex = reactive<Record<string, number>>({});

function toggle(productName: string, idx: number): void {
  openIndex[productName] = openIndex[productName] === idx ? -1 : idx;
}
</script>