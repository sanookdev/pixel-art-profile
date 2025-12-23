<script setup>
import { ref, onMounted } from 'vue';

const props = defineProps({
  theme: {
    type: String,
    default: 'meadow' // meadow, forest, mountain, sunset, night, beach
  }
});

const stars = ref([]);
const clouds = ref([]);

onMounted(() => {
  // Generate stars for night theme
  if (props.theme === 'night') {
    for (let i = 0; i < 60; i++) {
      stars.value.push({
        id: i,
        x: Math.random() * 100,
        y: Math.random() * 50,
        size: Math.random() * 3 + 1,
        delay: Math.random() * 3
      });
    }
  }
  
  // Generate clouds
  for (let i = 0; i < 5; i++) {
    clouds.value.push({
      id: i,
      x: i * 25 + Math.random() * 10,
      y: 5 + Math.random() * 15,
      scale: 0.8 + Math.random() * 0.4,
      speed: 40 + Math.random() * 30
    });
  }
});
</script>

<template>
  <div :class="['parallax-bg', `theme-${theme}`]">
    <!-- Sky gradient base -->
    <div class="sky-layer"></div>
    
    <!-- Sun/Moon -->
    <div v-if="theme !== 'night'" class="sun"></div>
    <div v-if="theme === 'night'" class="moon"></div>
    
    <!-- Clouds (pixel style) -->
    <div v-if="theme !== 'night'" class="clouds-layer">
      <div 
        v-for="cloud in clouds" 
        :key="cloud.id"
        class="pixel-cloud"
        :style="{
          left: cloud.x + '%',
          top: cloud.y + '%',
          transform: `scale(${cloud.scale})`,
          animationDuration: cloud.speed + 's'
        }"
      >
        <div class="cloud-part"></div>
        <div class="cloud-part p2"></div>
        <div class="cloud-part p3"></div>
        <div class="cloud-part p4"></div>
      </div>
    </div>
    
    <!-- Stars for night -->
    <div v-if="theme === 'night'" class="stars-layer">
      <div 
        v-for="star in stars" 
        :key="star.id"
        class="pixel-star"
        :style="{
          left: star.x + '%',
          top: star.y + '%',
          width: star.size + 'px',
          height: star.size + 'px',
          animationDelay: star.delay + 's'
        }"
      ></div>
    </div>
    
    <!-- Background mountains (far) -->
    <div class="mountain-layer far"></div>
    
    <!-- Middle mountains -->
    <div class="mountain-layer mid"></div>
    
    <!-- Trees layer (left and right) -->
    <div class="trees-layer">
      <div class="pixel-tree left t1"></div>
      <div class="pixel-tree left t2"></div>
      <div class="pixel-tree right t1"></div>
      <div class="pixel-tree right t2"></div>
    </div>
    
    <!-- River/Water (for meadow theme) -->
    <div v-if="theme === 'meadow' || theme === 'forest'" class="water-layer"></div>
    
    <!-- Waterfall (for mountain theme) -->
    <div v-if="theme === 'mountain'" class="waterfall">
      <div class="water-stream"></div>
    </div>
    
    <!-- Ground with grass -->
    <div class="ground-layer">
      <div class="grass-detail"></div>
    </div>
    
    <!-- Path/Road for character to walk -->
    <div class="path-layer"></div>
  </div>
</template>

<style scoped>
.parallax-bg {
  position: absolute;
  inset: 0;
  overflow: hidden;
  z-index: 0;
  image-rendering: pixelated;
}

/* === SKY === */
.sky-layer {
  position: absolute;
  inset: 0;
}

/* === SUN === */
.sun {
  position: absolute;
  right: 15%;
  top: 10%;
  width: 60px;
  height: 60px;
  background: #FFE135;
  border-radius: 50%;
  box-shadow: 
    0 0 40px #FFE135,
    0 0 80px rgba(255, 225, 53, 0.5);
  animation: sunPulse 4s ease-in-out infinite;
}

