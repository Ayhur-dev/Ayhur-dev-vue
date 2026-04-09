<!-- src/components/NavBar.vue -->

<template>
  <nav
    class="fixed top-0 left-0 right-0 z-50 bg-brand-yellow backdrop-blur border-b border-brand-yellow/30"
  >
    <div
      class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 flex items-center justify-between h-24"
    >
      <!-- Logo -->
      <div class="flex flex-col leading-none">
        <span
          class="font-display text-[clamp(1.2rem,5vw,1.875rem)] font-bold tracking-widest text-brand-dark"
        >
          金枕榴
        </span>

        <span
          class="text-[clamp(0.55rem,2vw,0.75rem)] tracking-[0.25em] uppercase text-brand-dark font-bold"
        >
          AYHUR-DEV
        </span>
      </div>

      <!-- Desktop navigation links -->
      <ul
        class="hidden min-[1020px]:flex gap-3 md:gap-6 lg:gap-10 text-[14px] font-bold uppercase tracking-widest text-brand-dark"
      >
        <li v-for="item in navItems" :key="item.label">
          <a :href="item.href" class="nav-link">
            <span class="nav-text">
              <span>{{ item.label }}</span>
              <span>{{ item.label }}</span>
            </span>
          </a>
        </li>
      </ul>

      <!-- Desktop CTA button -->

      <a
        href="#contact"
        class="hidden min-[1020px]:inline-block contact-btn bg-brand-yellow text-brand-dark font-semibold text-sm uppercase tracking-widest"
      >
        <span class="contact-text">
          <span>Contact Us</span>
          <span>Contact Us</span>
        </span>
      </a>

      <!-- Mobile burger button -->
      <button
        @click="menuOpen = !menuOpen"
        class="min-[1020px]:hidden flex flex-col gap-1.5 p-2"
        aria-label="Toggle menu"
      >
        <!-- Each span is one bar of the burger icon.
             When menuOpen is true, we rotate them into an X. -->
        <span
          class="block w-6 h-0.5 bg-brand-dark transition-all duration-300"
          :class="menuOpen ? 'rotate-45 translate-y-2' : ''"
        ></span>
        <span
          class="block w-6 h-0.5 bg-brand-dark transition-all duration-300"
          :class="menuOpen ? 'opacity-0' : ''"
        ></span>
        <span
          class="block w-6 h-0.5 bg-brand-dark transition-all duration-300"
          :class="menuOpen ? '-rotate-45 -translate-y-2' : ''"
        ></span>
      </button>
    </div>

    <!-- Mobile dropdown menu -->
    <!-- v-show toggles CSS display, keeping the element in the DOM.
         This is better than v-if here because it avoids re-mounting
         the list every time the menu opens. -->
    <Transition name="fade">
      <div
        v-show="menuOpen"
        class="min-[1020px]:hidden bg-brand-yellow border-t border-brand-yellow/30 px-6 py-4 flex flex-col gap-4"
      >
        <a
          v-for="item in navItems"
          :key="item.label"
          :href="item.href"
          @click="menuOpen = false"
          class="pl-4 text-sm font-semibold uppercase tracking-widest text-brand-dark hover:text-white transition-colors"
        >
          {{ item.label }}
        </a>

        <h1 class="pl-4 font-bold">
          EN | <span class="text-[#B19B19]">榴</span>
        </h1>
        <a
          href="#contact"
          class="contact-btn w-37 bg-brand-yellow text-brand-dark font-semibold text-sm uppercase tracking-widest"
        >
          <span class="contact-text">
            <span>Contact Us</span>
            <span>Contact Us</span>
          </span>
        </a>
      </div>
    </Transition>
  </nav>
</template>

<script setup lang="ts">
import { ref } from "vue";

// ref() creates a reactive value. When menuOpen changes,
// Vue automatically updates the DOM — you don't manually
// touch any HTML elements yourself.
const menuOpen = ref<boolean>(false);

// Defining the shape of a nav item using a TypeScript interface.
// This means if you accidentally write { lable: '...' } instead
// of { label: '...' }, TypeScript will flag it immediately.
interface NavItem {
  label: string;
  href: string;
}

const navItems: NavItem[] = [
  { label: "Our Story", href: "#story" },
  { label: "Products", href: "#products" },
  { label: "Our Promise", href: "#promise" },
  { label: "Find Us", href: "#findUs" },
  { label: "Partnerships", href: "#partner" },
];
</script>

<style scoped>
/* scoped means these styles ONLY apply to this component.
   They won't leak out and accidentally affect other elements. */

.nav-link {
  position: relative;
  display: inline-block;
  overflow: hidden;
  height: 1.2em;
}

.nav-text {
  display: inline-flex;
  flex-direction: column;
  transition: transform 0.38s cubic-bezier(0.65, 0, 0.35, 1);
}

.nav-link:hover .nav-text {
  transform: translateY(-50%);
}

.nav-link:hover {
  font-weight: 700;
}

.contact-btn {
  position: relative;
  overflow: hidden;
  height: 2.5rem; /* fixed height */
  padding: 0 1.25rem; /* horizontal padding */
  line-height: 2.5rem; /* center vertically */
  background-color: #000; /* keep your yellow */
  color: #fff; /* keep your dark text */
  font-weight: 600;
  border-radius: 20px;
}

.contact-text {
  display: inline-flex;
  flex-direction: column;
  transition: transform 0.68s cubic-bezier(0.65, 0, 0.35, 1);
}

.contact-btn:hover .contact-text {
  transform: translateY(-50%);
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.25s ease, transform 0.25s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
  transform: translateY(-8px);
}

.fade-enter-to,
.fade-leave-from {
  opacity: 1;
  transform: translateY(0);
}
</style>
