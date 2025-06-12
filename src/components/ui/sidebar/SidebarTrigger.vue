<script setup lang="ts">
import type { HTMLAttributes } from 'vue'

import { Icon } from '@iconify/vue'
import { useSidebar } from './utils'

const props = defineProps<{
  class?: HTMLAttributes['class']
}>()

const { toggleSidebar } = useSidebar()
</script>

<template>

  <button
    class="group px-4 py-2 border rounded-lg  flex items-center overflow-hidden transition-all duration-300 border-neutral-300 bg-neutral-50 dark:border-neutral-700 dark:bg-neutral-900 hover:bg-neutral-100 dark:hover:bg-neutral-800"
    @click="toggleSidebar">
    <Icon icon="lucide:menu" :height="24" :width="24"
      class="text-neutral-600 dark:text-neutral-300 group-hover:text-neutral-400" />
    <span class="sr-only">Toggle Sidebar</span>
  </button>
</template>
