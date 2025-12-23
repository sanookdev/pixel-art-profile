<script setup>
import { ref, onMounted } from 'vue';

const props = defineProps({
  theme: {
    type: String,
    default: 'sky' // sky, forest, cave, night, sunset
  }
});

const stars = ref([]);
const particles = ref([]);

onMounted(() => {
  // Generate stars for night theme
  if (props.theme === 'night' || props.theme === 'cave') {
    for (let i = 0; i < 50; i++) {
      stars.value.push({
        id: i,
        x: Math.random() * 100,
        y: Math.random() * 60,
        size: Math.random() * 3 + 1,
        delay: Math.random() * 3
      });
    }
  }
  
  // Generate floating particles
  for (let i = 0; i < 20; i++) {
    particles.value.push({
      id: i,
      x: Math.random() * 100,
      y: Math.random() * 100,
      size: Math.random() * 8 + 4,
      duration: Math.random() * 5 + 3,
      delay: Math.random() * 5
    });
  }
});
</script>

<template>
  <div :class="['parallax-bg', `theme-${theme}`]">
    <!-- Sky layers -->
    <div class="layer clouds-back"></div>
    <div class="layer clouds-front"></div>
    
    <!-- Stars (for night/cave) -->
    <div v-if="theme === 'night' || theme === 'cave'" class="stars-container">
      <div 
        v-for="star in stars" 
        :key="star.id"
        class="star"
        :style="{
          left: star.x + '%',
          top: star.y + '%',
          width: star.size + 'px',
          height: star.size + 'px',
          animationDelay: star.delay + 's'
        }"
      ></div>
    </div>
    
    <!-- Floating particles -->
    <div class="particles-container">
      <div 
        v-for="p in particles" 
        :key="p.id"
        :class="['particle', `particle-${theme}`]"
        :style="{
          left: p.x + '%',
          top: p.y + '%',
          width: p.size + 'px',
          height: p.size + 'px',
          animationDuration: p.duration + 's',
          animationDelay: p.delay + 's'
        }"
      ></div>
    </div>
    
    <!-- Mountains/Hills layer -->
    <div class="layer mountains"></div>
    
    <!-- Ground base -->
    <div class="ground-layer">
      <div class="ground-pattern"></div>
    </div>
  </div>
</template>

<style scoped>
.parallax-bg {
  position: absolute;
  inset: 0;
  overflow: hidden;
  z-index: 0;
}

.layer {
  position: absolute;
  width: 200%;
  height: 100%;
  pointer-events: none;
}

/* === CLOUDS === */
.clouds-back {
  top: 5%;
  background-image: 
    radial-gradient(ellipse 120px 80px at 10% 50%, rgba(255,255,255,0.6) 0%, transparent 70%),
    radial-gradient(ellipse 80px 50px at 30% 30%, rgba(255,255,255,0.5) 0%, transparent 70%),
    radial-gradient(ellipse 100px 60px at 60% 60%, rgba(255,255,255,0.5) 0%, transparent 70%),
    radial-gradient(ellipse 90px 55px at 85% 40%, rgba(255,255,255,0.6) 0%, transparent 70%);
  animation: cloudDrift 60s linear infinite;
}

.clouds-front {
  top: 10%;
  background-image: 
    radial-gradient(ellipse 150px 100px at 20% 40%, rgba(255,255,255,0.8) 0%, transparent 70%),
    radial-gradient(ellipse 100px 70px at 50% 60%, rgba(255,255,255,0.7) 0%, transparent 70%),
    radial-gradient(ellipse 120px 80px at 75% 35%, rgba(255,255,255,0.8) 0%, transparent 70%);
  animation: cloudDrift 40s linear infinite;
}

@keyframes cloudDrift {
  from { transform: translateX(0); }
  to { transform: translateX(-50%); }
}

/* === STARS === */
.stars-container {
  position: absolute;
  inset: 0;
}

.star {
  position: absolute;
  background: #fff;
  border-radius: 50%;
  animation: twinkle 2s ease-in-out infinite;
  box-shadow: 0 0 6px 2px rgba(255, 255, 255, 0.8);
}

@keyframes twinkle {
  0%, 100% { opacity: 1; transform: scale(1); }
  50% { opacity: 0.3; transform: scale(0.7); }
}

/* === PARTICLES === */
.particles-container {
  position: absolute;
  inset: 0;
}

.particle {
  position: absolute;
  border-radius: 50%;
  animation: floatParticle 5s ease-in-out infinite;
}

