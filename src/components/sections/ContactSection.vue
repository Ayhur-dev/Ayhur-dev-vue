<!-- src/components/sections/ContactSection.vue -->

<template>
  <section id="contact" class="relative bg-brand-dark overflow-hidden py-24">
    <!-- Decorative animated background circles.
         These are purely visual — large blurred circles that
         slowly drift giving the dark background depth and life. -->
    <div class="absolute inset-0 pointer-events-none overflow-hidden">
      <div class="glow-circle glow-1"></div>
      <div class="glow-circle glow-2"></div>
      <div class="glow-circle glow-3"></div>
    </div>

    <!-- Decorative large text watermark behind content -->
    <div
      class="absolute inset-0 flex items-center justify-center pointer-events-none select-none overflow-hidden"
    >
      <span
        class="font-display text-[20vw] text-white/[0.02] tracking-widest whitespace-nowrap"
      >
        CONNECT
      </span>
    </div>

    <div class="relative z-10 max-w-7xl mx-auto px-4 sm:px-8">
      <!-- Section heading — animated in by GSAP -->
      <div ref="headingRef" class="mb-20 opacity-0">
        <p
          class="text-xs uppercase tracking-[0.4em] text-brand-yellow font-semibold mb-4"
        >
          Get In Touch
        </p>
        <h2
          class="font-display text-6xl lg:text-8xl text-white tracking-wider leading-none"
        >
          LET'S<br />
          <span class="text-brand-yellow">CONNECT.</span>
        </h2>
      </div>

      <div class="grid lg:grid-cols-2 gap-20 items-start">
        <!-- Left: contact info cards -->
        <div ref="infoRef" class="opacity-0 space-y-6">
          <!-- Info cards -->
          <div
            v-for="info in contactInfo"
            :key="info.label"
            class="info-card flex items-center gap-5 p-5 border border-white/10 hover:border-brand-yellow/60 transition-all duration-500 group cursor-default"
          >
            <!-- Icon bubble -->
            <div
              class="w-12 h-12 bg-brand-yellow/10 border border-brand-yellow/20 flex items-center justify-center shrink-0 group-hover:bg-brand-yellow group-hover:scale-110 transition-all duration-300"
            >
              <img :src="info.icon" alt="" class="w-5 h-5 object-contain" />
            </div>
            <div>
              <p
                class="text-[10px] uppercase tracking-[0.3em] text-white/30 mb-1"
              >
                {{ info.label }}
              </p>
              <p class="text-sm text-white/80 font-medium">{{ info.value }}</p>
            </div>
          </div>

          <!-- Divider -->
          <div class="w-full h-px bg-white/10 my-8"></div>

          <!-- Social links -->
          <div>
            <p
              class="text-[10px] uppercase tracking-[0.3em] text-white/30 mb-4"
            >
              Follow Us
            </p>
            <div class="flex gap-3">
              <a
                v-for="social in socials"
                :key="social.label"
                :href="social.href"
                class="social-btn w-11 h-11 border border-white/20 flex items-center justify-center text-xs font-bold text-white/40 hover:border-brand-yellow hover:text-brand-yellow hover:bg-brand-yellow/10 transition-all duration-300"
              >
                {{ social.label }}
              </a>
            </div>
          </div>

          <!-- Decorative yellow line that animates width on scroll -->
          <div class="pt-8">
            <div
              ref="lineRef"
              class="h-px bg-brand-yellow origin-left"
              style="width: 0%"
            ></div>
          </div>
        </div>

        <!-- Right: contact form -->
        <div ref="formRef" class="opacity-0">
          <div class="space-y-5">
            <!-- Name + Email row -->
            <div class="grid sm:grid-cols-2 gap-5">
              <div class="form-field-wrapper">
                <label class="form-label">Your Name</label>
                <input
                  v-model="formData.name"
                  type="text"
                  placeholder="John Doe"
                  class="form-input"
                  @focus="handleFocus"
                  @blur="handleBlur"
                />
              </div>
              <div class="form-field-wrapper">
                <label class="form-label">Email Address</label>
                <input
                  v-model="formData.email"
                  type="email"
                  placeholder="john@example.com"
                  class="form-input"
                  @focus="handleFocus"
                  @blur="handleBlur"
                />
              </div>
            </div>

            <!-- Custom dropdown.
                 We build our own instead of a native <select>
                 so we can style it fully — native selects can't
                 be styled deeply across browsers. -->
            <div class="form-field-wrapper relative" ref="dropdownRef">
              <label class="form-label">I'm Interested In</label>
              <button
                @click="dropdownOpen = !dropdownOpen"
                type="button"
                class="form-input flex items-center justify-between text-left"
                :class="formData.interest ? 'text-white' : 'text-white/30'"
              >
                <span>{{ formData.interest || "Select an option..." }}</span>
                <!-- Animated chevron rotates when open -->
                <span
                  class="text-brand-yellow transition-transform duration-300 text-lg"
                  :class="dropdownOpen ? 'rotate-180' : ''"
                >
                  ▾
                </span>
              </button>

              <!-- Dropdown options panel.
                   v-show keeps it in DOM for smooth transition.
                   z-50 ensures it floats above other fields. -->
              <div
                v-show="dropdownOpen"
                class="absolute top-full left-0 right-0 z-50 bg-[#111] border border-brand-yellow/30 mt-1 overflow-hidden transition-all duration-300"
              >
                <button
                  v-for="option in interestOptions"
                  :key="option"
                  @click="selectOption(option)"
                  type="button"
                  class="w-full text-left px-4 py-3 text-sm text-white/70 hover:bg-brand-yellow hover:text-brand-dark font-medium transition-colors duration-150 border-b border-white/5 last:border-0"
                >
                  {{ option }}
                </button>
              </div>
            </div>

            <!-- Phone -->
            <div class="form-field-wrapper">
              <label class="form-label"
                >Phone Number
                <span class="text-white/20">(optional)</span></label
              >
              <input
                v-model="formData.phone"
                type="tel"
                placeholder="+1 234 567 8900"
                class="form-input"
                @focus="handleFocus"
                @blur="handleBlur"
              />
            </div>

            <!-- Message -->
            <div class="form-field-wrapper">
              <label class="form-label">Your Message</label>
              <textarea
                v-model="formData.message"
                rows="5"
                placeholder="Tell us what you have in mind..."
                class="form-input resize-none"
                @focus="handleFocus"
                @blur="handleBlur"
              ></textarea>
            </div>

            <!-- Submit button with animated state -->
            <button
              @click="handleSubmit"
              :disabled="submitted"
              class="submit-btn w-full py-4 font-semibold text-sm uppercase tracking-widest transition-all duration-500 relative overflow-hidden"
              :class="
                submitted
                  ? 'bg-white/10 text-white/40 cursor-not-allowed'
                  : 'bg-brand-yellow text-brand-dark hover:bg-yellow-400'
              "
            >
              <!-- Shimmer effect on hover -->
              <span class="shimmer"></span>
              <span class="relative z-10">
                {{ submitted ? "✓ Message Sent!" : "Send Message" }}
              </span>
            </button>
          </div>
        </div>
      </div>
    </div>
  </section>

  <!-- Footer bar -->
  <footer ref="footerRef" class="bg-black py-10 opacity-0">
    <div
      class="max-w-7xl mx-auto px-4 sm:px-8 flex flex-col md:flex-row items-center justify-between gap-6"
    >
      <!-- Logo -->
      <div class="flex flex-col items-center md:items-start gap-1">
        <span class="font-display text-2xl text-white/60 tracking-widest"
          >金枕榴</span
        >
        <span class="text-[10px] text-white/20 uppercase tracking-widest"
          >AYHUR-DEV · Pure Durian Joy</span
        >
      </div>

      <!-- Nav links -->
      <div class="flex flex-wrap gap-6 justify-center">
        <a
          v-for="link in footerLinks"
          :key="link.label"
          :href="link.href"
          class="text-xs text-white/30 uppercase tracking-widest hover:text-brand-yellow transition-colors duration-200"
        >
          {{ link.label }}
        </a>
      </div>

      <p class="text-xs text-white/20 uppercase tracking-widest">
        © 2026 Ayhur-dev.
      </p>
    </div>
  </footer>
