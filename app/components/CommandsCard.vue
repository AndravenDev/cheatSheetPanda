<script setup>
    defineProps({
        commands: {
            type: Array,
            default: () => []
        },
        title: String
    })
</script>

<template>
    <div class="w-full m-4 max-w-xs">
        <div class="w-[70%] rounded-tl-lg rounded-tr-lg px-4 py-2" style="background-color: #59e1d3;">{{ title }}</div>
        <div class="border border-gray-300 rounded-tr-lg rounded-br-lg rounded-bl-lg p-2">
            <ul>
                <li v-for="command in commands" :key="command.command">
                    {{ command.command }} - {{ command.description }}
                </li>
            </ul>
        </div>
    </div>
</template>