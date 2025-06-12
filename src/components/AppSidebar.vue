<script setup lang="ts">
import { ChevronRight } from 'lucide-vue-next'
import SearchForm from '@/components/SearchForm.vue'
import VersionSwitcher from '@/components/VersionSwitcher.vue'
import {
  Collapsible,
  CollapsibleContent,
  CollapsibleTrigger,
} from '@/components/ui/collapsible'
import {
  Sidebar,
  SidebarContent,
  SidebarGroup,
  SidebarGroupContent,
  SidebarGroupLabel,
  SidebarHeader,
  SidebarMenu,
  SidebarMenuButton,
  SidebarMenuItem,
  type SidebarProps,
  SidebarRail,
} from '@/components/ui/sidebar'
import SidebarFooter from './ui/sidebar/SidebarFooter.vue'
import NavUser from './NavUser.vue'

const props = defineProps<SidebarProps>()

// This is sample data.
const data = {
  user: {
    name: 'Abdullah Jasmin',
    email: 'UI/UX Engineer',
    avatar: '/Abdullah.webp',
  },
  versions: ['0.0.1'],
  navMain: [
    {
      title: 'Getting Started',
      url: '#',
      open: true,
      items: [
        {
          title: 'Installation',
          url: '#',
          isActive: true,
        },
        {
          title: 'Project Structure',
          url: '#',
        },
      ],
    },

    {
      title: 'Architecture',
      url: '#',
      items: [
        {
          title: 'Accessibility',
          url: '#',
        },
        {
          title: 'Fast Refresh',
          url: '#',
        },
        {
          title: 'Next.js Compiler',
          url: '#',
        },
        {
          title: 'Supported Browsers',
          url: '#',
        },
        {
          title: 'Turbopack',
          url: '#',
        },
      ],
    },
    {
      title: 'Community',
      url: '#',
      items: [
        {
          title: 'Contribution Guide',
          url: '#',
        },
      ],
    },
  ],
}
</script>

<template>
  <Sidebar v-bind="props">
    <SidebarHeader>
      <VersionSwitcher :versions="data.versions" :default-version="data.versions[0]" />
      <SearchForm />
    </SidebarHeader>
    <SidebarContent class="gap-0">
      <Collapsible v-for="item in data.navMain" :key="item.title" :title="item.title" default-closed :open="item.open"
        class="group/collapsible">
        <SidebarGroup>
          <SidebarGroupLabel as-child
            class="group/label text-sm text-sidebar-foreground hover:bg-sidebar-accent hover:text-sidebar-accent-foreground">
            <CollapsibleTrigger>
              {{ item.title }}
              <ChevronRight class="ml-auto transition-transform group-data-[state=open]/collapsible:rotate-90" />
            </CollapsibleTrigger>
          </SidebarGroupLabel>
          <CollapsibleContent>
            <SidebarGroupContent>
              <SidebarMenu>
                <SidebarMenuItem v-for="childItem in item.items" :key="childItem.title">
                  <SidebarMenuButton as-child :is-active="childItem.isActive">
                    <RouterLink :to="item.url">{{ childItem.title }}</RouterLink>
                  </SidebarMenuButton>
                </SidebarMenuItem>
              </SidebarMenu>
            </SidebarGroupContent>
          </CollapsibleContent>
        </SidebarGroup>
      </Collapsible>
    </SidebarContent>
    <SidebarFooter>
      <NavUser :user="data.user" />
    </SidebarFooter>
    <SidebarRail />
  </Sidebar>
</template>
