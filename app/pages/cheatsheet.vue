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
  <div class="min-h-screen bg-white overflow-x-hidden">
    <AppHeader />

    <div class="pt-16 max-w-7xl mx-auto px-4">
      <div class="flex items-center justify-center gap-3 py-4">
        <img src="/dockeLogo.webp" alt="Docker" class="w-12 h-12 sm:w-20 sm:h-20 object-contain" style="filter: drop-shadow(0 0 8px #7dd3fc);" />
        <span
          class="font-bold text-3xl sm:text-5xl"
          style="color: #0d3b69; text-shadow: 0 0 6px #7dd3fc, 0 0 14px #38bdf8;"
        >DOCKER</span>
      </div>

      <div class="flex flex-col lg:flex-row gap-4 lg:items-start">

        <!-- Main content -->
        <div class="flex-1 min-w-0">
          <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-4 px-3 sm:px-0">
            <div>
              <CommandsCard :commands="containerManagement" title="Container Management" icon="lucide:box" icon-bottom="/pandaQuestion.png" />
              <CommandsCard :commands="dockerSecrets" title="Docker Secrets" icon="lucide:key" />
            </div>
            <div>
              <CommandsCard :commands="imageManagement" title="Image Management" icon="lucide:layers" icon-bottom="/pandaWorker.png" />
              <CommandsCard :commands="volumeNetwork" title="Volume & Network" icon="lucide:hard-drive" />
            </div>
            <div>
              <CommandsCard :commands="advancedTips" type="tips" title="Advanced Tips" icon="lucide:lightbulb" />
              <CommandsCard :commands="containerLifecycle" title="Container Lifecycle" icon="lucide:refresh-cw" icon-top="/pandaQuestion.png" />
              <CommandsCard :commands="systemCommands" title="System Commands" icon="lucide:terminal" />
            </div>
            <div>
              <CommandsCard type="code" :codeBlock="dockerComposeCode" title="Docker Compose" icon="lucide:file-code" icon-top="/pandaPeek.png" icon-bottom="/pandaWorker.png" />
              <CommandsCard :commands="configFiles" title="Config Files" icon="lucide:file-cog" />
              <CommandsCard :commands="registryOperations" title="Registry Operations" icon="lucide:cloud" />
              <CommandsCard :commands="dockerOperations" title="Docker Operations" icon="lucide:activity" />
            </div>
          </div>

          <div class="mt-8 pb-8 flex justify-center">
            <div class="w-fit max-w-full">
              <div class="flex flex-wrap items-center justify-center gap-2">
                <span class="text-sm font-bold text-gray-700 uppercase tracking-widest shrink-0 mr-2">Tags</span>
                <span v-for="tag in ['DockerContainers','DockerOrchestration','DevOPs','Microservices','ContainerIPS','ContainerSecurity']" :key="tag" class="px-3 py-1.5 text-sm text-gray-600 bg-gray-100 border border-gray-300 rounded-full hover:text-gray-900 hover:border-gray-400 cursor-pointer transition-colors">#{{ tag }}</span>
              </div>
              <hr class="border-t-2 border-gray-300 mt-3" />
            </div>
          </div>
        </div>

        <!-- Sidebar -->
        <aside class="flex flex-col w-full lg:w-36 shrink-0 lg:sticky lg:top-20 gap-3 pb-6">
          <div class="flex flex-row lg:flex-col gap-3">
            <button type="button" class="flex items-center justify-center gap-1.5 flex-1 lg:flex-none px-3 py-2 rounded-lg text-xs font-semibold whitespace-nowrap" style="background-color: #59e1d3; color: #0d3b69;">
              <Icon name="lucide:download" size="13" />
              Download PDF
            </button>
            <button type="button" class="flex items-center justify-center gap-1.5 flex-1 lg:flex-none px-3 py-2 rounded-lg text-xs font-semibold whitespace-nowrap border border-gray-300 text-gray-600 hover:border-gray-400 hover:text-gray-800 transition-colors">
              <Icon name="lucide:star" size="13" />
              Add to Favourites
            </button>
          </div>

          <hr class="border-gray-200 my-1" />

          <p class="text-xs font-semibold text-gray-500 uppercase tracking-wide">Related Cheat Sheets</p>

          <div class="flex flex-row lg:flex-col flex-wrap gap-3">
            <a href="#" class="flex items-center gap-2 text-sm text-gray-600 hover:text-gray-900 transition-colors">
              <img src="/nginxSmallLogo.webp" alt="Nginx" class="w-6 h-6 object-contain" />
              Nginx
            </a>
            <a href="#" class="flex items-center gap-2 text-sm text-gray-600 hover:text-gray-900 transition-colors">
              <img src="/gitSmallLogo.png" alt="Git" class="w-6 h-6 object-contain" />
              Git
            </a>
            <a href="#" class="flex items-center gap-2 text-sm text-gray-600 hover:text-gray-900 transition-colors">
              <img src="/kubernetes.png" alt="Kubernetes" class="w-6 h-6 object-contain" />
              Kubernetes
            </a>
          </div>
        </aside>

      </div>
    </div>

    <footer class="mt-4">
      <div class="max-w-7xl mx-auto px-4 py-5 flex flex-col sm:flex-row items-center gap-4 sm:justify-between">
        <nav class="flex flex-wrap justify-center items-center gap-4 sm:gap-6">
          <a v-for="link in [{ label: 'Browse', href: '/' }, { label: 'Submit', href: '/' }, { label: 'Pricing', href: '/' }, { label: 'CheatSheet', href: '/cheatsheet' }]" :key="link.label" :href="link.href" class="text-sm font-semibold text-gray-700 hover:text-gray-900 transition-colors">{{ link.label }}</a>
        </nav>
        <span class="text-sm font-semibold text-gray-700 shrink-0">&copy; 2022 cheatsheetpanda.com</span>
      </div>
    </footer>
  </div>
</template>
