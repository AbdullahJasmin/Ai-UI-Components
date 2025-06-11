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
        class="group px-4 py-2 border rounded-lg  flex items-center overflow-hidden transition-all duration-300 border-gray-300 bg-gray-50 dark:border-gray-700 dark:bg-gray-900 hover:bg-gray-800 dark:hover:bg-gray-100">
        <Icon icon="lucide:moon" :height="24" class=" text-gray-500 dark:hidden group-hover:text-gray-400" />
        <Icon icon="lucide:sun" :height="24" class="hidden dark:block text-gray-400 group-hover:text-gray-500" />
        <span
            class="capitalize flex items-center w-0 opacity-0 group-hover:w-10 group-hover:opacity-100 group-hover:pl-2 transition-all duration-300 text-gray-500 dark:text-gray-400 group-hover:text-gray-400 dark:group-hover:text-gray-500">
            {{ isDark ? 'Light' : 'Dark' }}
        </span>

    </button>
</template>