<!-- src/components/sections/VideoSection.vue -->

<template>
  <section id="video" class="relative w-full overflow-hidden">
    <!-- Section heading overlaid on top of the video.
         absolute + z-10 floats it above the video layer. -->

    <div
      class="absolute inset-0 z-10 flex flex-col items-start justify-start p-8 sm:p-16 pb-16"
    >
      <p
        class="text-xs uppercase tracking-[0.4em] text-white/70 font-semibold mb-2"
      >
        Watch Us
      </p>
      <h2
        class="font-bold text-2xl lg:text-5xl text-white tracking-wider max-w-lg leading-tight"
      >
        JOYFUL TASTES <br />
        FROM THE LAND <br />
        OF SMILES
      </h2>

      <p
        class="font-[] max-w-[50ch] text-white pl-5 pt-35 text-xs leading-tight"
      >
        Delight in the creamy sweetness and wonderful aroma of the best Thai
        durian. Every Jin Zhen Lian treat is made with fine, fresh fruit from
        the famous seaside orchards of Eastern Thailand. You’ll taste the wow in
        every bite. So share the smiles with the durian lovers in your life.
        It’s pure durian joy!
      </p>
      <div class="absolute right-10 bottom-10">
        <svg viewBox="0 0 500 100" class="w-64 md:w-80">
          <text x="0" y="70" id="pure-joy" class="handwriting">
            Pure durian joy
          </text>
        </svg>
      </div>
    </div>

    <!-- Dark overlay so text is readable over the video.
         Adjust opacity to control how dark it gets. -->
    <div class="absolute inset-0 z-5 bg-black/30"></div>

    <!-- The video itself.
         - autoplay: starts playing immediately on page load
         - muted: required by browsers for autoplay to work
         - loop: restarts when it reaches the end
         - playsinline: prevents iOS from going fullscreen automatically
         - object-cover: fills the entire section like a background image
           without distorting the aspect ratio — it crops instead
         Put your mp4 file inside the /public folder and reference
         it with a leading slash like: src="/your-video.mp4" -->
    <video
      autoplay
      muted
      loop
      playsinline
      class="w-full h-screen object-cover block"
    >
      <source src="/your-video.mp4" type="video/mp4" />
    </video>
  </section>
</template>

<script setup lang="ts">
// No reactive data needed — everything is handled by
// native HTML video attributes
</script>

<style>
#pure-joy {
  font-family: "Satisfy", cursive;
  font-weight: 100;
}

.handwriting {
  fill: none;
  stroke: white;
  stroke-width: 2;
  stroke-dasharray: 500;
  stroke-dashoffset: 500;
  animation: handwriting 20s ease-in-out infinite;
  font-size: 40px;
  font-family: "Caveat", cursive;
}

@keyframes handwriting {
  0% {
    stroke-dashoffset: 500;
  }

  50% {
    stroke-dashoffset: 0;
  }

  80% {
    stroke-dashoffset: 0;
  }

  100% {
    stroke-dashoffset: 500;
  }
}
</style>
