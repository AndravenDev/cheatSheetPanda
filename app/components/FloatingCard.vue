<script setup lang="ts">
const props = defineProps<{
  name: string
  icon?: string
  image?: string
  glowColor?: string
  glassTint?: string
  innerGlow?: boolean
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

const dimMap: Record<string, number> = { sm: 100, md: 170, lg: 210 }
const dim = computed(() => `${dimMap[props.size ?? 'md'] ?? 170}px`)

const glow = computed(() => glowMap[props.glowColor ?? ''] ?? 'rgba(45,212,191,0.3)')
const iconColor = computed(() => iconColorMap[props.glowColor ?? ''] ?? '#2dd4bf')
const iconSize = computed(() => props.size === 'lg' ? 72 : props.size === 'sm' ? 44 : 56)
const labelClass = computed(() => props.size === 'lg' ? 'text-white/70 text-[12px] font-medium whitespace-nowrap leading-none' : props.size === 'sm' ? 'text-white/70 text-[9px] font-medium whitespace-nowrap leading-none' : 'text-white/70 text-[10px] font-medium whitespace-nowrap leading-none')
</script>

<template>
  <!-- Outer: rotation only (static) -->
  <div :style="{ transform: rotation ? `rotate(${rotation})` : undefined }">
    <!-- Inner: float animation only -->
    <div
      class="animate-float"
      :style="{ animationDelay: delay ?? '0s' }"
    >
      <!-- PNG mode -->
      <img
        v-if="image"
        :src="image"
        :alt="name"
        class="hover:scale-110 transition-transform duration-300 cursor-default select-none object-contain drop-shadow-[0_0_28px_var(--card-glow)]"
        :style="{
          width: dim,
          height: dim,
          '--card-glow': glow,
        }"
      />

      <!-- Icon mode -->
      <div
        v-else-if="icon"
        class="flex flex-col items-center justify-center gap-1.5 backdrop-blur-md border border-white/10 rounded-2xl hover:scale-110 transition-transform duration-300 cursor-default select-none"
        :style="{
          width: dim,
          height: dim,
          backgroundColor: glassTint ?? 'rgba(26,47,82,0.30)',
          boxShadow: innerGlow ? `0 0 28px ${glow}, inset 0 0 40px ${glow}, inset 0 0 80px ${glow}` : `0 0 28px ${glow}`,
          borderColor: innerGlow ? iconColor : undefined,
          borderWidth: innerGlow ? '3px' : undefined,
        }"
      >
        <Icon :name="icon" :size="iconSize" :style="{ color: iconColor }" aria-hidden="true" />
        <span :class="labelClass">{{ name }}</span>
      </div>
    </div>
  </div>
</template>
