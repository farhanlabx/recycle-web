<template>
  <div>
    <div class="relative w-full h-screen overflow-hidden flex items-end p-10 flex-row justify-between">
      <Navbar />
      <div class="absolute inset-0 -z-1">
        <video src="/trash-hero.mp4" autoplay muted loop playsinline class="object-cover w-full h-screen"></video>
        <div class="bg-linear-to-b from-transparent to-black/70 absolute inset-0 w-full h-full"></div>
      </div>

      <h1 class="text-white font-black leading-[1.04] tracking-tight text-7xl">
        Recycling Shouldn't<br />
        Be
        <div class="inline-flex items-center justify-center">
          <span class="absolute text-[#9edab4] mx-auto blur-xl text-start font-bold">Hard To Find.</span>
          <span class="relative text-[#22c55e] font-bold text-start">Hard To Find.</span>
        </div>
      </h1>

      <div class="flex flex-col relative gap-4 max-w-[26rem]">
        <p class="text-white">
          Discover nearby recycling centers, learn what you can recycle, and
          make sustainable living part of everyday life.
        </p>
        <div class="flex gap-3 w-full">
          <button class="bg-green-600 hover:bg-green-700 text-white px-6 py-3 rounded-lg font-bold text-sm flex-1">
            📍 Find Nearby Locations
          </button>
          <button class="bg-transparent border-2 border-gray-400 text-white px-5 py-2.5 rounded-lg font-bold text-sm">
            Explore Materials
          </button>
        </div>
      </div>
    </div>

    <div class="container bg-[#25343f] text-white w-full flex h-screen">
      <div class="Headline-Recycle text-center content-evenly max-w-6xl h-134 m-auto w-185">
        <div class="split-text text-8xl font-mocha-choco tracking-tighter -rotate-5 w-100">
          PEOPLE
        </div>
        <div class="split-text text-8xl font-mocha-choco tracking-tighter -rotate-6 relative -top-9 left-55 w-105">
          WANT TO
        </div>
        <div class="split-text text-8xl font-mocha-choco tracking-tighter rotate-5 relative -top-7 w-120">
          RECYCLE.
        </div>
        <div class="split-text text-8xl font-mocha-choco tracking-tighter my-3 relative -top-10 left-20 w-150">
          THE SYSTEM
        </div>
        <div class="split-text text-8xl font-mocha-choco tracking-tighter rotate-5 relative -top-10 -left-2 -mt-5 w-70">
          JUST
        </div>
        <div class="split-text text-8xl font-mocha-choco tracking-tighter relative -top-32 left-68 w-115">
          MAKES IT
        </div>
        <div class="split-text text-8xl font-mocha-choco tracking-tighter relative -top-32 left-40 w-80">
          HARD.
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { onMounted } from "vue";
import { gsap } from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";

gsap.registerPlugin(ScrollTrigger);

onMounted(() => {
  const texts = document.querySelectorAll(".split-text");

  // 🔥 Ambil posisi sekarang, lalu kasih offset dikit
  gsap.set(texts, {
    opacity: 0,
    y: 40, // offset dari posisi asli (bukan overwrite layout)
  });

  let tl = gsap.timeline({
    scrollTrigger: {
      trigger: ".container",
      start: "top top",
      end: "+=" + texts.length * 400,
      scrub: true,
      pin: true,
      pinSpacing: true,
    },
  });

  texts.forEach((el, i) => {
    tl.to(
      el,
      {
        opacity: 1,
        y: 0,
        duration: 1,
        ease: "power2.out",
      },
      i * 1,
    );
  });
});

// import nav

import Navbar from "../components/navbar.vue";
</script>

<style scoped>
@keyframes spin {
  from {
    transform: rotate(0deg);
  }

  to {
    transform: rotate(360deg);
  }
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.6s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>
