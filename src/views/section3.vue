<template>
  <div class="bg-[#25343f] py-20 flex">
    <div class="max-w-2xl  ml-20">
      <h2 class="text-white text-4xl font-bold mb-6">
        We’ve been there. <br />
        We know what makes people give up.
      </h2>
      <p class="text-gray-400 text-lg">
        Recycling information is scattered, outdated, and confusing.
        People don’t stop because they don’t care. They stop because the process feels frustrating,
        unclear, and inconvenient.
      </p>
    </div>
    <div class="flex justify-end">
    <div class="max-w-xl ml-24 flex flex-col gap-6">
      <div class="sticky top-16 bg-green-400 rounded-3xl p-10">
        <span class="text-3xl inline-block mb-4">🌍</span>
        <h3 class="text-white text-2xl font-semibold tracking-tight mb-2">Where do I even go?</h3>
        <p class="text-gray-500 leading-relaxed">Recycling locations are hard to find. Most people just give up when
          it's not nearby.</p>
      </div>

      <div class="sticky top-24 bg-green-400 rounded-3xl p-10">
        <span class="text-3xl inline-block mb-4">♻️</span>
        <h3 class="text-white text-2xl font-semibold tracking-tight mb-2">Can this be recycled?</h3>
        <p class="text-gray-500 leading-relaxed">Confusing labels make people hesitate. We simplify the rules for every
          material.</p>
      </div>

      <div class="sticky top-32 bg-green-400 rounded-3xl p-10">
        <span class="text-3xl inline-block mb-4">⏱️</span>
        <h3 class="text-white text-2xl font-semibold tracking-tight mb-2">Too much effort</h3>
        <p class="text-gray-500 leading-relaxed">If it’s not easy, it won’t happen. We’re here to cut down the process
          to seconds.</p>
      </div>

      <div class="sticky top-40 bg-green-400 rounded-3xl p-10">
        <span class="text-3xl inline-block mb-4">✨</span>
        <h3 class="text-white text-2xl font-semibold tracking-tight mb-2">Impact matters</h3>
        <p class="text-gray-500 leading-relaxed">Visualize your contribution. Small steps lead to big changes for the
          planet.</p>
      </div>

    </div>
    </div>
  </div>

  <div ref="sectionContainer" class="w-full min-h-[420vh] bg-white z-10 overflow-hidden relative">
    <section class="section-step relative z-10">
      <div class="headline-section-step w-150 text-center m-auto text-7xl mt-10 text-gray-800 relative z-20 bg-white p-5"> So we built a simpler way.</div>
      <div class="step relative z-30 w-90 left-120"><img src="../../public/example-picture-1.png" alt=""></div>
      <div class="add-picture relative z-30 justify-items-center left-50 -top-80"><img src="../../public/additional-picture/additional-element-14.png" alt="" class="w-35"></div>
      <div class="add-picture relative z-30 justify-items-end right-50 -top-110"><img src="../../public/additional-picture/additional-element.png" alt="" class="w-90"></div>
      <div class="add-picture relative z-30 -top-240 left-20"><img src="../../public/additional-picture/additional-element-7.png" alt="" class="w-90"></div>
      <div class="add-picture absolute z-30 left-25 top-290"><img src="../../public/additional-picture/additional-element-10.png" alt="" class="w-90 border-2 border-black rounded-4xl"></div>
      <div class="add-picture absolute z-30 left-25 top-300"><img src="../../public/additional-picture/additional-element-2.png" alt="" class="w-100"></div>
      <div class="add-picture absolute z-30 left-140 top-340"><img src="../../public/additional-picture/additional-element-5.png" alt="" class="w-50 border-2 border-black rounded-4xl"></div>
      <div class="add-picture absolute z-30 justify-items-end right-25 top-250"><img src="../../public/additional-picture/additional-element-3.png" alt="" class="w-60"></div>
      <div class="add-picture absolute z-30 left-140 top-440"><img src="../../public/additional-picture/additional-element-1.png" alt="" class="w-75"></div>
      <div class="add-picture absolute z-30 justify-items-end right-25 top-500"><img src="../../public/additional-picture/additional-element-9.png" alt="" class="w-50 border-2 border-black rounded-4xl"></div>
      <div class="add-picture absolute z-30 justify-items-end right-100 top-550"><img src="../../public/additional-picture/additional-element-17.png" alt="" class="w-20"></div>
      <div class="content-main relative z-50 flex flex-col -mt-160">
        <div class="content flex flex-row-reverse gap-40 justify-center items-center">
          <div class="step text-2xl w-180 bg-gray-600 h-fit rounded-4xl text-white p-5 z-30">1. Find nearby
            recycling locations
            <p>Search based on your area and discover verified recycling spots instantly.</p>
          </div>
          <div class="step w-120 z-30"><img src="../../public/example-step-1.png" alt="example-picture"
              class="border-4 border-black rounded-4xl"></div>
        </div>
        <div class="step relative z-30 w-90 left-195 -top-5"><img src="../../public/example-picture-2.png" alt=""
            class="w-100"></div>
        <div class="content flex flex-row gap-40 justify-center items-center">
          <div class="step text-2xl w-180 bg-gray-600 h-fit rounded-4xl text-white p-5 z-30">2. Choose what you
            want to recycle
            <p>From plastic bottles to old electronics, quickly see what each location accepts.</p>
          </div>
          <div class="step w-120 z-30"><img src="../../public/example-step-2.png" alt="example-picture"
              class="border-4 border-black rounded-4xl"></div>
        </div>
        <div class="step relative z-30 w-80 -top-5 left-40"><img src="../../public/example-picture-3.png" alt=""></div>
        <div class="step flex flex-row-reverse gap-40 justify-center items-center">
          <div class="step text-2xl w-180 bg-gray-600 h-fit rounded-4xl text-white p-5 z-30">3. Get directions and
            details
            <p>Opening hours, distance, instructions, and requirements. All in one place.</p>
          </div>
          <div class="step w-120 z-30"><img src="../../public/example-step-3.png" alt="example-picture"
              class="border-4 border-black rounded-4xl"></div>
        </div>
        <div class="step m-auto relative -bottom-50"><img src="../../public/additional-picture/additional-element-20.png" alt=""></div>
      </div>
      <div class="svg-path absolute inset-0 z-10 pointer-events-none overflow-visible">
        <svg width="752" height="1721" viewBox="-50 -50 852 1821" fill="none" xmlns="http://www.w3.org/2000/svg"
          class="absolute -top-10 h-[400vh] w-full">
          <path id="stroke-path"
            d="M377.5 27.501C401 384.501 27.5 123.501 27.5 411.001C27.5 698.501 722.835 637.001 724.278 865.001C725.575 1070 23.7777 1668 59.7777 1327.5C95.7777 987.001 377.5 1322.52 377.5 1495C377.5 1667.48 377.5 1693 377.5 1693"
            stroke="#00DA28" stroke-width="100" stroke-linecap="round" />
        </svg>
      </div>
    </section>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted, nextTick } from "vue";
