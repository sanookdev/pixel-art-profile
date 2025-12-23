<script setup>
const props = defineProps({
  theme: {
    type: String,
    default: 'grass' // grass, dirt, stone, castle, snow
  }
});
</script>

<template>
  <div :class="['pixel-ground', `ground-${theme}`]">
    <div class="ground-top">
      <div class="grass-blades" v-if="theme === 'grass'">
        <span v-for="n in 20" :key="n" class="blade"></span>
      </div>
    </div>
    <div class="ground-middle">
      <div class="block-pattern"></div>
    </div>
    <div class="ground-bottom"></div>
    
    <!-- Decorative elements -->
    <div class="decorations">
      <div v-if="theme === 'grass'" class="flower" style="left: 10%;">🌻</div>
      <div v-if="theme === 'grass'" class="flower" style="left: 30%;">🌷</div>
      <div v-if="theme === 'grass'" class="flower" style="left: 70%;">🌼</div>
      <div v-if="theme === 'stone'" class="gem" style="left: 25%;">💎</div>
      <div v-if="theme === 'stone'" class="gem" style="left: 65%;">💎</div>
      <div v-if="theme === 'dirt'" class="mushroom" style="left: 45%;">🍄</div>
      <div v-if="theme === 'castle'" class="flag" style="left: 50%;">🏰</div>
    </div>
  </div>
</template>

<style scoped>
.pixel-ground {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  height: 100px;
  z-index: 10;
  image-rendering: pixelated;
}

.ground-top {
  height: 20px;
  position: relative;
}

.ground-middle {
  height: 50px;
}

.ground-bottom {
  height: 30px;
}

/* === GRASS THEME === */
.ground-grass .ground-top {
  background: linear-gradient(180deg, #4CAF50 0%, #388E3C 100%);
  border-top: 4px solid #66BB6A;
}

.ground-grass .ground-middle {
  background: repeating-linear-gradient(
    0deg,
    #8D6E63 0px,
    #8D6E63 12px,
    #795548 12px,
    #795548 24px
  );
  background-size: 24px 24px;
}

.ground-grass .ground-bottom {
  background: #5D4037;
}

/* Grass blades animation */
.grass-blades {
  position: absolute;
  top: -15px;
  left: 0;
  right: 0;
  height: 20px;
  display: flex;
  justify-content: space-around;
}

.blade {
  width: 4px;
  height: 15px;
  background: #66BB6A;
  transform-origin: bottom center;
  animation: sway 2s ease-in-out infinite;
  animation-delay: calc(var(--i, 0) * 0.1s);
  border-radius: 2px 2px 0 0;
}

.blade:nth-child(odd) {
  animation-direction: reverse;
  height: 12px;
}

@keyframes sway {
  0%, 100% { transform: rotate(-5deg); }
  50% { transform: rotate(5deg); }
}

/* === DIRT THEME === */
.ground-dirt .ground-top {
  background: #8D6E63;
  border-top: 4px solid #A1887F;
}

.ground-dirt .ground-middle {
  background: repeating-linear-gradient(
    0deg,
    #795548 0px,
    #795548 16px,
    #5D4037 16px,
    #5D4037 32px
  );
}

.ground-dirt .ground-bottom {
  background: #4E342E;
}

/* === STONE THEME === */
.ground-stone .ground-top {
  background: #546E7A;
  border-top: 4px solid #78909C;
}

.ground-stone .ground-middle {
  background: 
    repeating-linear-gradient(
      90deg,
      #455A64 0px,
      #455A64 30px,
      #37474F 30px,
      #37474F 32px
    ),
    repeating-linear-gradient(
      0deg,
      #455A64 0px,
      #455A64 20px,
      #37474F 20px,
      #37474F 22px
    );
}

.ground-stone .ground-bottom {
  background: #263238;
}

/* === CASTLE THEME === */
.ground-castle .ground-top {
  background: linear-gradient(180deg, #E91E63 0%, #C2185B 100%);
  border-top: 4px solid #F48FB1;
}

.ground-castle .ground-middle {
  background: repeating-linear-gradient(
    90deg,
    #AD1457 0px,
    #AD1457 25px,
    #880E4F 25px,
    #880E4F 50px
  );
}

.ground-castle .ground-bottom {
  background: #4A0833;
}

/* === SNOW THEME === */
.ground-snow .ground-top {
  background: linear-gradient(180deg, #ECEFF1 0%, #CFD8DC 100%);
  border-top: 4px solid #FFFFFF;
}

.ground-snow .ground-middle {
  background: repeating-linear-gradient(
    0deg,
    #B0BEC5 0px,
    #B0BEC5 15px,
    #90A4AE 15px,
    #90A4AE 30px
  );
}

.ground-snow .ground-bottom {
  background: #78909C;
}

/* === DECORATIONS === */
.decorations {
  position: absolute;
  top: -30px;
  left: 0;
  right: 0;
  height: 30px;
}

.flower, .mushroom, .gem, .flag {
  position: absolute;
  font-size: 24px;
  animation: bounce 2s ease-in-out infinite;
}

.gem {
  animation: sparkle 1.5s ease-in-out infinite;
}

@keyframes bounce {
  0%, 100% { transform: translateY(0); }
  50% { transform: translateY(-5px); }
}

@keyframes sparkle {
  0%, 100% { 
    transform: scale(1);
    filter: brightness(1);
  }
  50% { 
    transform: scale(1.2);
    filter: brightness(1.5);
  }
}
</style>