.particle-sky {
  background: radial-gradient(circle, rgba(255,255,255,0.8) 0%, transparent 70%);
}

.particle-forest {
  background: radial-gradient(circle, rgba(144, 238, 144, 0.6) 0%, transparent 70%);
}

.particle-cave {
  background: radial-gradient(circle, rgba(255, 215, 0, 0.6) 0%, transparent 70%);
  box-shadow: 0 0 10px rgba(255, 215, 0, 0.5);
}

.particle-night {
  background: radial-gradient(circle, rgba(138, 43, 226, 0.5) 0%, transparent 70%);
  box-shadow: 0 0 8px rgba(138, 43, 226, 0.4);
}

.particle-sunset {
  background: radial-gradient(circle, rgba(255, 182, 193, 0.7) 0%, transparent 70%);
  box-shadow: 0 0 8px rgba(255, 105, 180, 0.4);
}

@keyframes floatParticle {
  0%, 100% { 
    transform: translateY(0) translateX(0) rotate(0deg);
    opacity: 0.7;
  }
  25% { transform: translateY(-20px) translateX(10px) rotate(90deg); }
  50% { 
    transform: translateY(-30px) translateX(-10px) rotate(180deg);
    opacity: 1;
  }
  75% { transform: translateY(-15px) translateX(15px) rotate(270deg); }
}

/* === MOUNTAINS === */
.mountains {
  bottom: 100px;
  height: 200px;
  background-image: 
    linear-gradient(135deg, transparent 40%, rgba(0,0,0,0.1) 40%, rgba(0,0,0,0.1) 60%, transparent 60%),
    linear-gradient(225deg, transparent 40%, rgba(0,0,0,0.1) 40%, rgba(0,0,0,0.1) 60%, transparent 60%);
  background-size: 100px 100px;
  background-position: 0 100%;
}

/* === GROUND === */
.ground-layer {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  height: 100px;
}

.ground-pattern {
  width: 100%;
  height: 100%;
  background-image: 
    repeating-linear-gradient(
      90deg,
      transparent,
      transparent 30px,
      rgba(0,0,0,0.1) 30px,
      rgba(0,0,0,0.1) 32px
    );
}

/* === THEME COLORS === */
.theme-sky {
  background: linear-gradient(180deg, 
    #87CEEB 0%, 
    #B0E0E6 50%, 
    #E0F7FA 100%
  );
}

.theme-sky .ground-layer {
  background: linear-gradient(180deg, #8BC34A 0%, #4CAF50 100%);
}

.theme-forest {
  background: linear-gradient(180deg,
    #90EE90 0%,
    #98FB98 50%,
    #F1F8E9 100%
  );
}

.theme-forest .ground-layer {
  background: linear-gradient(180deg, #8D6E63 0%, #5D4037 100%);
}

.theme-forest .clouds-back,
.theme-forest .clouds-front {
  opacity: 0.3;
}

.theme-cave {
  background: linear-gradient(180deg,
    #1a0f0f 0%,
    #3E2723 50%,
    #4E342E 100%
  );
}

.theme-cave .ground-layer {
  background: linear-gradient(180deg, #5D4037 0%, #3E2723 100%);
}

.theme-cave .clouds-back,
.theme-cave .clouds-front {
  display: none;
}

.theme-night {
  background: linear-gradient(180deg,
    #0d0d2b 0%,
    #1a1a3e 40%,
    #263238 100%
  );
}

.theme-night .ground-layer {
  background: linear-gradient(180deg, #37474F 0%, #263238 100%);
}

.theme-night .clouds-back,
.theme-night .clouds-front {
  opacity: 0.1;
}

.theme-sunset {
  background: linear-gradient(180deg,
    #FF6B6B 0%,
    #FFB6C1 40%,
    #FFECEF 100%
  );
}

.theme-sunset .ground-layer {
  background: linear-gradient(180deg, #E91E63 0%, #C2185B 100%);
}

.theme-sunset .clouds-back,
.theme-sunset .clouds-front {
  background-image: 
    radial-gradient(ellipse 120px 80px at 10% 50%, rgba(255,200,200,0.7) 0%, transparent 70%),
    radial-gradient(ellipse 80px 50px at 30% 30%, rgba(255,180,180,0.6) 0%, transparent 70%),
    radial-gradient(ellipse 100px 60px at 60% 60%, rgba(255,220,220,0.6) 0%, transparent 70%);
}
</style>
