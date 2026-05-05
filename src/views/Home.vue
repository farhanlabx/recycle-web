<template>
  <div class="bg-[#25343f]">
    <div class="relative w-full h-screen overflow-hidden">
      <Navbar />
      <h3
        class="absolute bottom-12 left-12 z-20 flex flex-col text-white text-6xl font-bold tracking-tight font-poppins leading-tight"
      >
        Recycling Shouldn’t <br> Be<span class="text-[#16A34A] drop-shadow-[0_0_12px_rgba(34,197,94,0.4)]"
        >Hard To Find
        </span>
      </h3>
      <video
        src="/trash-hero.mp4"
        autoplay
        muted
        loop
        playsinline
        class="absolute top-0 left-0 w-full h-full object-cover"
      ></video>
      <div class="absolute inset-0 flex items-end justify-end p-12 z-50">
        <button
          class="bg-green-600 hover:bg-green-700 text-white px-6 py-3 rounded-lg font-bold text-sm"
        >
          Find Nearby Locations
        </button>
      </div>
    </div>

    <div class="container bg-[#25343f] text-white w-full flex h-screen">
      <div
        class="Headline-Recycle text-center content-evenly w-185 h-134 m-auto"
      >
        <div
          class="split-text text-8xl font-mocha-choco tracking-tighter -rotate-5 w-100"
        >
          PEOPLE
        </div>
        <div
          class="split-text text-8xl font-mocha-choco tracking-tighter -rotate-6 relative -top-9 left-55 w-105"
        >
          WANT TO
        </div>
        <div
          class="split-text text-8xl font-mocha-choco tracking-tighter rotate-5 relative -top-7 w-120"
        >
          RECYCLE.
        </div>
        <div
          class="split-text text-8xl font-mocha-choco tracking-tighter my-3 relative -top-10 left-20 w-150"
        >
          THE SYSTEM
        </div>
        <div
          class="split-text text-8xl font-mocha-choco tracking-tighter rotate-5 relative -top-10 -left-2 -mt-5 w-70"
        >
          JUST
        </div>
        <div
          class="split-text text-8xl font-mocha-choco tracking-tighter relative -top-32 left-68 w-115"
        >
          MAKES IT
        </div>
        <div
          class="split-text text-8xl font-mocha-choco tracking-tighter relative -top-32 left-40 w-80"
        >
          HARD.
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
// Gsap Animation scroll

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
      i * 0.4,
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
