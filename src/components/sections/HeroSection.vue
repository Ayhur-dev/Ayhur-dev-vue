<!-- src/components/sections/HeroSection.vue -->

<template>
  <!-- min-h-screen makes the hero fill the full viewport height.
       pt-16 pushes content down so it doesn't hide behind the
       fixed navbar, which is 16 units (4rem / 64px) tall. -->
  <section
    id="home"
    class="relative min-h-screen pt-4 lg:pt-11 overflow-hidden bg-brand-yellow"
  >
    <!-- Main content grid.
         On large screens it's 2 columns (text left, visual right).
         On mobile it stacks into a single column. -->
    <div
      class="relative z-10 max-w-7xl mx-auto px-4 sm:px-8 lg:px-16 pt-20 pb-16 grid lg:grid-cols-2 gap-12 items-center min-h-[calc(100vh-4rem)] md:grid-cols-2"
    >
      <!-- Left: Text content -->
      <div class="fade-up max-[765px]:text-center">
        <!-- Eyebrow label -->
        <p
          class="lg:text-sm md:text-sm text-xl uppercase tracking-[0.3em] text-brand-dark/60 mb-3"
        >
          金枕榴 · Thailand
        </p>

        <!-- Main headline.
             clamp(4rem, 10vw, 8rem) means: minimum 4rem, scale with
             viewport width, maximum 8rem. This makes it fluid and
             responsive without needing breakpoint classes. -->
        <h1
          class="leading-none text-brand-dark tracking-[1.4rem] mb-3 lg:text-8xl md:text-6xl text-[5rem]"
        >
          PURE<br />DURIAN<br />JOY
        </h1>

        <p
          class="hidden min-[765px]:block text-base text-brand-dark/70 max-w-sm mb-8 leading-relaxed"
        >
          Joyful tastes from the Land of Smiles. Premium Eastern Monthong
          durian, crafted into extraordinary frozen delights.
        </p>
      </div>

      <!-- Right: Visual circle + badge -->
      <div class="fade-up delay-2 flex justify-center items-center relative">
        <!-- Concentric circles create depth and frame the emoji -->

        <div class="w-full flex items-center justify-center">
          <span class="text-[8rem] lg:text-[10rem] select-none">
            <img
              :src="heroImage"
              alt="Hero"
              class="relative z-10 w-full max-w-[clamp(680px,50vw,620px)] mx-auto"
            />
          </span>

          <div
            class="absolute bottom-0 left-1/2 -translate-x-1/2 translate-y-4 w-39 h-7 bg-black blur-xl rounded-full"
          ></div>
        </div>

        <!-- Floating "100% Natural" badge.
             absolute positions it relative to the nearest
             positioned ancestor, which is the outer div above. -->
        <div
          class="absolute top-4 right-4 lg:right-0 bg-brand-dark text-brand-yellow rounded-full w-20 h-20 flex flex-col items-center justify-center text-center"
        >
          <span class="font-display text-xl leading-none">100%</span>
          <span class="text-[9px] uppercase tracking-wider leading-tight"
            >Natural</span
          >
        </div>
      </div>
    </div>

    <div
      @click="scrollToVideo"
      class="absolute lg:bottom-25 bottom-15 sm:bottom-10 left-1/2 -translate-x-1/2 flex flex-col items-center gap-2 z-10 cursor-pointer"
    >
      <span
        class="text-xs text-center uppercase tracking-[0.3em] text-brand-dark/50"
      >
        Scroll to bite <br />
        into joy
      </span>

      <div
        class="mt-4 w-10 h-10 text-3xl flex items-center justify-center rounded-full border border-brand-dark animate-bounce"
      >
        ▿
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
import heroImage from "/src/assets/YellowDragonfruit_DSC05080_1x1.png";
// No props or reactive state needed here — this section is
// purely presentational. The data is static so we define it
// as a plain const, not a ref().

const scrollToVideo = () => {
  const section = document.getElementById("video");

  section?.scrollIntoView({
    behavior: "smooth",
  });
};
</script>

<style scoped>
/* Fade up animation for the hero content on page load */
@keyframes fadeUp {
  from {
    opacity: 0;
    transform: translateY(30px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.fade-up {
  animation: fadeUp 0.7s ease both;
}

/* animation-delay staggers the appearance of elements so they
   don't all pop in at the same time — creates a polished feel */
.delay-2 {
  animation-delay: 0.3s;
}
</style>
