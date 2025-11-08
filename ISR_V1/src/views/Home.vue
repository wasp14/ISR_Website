<template>
  <div class="w-full min-h-screen bg-gradient-to-b from-gray-50 via-gray-100 to-gray-200 text-gray-900 overflow-x-hidden">
    <!-- HERO SECTION -->
    <section
      ref="hero"
      class="relative w-full h-screen flex justify-center items-center overflow-hidden"
      :style="{ transform: `translateY(${parallaxOffset * 0.3}px)` }"
    >
      <!-- Carousel Image with zoom + fade -->
      <transition name="fade-zoom" mode="out-in">
        <img
          :key="currentImage"
          :src="images[currentImage]"
          alt="carousel"
          class="absolute w-full h-full object-cover"
        />
      </transition>

      <!-- Overlay -->
      <div class="absolute inset-0 bg-gradient-to-t from-white/80 to-transparent"></div>

      <!-- Cinematic Text -->
      <transition name="fade-up">
        <div
          v-if="textVisible"
          class="relative z-10 text-center px-6"
        >
          <h1 class="text-5xl md:text-6xl font-bold tracking-wide mb-3">
            Welcome to ISR
          </h1>
          <p class="text-gray-700 text-lg md:text-xl">
            Empowering communities through collective action
          </p>
        </div>
      </transition>

      <!-- Carousel Controls -->
      <button
        @click="prevImage"
        class="absolute left-5 top-1/2 transform -translate-y-1/2 bg-white/70 text-gray-900 rounded-full p-3 hover:bg-white/90 transition"
      >
        &#8592;
      </button>
      <button
        @click="nextImage"
        class="absolute right-5 top-1/2 transform -translate-y-1/2 bg-white/70 text-gray-900 rounded-full p-3 hover:bg-white/90 transition"
      >
        &#8594;
      </button>

      <!-- Dots Indicators -->
      <div class="absolute bottom-10 left-1/2 transform -translate-x-1/2 flex space-x-3 z-10">
        <span
          v-for="(image, index) in images"
          :key="index"
          @click="goToImage(index)"
          :class="[
            'w-3 h-3 rounded-full cursor-pointer transition-all',
            currentImage === index ? 'bg-gray-900' : 'bg-gray-400/60'
          ]"
        ></span>
      </div>
    </section>

    <!-- CARDS SECTION -->
    <section class="w-full flex justify-center items-center py-24">
      <div class="w-full max-w-6xl grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-10 px-6">
        <div
          v-for="(card, index) in cards"
          :key="index"
          class="bg-white p-8 rounded-2xl shadow-lg hover:shadow-2xl hover:-translate-y-2 transform transition-all duration-700"
          v-intersect="onIntersect"
          :class="card.visible ? 'opacity-100 translate-y-0 scale-100' : 'opacity-0 translate-y-10 scale-95'"
        >
          <div class="flex justify-center mb-4">
            <img :src="card.icon" alt="icon" class="w-16 h-16 object-contain" />
          </div>
          <h3 class="text-2xl font-semibold text-center mb-2">{{ card.title }}</h3>
          <p class="text-gray-600 text-center">{{ card.description }}</p>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
export default {
  name: "Home",
  data() {
    return {
      currentImage: 0,
      parallaxOffset: 0,
      textVisible: false,
      images: [
        "https://images.unsplash.com/photo-1508780709619-79562169bc64?auto=format&fit=crop&w=1500&q=80",
        "https://images.unsplash.com/photo-1522202176988-66273c2fd55f?auto=format&fit=crop&w=1500&q=80",
        "https://images.unsplash.com/photo-1515378791036-0648a3ef77b2?auto=format&fit=crop&w=1500&q=80",
      ],
      cards: [
        { title: "Education Drives", description: "Empowering students with access to quality learning opportunities.", icon: "https://cdn-icons-png.flaticon.com/512/3135/3135755.png", visible: false },
        { title: "Health Camps", description: "Organizing medical check-ups and health awareness programs.", icon: "https://cdn-icons-png.flaticon.com/512/3774/3774299.png", visible: false },
        { title: "Environmental Care", description: "Initiatives towards sustainability and greener communities.", icon: "https://cdn-icons-png.flaticon.com/512/3534/3534060.png", visible: false },
        { title: "Women Empowerment", description: "Workshops and projects to promote gender equality.", icon: "https://cdn-icons-png.flaticon.com/512/4359/4359963.png", visible: false },
        { title: "Skill Development", description: "Training programs to build professional and life skills.", icon: "https://cdn-icons-png.flaticon.com/512/1077/1077012.png", visible: false },
        { title: "Community Outreach", description: "Connecting with local communities for impactful change.", icon: "https://cdn-icons-png.flaticon.com/512/3135/3135715.png", visible: false },
      ],
      carouselInterval: null,
    };
  },
  mounted() {
    this.startCarousel();
    window.addEventListener("scroll", this.handleScroll);
    setTimeout(() => (this.textVisible = true), 600);
  },
  beforeUnmount() {
    window.removeEventListener("scroll", this.handleScroll);
    clearInterval(this.carouselInterval);
  },
  methods: {
    startCarousel() {
      this.carouselInterval = setInterval(() => {
        this.nextImage();
      }, 4000);
    },
    nextImage() {
      this.currentImage = (this.currentImage + 1) % this.images.length;
    },
    prevImage() {
      this.currentImage = (this.currentImage - 1 + this.images.length) % this.images.length;
    },
    goToImage(index) {
      this.currentImage = index;
    },
    handleScroll() {
      this.parallaxOffset = window.scrollY * 0.5;
    },
    onIntersect(entries) {
      entries.forEach((entry) => {
        if (entry.isIntersecting) {
          const card = this.cards.find((c) => !c.visible);
          if (card) card.visible = true;
        }
      });
    },
  },
  directives: {
    intersect: {
      mounted(el, binding) {
        const observer = new IntersectionObserver(binding.value, { threshold: 0.2 });
        observer.observe(el);
      },
    },
  },
};
</script>

<style scoped>
/* Fade for carousel */
.fade-zoom-enter-active, .fade-zoom-leave-active {
  transition: all 1.5s ease;
}
.fade-zoom-enter-from, .fade-zoom-leave-to {
  opacity: 0;
  transform: scale(1.05);
}
.fade-zoom-enter-to, .fade-zoom-leave-from {
  opacity: 1;
  transform: scale(1);
}

/* Text fade-up animation */
.fade-up-enter-active {
  transition: all 1s ease;
}
.fade-up-enter-from {
  opacity: 0;
  transform: translateY(40px);
}
</style>
