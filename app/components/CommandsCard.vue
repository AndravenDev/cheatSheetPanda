<script setup>
    defineProps({
        commands: {
            type: Array,
            default: () => []
        },
        title: String,
        icon: String,
        type: {
            type: String,
            default: 'commands'
        },
        codeBlock: String
    })
</script>

<template>
    <div class="break-inside-avoid mb-4">
        <div class="w-fit whitespace-nowrap rounded-tl-lg rounded-tr-lg px-4 py-2 flex items-center gap-2" style="background-color: #59e1d3;">
            <Icon v-if="icon" :name="icon" size="15" />
            {{ title }}
        </div>
        <div class="border border-gray-300 rounded-tr-lg rounded-br-lg rounded-bl-lg p-2">
            <ul v-if="type === 'commands'">
                <li v-for="command in commands" :key="command.command" class="flex items-center gap-2 mb-2">
                    <span class="bg-gray-100 rounded px-1.5 py-0.5 text-xs font-mono w-28 sm:w-36 shrink-0">{{ command.command }}</span>
                    <span class="text-gray-600 text-xs">{{ command.description }}</span>
                </li>
            </ul>
            <ul v-else-if="type === 'tips'" class="list-disc pl-4 space-y-1 text-xs">
                <li v-for="(tip, i) in commands" :key="i">
                    {{ tip.description }}
                </li>
            </ul>
            <pre v-else-if="type === 'code'" class="text-xs overflow-auto bg-gray-50 p-2 rounded"><code>{{ codeBlock }}</code></pre>
        </div>
    </div>
</template>
