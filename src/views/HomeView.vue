<script setup lang="ts">

import ChatBox from '@/components/ChatBox.vue';
import { ref } from 'vue';

 

const layout = ref('single');

</script>

<template>
  <main class="flex flex-col items-center justify-center bg-gray-100 h-screen w-full">

    <ChatBox :layout="layout" />

   
  </main>

</template>
