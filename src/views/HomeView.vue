<script setup lang="ts">

import ChatBox from '@/components/ChatBox.vue';
import { ref } from 'vue';

import {
  Select,
  SelectContent,
  SelectGroup,
  SelectItem,
  SelectLabel,
  SelectTrigger,
  SelectValue,
} from '@/components/ui/select';
import ChatBoxPage from './pages/ChatBoxPage.vue';


const data = [
  {
    name: 'Single',
    value: 'single',
  },
  {
    name: 'Double',
    value: 'double',
  }];


const layout = ref('single');

</script>

<template>

  <ChatBoxPage />
  <!-- <div class="flex flex-col items-center justify-center h-screen w-full">

      <ChatBox :layout="layout" /> -->

    <!-- <Select  v-model="layout">
      <SelectTrigger class="w-[180px]">
        <SelectValue placeholder="Select a Layout" />
      </SelectTrigger>
      <SelectContent> 
          <SelectItem v-for="item in data" :value="item.value" :key="item.value" >
            {{ item.name }} 
          </SelectItem> 
      </SelectContent>
    </Select>  
  </div> -->

</template>
