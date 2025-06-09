<script setup lang="ts">

import { ref } from 'vue';
import { Icon } from "@iconify/vue";

const theme = ref('light');

const toggleTheme = () => {
    const htmlElement = document.documentElement;
    if (htmlElement.classList.contains('dark')) {
        htmlElement.classList.remove('dark');
        localStorage.setItem('theme', 'light');
        theme.value = 'dark';
    } else {
        htmlElement.classList.add('dark');
        localStorage.setItem('theme', 'dark');
        theme.value = 'light';
    }


}

</script>
<template>
    <button @click="toggleTheme"
        class="group px-4 py-2 border rounded-lg  flex items-center overflow-hidden border-gray-300 bg-gray-50 dark:border-gray-700 dark:bg-gray-900 hover:bg-gray-800 dark:hover:bg-gray-100 transition-all duration-300">
        <Icon icon="lucide:moon" :height="24" class=" text-gray-500 dark:hidden group-hover:text-gray-400" />
        <Icon icon="lucide:sun" :height="24" class="hidden dark:block text-gray-400 group-hover:text-gray-500" />
        <span
            class="capitalize flex items-center w-0 opacity-0 group-hover:w-10 group-hover:opacity-100 group-hover:pl-2 transition-all duration-300 text-gray-500 dark:text-gray-400 group-hover:text-gray-400 dark:group-hover:text-gray-500">
            {{ theme }}
        </span>

    </button>
</template>