</template>

<script setup lang="ts">
import { ref, reactive, onMounted, onUnmounted } from "vue";
import { gsap } from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";

import emailIcon from "@/assets/icons/mail.png";
import locationIcon from "@/assets/icons/map.png";
import phoneIcon from "@/assets/icons/telephone.png";
import clockIcon from "@/assets/icons/wall-clock.png";

// Register the ScrollTrigger plugin with GSAP.
// Without this, ScrollTrigger won't work even if imported.
gsap.registerPlugin(ScrollTrigger);

// Template refs — these give us direct access to DOM elements
// so GSAP can animate them.
const headingRef = ref<HTMLElement | null>(null);
const infoRef = ref<HTMLElement | null>(null);
const formRef = ref<HTMLElement | null>(null);
const lineRef = ref<HTMLElement | null>(null);
const footerRef = ref<HTMLElement | null>(null);
const dropdownRef = ref<HTMLElement | null>(null);

const dropdownOpen = ref<boolean>(false);
const submitted = ref<boolean>(false);

interface FormData {
  name: string;
  email: string;
  interest: string;
  phone: string;
  message: string;
}

const formData = reactive<FormData>({
  name: "",
  email: "",
  interest: "",
  phone: "",
  message: "",
});

const interestOptions: string[] = [
  "Partnership / Distribution",
  "Bulk Orders",
  "Product Inquiry",
  "General Inquiry",
];

