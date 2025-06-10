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
const fileCount = ref(0);

const webSearch = ref(false);
const toggleWebSearch = () => {
    webSearch.value = !webSearch.value;
    console.log("Web search toggled:", webSearch.value);
};

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
        // Trigger the file input click event to open the file dialog
        console.log("Opening file input dialog...");

        fileInput.value.click();
    } else {
        console.error("File input reference is not set.");
        return;
    }
    if (fileInput.value && fileInput.value.files && fileInput.value.files.length > 0) {
        fileCount.value = fileInput.value.files.length;
        const fileNames = Array.from(fileInput.value.files).map(file => file.name).join(", ");
        console.log("Files selected:", fileNames);

    } else {
        fileCount.value = 0;
        console.log("No files selected");
    }
};

const sendMessage = () => {
    if (textInput.value.trim() === "") return;
    console.log("Message sent:", textInput.value);
    if (fileInput.value && fileInput.value.files && fileInput.value.files.length > 0) {
        const files = Array.from(fileInput.value.files);
        console.log("Files attached:", files.map(file => file.name).join(", "));
    } else {
        console.log("No files attached");
    }
    textInput.value = "";
    typing.value = false;
    fileCount.value = 0;
    if (fileInput.value) {
        fileInput.value.value = ""; // Clear the file input
    }
};

