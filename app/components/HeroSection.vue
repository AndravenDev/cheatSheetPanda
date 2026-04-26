<script setup lang="ts">
const searchFocused = ref(false);

// Decorative background symbols — scattered asymmetrically
const codeSymbols = [
  {
    text: "{}",
    style: {
      top: "8%",
      left: "4%",
      fontSize: "1.5rem",
      opacity: "0.12",
      animationDelay: "0s",
    },
  },
  {
    text: "[]",
    style: {
      top: "15%",
      right: "6%",
      fontSize: "1.2rem",
      opacity: "0.10",
      animationDelay: "1s",
    },
  },
  {
    text: "<>",
    style: {
      top: "55%",
      left: "8%",
      fontSize: "1.8rem",
      opacity: "0.08",
      animationDelay: "2s",
    },
  },
  {
    text: "...",
    style: {
      top: "70%",
      right: "10%",
      fontSize: "1.1rem",
      opacity: "0.12",
      animationDelay: "0.5s",
    },
  },
  {
    text: "→",
    style: {
      top: "30%",
      right: "3%",
      fontSize: "1.4rem",
      opacity: "0.15",
      animationDelay: "1.5s",
    },
  },
  {
    text: "</>",
    style: {
      top: "82%",
      left: "15%",
      fontSize: "1.6rem",
      opacity: "0.10",
      animationDelay: "3s",
    },
  },
  {
    text: "=>",
    style: {
      top: "45%",
      right: "20%",
      fontSize: "1.3rem",
      opacity: "0.08",
      animationDelay: "2.5s",
    },
  },
  {
    text: "()",
    style: {
      top: "22%",
      left: "18%",
      fontSize: "1.1rem",
      opacity: "0.10",
      animationDelay: "0.8s",
    },
  },
];

// Arch arc: parabola peaking at center (Docker, directly above panda),
// descending symmetrically to both sides. Step = 100px, depth = 200px.
const cards = [
  {
    name: "Frag",
    image: "/frag.png",
    glowColor: "teal",
    size: "md" as const,
    zIndex: 1,
    side: "left",
    pos: { top: "340px", left: "20px" },
    rotation: "-15deg",
    delay: "1s",
  },
  {
    name: "Python",
    image: "/pythonBetter.png",
    glowColor: "yellow",
    size: "lg" as const,
    zIndex: 2,
    side: "left",
    pos: { top: "200px", left: "90px" },
    rotation: "-9deg",
    delay: "0s",
  },
  {
    name: "Node",
    icon: "simple-icons:nginx",
    glowColor: "green",
    innerGlow: true,
    size: "sm" as const,
    zIndex: 1,
    side: "left",
    pos: { top: "270px", left: "220px" },
    rotation: "-7deg",
    delay: "1s",
  },
  {
    name: "React",
    image: "/react.png",
    glowColor: "cyan",
    size: "lg" as const,
    zIndex: 1,
    side: "left",
    pos: { top: "160px", left: "280px" },
    rotation: "-3deg",
    delay: "0.5s",
  },
  {
    name: "CSS Grid",
    image: "/cssGridUpscaled.png",
    glowColor: "purple",
    size: "lg" as const,
    zIndex: 1,
    side: "left",
    pos: { top: "150px", left: "400px" },
    rotation: "0deg",
    delay: "1.7s",
  },
  {
    name: "SQL",
    image: "/sql.png",
    glowColor: "blue",
    size: "md" as const,
    zIndex: 1,
    side: "right",
    pos: { top: "60px", left: "160px" },
    rotation: "3deg",
    delay: "0.7s",
  },
  {
    name: "Docker",
    image: "/docker.png",
    glowColor: "blue",
    size: "md" as const,
    zIndex: 1,
    side: "right",
    pos: { top: "28px", left: "280px" },
    rotation: "-3deg",
    delay: "1.2s",
  },
  {
    name: "Command",
    image: "/command.png",
    glowColor: "green",
    size: "md" as const,
    zIndex: 1,
    side: "right",
    pos: { top: "50px", left: "380px" },
    rotation: "-8deg",
    delay: "2.2s",
  },
  {
    name: "Git",
    image: "/gitUpscaled.png",
    glowColor: "orange",
    glassTint: "rgba(30,64,175,0.30)",
    size: "md" as const,
    zIndex: 1,
    side: "right",
    pos: { top: "90px", left: "480px" },
    rotation: "-4deg",
    delay: "0.3s",
  },
  {
    name: "Args",
    icon: "lucide:chevron-right",
    glowColor: "teal",
    innerGlow: true,
    size: "md" as const,
    zIndex: 1,
    side: "right",
    pos: { top: "148px", left: "580px" },
    rotation: "5deg",
    delay: "1.5s",
  },
  {
    name: "JavaScript",
    icon: "simple-icons:javascript",
    glowColor: "yellow",
    innerGlow: true,
    size: "md" as const,
    zIndex: 1,
    side: "right",
    pos: { top: "220px", left: "680px" },
    rotation: "8deg",
    delay: "2s",
  },
];