const contactInfo = [
  { icon: emailIcon, label: "Email Us", value: "info@jinzhenlian.com" },
  { icon: locationIcon, label: "Headquarters", value: "Bangkok, Thailand" },
  { icon: phoneIcon, label: "Call Us", value: "+66 (0) 00 000 0000" },
  {
    icon: clockIcon,
    label: "Working Hours",
    value: "Mon – Fri, 9AM – 6PM ICT",
  },
];

const socials = [
  { label: "FB", href: "#" },
  { label: "IG", href: "#" },
  { label: "LI", href: "#" },
  { label: "YT", href: "#" },
];

const footerLinks = [
  { label: "About", href: "#about" },
  { label: "Products", href: "#products" },
  { label: "Partner", href: "#partner" },
  { label: "FAQ", href: "#faq" },
  { label: "Contact", href: "#contact" },
];

function selectOption(option: string): void {
  formData.interest = option;
  dropdownOpen.value = false;
}

// Close dropdown when clicking outside of it
function handleClickOutside(e: MouseEvent): void {
  if (dropdownRef.value && !dropdownRef.value.contains(e.target as Node)) {
    dropdownOpen.value = false;
  }
}

// Input focus/blur — GSAP animates the border color
function handleFocus(e: FocusEvent): void {
  const input = e.target as HTMLElement;
  gsap.to(input, {
    borderColor: "#F5C800",
    duration: 0.3,
    ease: "power2.out",
  });
}

function handleBlur(e: FocusEvent): void {
  const input = e.target as HTMLElement;
  gsap.to(input, {
    borderColor: "rgba(255,255,255,0.1)",
    duration: 0.3,
    ease: "power2.out",
  });
}

function handleSubmit(): void {
  if (!formData.name || !formData.email || !formData.message) {
    gsap.to(formRef.value, {
      keyframes: [
        { x: -10 },
        { x: 10 },
        { x: -8 },
        { x: 8 },
        { x: -4 },
        { x: 4 },
        { x: 0 },
      ],
      duration: 0.5,
      ease: "power2.out",
    });

    return;
  }

  console.log("Form submitted:", formData);
  submitted.value = true;

  // Animate the button on success
  gsap.from(".submit-btn", {
    scale: 0.95,
    duration: 0.3,
    ease: "back.out(2)",
  });
}