@keyframes sunPulse {
  0%, 100% { transform: scale(1); box-shadow: 0 0 40px #FFE135, 0 0 80px rgba(255, 225, 53, 0.5); }
  50% { transform: scale(1.05); box-shadow: 0 0 50px #FFE135, 0 0 100px rgba(255, 225, 53, 0.6); }
}

/* === MOON === */
.moon {
  position: absolute;
  right: 20%;
  top: 10%;
  width: 50px;
  height: 50px;
  background: #FFFACD;
  border-radius: 50%;
  box-shadow: 0 0 30px rgba(255, 250, 205, 0.8);
}

/* === PIXEL CLOUDS === */
.clouds-layer {
  position: absolute;
  inset: 0;
  pointer-events: none;
}

.pixel-cloud {
  position: absolute;
  animation: cloudFloat linear infinite;
}

.cloud-part {
  position: absolute;
  background: #fff;
  border-radius: 4px;
}

.cloud-part:nth-child(1) { width: 40px; height: 20px; left: 10px; top: 10px; }
.cloud-part:nth-child(2) { width: 25px; height: 25px; left: 0; top: 15px; }
.cloud-part:nth-child(3) { width: 30px; height: 25px; left: 30px; top: 15px; }
.cloud-part:nth-child(4) { width: 50px; height: 15px; left: 5px; top: 25px; }

@keyframes cloudFloat {
  0% { transform: translateX(0); }
  100% { transform: translateX(150vw); }
}

/* === STARS === */
.stars-layer {
  position: absolute;
  inset: 0;
}

.pixel-star {
  position: absolute;
  background: #fff;
  animation: twinkle 2s ease-in-out infinite;
}

@keyframes twinkle {
  0%, 100% { opacity: 1; }
  50% { opacity: 0.3; }
}

/* === MOUNTAINS === */
.mountain-layer {
  position: absolute;
  bottom: 100px;
  left: 0;
  right: 0;
}

.mountain-layer.far {
  height: 180px;
  background: 
    linear-gradient(135deg, transparent 50%, #5B7C6F 50%) 0 100%,
    linear-gradient(225deg, transparent 50%, #4A6B5E 50%) 0 100%,
    linear-gradient(135deg, transparent 50%, #6B8C7F 50%) 200px 100%,
    linear-gradient(225deg, transparent 50%, #5B7C6F 50%) 200px 100%,
    linear-gradient(135deg, transparent 50%, #5B7C6F 50%) 400px 100%,
    linear-gradient(225deg, transparent 50%, #4A6B5E 50%) 400px 100%;
  background-size: 200px 180px;
  background-repeat: repeat-x;
  opacity: 0.6;
}

.mountain-layer.mid {
  height: 140px;
  background: 
    linear-gradient(140deg, transparent 45%, #3D5C4B 45%) 0 100%,
    linear-gradient(220deg, transparent 45%, #2D4C3B 45%) 0 100%,
    linear-gradient(140deg, transparent 45%, #4D6C5B 45%) 150px 100%,
    linear-gradient(220deg, transparent 45%, #3D5C4B 45%) 150px 100%;
  background-size: 150px 140px;
  background-repeat: repeat-x;
  opacity: 0.8;
}

/* === PIXEL TREES === */
.trees-layer {
  position: absolute;
  bottom: 80px;
  left: 0;
  right: 0;
  height: 120px;
  pointer-events: none;
}

.pixel-tree {
  position: absolute;
  width: 0;
  height: 0;
}

.pixel-tree.left.t1 {
  left: 5%;
  border-left: 25px solid transparent;
  border-right: 25px solid transparent;
  border-bottom: 70px solid #2E7D32;
}

.pixel-tree.left.t1::before {
  content: '';
  position: absolute;
  left: -15px;
  top: 35px;
  border-left: 20px solid transparent;
  border-right: 20px solid transparent;
  border-bottom: 50px solid #388E3C;
}

.pixel-tree.left.t1::after {
  content: '';
  position: absolute;
  left: -5px;
  top: 65px;
  width: 12px;
  height: 25px;
  background: #5D4037;
}

.pixel-tree.left.t2 {
  left: 12%;
  border-left: 20px solid transparent;
  border-right: 20px solid transparent;
  border-bottom: 55px solid #43A047;
}

.pixel-tree.left.t2::after {
  content: '';
  position: absolute;
  left: -4px;
  top: 50px;
  width: 10px;
  height: 20px;
  background: #6D4C41;
}

.pixel-tree.right.t1 {
  right: 5%;
  border-left: 25px solid transparent;
  border-right: 25px solid transparent;
  border-bottom: 65px solid #2E7D32;
}

.pixel-tree.right.t1::after {
  content: '';
  position: absolute;
  left: -5px;
  top: 60px;
  width: 12px;
  height: 22px;
  background: #5D4037;
}

.pixel-tree.right.t2 {
  right: 12%;
  border-left: 18px solid transparent;
  border-right: 18px solid transparent;
  border-bottom: 50px solid #66BB6A;
}

.pixel-tree.right.t2::after {
  content: '';
  position: absolute;
  left: -4px;
  top: 46px;
  width: 9px;
  height: 18px;
  background: #6D4C41;
}

/* === WATER/RIVER === */
.water-layer {
  position: absolute;
  bottom: 70px;
  left: 30%;
  right: 20%;
  height: 30px;
  background: linear-gradient(90deg, 
    transparent 0%,
    #64B5F6 10%,
    #42A5F5 50%,
    #64B5F6 90%,
    transparent 100%
  );
  border-radius: 50%;
  opacity: 0.9;
  animation: waterShimmer 2s ease-in-out infinite;
}

@keyframes waterShimmer {
  0%, 100% { opacity: 0.9; }
  50% { opacity: 0.7; }
}

/* === WATERFALL === */
.waterfall {
  position: absolute;
  right: 20%;
  bottom: 80px;
  width: 30px;
  height: 100px;
}

.water-stream {
  width: 100%;
  height: 100%;
  background: linear-gradient(180deg, 
    #90CAF9 0%,
    #64B5F6 50%,
    #42A5F5 100%
  );
  animation: waterfallFlow 0.5s linear infinite;
}

@keyframes waterfallFlow {
  0% { background-position: 0 0; }
  100% { background-position: 0 20px; }
}

/* === GROUND === */
.ground-layer {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  height: 80px;
}

.grass-detail {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  height: 15px;
  background: repeating-linear-gradient(
    90deg,
    transparent 0px,
    transparent 8px,
    rgba(0,0,0,0.1) 8px,
    rgba(0,0,0,0.1) 10px
  );
}

/* === PATH/ROAD === */
.path-layer {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  height: 50px;
  background: linear-gradient(180deg, 
    #8D6E63 0%,
    #795548 30%,
    #6D4C41 100%
  );
  border-top: 4px solid #A1887F;
}

.path-layer::before {
  content: '';
  position: absolute;
  top: 50%;
  left: 0;
  right: 0;
  height: 4px;
  background: repeating-linear-gradient(
    90deg,
    #BCAAA4 0px,
    #BCAAA4 30px,
    transparent 30px,
    transparent 50px
  );
  transform: translateY(-50%);
}

/* === THEME VARIATIONS === */

/* Meadow - Bright sunny day */
.theme-meadow .sky-layer {
  background: linear-gradient(180deg, 
    #87CEEB 0%, 
    #B0E2FF 40%,
    #E8F5E9 100%
  );
}

.theme-meadow .ground-layer {
  background: linear-gradient(180deg, #7CB342 0%, #558B2F 100%);
}

/* Forest - Dense green */
.theme-forest .sky-layer {
  background: linear-gradient(180deg, 
    #81C784 0%, 
    #A5D6A7 40%,
    #C8E6C9 100%
  );
}

.theme-forest .ground-layer {
  background: linear-gradient(180deg, #33691E 0%, #1B5E20 100%);
}

.theme-forest .sun {
  opacity: 0.6;
  filter: blur(2px);
}

/* Mountain - Rocky terrain */
.theme-mountain .sky-layer {
  background: linear-gradient(180deg, 
    #90CAF9 0%, 
    #BBDEFB 50%,
    #E3F2FD 100%
  );
}

.theme-mountain .ground-layer {
  background: linear-gradient(180deg, #78909C 0%, #546E7A 100%);
}

.theme-mountain .mountain-layer.far {
  background: 
    linear-gradient(130deg, transparent 40%, #78909C 40%) 0 100%,
    linear-gradient(230deg, transparent 40%, #607D8B 40%) 0 100%;
  background-size: 180px 200px;
  height: 220px;
  opacity: 0.9;
}

/* Sunset - Orange/pink sky */
.theme-sunset .sky-layer {
  background: linear-gradient(180deg, 
    #FF8A65 0%, 
    #FFAB91 30%,
    #FFCCBC 60%,
    #FBE9E7 100%
  );
}

.theme-sunset .sun {
  background: #FF5722;
  box-shadow: 0 0 60px #FF5722, 0 0 120px rgba(255, 87, 34, 0.5);
  top: 25%;
  width: 70px;
  height: 70px;
}

.theme-sunset .ground-layer {
  background: linear-gradient(180deg, #8D6E63 0%, #5D4037 100%);
}

.theme-sunset .pixel-cloud .cloud-part {
  background: #FFCCBC;
}

/* Night - Dark starry sky */
.theme-night .sky-layer {
  background: linear-gradient(180deg, 
    #0D1B2A 0%, 
    #1B263B 40%,
    #415A77 100%
  );
}

.theme-night .ground-layer {
  background: linear-gradient(180deg, #1B3A4B 0%, #0D1B2A 100%);
}

.theme-night .pixel-tree.left.t1,
.theme-night .pixel-tree.right.t1 {
  border-bottom-color: #1B4332;
}

.theme-night .pixel-tree.left.t2,
.theme-night .pixel-tree.right.t2 {
  border-bottom-color: #2D6A4F;
}

.theme-night .path-layer {
  background: linear-gradient(180deg, #37474F 0%, #263238 100%);
  border-top-color: #455A64;
}

.theme-night .path-layer::before {
  background: repeating-linear-gradient(
    90deg,
    #546E7A 0px,
    #546E7A 30px,
    transparent 30px,
    transparent 50px
  );
}

/* Beach - Sandy with ocean */
.theme-beach .sky-layer {
  background: linear-gradient(180deg, 
    #4FC3F7 0%, 
    #81D4FA 40%,
    #B3E5FC 100%
  );
}

.theme-beach .ground-layer {
  background: linear-gradient(180deg, #FFE082 0%, #FFCA28 100%);
}

.theme-beach .water-layer {
  bottom: 50px;
  height: 50px;
  left: 0;
  right: 0;
  background: linear-gradient(180deg, 
    #4FC3F7 0%,
    #29B6F6 50%,
    #03A9F4 100%
  );
  border-radius: 0;
  animation: waves 3s ease-in-out infinite;
}

@keyframes waves {
  0%, 100% { transform: translateY(0); }
  50% { transform: translateY(-5px); }
}

.theme-beach .path-layer {
  background: linear-gradient(180deg, #FFECB3 0%, #FFE082 100%);
  border-top-color: #FFF8E1;
}

.theme-beach .path-layer::before {
  display: none;
}

/* Desert theme */
.theme-desert .sky-layer {
  background: linear-gradient(180deg, 
    #FFEB3B 0%, 
    #FFF59D 40%,
    #FFFDE7 100%
  );
}

.theme-desert .ground-layer {
  background: linear-gradient(180deg, #D7CCC8 0%, #A1887F 100%);
}

.theme-desert .path-layer {
  background: linear-gradient(180deg, #BCAAA4 0%, #8D6E63 100%);
}

.theme-desert .pixel-tree {
  display: none;
}

.theme-desert .mountain-layer.far,
.theme-desert .mountain-layer.mid {
  background: 
    linear-gradient(135deg, transparent 50%, #D7CCC8 50%) 0 100%,
    linear-gradient(225deg, transparent 50%, #BCAAA4 50%) 0 100%;
  background-size: 120px 100px;
}
</style>
