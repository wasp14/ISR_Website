<template>
  <header class="fixed top-3 left-0 w-full z-50 flex justify-center items-start h-12">
    <!-- Glass background bar -->
    <div
      :class="[
        'absolute top-0 w-4/5 h-10 rounded-2xl shadow-lg backdrop-blur-md transition-all duration-500 ease-in-out',
        isHidden ? '-translate-y-full opacity-0' : 'translate-y-0 opacity-100 bg-gray-900/70'
      ]"
    ></div>

    <!-- Navbar links/icons (slide and fade on scroll) -->
    <nav
      class="absolute flex items-center justify-between h-10 w-4/5 transition-all duration-500 ease-in-out"
      :class="isHidden ? '-translate-y-2 opacity-80' : 'translate-y-0 opacity-100'"
    >
      <!-- Left links -->
      <div class="flex items-center space-x-4">
        <a
          v-for="item in leftItems"
          :key="item.name"
          :href="item.link"
          class="flex items-center transition-all duration-300 ease-in-out text-sm group px-2 py-1 rounded-md hover:scale-105 hover:bg-white/10"
        >
          <!-- <component
            :is="item.icon"
            class="w-4 h-4 mr-1 text-white group-hover:text-blue-400 transition-colors duration-300 ease-in-out"
          /> -->
          <span class="font-semibold leading-none text-white group-hover:text-blue-400 transition-colors duration-300 ease-in-out">
            {{ item.name }}
          </span>
        </a>
      </div>

      <!-- Center logo -->
      <div class="flex justify-center items-center">
        <img src="@/assets/isr_logo.png" alt="Committee Logo" class="h-8 w-auto"/>
      </div>

      <!-- Right links -->
      <div class="flex items-center space-x-4">
        <a
          v-for="item in rightItems"
          :key="item.name"
          :href="item.link"
          class="flex items-center transition-all duration-300 ease-in-out text-sm group px-2 py-1 rounded-md hover:scale-105 hover:bg-white/10"
        >
          <!-- <component
            :is="item.icon"
            class="w-4 h-4 mr-1 text-white group-hover:text-blue-400 transition-colors duration-300 ease-in-out"
          /> -->
          <span class="font-semibold leading-none text-white group-hover:text-blue-400 transition-colors duration-300 ease-in-out">
            {{ item.name }}
          </span>
        </a>
      </div>
    </nav>
  </header>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import { IconHome, IconUser, IconMessage, IconTilde, IconChalkboardTeacher, IconCalendarEvent } from '@tabler/icons-vue'

const isHidden = ref(false)
let lastScrollY = 0

// Split links to left and right of logo
const leftItems = [
  { name: 'Home', link: '/', icon: IconHome },
    { name: 'About', link: '/about', icon: IconTilde },
  { name: 'Contact', link: '/contact', icon: IconMessage },
  { name: 'ISR Team', link: '/about', icon: IconUser },
]
const rightItems = [

  { name: 'ISR Initiatives', link: '/contact', icon: IconMessage },
  { name: 'ISR Teach', link: '/about', icon: IconChalkboardTeacher },
  { name: 'Annual Events', link: '/contact', icon: IconCalendarEvent },
  { name: 'Research', link: '/about', icon: IconUser },
  
]

const handleScroll = () => {
  const currentScroll = window.scrollY
  if (currentScroll > lastScrollY && currentScroll > 30) {
    isHidden.value = true
  } else {
    isHidden.value = false
  }
  lastScrollY = currentScroll
}

onMounted(() => window.addEventListener('scroll', handleScroll))
onUnmounted(() => window.removeEventListener('scroll', handleScroll))
</script>

<style scoped>
nav a {
  letter-spacing: 0.5px;
}
</style>
