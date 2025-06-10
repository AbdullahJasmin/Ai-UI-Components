<script setup lang="ts">
import { ref, defineProps } from "vue";
import { Icon } from "@iconify/vue";

const props = defineProps({
    layout: {
        type: String,
        default: "single",
    },
});

const textInput = ref("");
const typing = ref(false);
const hasTyped = () => {
    if (!textInput.value) {
        typing.value = false;
        return;
    }
    typing.value = true;
};

const fileInput = ref<HTMLInputElement | null>(null);
const handleFileInput = () => {
    if (fileInput.value) {
        fileInput.value.click();
    }
};

const sendMessage = () => {
    if (textInput.value.trim() === "") return;
    console.log("Message sent:", textInput.value);
    textInput.value = "";
    typing.value = false;
};

</script>
<template>
    <form v-if="layout == 'single'" @submit.prevent="sendMessage" class="group p-2 border rounded-lg w-fit flex items-center gap-2 transition-all duration-300 border-gray-300 dark:border-gray-700 bg-gray-50 
    dark:bg-gray-900 hover:bg-gray-100 dark:hover:border-indigo-300 hover:border-indigo-500 dark:hover:bg-gray-800 focus-within:bg-gray-100 focus-within:border-indigo-600 
    dark:focus-within:bg-gray-800   dark:focus-within:border-indigo-300">
        <span>
            <Icon icon="lucide:wand-sparkles" :height="40" :width="40"
                class="p-2 transition-all duration-300 text-gray-500 dark:text-gray-400 group-hover:text-indigo-600 dark:group-hover:text-indigo-300 group-focus-within:text-indigo-600 dark:group-focus-within:text-indigo-300" />
        </span>
        <input type="text" placeholder="How can I help you?" @input="hasTyped"
            class="text-xl w-full focus:outline-none placeholder:text-gray-500 placeholder:dark:text-gray-400 dark:text-gray-50"
            v-model.trim="textInput" />
        <button
            class="rounded-md cursor-pointer transition-all duration-300 hover:bg-gray-700 dark:hover:bg-gray-300"
            @click="handleFileInput">
            <Icon icon="lucide:paperclip" :height="40" :width="40"
                class="p-2  rounded-md cursor-pointer transition-all duration-300 text-gray-700 dark:text-gray-300 hover:text-gray-300 dark:hover:text-gray-700 " />
        </button>
        <input type="file" class="hidden" @change="handleFileInput" ref="fileInput" />
        <button v-if="!typing"
            class="rounded-md cursor-pointer transition-all duration-300 hover:bg-indigo-500 dark:hover:bg-indigo-300 ">
            <Icon icon="lucide:audio-waveform" :height="40" :width="40"
                class="p-2 cursor-pointer transition-all duration-300 text-indigo-600 dark:text-indigo-300 hover:text-gray-300 dark:hover:text-gray-700" />
        </button>
        <button v-if="typing" @click="sendMessage"
            class="rounded-md cursor-pointer transition-all duration-300  bg-indigo-500 dark:bg-indigo-300  hover:bg-indigo-600 dark:hover:bg-indigo-200">
            <Icon icon="lucide:send" :height="40" :width="40"
                class="p-2 cursor-pointer transition-all duration-300 text-gray-300 dark:text-gray-700  hover:text-gray-200 dark:hover:text-gray-800" />
        </button>
    </form>

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
