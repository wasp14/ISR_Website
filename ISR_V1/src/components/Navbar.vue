<template>
  <transition name="fade-slide">
    <nav
      v-show="isVisible"
      class="fixed top-6 left-1/2 transform -translate-x-1/2 z-50
             bg-gray-900/70 text-white border border-gray-700/50
             rounded-full shadow-lg px-10 py-3 flex items-center justify-center
             space-x-10 backdrop-blur-md"
    >
      <!-- Navbar items inline -->
      <a
        v-for="item in navItems"
        :key="item.name"
        :href="item.link"
        class="flex items-center gap-2 text-sm font-semibold transition hover:scale-105"
        :class="activeSection === item.name
          ? 'text-blue-400'
          : 'text-gray-300'"
      >
        <component
          :is="item.icon"
          class="h-5 w-5"
          :class="activeSection === item.name
            ? 'text-blue-400'
            : 'text-gray-300'"
        />
        <span>{{ item.name }}</span>
      </a>
    </nav>
  </transition>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from "vue";
import { IconHome, IconMessage, IconUser } from "@tabler/icons-vue";

const navItems = [
  { name: "Home", link: "#home", icon: IconHome },
  { name: "About", link: "#about", icon: IconUser },
  { name: "Contact", link: "#contact", icon: IconMessage },
];

// Show/hide navbar on scroll
const isVisible = ref(true);
let lastScrollY = window.scrollY;

const handleScroll = () => {
  const currentScrollY = window.scrollY;
  if (currentScrollY > lastScrollY && currentScrollY > 100) {
    isVisible.value = false;
  } else {
    isVisible.value = true;
  }
  lastScrollY = currentScrollY;
};

// Highlight active section
const activeSection = ref("Home");

const observeSections = () => {
  const sections = document.querySelectorAll("section");
  const options = { threshold: 0.6 };

  const observer = new IntersectionObserver((entries) => {
    entries.forEach((entry) => {
      if (entry.isIntersecting) {
        activeSection.value = entry.target.getAttribute("data-name");
      }
    });
  }, options);

  sections.forEach((section) => observer.observe(section));
};

onMounted(() => {
  window.addEventListener("scroll", handleScroll);
  observeSections();
});

onUnmounted(() => {
  window.removeEventListener("scroll", handleScroll);
});
</script>

<style scoped>
.fade-slide-enter-active,
.fade-slide-leave-active {
  transition: all 0.4s ease;
}
.fade-slide-enter-from,
.fade-slide-leave-to {
  opacity: 0;
  transform: translateY(-30px);
}
</style>
