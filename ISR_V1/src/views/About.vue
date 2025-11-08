<template>
  <div class="about-page-wrapper">
    <div class="background-shapes">
      <div class="shape shape1"></div>
      <div class="shape shape2"></div>
      <div class="shape shape3"></div>
    </div>
    <div class="content-container">

      <!-- Main Header -->
      <header ref="headerEl" class="page-header">
        <h1 class="main-heading">
          <span class="heading-line heading-line-1">
            <span class="char" v-for="(char, i) in 'About'.split('')" :key="`a-${i}`" :style="{ 'animation-delay': `${i * 0.05}s` }">
              {{ char }}
            </span>
          </span>
          <span class="heading-line heading-line-2">
            <span class="char gradient-text" v-for="(char, i) in 'SCIT ISR'.split('')" :key="`b-${i}`" :style="{ 'animation-delay': `${(i + 5) * 0.05}s` }">
              {{ char === ' ' ? '&nbsp;' : char }}
            </span>
          </span>
        </h1>
        <p class="header-subtitle">
          SCIT ISR aims at integrating socially beneficial programs and practices into our institute`s learning programs and culture. ISR aims to make a difference by reaching out and giving back to the society. Through its various programmes it also strives make the world a better place to live.
        </p>
      </header>

      <!-- Main Content Grid -->
      <div class="main-grid">

        <!-- Left Column: Interactive Key Focus Areas -->
        <aside class="sidebar">
          <div
            v-for="(area, index) in focusAreas"
            :key="area.title"
            class="focus-card-wrapper"
            :class="{ 'active': activeArea === area.title }"
            @mouseover="activeArea = area.title"
            @mouseleave="activeArea = null"
          >
            <div class="focus-card-header">
              <div class="icon-wrapper">
                <component :is="area.icon" class="icon" />
              </div>
              <h3 class="focus-card-title">{{ area.title }}</h3>
            </div>
            <div class="focus-card-content">
              <img :src="area.image" :alt="area.title" class="content-image" />
              <p class="content-description">{{ area.description }}</p>
            </div>
          </div>
        </aside>

        <!-- Right Column: What We Do, Who We Are -->
        <main class="main-content">
          <div ref="mainContentEl" class="main-content-card animate-on-scroll">
            <div class="content-section">
              <section>
                <h2 ref="whatWeDoEl" class="section-heading animate-on-scroll"><span>What We Do?</span></h2>
                <div ref="missionPointsEl" class="mission-points-container animate-on-scroll">
                  <div class="mission-point" v-for="(point, index) in missionPoints" :key="point.title" :style="{'--delay-index': index}">
                    <div class="mission-icon-wrapper">
                      <component :is="point.icon" class="mission-icon" />
                    </div>
                    <div class="mission-text">
                      <h4 class="mission-title">{{ point.title }}</h4>
                      <p class="mission-description">{{ point.description }}</p>
                    </div>
                  </div>
                </div>
              </section>

              <section class="section-spacing">
                <h2 ref="whoWeAreEl" class="section-heading animate-on-scroll"><span>Who We Are?</span></h2>
                <div 
                  ref="teamImageContainerEl" 
                  class="image-container group animate-on-scroll"
                  @mousemove="handleMouseMove"
                  @mouseleave="resetImageTransform"
                >
                   <img src="https://isr.scit.edu/assets/img/slider/isr-about.jpg" alt="ISR Team" class="team-image" ref="teamImageEl">
                   <div class="image-overlay"></div>
                </div>
                <div ref="quoteEl" class="quote-block animate-on-scroll">
                  <blockquote class="quote-content">
                    <p>“We, as humans, have actually developed a sense of social responsibility. We have gone beyond our basic instincts.”</p>
                    <footer class="quote-author">— Jane Goodall</footer>
                  </blockquote>
                </div>
              </section>
            </div>
          </div>
        </main>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted, markRaw } from 'vue';
import { IconHeartHandshake, IconSchool, IconLeaf, IconUsers, IconPlant, IconBuildingCommunity, IconCpu } from '@tabler/icons-vue';

const activeArea = ref(null);

const focusAreas = ref([
  {
    title: 'Healthcare',
    description: 'SCIT students have contributed to the notion in "Don\'t add Years to your life, add life to Years" by helping severely ill people at organisations such as CIPLA, a palliative healthcare centre. Initiatives for awareness such as Thalassemia awareness, Breast cancer awareness, etc. have been conducted regularly through ISR.',
    icon: markRaw(IconHeartHandshake),
    image: 'https://images.unsplash.com/photo-1576091160550-2173dba999ef?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1170&q=80',
  },
  {
    title: 'Education',
    description: 'ISR TEACH has been consistently teaching to primary and secondary high school students. A group of highly motivated ISR members dedicate their time to help these school students excel in their curricular and co-curricular activities.',
    icon: markRaw(IconSchool),
    image: 'https://images.unsplash.com/photo-1523050854058-8df90110c9f1?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1170&q=80',
  },
  {
    title: 'Eco-Friendly',
    description: 'With initiatives such as Green Ganesh, tree plantation drives SCIT ISR students have learned the best way to contribute positively and give back to the environment.',
    icon: markRaw(IconLeaf),
    image: 'https://images.unsplash.com/photo-1421789665209-c9b2a435e3dc?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1171&q=80',
  },
  {
    title: 'Community Outreach',
    description: 'SCIT ISR students have travelled to the various orphanges and old age homes around Pune area.',
    icon: markRaw(IconUsers),
    image: 'https://images.unsplash.com/photo-1593113598332-cd288d649433?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1170&q=80',
  },
  {
    title: 'Go Green',
    description: 'Aims to promote the spirit of ‘Greener business, healthier bottom line’ which focuses on the awareness among Corporate regarding Green IT.',
    icon: markRaw(IconPlant),
    image: 'https://images.unsplash.com/photo-1509316975850-ff9c5deb0cf1?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1170&q=80',
  },
]);

const missionPoints = ref([
    {
        title: 'Youth Empowerment & Community Support',
        description: 'Assisting underprivileged children and orphans, raising awareness on reducing child labor, and making the youth believe in their potential to achieve their special purpose.',
        icon: markRaw(IconBuildingCommunity)
    },
    {
        title: 'Environmental Preservation',
        description: 'Striving for a pollution-free, clean environment by promoting renewable energy, reducing waste, saving resources, and encouraging tree plantation.',
        icon: markRaw(IconLeaf)
    },
    {
        title: 'Corporate Responsibility & Green IT',
        description: 'Promoting a ‘Greener business, healthier bottom line’ by bridging the gap between awareness and perception of Green IT among corporates.',
        icon: markRaw(IconCpu)
    }
]);

// --- Template Refs ---
const headerEl = ref(null);
const mainContentEl = ref(null);
const whatWeDoEl = ref(null);
const missionPointsEl = ref(null);
const whoWeAreEl = ref(null);
const teamImageContainerEl = ref(null);
const teamImageEl = ref(null);
const quoteEl = ref(null);

// --- 3D Parallax Image Logic ---
const handleMouseMove = (e) => {
  const container = teamImageContainerEl.value;
  const image = teamImageEl.value;
  if (!container || !image) return;

  const { left, top, width, height } = container.getBoundingClientRect();
  const x = (e.clientX - left) / width - 0.5;
  const y = (e.clientY - top) / height - 0.5;

  const rotateX = y * -10; // Max rotation
  const rotateY = x * 10;

  image.style.transform = `perspective(1000px) rotateX(${rotateX}deg) rotateY(${rotateY}deg) scale3d(1.05, 1.05, 1.05)`;
};

const resetImageTransform = () => {
  const image = teamImageEl.value;
  if (image) {
    image.style.transform = 'perspective(1000px) rotateX(0) rotateY(0) scale3d(1, 1, 1)';
  }
};


// --- Scroll Animation Logic ---
const observer = ref(null);

onMounted(() => {
  const elementsToObserve = [
    mainContentEl.value,
    whatWeDoEl.value,
    missionPointsEl.value,
    whoWeAreEl.value,
    teamImageContainerEl.value,
    quoteEl.value
  ].filter(Boolean);

  observer.value = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        entry.target.classList.add('is-visible');
      }
    });
  }, {
    threshold: 0.1
  });

  elementsToObserve.forEach(el => {
    if (el) observer.value.observe(el);
  });
});

onUnmounted(() => {
  if (observer.value) {
    observer.value.disconnect();
  }
});
</script>

<style scoped>
/* --- Keyframes for Animations --- */
@keyframes gradient-animation {
  0% { background-position: 0% 50%; }
  50% { background-position: 100% 50%; }
  100% { background-position: 0% 50%; }
}
@keyframes gradient-shine {
  0% { background-position: 200% center; }
  100% { background-position: -200% center; }
}
@keyframes float-shape {
  0% { transform: translateY(0px) translateX(0px) rotate(0deg); }
  50% { transform: translateY(-20px) translateX(10px) rotate(180deg); }
  100% { transform: translateY(0px) translateX(0px) rotate(360deg); }
}

@keyframes char-reveal {
  0% { opacity: 0; transform: translateY(20px) scale(0.8); }
  100% { opacity: 1; transform: translateY(0) scale(1); }
}

@keyframes draw-line {
  from { transform: scaleY(0); }
  to { transform: scaleY(1); }
}


/* --- General Page Styles --- */
.about-page-wrapper {
  background: linear-gradient(135deg, #e0f2f1, #e8f5e9, #e0f7fa);
  background-size: 200% 200%;
  color: #334155;
  font-family: 'Inter', sans-serif;
  padding-top: 8rem;
  padding-bottom: 8rem;
  overflow: hidden;
  position: relative;
  animation: gradient-animation 15s ease infinite;
}

.background-shapes {
  position: absolute; top: 0; left: 0;
  width: 100%; height: 100%;
  overflow: hidden; z-index: 0;
}
.shape {
  position: absolute; border-radius: 50%;
  background: radial-gradient(circle, rgba(16, 185, 129, 0.1), transparent 70%);
  animation: float-shape 20s ease-in-out infinite;
}
.shape1 { width: 300px; height: 300px; top: 10%; left: 5%; animation-duration: 25s; }
.shape2 { width: 200px; height: 200px; top: 50%; right: 10%; animation-duration: 20s; animation-delay: -5s; }
.shape3 { width: 250px; height: 250px; bottom: 10%; left: 20%; animation-duration: 30s; animation-delay: -10s; }

.content-container {
  max-width: 1280px; margin: 0 auto;
  padding: 0 1.5rem; position: relative; z-index: 1;
}

/* --- Header --- */
.page-header {
  text-align: center; margin-bottom: 6rem;
  min-height: 250px; display: flex;
  flex-direction: column; justify-content: center;
}
.main-heading {
  font-size: 3.5rem; font-weight: 800;
  color: #0f172a; letter-spacing: -0.025em;
  line-height: 1.1; margin-bottom: 1.5rem;
}
.main-heading .heading-line { display: block; }
.main-heading .char {
  display: inline-block; opacity: 0;
  animation: char-reveal 0.8s cubic-bezier(0.23, 1, 0.32, 1) forwards;
}
.gradient-text {
  background-image: linear-gradient(to right, #059669, #10b981, #22c55e, #10b981, #059669);
  -webkit-background-clip: text; background-clip: text;
  color: transparent;
  background-size: 200% auto;
  animation: gradient-shine 3s linear infinite;
}
.header-subtitle {
  font-size: 1.125rem; max-width: 48rem;
  margin: 0 auto; color: #475569; line-height: 1.75;
  opacity: 0; transform: translateY(10px);
  animation: char-reveal 1s ease 0.8s forwards; /* Delay starts after heading */
}

/* --- Grid Layout --- */
.main-grid {
  display: grid; grid-template-columns: 1fr; gap: 4rem;
}

/* --- Interactive Sidebar --- */
.sidebar {
  display: flex; flex-direction: column; gap: 1.5rem;
}
.focus-card-wrapper {
  background-color: rgba(255, 255, 255, 0.8); backdrop-filter: blur(10px);
  border-radius: 1rem;
  box-shadow: 0 4px 6px -1px rgb(0 0 0 / 0.05), 0 2px 4px -2px rgb(0 0 0 / 0.05);
  border: 1px solid rgba(255, 255, 255, 0.5);
  cursor: pointer; overflow: hidden;
  max-height: 95px;
  transition: max-height 0.5s cubic-bezier(0.23, 1, 0.32, 1), box-shadow 0.3s ease;
}
.focus-card-wrapper:hover, .focus-card-wrapper.active {
  max-height: 500px;
  box-shadow: 0 10px 15px -3px rgb(0 0 0 / 0.1), 0 4px 6px -4px rgb(0 0 0 / 0.1);
}
.focus-card-header {
  display: flex; align-items: center;
  padding: 1.5rem; gap: 1.25rem;
}
.icon-wrapper {
  flex-shrink: 0;
  background-image: linear-gradient(to bottom right, #10b981, #22c55e);
  color: white; border-radius: 0.75rem; padding: 0.75rem;
  box-shadow: 0 4px 10px rgba(16, 185, 129, 0.3);
  transition: transform 0.3s ease;
}
.focus-card-wrapper:hover .icon-wrapper { transform: scale(1.1); }
.icon { height: 1.75rem; width: 1.75rem; }
.focus-card-title { font-size: 1.25rem; font-weight: 700; color: #1e293b; }
.focus-card-content {
  padding: 0 1.5rem 1.5rem 1.5rem;
  opacity: 0; transition: opacity 0.5s ease 0.1s;
}
.focus-card-wrapper.active .focus-card-content { opacity: 1; }
.content-image {
  width: 100%; height: 160px; object-fit: cover;
  border-radius: 0.75rem; margin-bottom: 1rem;
}
.content-description { color: #475569; line-height: 1.625; font-size: 0.9rem; }

/* --- Main Content (Right Column) --- */
.main-content-card {
  background-color: rgba(255, 255, 255, 0.8); backdrop-filter: blur(10px);
  padding: 2.5rem; border-radius: 1rem; border: 1px solid rgba(255, 255, 255, 0.5);
  box-shadow: 0 4px 6px -1px rgb(0 0 0 / 0.05), 0 2px 4px -2px rgb(0 0 0 / 0.05);
}
.section-heading {
  font-size: 1.875rem; font-weight: 700; color: #0f172a;
  margin-bottom: 2.5rem; position: relative; display: inline-block;
}
.section-heading span { display: block; }
.section-heading::after {
  content: ''; position: absolute; bottom: -8px; left: 0;
  width: 50%; height: 4px;
  background-image: linear-gradient(to right, #10b981, #22c55e);
  border-radius: 2px;
}
.section-spacing { margin-top: 4rem; }
.image-container {
  border-radius: 0.75rem; overflow: hidden; position: relative;
  box-shadow: 0 10px 15px -3px rgb(0 0 0 / 0.1), 0 4px 6px -4px rgb(0 0 0 / 0.1);
  transform: perspective(1000px); /* Enable 3D space */
}
.team-image {
  width: 100%; height: auto; object-fit: cover;
  transition: transform 0.6s cubic-bezier(0.23, 1, 0.32, 1);
}
.image-overlay {
  position: absolute; inset: 0;
  background: linear-gradient(to top, rgba(0,0,0,0.5), transparent);
}
.quote-block {
  margin-top: 2rem; border-left: 4px solid #10b981;
  background-color: #f0fdf4; padding: 2rem;
  border-radius: 0 0.5rem 0.5rem 0; position: relative;
}
.quote-block::before {
  content: '“';
  position: absolute;
  top: -10px;
  left: -20px;
  font-size: 6rem;
  color: rgba(16, 185, 129, 0.1);
  font-family: serif;
  z-index: 0;
  line-height: 1;
}
.quote-content { font-style: italic; position: relative; z-index: 1; }
.quote-author {
  margin-top: 1rem; font-weight: 600;
  color: #059669; font-style: normal;
}

/* --- New Mission Points Section --- */
.mission-points-container {
  display: flex; flex-direction: column; gap: 2.5rem;
  position: relative; padding-left: 20px;
}
.mission-points-container::before {
  content: ''; position: absolute; left: 2px; top: 1.25rem;
  bottom: 1.25rem; width: 2px; background-color: #e2e8f0;
  transform-origin: top; transform: scaleY(0);
}
.mission-points-container.is-visible::before {
  animation: draw-line 1s cubic-bezier(0.23, 1, 0.32, 1) forwards;
}
.mission-point {
  display: flex; gap: 1.5rem; align-items: flex-start;
  position: relative;
  opacity: 0;
  transform: translateX(-20px);
  transition: opacity 0.5s ease, transform 0.5s ease;
  transition-delay: calc(var(--delay-index) * 0.2s + 0.5s); /* Delay based on line draw */
}
.mission-points-container.is-visible .mission-point {
  opacity: 1;
  transform: translateX(0);
}
.mission-icon-wrapper {
  flex-shrink: 0; width: 50px; height: 50px;
  display: flex; align-items: center; justify-content: center;
  border-radius: 50%; background-color: #10b981; color: white;
  box-shadow: 0 0 0 8px #f0fdf4; z-index: 1;
  margin-left: -24px;
}
.mission-icon { width: 24px; height: 24px; }
.mission-title { font-size: 1.125rem; font-weight: 600; color: #1e293b; margin-bottom: 0.5rem; }
.mission-description { font-size: 0.95rem; color: #475569; line-height: 1.6; }

/* --- Responsive Styles --- */
@media (min-width: 1024px) {
  .main-grid {
    grid-template-columns: 1fr 1.5fr; align-items: flex-start;
  }
  .main-heading { font-size: 4.5rem; }
}

/* --- Scroll Animation --- */
.animate-on-scroll {
  opacity: 0; transform: translateY(20px);
  transition: opacity 0.6s ease-out, transform 0.6s ease-out;
}
.animate-on-scroll.is-visible {
  opacity: 1; transform: translateY(0);
}
</style>

