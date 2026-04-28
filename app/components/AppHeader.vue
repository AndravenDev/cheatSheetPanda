<script setup lang="ts">
const scrolled = ref(false)
const menuOpen = ref(false)

function onScroll() {
  scrolled.value = window.scrollY > 20
}

onMounted(() => window.addEventListener('scroll', onScroll, { passive: true }))
onUnmounted(() => window.removeEventListener('scroll', onScroll))

const navLinks = [
  { label: 'Browse', href: '/' },
  { label: 'Submit', href: '/' },
  { label: 'Pricing', href: '/' },
  { label: 'CheatSheet', href: '/cheatsheet' },
]
</script>

<template>
  <header
    class="fixed top-0 left-0 right-0 z-50 border-b border-white/5 transition-all duration-300"
    :class="scrolled || menuOpen
      ? 'bg-navy-deep backdrop-blur-lg'
      : 'bg-navy-deep backdrop-blur-md'"
  >
    <div class="max-w-7xl mx-auto px-4 h-16 flex items-center gap-8">

      <!-- Logo group -->
      <div class="flex items-center gap-2 shrink-0">
        <img src="/pandaLogo.png" alt="Panda logo" class="w-24 h-24 object-contain" aria-hidden="true" />
        <span class="font-bold tracking-wide text-base sm:text-xl md:text-2xl lg:text-3xl text-white">CHEATSHEET</span>
        <span class="font-bold tracking-wide text-base sm:text-xl md:text-2xl lg:text-3xl text-teal-glow">PANDA</span>
      </div>

      <!-- Desktop: nav + CTA -->
      <div class="ml-auto hidden md:flex items-center gap-6">
        <nav class="flex items-center gap-6" aria-label="Main navigation">
          <a
            v-for="link in navLinks"
            :key="link.label"
            :href="link.href"
            class="text-sm text-gray-300 hover:text-white transition-colors duration-200"
          >
            {{ link.label }}
          </a>
        </nav>
        <button
          type="button"
          class="shrink-0 px-5 py-2 bg-mint text-navy-deep text-sm font-semibold rounded-full hover:scale-105 active:scale-95 transition-transform duration-200 focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-mint/60"
        >
          Get Started — Free
        </button>
      </div>

      <!-- Mobile: hamburger -->
      <button
        type="button"
        class="ml-auto md:hidden text-gray-300 hover:text-white focus-visible:outline-none"
        :aria-expanded="menuOpen"
        aria-label="Toggle menu"
        @click="menuOpen = !menuOpen"
      >
        <Icon :name="menuOpen ? 'lucide:x' : 'lucide:menu'" size="22" />
      </button>
    </div>

    <!-- Mobile menu dropdown -->
    <div
      v-if="menuOpen"
      class="md:hidden border-t border-white/5 bg-navy-deep/95 backdrop-blur-lg px-6 pb-5 pt-3 flex flex-col gap-4"
    >
      <nav class="flex flex-col gap-3" aria-label="Mobile navigation">
        <a
          v-for="link in navLinks"
          :key="link.label"
          :href="link.href"
          class="text-sm text-gray-300 hover:text-white transition-colors duration-200"
          @click="menuOpen = false"
        >
          {{ link.label }}
        </a>
      </nav>
      <button
        type="button"
        class="self-start px-5 py-2 bg-mint text-navy-deep text-sm font-semibold rounded-full hover:scale-105 active:scale-95 transition-transform duration-200 focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-mint/60"
      >
        Get Started — Free
      </button>
    </div>
  </header>
</template>
