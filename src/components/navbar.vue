<template>
  <nav
    class="fixed top-0 left-0 right-0 z-50 flex items-center justify-between px-8 py-5 transition-all duration-500"
    :class="scrolled ? 'bg-black/60 backdrop-blur-md border-b border-white/10' : 'bg-transparent'"
  >
  
    <div class="flex items-center gap-2 flex-1">
      <span class="text-white font-black text-lg tracking-tight">
        ♻ <span class="font-light">recycle</span><span class="text-green-400">web</span>
      </span>
    </div>

    <div class="hidden md:flex items-center gap-8">
      <a
        v-for="link in navLinks"
        :key="link.label"
        :href="link.href"
        class="text-white/70 hover:text-white text-sm font-medium tracking-wide transition-colors duration-200 relative group"
      >
        {{ link.label }}
        <span class="absolute -bottom-0.5 left-0 w-0 h-px bg-green-400 transition-all duration-300 group-hover:w-full" />
      </a>
    </div>

    <div class="flex items-center gap-3 flex-1 justify-end relative">
      <div class="relative" data-lang>
        <button
          class="flex items-center gap-1.5 text-white/60 hover:text-white text-sm transition-colors duration-200 px-2 py-1 rounded-md hover:bg-white/10"
          @click.stop="langOpen = !langOpen"
        >
          <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5"
              d="M12 21a9 9 0 1 0 0-18 9 9 0 0 0 0 18Zm0 0c2.485 0 4-4.03 4-9s-1.515-9-4-9m0 18c-2.485 0-4-4.03-4-9s1.515-9 4-9M3 12h18" />
          </svg>
          <span class="font-mono text-xs tracking-wider">{{ currentLang }}</span>
          <svg
            class="w-3 h-3 opacity-50 transition-transform duration-200"
            :class="langOpen ? 'rotate-180' : ''"
            fill="none" stroke="currentColor" viewBox="0 0 24 24"
          >
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7" />
          </svg>
        </button>

        <transition name="dropdown">
          <div
            v-if="langOpen"
            class="absolute top-10 right-0 bg-black/90 backdrop-blur-xl border border-white/10 rounded-xl overflow-hidden shadow-2xl min-w-[140px]"
          >
            <button
              v-for="lang in langs"
              :key="lang.code"
              class="flex items-center gap-3 w-full px-4 py-2.5 text-sm text-white/70 hover:text-white hover:bg-white/10 transition-colors text-left"
              @click="selectLang(lang)"
            >
              <span>{{ lang.flag }}</span>
              <span>{{ lang.label }}</span>
              <span v-if="currentLang === lang.code" class="ml-auto text-green-400 text-xs">✓</span>
            </button>
          </div>
        </transition>
      </div>

      <div class="w-px h-4 bg-white/20" />

      <a
        href="#"
        class="text-white/70 hover:text-white text-sm font-medium transition-colors duration-200 px-3 py-1.5 rounded-lg hover:bg-white/10"
      >
        Sign In
      </a>

      <a
        href="#"
        class="text-sm font-semibold bg-green-500 hover:bg-green-400 text-black px-4 py-1.5 rounded-full transition-all duration-200 hover:scale-105 active:scale-95 shadow-lg shadow-green-500/25"
      >
        Sign Up
      </a>
    </div>
  </nav>
</template>

<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue'

const scrolled  = ref(false)
const langOpen  = ref(false)
const currentLang = ref('EN')

const navLinks = [
  { label: 'Home',    href: '#' },
  { label: 'About',  href: '#' },
  { label: 'Stories',href: '#' },
  { label: 'Contact',href: '#' },
]

const langs = [
  { code: 'EN', label: 'English',   flag: '🇺🇸' },
  { code: 'ID', label: 'Indonesia', flag: '🇮🇩' },
  { code: 'ZH', label: '中文',      flag: '🇨🇳' },
]

function onScroll() {
  scrolled.value = window.scrollY > 20
}

function onClickOutside(e) {
  if (!e.target.closest('[data-lang]')) {
    langOpen.value = false
  }
}

function selectLang(lang) {
  currentLang.value = lang.code
  langOpen.value = false
}

onMounted(() => {
  window.addEventListener('scroll', onScroll, { passive: true })
  window.addEventListener('click', onClickOutside)
})

onBeforeUnmount(() => {
  window.removeEventListener('scroll', onScroll)
  window.removeEventListener('click', onClickOutside)
})
</script>

<style scoped>
.dropdown-enter-active,
.dropdown-leave-active {
  transition: opacity 0.15s ease, transform 0.15s ease;
}
.dropdown-enter-from,
.dropdown-leave-to {
  opacity: 0;
  transform: translateY(-6px);
}
</style>
