<script setup lang="ts">

import { ref, onMounted } from 'vue';
import { Icon } from "@iconify/vue";

const isDark = ref(false)



const toggleTheme = () => {
    isDark.value = !isDark.value
    document.documentElement.classList.toggle('dark', isDark.value)
    localStorage.setItem('darkMode', isDark.value ? 'true' : 'false')
}

onMounted(() => {
    const saved = localStorage.getItem('darkMode')
    const prefersDark = window.matchMedia('(prefers-color-scheme: dark)').matches

    isDark.value = saved ? JSON.parse(saved) : prefersDark
    document.documentElement.classList.toggle('dark', isDark.value)
})

</script>
<template>
    <button @click="toggleTheme"
        class="group px-4 py-2 border rounded-lg  flex items-center overflow-hidden transition-all duration-300 border-neutral-300 bg-neutral-50 dark:border-neutral-700 dark:bg-neutral-900 hover:bg-neutral-800 dark:hover:bg-neutral-100">
        <Icon icon="lucide:moon" :height="24" class=" text-neutral-500 dark:hidden group-hover:text-neutral-400" />
        <Icon icon="lucide:sun" :height="24" class="hidden dark:block text-neutral-400 group-hover:text-neutral-500" />
        <span
            class="capitalize flex items-center w-0 opacity-0 group-hover:w-10 group-hover:opacity-100 group-hover:pl-2 transition-all duration-300 text-neutral-500 dark:text-neutral-400 group-hover:text-neutral-400 dark:group-hover:text-neutral-500">
            {{ isDark ? 'Light' : 'Dark' }}
        </span>

    </button>
</template>