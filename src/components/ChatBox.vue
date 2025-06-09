<script setup lang="ts">
import { ref, defineProps } from 'vue';
import { Icon } from "@iconify/vue";

const props = defineProps({
    layout: {
        type: String,
        default: 'single'
    }
});

</script>
<template>
    <div v-if="layout == 'single'"
        class="p-2 border rounded-lg w-fit flex items-center gap-2 focus-within:border-indigo-500 dark:focus-within:border-indigo-300  border-gray-300 bg-gray-50  dark:border-gray-700 dark:bg-gray-900">
        <Icon icon="lucide:wand-sparkles" :height="48" class="p-2 text-gray-500 dark:text-gray-400" />
        <input type="text" placeholder="How can I help you?"
            class=" text-xl w-full focus:outline-none placeholder:text-gray-500  placeholder:dark:text-gray-400  dark:text-gray-50" />
        <Icon icon="lucide:paperclip" :height="48" class="p-2 text-gray-700 dark:text-gray-300" />
        <Icon icon="lucide:audio-waveform" :height="48" class="p-2 text-indigo-600 dark:text-indigo-300" />
    </div>


    <!-- <div v-if="layout == 'double'"
        class="p-2 border rounded-lg w-fit flex items-center  flex-wrap gap-2 focus-within:border-indigo-500 dark:focus-within:border-indigo-300  border-gray-300 bg-gray-50  dark:border-gray-700 dark:bg-gray-900">
        <div class="w-full flex">
            <Icon icon="lucide:wand-sparkles" :height="40" class="p-2 text-gray-500 dark:text-gray-400" />
            <input type="text" placeholder="How can I help you?"
                class=" text-lg w-full focus:outline-none placeholder:text-gray-500  placeholder:dark:text-gray-400  dark:text-gray-50" />
        </div>
        <div class="w-full flex flex-row justify-start">
            <Icon icon="lucide:paperclip" :height="40" class="p-2 text-gray-700 dark:text-gray-300" />
            <Icon icon="lucide:audio-waveform" :height="40" class="p-2 text-indigo-600 dark:text-indigo-300 ml-auto" />
        </div>
    </div> -->
</template>