onMounted(() => {
  document.addEventListener("click", handleClickOutside);

  // Wait until everything (images/fonts) is loaded, then refresh ScrollTrigger
  window.addEventListener("load", () => {
    ScrollTrigger.refresh();
  });

  // ── GSAP ANIMATIONS ──
  // Set initial states
  gsap.set([headingRef.value, infoRef.value, formRef.value, lineRef.value, footerRef.value], { opacity: 0, y: 20 });
  gsap.set(infoRef.value?.querySelectorAll(".info-card") || [], { opacity: 0, x: -30 });
gsap.set(formRef.value?.querySelectorAll(".form-field-wrapper") || [], { opacity: 0, y: 20 });
  gsap.set(".social-btn", { opacity: 0, scale: 0.5 });

  // Heading animation
  gsap.to(headingRef.value, {
    opacity: 1,
    y: 0,
    duration: 1,
    ease: "power3.out",
    scrollTrigger: {
      trigger: headingRef.value,
      start: "top 85%",
      once: true, // trigger only once
    },
  });

  // Info container animation
  gsap.to(infoRef.value, {
    opacity: 1,
    x: 0,
    duration: 0.9,
    ease: "power3.out",
    scrollTrigger: {
      trigger: infoRef.value,
      start: "top 80%",
      once: true,
    },
  });

  // Info cards stagger in
gsap.to(infoRef.value?.querySelectorAll(".info-card") || [], {
  opacity: 1,
  x: 0,
  duration: 0.6,
  stagger: 0.12,
  ease: "power2.out",
  scrollTrigger: {
    trigger: infoRef.value,
    start: "top 80%",
  },
});


  // Yellow line grows
  gsap.to(lineRef.value, {
    width: "100%",
    duration: 1.5,
    ease: "power3.inOut",
    scrollTrigger: {
      trigger: lineRef.value,
      start: "top 90%",
      once: true,
    },
  });

  // Form slides in
  gsap.to(formRef.value, {
    opacity: 1,
    x: 0,
    duration: 0.9,
    ease: "power3.out",
    scrollTrigger: {
      trigger: formRef.value,
      start: "top 80%",
      once: true,
    },
  });

  // Form fields stagger
  gsap.to(formRef.value?.querySelectorAll(".form-field-wrapper") || [], {
  opacity: 1,
  y: 0,
  stagger: 0.1,
  duration: 0.5,
  ease: "power2.out",
  scrollTrigger: {
    trigger: formRef.value,
    start: "top 75%",
    once: true,
  },
});

  // Footer fade in
  gsap.to(footerRef.value, {
    opacity: 1,
    y: 0,
    duration: 0.8,
    ease: "power2.out",
    scrollTrigger: {
      trigger: footerRef.value,
      start: "top 95%",
      once: true,
    },
  });

  // Social buttons stagger
  gsap.to(".social-btn", {
    opacity: 1,
    scale: 1,
    stagger: 0.08,
    duration: 0.4,
    ease: "back.out(2)",
    scrollTrigger: {
      trigger: infoRef.value,
      start: "top 70%",
      once: true,
    },
  });
});

onMounted(() => {
  document.addEventListener("click", handleClickOutside);

  // Refresh ScrollTrigger after images or fonts load
  window.addEventListener("load", () => {
    ScrollTrigger.refresh();
  });

  // Your existing GSAP animations...
});
</script>

<style scoped>
/* Glowing background circles that drift slowly */
.glow-circle {
  position: absolute;
  border-radius: 50%;
  filter: blur(80px);
  opacity: 0.15;
  animation: drift 12s ease-in-out infinite alternate;
}

.glow-1 {
  width: 400px;
  height: 400px;
  background: #f5c800;
  top: -100px;
  left: -100px;
  animation-delay: 0s;
}

.glow-2 {
  width: 300px;
  height: 300px;
  background: #f5c800;
  bottom: 0;
  right: 10%;
  animation-delay: -4s;
}

.glow-3 {
  width: 200px;
  height: 200px;
  background: #fff;
  top: 40%;
  left: 40%;
  animation-delay: -8s;
  opacity: 0.03;
}

@keyframes drift {
  from {
    transform: translate(0, 0) scale(1);
  }
  to {
    transform: translate(30px, 40px) scale(1.1);
  }
}

/* Form input base styles */
.form-label {
  display: block;
  font-size: 10px;
  text-transform: uppercase;
  letter-spacing: 0.3em;
  color: rgba(255, 255, 255, 0.4);
  margin-bottom: 8px;
  font-weight: 600;
}

.form-input {
  width: 100%;
  background: rgba(255, 255, 255, 0.04);
  border: 1px solid rgba(255, 255, 255, 0.1);
  color: white;
  padding: 14px 16px;
  font-size: 14px;
  outline: none;
  transition: border-color 0.3s ease;
  font-family: "DM Sans", sans-serif;
}

.form-input::placeholder {
  color: rgba(255, 255, 255, 0.2);
}

/* Shimmer sweep effect on the submit button */
.shimmer {
  position: absolute;
  inset: 0;
  background: linear-gradient(
    105deg,
    transparent 40%,
    rgba(255, 255, 255, 0.3) 50%,
    transparent 60%
  );
  transform: translateX(-100%);
  transition: transform 0s;
}

.submit-btn:hover .shimmer {
  transform: translateX(100%);
  transition: transform 0.6s ease;
}
</style>
