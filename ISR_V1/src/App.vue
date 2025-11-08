<template>
  <div class="w-full flex flex-col items-center">
    <Navbar />    <!-- 👈 navbar is here -->
    <router-view /> <!-- 👈 page content (Home.vue etc.) -->
  </div>
</template>

<script>
import Navbar from './components/Navbar.vue'

export default {
  components: { Navbar }
}
</script>
