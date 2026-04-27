<script setup>
const containerManagement = [{ command: "docker test", description: "Docker lifts container" }, { command: "docker test", description: "Docker lifts container" }];
</script>


<template>
  <div class="min-h-screen bg-white">
    <AppHeader />

    <div class="pt-16 max-w-7xl mx-auto px-6 flex">
      <div class="w-full">
        <div class="flex items-center justify-center gap-3 py-4">
          <img src="/dockeLogo.webp" alt="Docker" class="w-20 h-20 object-contain" />
          <span
            class="font-bold text-5xl"
            style="color: #0d3b69; text-shadow: 0 0 6px #7dd3fc, 0 0 14px #38bdf8;"
          >DOCKER</span>
        </div>
        <div>
          <CommandsCard :commands="containerManagement" title="Container Management"/>
          <CommandsCard :commands="containerManagement" title="Container Management"/>
          <CommandsCard :commands="containerManagement" title="Container Management"/>
          <CommandsCard :commands="containerManagement" title="Container Management"/>
          <CommandsCard :commands="containerManagement" title="Container Management"/>
          <CommandsCard :commands="containerManagement" title="Container Management"/>
          <CommandsCard :commands="containerManagement" title="Container Management"/>
          <CommandsCard :commands="containerManagement" title="Container Management"/>
          <CommandsCard :commands="containerManagement" title="Container Management"/>
          <CommandsCard :commands="containerManagement" title="Container Management"/>
          <CommandsCard :commands="containerManagement" title="Container Management"/>
          <CommandsCard :commands="containerManagement" title="Container Management"/>
        </div>

      </div>
      <div>Heyy ZZZ</div>
    </div>
  </div>
</template>
