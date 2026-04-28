<script setup>
import {
  containerManagement,
  imageManagement,
  systemCommands,
  volumeNetwork,
  containerLifecycle,
  dockerComposeCode,
  registryOperations,
  dockerSecrets,
  advancedTips,
  dockerOperations,
  configFiles,
} from '~/data/docker.js'
</script>


<template>
  <div class="min-h-screen bg-white">
    <AppHeader />

    <div class="pt-16 max-w-7xl mx-auto px-4 sm:px-6">
      <div class="w-full">
        <div class="flex items-center justify-center gap-3 py-4">
          <img src="/dockeLogo.webp" alt="Docker" class="w-12 h-12 sm:w-20 sm:h-20 object-contain" style="filter: drop-shadow(0 0 8px #7dd3fc);" />
          <span
            class="font-bold text-3xl sm:text-5xl"
            style="color: #0d3b69; text-shadow: 0 0 6px #7dd3fc, 0 0 14px #38bdf8;"
          >DOCKER</span>
        </div>
        <div class="columns-1 sm:columns-2 lg:columns-3 xl:columns-4 gap-4">
          <CommandsCard :commands="containerManagement" title="Container Management" icon="lucide:box" />
          <CommandsCard :commands="imageManagement" title="Image Management" icon="lucide:layers" />
          <CommandsCard :commands="systemCommands" title="System Commands" icon="lucide:terminal" />
          <CommandsCard :commands="volumeNetwork" title="Volume & Network" icon="lucide:hard-drive" />
          <CommandsCard :commands="containerLifecycle" title="Container Lifecycle" icon="lucide:refresh-cw" />
          <CommandsCard type="code" :codeBlock="dockerComposeCode" title="Docker Compose" icon="lucide:file-code" />
          <CommandsCard :commands="registryOperations" title="Registry Operations" icon="lucide:cloud" />
          <CommandsCard :commands="dockerSecrets" title="Docker Secrets" icon="lucide:key" />
          <CommandsCard :commands="advancedTips" type="tips" title="Advanced Tips & Optimization" icon="lucide:lightbulb" />
          <CommandsCard :commands="dockerOperations" title="Docker Operations" icon="lucide:activity" />
          <CommandsCard :commands="configFiles" title="Config Files" icon="lucide:file-cog" />
        </div>

      </div>
    </div>
  </div>
</template>
