<script setup lang="ts">
import { RouterLink, RouterView } from "vue-router"; 

import ToggleTheme from '@/components/ToggleTheme.vue';
</script>

<template>
  <ToggleTheme class="fixed right-2 top-2" />
  <RouterView class="bg-white dark:bg-black" />
</template>
