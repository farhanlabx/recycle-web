<template>
  <div class="relative flex flex-col w-full h-screen overflow-hidden" style="background: #050810;">
    <Navbar />


  </div>

  <div class="container bg-[#050810] text-white w-full flex h-screen">
    <div class="Headline-Recycle text-center content-evenly w-185 h-134 m-auto">
      <div class="split-text text-8xl font-mocha-choco tracking-tighter -rotate-5 w-100">PEOPLE</div>
      <div class="split-text text-8xl font-mocha-choco tracking-tighter -rotate-6 relative -top-9 left-55 w-105">WANT TO
      </div>
      <div class="split-text text-8xl font-mocha-choco tracking-tighter rotate-5 relative -top-7 w-120">RECYCLE.</div>
      <div class="split-text text-8xl font-mocha-choco tracking-tighter my-3 relative -top-10 left-20 w-150">THE SYSTEM
      </div>
      <div class="split-text text-8xl font-mocha-choco tracking-tighter rotate-5 relative -top-10 -left-2 -mt-5 w-70">
        JUST</div>
      <div class="split-text text-8xl font-mocha-choco tracking-tighter relative -top-32 left-68 w-115">MAKES IT</div>
      <div class="split-text text-8xl font-mocha-choco tracking-tighter relative -top-32 left-40 w-80">HARD.</div>
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
  const texts = document.querySelectorAll('.split-text');

  // 🔥 Ambil posisi sekarang, lalu kasih offset dikit
  gsap.set(texts, {
    opacity: 0,
    y: 40, // offset dari posisi asli (bukan overwrite layout)
  });

  let tl = gsap.timeline({
    scrollTrigger: {
      trigger: ".container",
      start: "top top",
      end: "+=" + (texts.length * 400),
      scrub: true,
      pin: true,
      pinSpacing: true
    }
  });

  texts.forEach((el, i) => {
    tl.to(el, {
      opacity: 1,
      y: 0,
      duration: 1,
      ease: "power2.out"
    }, i * 0.4);
  });
});

// import nav 

import Navbar from '../components/navbar.vue'
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