import { gsap } from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";
import Lenis from "lenis";

gsap.registerPlugin(ScrollTrigger);

const sectionContainer = ref(null);

let lenis;
let animationFrame;

onMounted(async () => {

  await nextTick();

  // LENIS
  lenis = new Lenis({
    lerp: 0.1,
    smoothWheel: true,
  });

  // RAF
  const raf = (time) => {
    lenis.raf(time);
    animationFrame = requestAnimationFrame(raf);
  };

  animationFrame = requestAnimationFrame(raf);

  // sinkron scroll
  lenis.on("scroll", () => {
    ScrollTrigger.update();
  });

  // kasih delay dikit biar DOM fix dulu
  setTimeout(() => {

    const path = document.querySelector("#stroke-path");

    if (!path) return;

    const pathLength = path.getTotalLength();

    // reset dulu
    gsap.set(path, {
      strokeDasharray: pathLength,
      strokeDashoffset: pathLength,
    });

    // animasi
    gsap.to(path, {
      strokeDashoffset: 0,
      ease: "none",

      scrollTrigger: {
        trigger: sectionContainer.value,

        start: "top 20%",

        end: "bottom bottom",

        scrub: 1.5,

        invalidateOnRefresh: true,
      },
    });

    // STEP ANIMATION
    const steps = gsap.utils.toArray(".step");

    steps.forEach((step, index) => {

      gsap.fromTo(
        step,

        {
          opacity: 0,
          scale: 0.5,
          y: 0,
        },

        {
          opacity: 1,
          scale: 1,
          y: 0,

          duration: 4,

          ease: "back.out(2.5)",

          scrollTrigger: {
            trigger: step,

            start: "top 60%",

            end: "top center",

            scrub: 1,
          },
        }
      );

    });

    ScrollTrigger.refresh();

  }, 300);

});

onUnmounted(() => {

  if (lenis) {
    lenis.destroy();
  }

  cancelAnimationFrame(animationFrame);

  ScrollTrigger.getAll().forEach((trigger) => {
    trigger.kill();
  });

});
</script>