<script setup lang="ts">
const scrolled = ref(false)

function onScroll() {
  scrolled.value = window.scrollY > 20
}

onMounted(() => window.addEventListener('scroll', onScroll, { passive: true }))
onUnmounted(() => window.removeEventListener('scroll', onScroll))

const navLinks = ['Browse', 'Submit', 'Pricing', 'Blog']
</script>

<template>
  <header
    class="fixed top-0 left-0 right-0 z-50 border-b border-white/5 transition-all duration-300"
    :class="scrolled
      ? 'bg-navy-deep/95 backdrop-blur-lg'
      : 'bg-navy-deep/60 backdrop-blur-md'"
  >
    <div class="max-w-7xl mx-auto px-6 h-16 flex items-center gap-8">

      <!-- Logo group -->
      <div class="flex items-center gap-2 shrink-0">
        <!-- Placeholder panda icon — replace src with /panda-logo.png when ready -->
        <div
          class="w-8 h-8 rounded-full bg-navy-light border border-white/10 flex items-center justify-center text-base leading-none"
          aria-hidden="true"
        >
          🐼
        </div>
        <Icon name="lucide:code-2" class="text-teal-glow" size="18" aria-hidden="true" />
        <span class="font-bold tracking-wide text-sm text-white">CHEATSHEET</span>
        <span class="font-bold tracking-wide text-sm text-teal-glow">PANDA</span>
      </div>

      <!-- Nav links + CTA grouped on the right -->
      <div class="ml-auto flex items-center gap-6">
        <nav class="hidden md:flex items-center gap-6" aria-label="Main navigation">
          <a
            v-for="link in navLinks"
            :key="link"
            href="#"
            class="text-sm text-gray-300 hover:text-white transition-colors duration-200"
          >
            {{ link }}
          </a>
        </nav>

        <!-- CTA button -->
        <button
          type="button"
          class="shrink-0 px-5 py-2 bg-mint text-navy-deep text-sm font-semibold rounded-full hover:scale-105 active:scale-95 transition-transform duration-200 focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-mint/60"
        >
          Get Started — Free
        </button>
      </div>

    </div>
  </header>
</template>