</script>
<template>
    <form v-if="layout == 'single'" @submit.prevent="sendMessage" class="
        group max-w-2xl w-full m-2 p-2 border rounded-lg  flex items-center gap-2 transition-all duration-300 
        border-gray-300 dark:border-gray-700 bg-gray-50 dark:bg-gray-900 
        hover:bg-gray-100 dark:hover:border-indigo-300 hover:border-indigo-500 dark:hover:bg-gray-800 
        focus-within:bg-gray-100 focus-within:border-indigo-600 dark:focus-within:bg-gray-800   dark:focus-within:border-indigo-300
    ">
        <span class="
                p-2 transition-all duration-300 
                text-gray-500 dark:text-gray-400 group-hover:text-indigo-600 dark:group-hover:text-indigo-300 
                group-focus-within:text-indigo-600 dark:group-focus-within:text-indigo-300
            ">
            <Icon icon="lucide:wand-sparkles" :height="24" :width="24" />
        </span>
        <input type="text" placeholder="How can I help you?" @input="hasTyped" class="
                text-xl w-full focus:outline-none placeholder:text-gray-500 placeholder:dark:text-gray-400 dark:text-gray-50
            " v-model.trim="textInput" />
        <button @click="handleFileInput" type="button" class="
                p-2 rounded-md cursor-pointer transition-all duration-300 flex items-center gap-2  
            " :class="fileCount > 0 ?
                'text-gray-300 dark:text-gray-700  bg-gray-600 dark:bg-gray-300 hover:bg-gray-700 dark:hover:bg-gray-200' :
                'text-gray-700 dark:text-gray-300 hover:text-gray-300 dark:hover:text-gray-700  hover:bg-gray-700 dark:hover:bg-gray-300'
                ">
            <Icon icon="lucide:paperclip" :height="24" :width="24" />
            <span v-if="fileCount > 0">
                {{ fileCount }}
            </span>
        </button>
        <input type="file" class="hidden" @change="handleFileInput" ref="fileInput" multiple />
        <button v-if="!typing" class="
                p-2 rounded-md cursor-pointer transition-all duration-300 
                text-indigo-600 dark:text-indigo-300 hover:text-gray-300 dark:hover:text-gray-700 hover:bg-indigo-500 dark:hover:bg-indigo-300 
            ">
            <Icon icon="lucide:audio-waveform" :height="24" :width="24" />
        </button>
        <button v-if="typing" @click="sendMessage" class="
                p-2 rounded-md cursor-pointer transition-all duration-300 
                text-gray-300 dark:text-gray-700  hover:text-gray-200 dark:hover:text-gray-800 
                bg-indigo-500 dark:bg-indigo-300  hover:bg-indigo-600 dark:hover:bg-indigo-200
            ">
            <Icon icon="lucide:send" :height="24" :width="24" />
        </button>
    </form>


    <form v-if="layout == 'double'" @submit.prevent="sendMessage" class="
        group max-w-2xl w-full m-2 p-4 border rounded-lg  flex flex-col items-center gap-5 transition-all duration-300 
        border-gray-300 dark:border-gray-700 bg-gray-50 dark:bg-gray-900 hover:bg-gray-100 
        dark:hover:border-indigo-300 hover:border-indigo-500 dark:hover:bg-gray-800 
        focus-within:bg-gray-100 focus-within:border-indigo-600 dark:focus-within:bg-gray-800   dark:focus-within:border-indigo-300
    ">
        <div class="
            flex w-full items-center gap-3
        ">
            <span class="
                    transition-all duration-300 
                    text-gray-500 dark:text-gray-400 group-hover:text-indigo-600 dark:group-hover:text-indigo-300 
                    group-focus-within:text-indigo-600 dark:group-focus-within:text-indigo-300
                ">
                <Icon icon="lucide:wand-sparkles" :height="24" :width="24" />
            </span>
            <input type="text" placeholder="How can I help you?" @input="hasTyped" class="
                    text-xl w-full focus:outline-none placeholder:text-gray-500 placeholder:dark:text-gray-400 dark:text-gray-50
                " v-model.trim="textInput" />
        </div>
        <div class="w-full flex gap-2 flex-row justify-start">
            <button @click="handleFileInput" type="button" class="
                group/button px-3 py-2 rounded-md flex gap-1 cursor-pointer text-sm items-center justify-center transition-all duration-300  
                 " :class="fileCount > 0 ?
                    'text-gray-300 dark:text-gray-700  bg-gray-600 dark:bg-gray-300 hover:bg-gray-700 dark:hover:bg-gray-200' :
                    'text-gray-700 dark:text-gray-300 hover:text-gray-300 dark:hover:text-gray-700  hover:bg-gray-700 dark:hover:bg-gray-300 border'
                    ">
                <Icon icon="lucide:paperclip" :height="16" :width="16" />
                <span v-if="fileCount > 0">
                    {{ fileCount }} file(s)
                </span>
                <span v-else>
                    Attach
                </span>

            </button>

            <input type="file" class="hidden" @change="handleFileInput" ref="fileInput" multiple />

            <button type="button" @click="toggleWebSearch" class="
                    group/button px-3 py-2 rounded-md flex gap-1 cursor-pointer text-sm items-center justify-center transition-all duration-300 border
                     "
                     :class="webSearch ? 
                     ' text-gray-300 dark:text-gray-700   bg-gray-700 dark:bg-gray-300 hover:text-gray-200 dark:hover:text-gray-800 hover:bg-gray-800 dark:hover:bg-gray-200' : 
                     '  text-gray-700 dark:text-gray-300  hover:bg-gray-200 dark:hover:bg-gray-600'"
                     >
                <Icon icon="lucide:globe" :height="16" :width="16" />
                Web
            </button>

            <button v-if="!typing" class="
                    group/button ml-auto  px-3 py-2 rounded-md flex gap-2 cursor-pointer text-sm items-center justify-center transition-all duration-300 border 
                     border-indigo-600 dark:border-indigo-300 text-indigo-600 dark:text-indigo-300 hover:text-gray-300 dark:hover:text-gray-700  hover:bg-indigo-500 dark:hover:bg-indigo-300 
                     ">
                <Icon icon="lucide:audio-waveform" :height="24" :width="24" />
                Voice
            </button>

            <button v-if="typing" @click="sendMessage" class="
                    group/button ml-auto  px-3 py-2 rounded-md flex gap-2 cursor-pointer text-sm items-center justify-center transition-all duration-300 
                     text-gray-300 dark:text-gray-700  hover:text-gray-200 dark:hover:text-gray-800  bg-indigo-500 dark:bg-indigo-300  hover:bg-indigo-600 dark:hover:bg-indigo-200
                     ">
                <Icon icon="lucide:send" :height="24" :width="24" />
                Send
            </button>

        </div>
    </form>
</template>
