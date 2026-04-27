<script setup>
    defineProps({
        commands: {
            type: Array,
            default: () => []
        },
        title: String,
        type: {
            type: String,
            default: 'commands'
        },
        codeBlock: String
    })
</script>

<template>
    <div class="w-full m-4 max-w-xs">
        <div class="w-[70%] rounded-tl-lg rounded-tr-lg px-4 py-2" style="background-color: #59e1d3;">{{ title }}</div>
        <div class="border border-gray-300 rounded-tr-lg rounded-br-lg rounded-bl-lg p-2">
            <ul v-if="type === 'commands'">
                <li v-for="command in commands" :key="command.command" class="flex items-center gap-2 mb-2">
                    <span class="bg-gray-100 rounded px-1.5 py-0.5 text-sm font-mono w-44 shrink-0">{{ command.command }}</span>
                    <span class="text-gray-600 text-sm">{{ command.description }}</span>
                </li>
            </ul>
            <ul v-else-if="type === 'tips'" class="list-disc pl-4 space-y-1">
                <li v-for="(tip, i) in commands" :key="i">
                    {{ tip.description }}
                </li>
            </ul>
            <pre v-else-if="type === 'code'" class="text-xs overflow-auto bg-gray-50 p-2 rounded"><code>{{ codeBlock }}</code></pre>
        </div>
    </div>
</template>
