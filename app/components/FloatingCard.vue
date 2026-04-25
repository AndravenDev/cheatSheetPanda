<script setup lang="ts">
const props = defineProps<{
  name: string
  icon?: string
  image?: string   // path to a PNG in /public, e.g. "/python.png"
  glowColor?: string
  glassTint?: string  // CSS color to tint the card background, e.g. 'rgba(37,99,235,0.25)'
  size?: 'sm' | 'md' | 'lg'
  rotation?: string
  delay?: string
}>()

const glowMap: Record<string, string> = {
  yellow: 'rgba(234,179,8,0.35)',
  cyan: 'rgba(34,211,238,0.35)',
  purple: 'rgba(168,85,247,0.35)',
  blue: 'rgba(59,130,246,0.35)',
  orange: 'rgba(249,115,22,0.35)',
  green: 'rgba(74,222,128,0.35)',
  teal: 'rgba(45,212,191,0.35)',
}

const iconColorMap: Record<string, string> = {
  yellow: '#eab308',
  cyan: '#22d3ee',
  purple: '#a855f7',
  blue: '#3b82f6',
  orange: '#f97316',
  green: '#4ade80',
  teal: '#2dd4bf',
}

const glow = computed(() => glowMap[props.glowColor ?? ''] ?? 'rgba(45,212,191,0.3)')
const iconColor = computed(() => iconColorMap[props.glowColor ?? ''] ?? '#2dd4bf')

const padding = computed(() => ({ sm: 'p-3', md: 'p-4', lg: 'p-5' }[props.size ?? 'md']))
const iconSize = computed(() => ({ sm: '20', md: '28', lg: '36' }[props.size ?? 'md']))
const imgSize = computed(() => ({ sm: '64px', md: '96px', lg: '128px' }[props.size ?? 'md']))
</script>

<template>
  <div :style="{ transform: rotation ? `rotate(${rotation})` : undefined }">
    <!-- PNG mode: image fills the whole element, no card chrome -->
    <img
      v-if="image"
      :src="image"
      :alt="name"
      class="animate-float hover:scale-110 transition-transform duration-300 cursor-default select-none object-contain drop-shadow-[0_0_28px_var(--card-glow)]"
      :style="{
        width: imgSize,
        height: imgSize,
        animationDelay: delay ?? '0s',
        '--card-glow': glow,
      }"
    />

    <!-- Icon mode: glassmorphism card -->
    <div
      v-else-if="icon"
      class="flex flex-col items-center gap-1.5 backdrop-blur-md border border-white/10 rounded-2xl animate-float hover:scale-110 transition-transform duration-300 cursor-default select-none"
      :class="padding"
      :style="{
        backgroundColor: glassTint ?? 'rgba(26,47,82,0.30)',
        boxShadow: `0 0 28px ${glow}`,
        animationDelay: delay ?? '0s',
      }"
    >
      <Icon :name="icon" :size="iconSize" :style="{ color: iconColor }" aria-hidden="true" />
      <span class="text-white/70 text-[10px] font-medium whitespace-nowrap leading-none">{{ name }}</span>
    </div>
  </div>
</template>