const leftCards = computed(() => cards.filter(c => c.side === 'left'));
const rightCards = computed(() => cards.filter(c => c.side === 'right'));

const suggestions = [
  { label: "React Hooks", icon: "simple-icons:react" },
  { label: "Nginx Config", icon: "simple-icons:nginx" },
  { label: "Python Regex", icon: "simple-icons:python" },
  { label: "Git Commands", icon: "simple-icons:git" },
  { label: "JS Array Methods", icon: "simple-icons:javascript" },
];
</script>

<template>
  <section
    class="relative min-h-screen bg-gradient-to-b from-navy-deep via-navy-mid to-navy-deep overflow-hidden pt-16"
    aria-label="Hero"
  >
    <!-- Decorative background code symbols -->
    <div aria-hidden="true" class="pointer-events-none select-none">
      <span
        v-for="(sym, i) in codeSymbols"
        :key="i"
        class="absolute font-mono text-teal-glow animate-float"
        :style="sym.style"
        >{{ sym.text }}</span
      >
    </div>

    <div class="relative max-w-7xl mx-auto px-6 flex flex-col items-center">
      <!-- Pill badge -->
      <div class="mt-20 mb-10">
        <span
          class="inline-flex items-center gap-2 px-4 py-2 bg-navy-light/50 border border-white/10 rounded-full text-sm text-gray-300 backdrop-blur-sm"
        >
          👋 Fast track your dev knowledge
        </span>
      </div>

      <!-- Floating cards arena + central panda -->
      <div class="relative w-full max-w-6xl flex" style="min-height: 560px">
        <!-- Left cards container — hidden on mobile -->
        <div class="flex relative" style="width: 540px">
          <div
            v-for="card in leftCards"
            :key="card.name"
            class=""
            :style="{ ...card.pos, zIndex: card.zIndex }"
          >
            <FloatingCard
              :name="card.name"
              :icon="card.icon"
              :image="card.image"
              :glow-color="card.glowColor"
              :glass-tint="card.glassTint"
              :inner-glow="card.innerGlow"
              :size="card.size"
              :rotation="card.rotation"
              :delay="card.delay"
            />
          </div>
        </div>

        <!-- Right cards container — hidden on mobile -->
        <div class="flex ml-18 relative" style="left: 40px">
          <div
            v-for="card in rightCards"
            :key="card.name"
            class=""
            :style="{ ...card.pos, zIndex: card.zIndex }"
          >
            <FloatingCard
              :name="card.name"
              :icon="card.icon"
              :image="card.image"
              :glow-color="card.glowColor"
              :glass-tint="card.glassTint"
              :inner-glow="card.innerGlow"
              :size="card.size"
              :rotation="card.rotation"
              :delay="card.delay"
            />
          </div>
        </div>

        <!-- Central panda mascot -->
        <div
          class="absolute inset-0 flex items-center justify-center pointer-events-none" style="z-index: 10"
        >
          <img
            src="/largePandaUpscale.png"
            alt="Panda mascot at laptop"
            class="w-[520px] h-[520px] object-contain select-none"
            style="
              filter: drop-shadow(0 0 60px rgba(120, 180, 255, 0.35))
                drop-shadow(0 0 180px rgba(100, 160, 240, 0.25))
                drop-shadow(0 0 400px rgba(80, 140, 220, 0.15));
            "
          />
        </div>
      </div>

      <!-- Search bar -->
      <div class="w-full max-w-2xl mt-4">
        <label for="cheatsheet-search" class="sr-only"
          >Search cheatsheets</label
        >
        <div
          class="relative flex items-center rounded-full border transition-all duration-300"
          :class="
            searchFocused
              ? 'border-teal-glow/60 bg-navy-light/70 shadow-[0_0_30px_rgba(45,212,191,0.45)] scale-[1.01]'
              : 'border-white/10 bg-navy-light/40 shadow-[0_0_20px_rgba(45,212,191,0.15)]'
          "
        >
          <Icon
            name="lucide:search"
            size="20"
            class="absolute left-5 text-gray-400 pointer-events-none"
            aria-hidden="true"
          />
          <input
            id="cheatsheet-search"
            type="search"
            placeholder="Search for language, library, or tool..."
            class="w-full bg-transparent py-4 pl-14 pr-6 text-white placeholder-gray-500 outline-none text-base rounded-full"
            @focus="searchFocused = true"
            @blur="searchFocused = false"
          />
        </div>
      </div>

      <!-- Suggestion pills -->
      <div class="flex flex-wrap justify-center gap-2 mt-5 pb-24">
        <button
          v-for="s in suggestions"
          :key="s.label"
          type="button"
          class="inline-flex items-center gap-1.5 px-3 py-1.5 bg-navy-light/40 border border-white/10 rounded-full text-xs text-gray-300 hover:text-white hover:border-white/30 transition-colors duration-200 focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-teal-glow/50"
        >
          <Icon :name="s.icon" size="12" aria-hidden="true" />
          {{ s.label }}
        </button>
      </div>
    </div>
  </section>
</template>
