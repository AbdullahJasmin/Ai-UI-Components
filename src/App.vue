<script setup lang="ts">
import { RouterLink, RouterView } from "vue-router";

import AppSidebar from '@/components/AppSidebar.vue'
import { SidebarProvider, SidebarTrigger } from '@/components/ui/sidebar'

import ToggleTheme from '@/components/ToggleTheme.vue';
import SidebarInset from "./components/ui/sidebar/SidebarInset.vue";
import Separator from "./components/ui/separator/Separator.vue";



</script>

<template>


    <SidebarProvider>
        <AppSidebar />

        <SidebarInset class="overflow-hidden h-screen">
            <header
                class=" absolute w-full z-50  flex h-16 shrink-0 items-center gap-2 border-b border-neutral-200 dark:border-neutral-700 bg-white dark:bg-neutral-900">
                <div class="flex items-center gap-2 px-3">
                    <SidebarTrigger />
                    <Separator orientation="vertical" class="mr-2 h-4" />
                    AI App Components UI Kit
                </div>
                <ToggleTheme class=" ml-auto mr-3" />
            </header>
            <div class="w-full transition-all duration-300 h-screen p-10 mt-5 sm:px-20 overflow-auto">
                <RouterView />
            </div>
        </SidebarInset>
    </SidebarProvider>

</template>