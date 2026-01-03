<script setup>
import { ref, onMounted } from 'vue';

const props = defineProps({
  type: {
    type: String,
    default: 'coins' // coins, hearts, stars, mushrooms
  },
  count: {
    type: Number,
    default: 5
  }
});

const elements = ref([]);

const getEmoji = (type) => {
  const emojiMap = {
    coins: '🪙',
    hearts: '❤️',
    stars: '⭐',
    mushrooms: '🍄',
    gems: '💎',
    flowers: '🌸',
    butterflies: '🦋',
    coffee: '☕',
    phone: '📱',
    laptop: '💻',
    mouse: '🖱️',
    keyboard: '⌨️',
    codetag:'</>',
    PHP:'🐘',
    atom:'⚛️',
    wing:'✨'
};
  return emojiMap[type] || '⭐';
};

onMounted(() => {
  for (let i = 0; i < props.count; i++) {
    elements.value.push({
      id: i,
      x: 10 + Math.random() * 80, // 10% - 90% to avoid edges
      y: 15 + Math.random() * 50, // Top half only
      size: 20 + Math.random() * 20,
      duration: 2 + Math.random() * 3,
      delay: Math.random() * 2,
      rotation: Math.random() * 360
    });
  }
});
</script>

<template>
  <div class="floating-elements">
    <div 
      v-for="el in elements" 
      :key="el.id"
      class="floating-item"
      :style="{
        left: el.x + '%',
        top: el.y + '%',
        fontSize: el.size + 'px',
        animationDuration: el.duration + 's',
        animationDelay: el.delay + 's',
        '--rotation': el.rotation + 'deg'
      }"
    >
      <span class="emoji-wrapper">{{ getEmoji(type) }}</span>
      <span class="glow"></span>
    </div>
  </div>
</template>

<style scoped>
.floating-elements {
  position: absolute;
  inset: 0;
  pointer-events: none;
  z-index: 5;
}

.floating-item {
  position: absolute;
  animation: float 3s ease-in-out infinite;
  filter: drop-shadow(0 0 8px rgba(255, 215, 0, 0.6));
  will-change: transform;
  transform: translateZ(0);
}

.emoji-wrapper {
  display: block;
  animation: spin 4s linear infinite;
  transform: rotate(var(--rotation));
}

.glow {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 150%;
  height: 150%;
  background: radial-gradient(circle, rgba(255, 215, 0, 0.4) 0%, transparent 70%);
  animation: pulse 2s ease-in-out infinite;
  border-radius: 50%;
}

@keyframes float {
  0%, 100% {
    transform: translateY(0);
  }
  50% {
    transform: translateY(-20px);
  }
}

@keyframes spin {
  0% { transform: rotate(0deg); }
  100% { transform: rotate(360deg); }
}

@keyframes pulse {
  0%, 100% {
    opacity: 0.5;
    transform: translate(-50%, -50%) scale(1);
  }
  50% {
    opacity: 1;
    transform: translate(-50%, -50%) scale(1.2);
  }
}
</style>
