<script setup lang="ts">
const searchFocused = ref(false);

const arenaScale = ref(1);
let rafId: number | null = null;
const updateScale = () => {
  if (rafId !== null) return;
  rafId = requestAnimationFrame(() => {
    arenaScale.value = Math.min(1, Math.max(0.28, window.innerWidth / 1252));
    rafId = null;
  });
};
onMounted(() => {
  updateScale();
  window.addEventListener('resize', updateScale, { passive: true });
});
onUnmounted(() => {
  window.removeEventListener('resize', updateScale);
  if (rafId !== null) cancelAnimationFrame(rafId);
});

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
    size: "sm" as const,
    zIndex: 1,
    side: "left",
    pos: { top: "270px", left: "30px" },
    rotation: "-15deg",
    delay: "1s",
  },
  {
    name: "Python",
    image: "/pythongenlow.png",
    glowColor: "yellow",
    size: "lg" as const,
    zIndex: 2,
    side: "left",
    pos: { top: "90px", left: "100px" },
    rotation: "-12deg",
    delay: "0s",
  },
  {
    name: "Node",
    image: "/node.png",
    glowColor: "green",
    innerGlow: true,
    size: "sm" as const,
    zIndex: 1,
    side: "left",
    pos: { top: "210px", left: "230px" },
    rotation: "-10deg",
    delay: "1s",
  },
  {
    name: "React",
    image: "/reactGlowLow.png",
    glowColor: "cyan",
    size: "lg" as const,
    zIndex: 1,
    side: "left",
    pos: { top: "90px", left: "300px" },
    rotation: "-7deg",
    delay: "0.5s",
  },
  {
    name: "CSS Grid",
    image: "/cssGridUpscaled3Glow.png",
    glowColor: "purple",
    size: "lg" as const,
    zIndex: 1,
    side: "left",
    pos: { top: "80px", left: "440px" },
    rotation: "-3deg",
    delay: "1.7s",
  },
  {
    name: "SQL",
    image: "/sqlUpscaled.png",
    glowColor: "blue",
    size: "lg" as const,
    zIndex: 1,
    side: "right",
    pos: { top: "60px", left: "120px" },
    rotation: "6deg",
    delay: "0.7s",
  },
  {
    name: "Docker",
    image: "/dockerGlow.png",
    glowColor: "blue",
    size: "lg" as const,
    zIndex: 3,
    side: "right",
    pos: { top: "60px", left: "240px" },
    rotation: "7deg",
    delay: "1.2s",
  },
  {
    name: "Command",
    image: "/command.png",
    glowColor: "green",
    size: "sm" as const,
    zIndex: 2,
    side: "right",
    pos: { top: "210px", left: "370px" },
    rotation: "10deg",
    delay: "2.2s",
  },
  {
    name: "Git",
    image: "/gitUpscaledGlow.png",
    glowColor: "orange",
    glassTint: "rgba(30,64,175,0.30)",
    size: "lg" as const,
    zIndex: 3,
    side: "right",
    pos: { top: "90px", left: "370px" },
    rotation: "14deg",
    delay: "0.3s",
  },
  {
    name: "Args",
    image: "/unixUpscaled.png",
    glowColor: "teal",
    innerGlow: true,
    size: "sm" as const,
    zIndex: 1,
    side: "right",
    pos: { top: "260px", left: "520px" },
    rotation: "15deg",
    delay: "1.5s",
  },
  {
    name: "JavaScript",
    image: "/jsGlow.png",
    glowColor: "yellow",
    innerGlow: true,
    size: "lg" as const,
    zIndex: 1,
    side: "right",
    pos: { top: "90px", left: "520px" },
    rotation: "18deg",
    delay: "2s",
  },
];

const leftCards = computed(() => cards.filter(c => c.side === 'left'));
const rightCards = computed(() => cards.filter(c => c.side === 'right'));

const mobileTopCards = ['Python', 'React', 'CSS Grid'].map(n => cards.find(c => c.name === n)!);
const mobileBottomCards = ['Docker', 'Git', 'JavaScript'].map(n => cards.find(c => c.name === n)!);

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

    <div class="relative  mx-auto px-2 flex flex-col items-center">
      <!-- Pill badge -->
      <div class="mt-12 mb-2 lg:mt-20 lg:mb-4">
        <span
          class="inline-flex items-center gap-2 px-4 py-2 bg-navy-light/50 border border-white/10 rounded-full text-sm text-gray-300 backdrop-blur-sm"
        >
          👋 Fast track your dev knowledge
        </span>
      </div>

      <!-- Mobile: selected cards + panda -->
      <div class="md:hidden flex flex-col items-center mt-6 mb-2">
        <div class="flex justify-center gap-4 mb-2">
          <FloatingCard
            v-for="card in mobileTopCards"
            :key="card.name"
            :name="card.name"
            :image="card.image"
            :glow-color="card.glowColor"
            size="sm"
          />
        </div>
        <img
          src="/largePandaUpscale.png"
          alt="Panda mascot at laptop"
          class="w-56 h-56 object-contain select-none"
        />
        <div class="flex justify-center gap-4 mt-2">
          <FloatingCard
            v-for="card in mobileBottomCards"
            :key="card.name"
            :name="card.name"
            :image="card.image"
            :glow-color="card.glowColor"
            size="sm"
          />
        </div>
      </div>

      <!-- Floating cards arena + central panda (md+) -->
      <!-- Outer wrapper controls vertical space in the flow -->
      <div class="relative w-full hidden md:block" :style="{ height: `${560 * arenaScale}px` }">
        <!-- Inner arena: fixed design width, scaled down from top-center -->
        <div
          class="absolute top-0 left-1/2 flex"
          :style="{
            width: '1252px',
            minHeight: '560px',
            transform: `translateX(-50%) scale(${arenaScale})`,
            transformOrigin: 'top center',
          }"
        >
          <!-- Left cards container -->
          <div class="relative" style="width: 540px; flex-shrink: 0">
            <div
              v-for="card in leftCards"
              :key="card.name"
              class="absolute"
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

          <!-- Right cards container -->
          <div class="relative flex-1">
            <div
              v-for="card in rightCards"
              :key="card.name"
              class="absolute"
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
            class="absolute inset-0 flex items-center justify-center pointer-events-none"
            style="z-index: 10"
          >
            <img
              src="/largePandaUpscale.png"
              alt="Panda mascot at laptop"
              class="w-[520px] h-[520px] object-contain select-none"

            />
          </div>
        </div>
      </div>

      <!-- Search bar -->
      <div class="w-full max-w-2xl mt-4 md:mt-[-120px] px-4 sm:px-0">
        <label for="cheatsheet-search" class="sr-only"
          >Search cheatsheets</label
        >
        <div
          class="relative flex items-center rounded-full transition-all duration-300"
          style="border-width: 3px"
          :class="
            searchFocused
              ? 'border-cyan-300 bg-navy-light/70 shadow-[0_0_12px_rgba(6,182,212,0.6),0_0_35px_rgba(6,182,212,0.3),0_0_70px_rgba(6,182,212,0.15)] scale-[1.01]'
              : 'border-cyan-300/60 bg-navy-light/40 shadow-[0_0_8px_rgba(6,182,212,0.4),0_0_25px_rgba(6,182,212,0.2),0_0_50px_rgba(6,182,212,0.08)]'
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
