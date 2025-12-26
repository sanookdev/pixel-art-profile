<script setup>
defineProps({
  isMoving: {
    type: Boolean,
    default: false
  },
  facingRight: {
    type: Boolean,
    default: true
  },
  isFlying: {
    type: Boolean,
    default: false
  }
})
</script>

<template>
  <div :class="['character-wrapper', { 'facing-left': !facingRight }]">
    <!-- WALKING MODE - Show characters -->
    <template v-if="!isFlying">
      <!-- CSS Pixel Art Hero - Basketball Player with Sword -->
      <div :class="['hero', { 'walking': isMoving }]">
        <div class="pixel-character">
          <!-- Head -->
          <div class="head">
            <div class="hair"></div>
            <div class="face">
              <div class="eyes">
                <span class="eye"></span>
                <span class="eye"></span>
              </div>
              <div class="mouth"></div>
            </div>
          </div>
          
          <!-- Body - Basketball Jersey -->
          <div class="body">
            <div class="jersey">
              <div class="jersey-stripes"></div>
              <div class="jersey-number">8</div>
            </div>
            <div class="arms">
              <div class="arm left">
                <!-- Basketball -->
                <div class="basketball"></div>
              </div>
              <div class="arm right"></div>
            </div>
          </div>
          
          <!-- Basketball Shorts -->
          <div class="shorts">
            <div class="short left"></div>
            <div class="short right"></div>
          </div>
          
          <!-- Legs -->
          <div class="legs">
            <div class="leg left"></div>
            <div class="leg right"></div>
          </div>
          
          <!-- Shoes -->
          <div class="shoes">
            <div class="shoe left"></div>
            <div class="shoe right"></div>
          </div>
        </div>
      </div>
      
      <!-- CSS Pixel Art Cat (Orange) -->
      <div :class="['cat', { 'walking': isMoving }]">
        <div class="pixel-cat">
          <div class="cat-ear left"></div>
          <div class="cat-ear right"></div>
          <div class="cat-head">
            <div class="cat-eyes">
              <span class="cat-eye"></span>
              <span class="cat-eye"></span>
            </div>
            <div class="cat-nose"></div>
            <div class="cat-whiskers left"></div>
            <div class="cat-whiskers right"></div>
          </div>
          <div class="cat-body"></div>
          <div class="cat-legs">
            <div class="cat-leg"></div>
            <div class="cat-leg"></div>
            <div class="cat-leg back"></div>
            <div class="cat-leg back"></div>
          </div>
          <div class="cat-tail"></div>
        </div>
      </div>
      
      <!-- CSS Pixel Art Gray Persian Cat -->
      <div :class="['persian-cat', { 'walking': isMoving }]">
        <div class="pixel-persian">
          <div class="persian-ear left"></div>
          <div class="persian-ear right"></div>
          <div class="persian-head">
            <div class="persian-fluff"></div>
            <div class="persian-face">
              <div class="persian-eyes">
                <span class="persian-eye"></span>
                <span class="persian-eye"></span>
              </div>
              <div class="persian-nose"></div>
            </div>
          </div>
          <div class="persian-body"></div>
          <div class="persian-legs">
            <div class="persian-leg"></div>
            <div class="persian-leg"></div>
            <div class="persian-leg back"></div>
            <div class="persian-leg back"></div>
          </div>
          <div class="persian-tail"></div>
        </div>
      </div>
    </template>
    
    <!-- DRIVING MODE - Show car with passengers -->
    <template v-else>
      <div :class="['car', { 'driving': isMoving }]">
        <div class="pixel-car">
          <!-- Car Roof (behind windows) -->
          <div class="car-roof"></div>
          
          <!-- Windows with passengers (on top of roof) -->
          <div class="car-windows">
            <div class="car-window front">
              <div class="passenger hero-head"></div>
            </div>
            <div class="car-window back">
              <div class="passenger cat-head-mini orange"></div>
              <div class="passenger cat-head-mini gray"></div>
            </div>
          </div>
          
          <!-- Car Body -->
          <div class="car-body">
            <!-- Hood -->
            <div class="car-hood"></div>
            <!-- Trunk -->
            <div class="car-trunk"></div>
          </div>
          
          <!-- Headlights -->
          <div class="headlight front"></div>
          <div class="headlight back"></div>
          
          <!-- Wheels -->
          <div class="wheel front">
            <div class="wheel-rim"></div>
          </div>
          <div class="wheel back">
            <div class="wheel-rim"></div>
          </div>
          
          <!-- Side Mirror -->
          <div class="side-mirror"></div>
        </div>
        
        <!-- Dust/smoke effect when driving -->
        <div v-if="isMoving" class="dust-trail">
          <span class="dust-puff"></span>
          <span class="dust-puff delay-1"></span>
          <span class="dust-puff delay-2"></span>
        </div>
      </div>
    </template>
  </div>
</template>

<style scoped>
.character-wrapper {
  position: relative;
  display: flex;
  align-items: flex-end;
  gap: 30px;
  transition: transform 0.2s ease;
}

.character-wrapper.facing-left {
  transform: scaleX(-1);
}

/* ============ HERO CHARACTER ============ */
.hero {
  position: relative;
}

.pixel-character {
  display: flex;
  flex-direction: column;
  align-items: center;
  filter: drop-shadow(2px 4px 6px rgba(0,0,0,0.3));
  transform: scale(2);
  transform-origin: bottom center;
  position: relative;
}

/* Head */
.head {
  position: relative;
  width: 28px;
  height: 26px;
  z-index: 10;
}

.hair {
  position: absolute;
  top: 0;
  left: 2px;
  width: 24px;
  height: 12px;
  background: #1a1a1a;
  border-radius: 10px 10px 0 0;
}

.face {
  position: absolute;
  top: 8px;
  left: 4px;
  width: 20px;
  height: 18px;
  background: #fcd8b5;
  border-radius: 4px 4px 8px 8px;
}

.eyes {
  display: flex;
  justify-content: space-around;
  padding-top: 4px;
  padding-left: 3px;
  padding-right: 3px;
}

.eye {
  width: 3px;
  height: 3px;
  background: #1a1a1a;
  border-radius: 50%;
}

.mouth {
  width: 6px;
  height: 2px;
  background: #d4725a;
  margin: 4px auto 0;
  border-radius: 1px;
}

/* Body - Basketball Jersey */
.body {
  position: relative;
  width: 26px;
  height: 22px;
  margin-top: -2px;
  z-index: 8;
}

.jersey {
  width: 26px;
  height: 22px;
  background: linear-gradient(180deg, #fff 0%, #f5f5f5 100%);
  border-radius: 4px 4px 2px 2px;
  position: relative;
  border: 2px solid #1e3a8a;
  z-index: 12;
  overflow: hidden;
}

.jersey-stripes {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  height: 10px;
  background: repeating-linear-gradient(
    90deg,
    #dc2626 0px,
    #dc2626 3px,
    #1e3a8a 3px,
    #1e3a8a 6px,
    #fff 6px,
    #fff 9px
  );
}

.jersey-number {
  position: absolute;
  top: 2px;
  left: 50%;
  transform: translateX(-50%);
  font-size: 8px;
  font-weight: bold;
  color: #1e3a8a;
  font-family: Arial, sans-serif;
  text-shadow: 1px 1px 0 #fff;
}

.arms {
  position: absolute;
  top: 2px;
  left: -8px;
  right: -8px;
  display: flex;
  justify-content: space-between;
}

.arm {
  width: 8px;
  height: 16px;
  background: linear-gradient(180deg, #1a1a1a 50%, #fcd8b5 50%);
  border-radius: 4px;
  transform-origin: top center;
  position: relative;
}

.arm.left {
  transform: rotate(30deg); /* Angled forward for dribbling */
  background: #fcd8b5; /* Skin color arm */
}

/* Basketball */
.basketball {
  position: absolute;
  bottom: -4px;
  left: -4px;
  width: 14px;
  height: 14px;
  background: radial-gradient(circle at 4px 4px, #fdba74 0%, #f97316 60%, #ea580c 100%);
  border-radius: 50%;
  border: 1px solid #9a3412;
  z-index: 20;
  box-shadow: 1px 1px 3px rgba(0,0,0,0.4);
  /* Counter-rotate the ball so translateY acts vertically */
  transform: rotate(-30deg);
}

.basketball::before {
  content: '';
  position: absolute;
  width: 100%;
  height: 100%;
  border-radius: 50%;
  border: 1px solid transparent;
  border-right-color: #7c2d12;
  transform: rotate(45deg);
  opacity: 0.8;
}

.basketball::after {
  content: '';
  position: absolute;
  width: 100%;
  height: 1px;
  top: 50%;
  left: 0;
  background: #7c2d12;
  transform: rotate(-30deg);
  opacity: 0.8;
}

.hand-grip {
  position: absolute;
  bottom: -2px;
  left: -2px;
  width: 6px;
  height: 6px;
  background: #fcd8b5;
  border-radius: 50%;
  z-index: 20;
}

.arm.right {
  background: #fcd8b5;
}

/* Basketball Shorts */
.shorts {
  display: flex;
  gap: 1px;
  margin-top: -2px;
  z-index: 6;
}

.short {
  width: 12px;
  height: 10px;
  background: linear-gradient(180deg, #FDB927 0%, #F5A623 100%);
  border-radius: 0 0 3px 3px;
  border-left: 1px solid #552583;
  border-right: 1px solid #552583;
}

/* Legs */
.legs {
  display: flex;
  gap: 2px;
  margin-top: -1px;
  z-index: 5;
}

.leg {
  width: 8px;
  height: 12px;
  background: #fcd8b5;
  border-radius: 0 0 2px 2px;
  transform-origin: top center;
}

/* Shoes */
.shoes {
  display: flex;
  gap: 2px;
  margin-top: -1px;
}

.shoe {
  width: 10px;
  height: 5px;
  background: #1a1a1a;
  border-radius: 2px 4px 2px 2px;
}

/* Walking Animation */
.hero.walking .arm.left {
  animation: dribbleArm 1.2s ease-in-out infinite;
}

.hero.walking .basketball {
  animation: dribbleBall 1.2s ease-in-out infinite;
}

@keyframes dribbleArm {
  0%, 100% { transform: rotate(30deg); }
  50% { transform: rotate(45deg); }
}

@keyframes dribbleBall {
  0% { transform: rotate(-30deg) translateY(0); }
  45% { transform: rotate(-30deg) translateY(20px) scale(0.9, 1.1); } /* Stretch when falling */
  50% { transform: rotate(-30deg) translateY(22px) scale(1.1, 0.9); } /* Squash on impact */
  55% { transform: rotate(-30deg) translateY(20px) scale(0.9, 1.1); } /* Stretch when rising */
  100% { transform: rotate(-30deg) translateY(0); }
}

.hero.walking .arm.right {
  animation: swingArm 1.0s ease-in-out infinite alternate-reverse;
}

.hero.walking .leg.left {
  animation: walkLeg 1.0s ease-in-out infinite alternate;
}

.hero.walking .leg.right {
  animation: walkLeg 1.0s ease-in-out infinite alternate-reverse;
}

.hero.walking .pixel-character {
  animation: bounce 0.5s ease-in-out infinite;
}

@keyframes swingArm {
  from { transform: rotate(-20deg); }
  to { transform: rotate(20deg); }
}

@keyframes walkLeg {
  from { transform: rotate(-15deg); }
  to { transform: rotate(15deg); }
}

@keyframes bounce {
  0%, 100% { transform: scale(2) translateY(0); }
  50% { transform: scale(2) translateY(-3px); }
}

/* ============ CAT ============ */
.cat {
  position: relative;
}

.pixel-cat {
  position: relative;
  filter: drop-shadow(2px 3px 4px rgba(0,0,0,0.3));
}

.cat-ear {
  position: absolute;
  width: 0;
  height: 0;
  border-left: 6px solid transparent;
  border-right: 6px solid transparent;
  border-bottom: 10px solid #FF8C00;
  top: -8px;
}

.cat-ear.left {
  left: 2px;
  transform: rotate(-15deg);
}

.cat-ear.right {
  right: 2px;
  transform: rotate(15deg);
}

.cat-head {
  position: relative;
  width: 32px;
  height: 22px;
  background: linear-gradient(90deg, #fff 0%, #fff 40%, #FF8C00 60%, #FF8C00 100%);
  border-radius: 10px 10px 8px 8px;
}

.cat-eyes {
  display: flex;
  justify-content: space-around;
  padding-top: 6px;
  padding-left: 4px;
  padding-right: 4px;
}

.cat-eye {
  width: 6px;
  height: 8px;
  background: #1a1a1a;
  border-radius: 50%;
  position: relative;
}

.cat-eye::after {
  content: '';
  position: absolute;
  top: 1px;
  left: 2px;
  width: 2px;
  height: 2px;
  background: white;
  border-radius: 50%;
}

.cat-nose {
  width: 4px;
  height: 3px;
  background: #ff6699;
  margin: 2px auto 0;
  border-radius: 50%;
}

.cat-whiskers {
  position: absolute;
  top: 14px;
  width: 12px;
  height: 1px;
  background: #666;
}

.cat-whiskers.left {
  left: -8px;
  transform: rotate(-5deg);
}

.cat-whiskers.right {
  right: -8px;
  transform: rotate(5deg);
}

.cat-whiskers::before,
.cat-whiskers::after {
  content: '';
  position: absolute;
  width: 10px;
  height: 1px;
  background: #666;
  left: 0;
}

.cat-whiskers.right::before,
.cat-whiskers.right::after {
  left: auto;
  right: 0;
}

.cat-whiskers::before {
  top: -3px;
  transform: rotate(10deg);
}

.cat-whiskers::after {
  top: 3px;
  transform: rotate(-10deg);
}

.cat-body {
  width: 28px;
  height: 18px;
  background: linear-gradient(90deg, #fff 0%, #fff 50%, #FF8C00 50%, #FF8C00 100%);
  border-radius: 6px;
  margin: -4px auto 0;
  position: relative;
}

.cat-legs {
  display: flex;
  justify-content: space-between;
  width: 26px;
  margin: -2px auto 0;
}

.cat-leg {
  width: 6px;
  height: 10px;
  background: #fff;
  border-radius: 0 0 3px 3px;
  transform-origin: top center;
}

.cat-tail {
  position: absolute;
  right: -12px;
  top: 24px;
  width: 4px;
  height: 18px;
  background: #FF8C00;
  border-radius: 2px;
  transform: rotate(45deg);
  transform-origin: top center;
}

/* Cat Walking Animation */
.cat.walking .cat-leg:nth-child(1) {
  animation: walkLeg 0.6s ease-in-out infinite alternate;
}

.cat.walking .cat-leg:nth-child(2) {
  animation: walkLeg 0.6s ease-in-out infinite alternate-reverse;
}

.cat.walking .cat-leg:nth-child(3) {
  animation: walkLeg 0.6s ease-in-out infinite alternate-reverse;
}

.cat.walking .cat-leg:nth-child(4) {
  animation: walkLeg 0.6s ease-in-out infinite alternate;
}

.cat.walking .cat-tail {
  animation: wagTail 0.8s ease-in-out infinite alternate;
}

.cat.walking .pixel-cat {
  animation: catBounce 0.3s ease-in-out infinite;
}

@keyframes wagTail {
  from { transform: rotate(30deg); }
  to { transform: rotate(60deg); }
}

@keyframes catBounce {
  0%, 100% { transform: translateY(0); }
  50% { transform: translateY(-2px); }
}

/* ============ GRAY PERSIAN CAT ============ */
.persian-cat {
  position: relative;
}

.pixel-persian {
  position: relative;
  filter: drop-shadow(2px 3px 4px rgba(0,0,0,0.3));
  transform: scale(1);
  transform-origin: bottom center;
}

.persian-ear {
  position: absolute;
  width: 0;
  height: 0;
  border-left: 5px solid transparent;
  border-right: 5px solid transparent;
  border-bottom: 8px solid #5c5c5c;
  top: -5px;
  z-index: 1;
}

.persian-ear.left {
  left: 3px;
  transform: rotate(-10deg);
}

.persian-ear.right {
  right: 3px;
  transform: rotate(10deg);
}

.persian-head {
  position: relative;
  width: 36px;
  height: 28px;
  background: #6b6b6b;
  border-radius: 50%;
  z-index: 2;
}

.persian-fluff {
  position: absolute;
  top: -3px;
  left: -3px;
  right: -3px;
  bottom: 5px;
  background: radial-gradient(ellipse, #7a7a7a 0%, #5c5c5c 100%);
  border-radius: 50%;
  z-index: 0;
}

.persian-face {
  position: absolute;
  top: 8px;
  left: 8px;
  right: 8px;
  bottom: 4px;
  z-index: 3;
}

.persian-eyes {
  display: flex;
  justify-content: space-around;
  padding-top: 2px;
}

.persian-eye {
  width: 8px;
  height: 8px;
  background: radial-gradient(circle, #d4a017 30%, #8b6914 100%);
  border-radius: 50%;
  position: relative;
  border: 1px solid #333;
}

.persian-eye::after {
  content: '';
  position: absolute;
  top: 2px;
  left: 3px;
  width: 3px;
  height: 4px;
  background: #1a1a1a;
  border-radius: 50%;
}

.persian-nose {
  width: 5px;
  height: 4px;
  background: #4a3c31;
  margin: 3px auto 0;
  border-radius: 50% 50% 40% 40%;
}

.persian-body {
  width: 34px;
  height: 20px;
  background: linear-gradient(180deg, #6b6b6b 0%, #5c5c5c 100%);
  border-radius: 8px;
  margin: -6px auto 0;
  position: relative;
}

.persian-legs {
  display: flex;
  justify-content: space-between;
  width: 30px;
  margin: -3px auto 0;
}

.persian-leg {
  width: 7px;
  height: 8px;
  background: #5c5c5c;
  border-radius: 0 0 4px 4px;
  transform-origin: top center;
}

.persian-tail {
  position: absolute;
  right: -10px;
  top: 28px;
  width: 5px;
  height: 15px;
  background: #6b6b6b;
  border-radius: 3px;
  transform: rotate(40deg);
  transform-origin: top center;
}

/* Persian Cat Walking Animation */
.persian-cat.walking .persian-leg:nth-child(1) {
  animation: walkLeg 0.6s ease-in-out infinite alternate;
}

.persian-cat.walking .persian-leg:nth-child(2) {
  animation: walkLeg 0.6s ease-in-out infinite alternate-reverse;
}

.persian-cat.walking .persian-leg:nth-child(3) {
  animation: walkLeg 0.6s ease-in-out infinite alternate-reverse;
}

.persian-cat.walking .persian-leg:nth-child(4) {
  animation: walkLeg 0.6s ease-in-out infinite alternate;
}

.persian-cat.walking .persian-tail {
  animation: wagTail 0.8s ease-in-out infinite alternate;
}

.persian-cat.walking .pixel-persian {
  animation: catBounce 0.3s ease-in-out infinite;
}

/* ============ CAR MODE ============ */
.car {
  position: relative;
  filter: drop-shadow(3px 5px 8px rgba(0,0,0,0.4));
}

.pixel-car {
  position: relative;
  transform: scale(1.8);
  transform-origin: bottom center;
}

/* Car Body - Sleek Sedan */
.car-body {
  width: 100px;
  height: 30px;
  background: linear-gradient(180deg, #e53935 0%, #c62828 50%, #b71c1c 100%);
  border-radius: 8px 15px 5px 5px;
  position: relative;
  border: 2px solid #7f1d1d;
  z-index: 10;
}

/* Car Roof/Cabin - Behind windows */
.car-roof {
  position: absolute;
  top: -28px;
  left: 20px;
  width: 60px;
  height: 32px;
  background: linear-gradient(180deg, #e53935 0%, #c62828 100%);
  border-radius: 15px 15px 0 0;
  border: 2px solid #7f1d1d;
  border-bottom: none;
  z-index: 5;
}

/* Windows - On top of roof */
.car-windows {
  position: absolute;
  top: -26px;
  left: 22px;
  display: flex;
  gap: 4px;
  z-index: 15;
}

.car-window {
  height: 22px;
  background: linear-gradient(180deg, #e3f2fd 0%, #90caf9 100%);
  border-radius: 6px 6px 0 0;
  border: 2px solid #1976d2;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 3px;
  padding: 2px 4px;
}

.car-window.front {
  width: 24px;
}

.car-window.back {
  width: 28px;
}

/* Passenger heads - Enlarged for visibility */
.passenger {
  width: 12px;
  height: 12px;
  border-radius: 50%;
  border: 1px solid rgba(0,0,0,0.2);
}

.passenger.hero-head {
  background: #fcd8b5;
  position: relative;
}

.passenger.hero-head::before {
  content: '';
  position: absolute;
  top: -3px;
  left: 0px;
  width: 12px;
  height: 6px;
  background: #1a1a1a;
  border-radius: 6px 6px 0 0;
}

/* Eyes for hero */
.passenger.hero-head::after {
  content: '';
  position: absolute;
  top: 4px;
  left: 2px;
  width: 3px;
  height: 2px;
  background: #1a1a1a;
  border-radius: 50%;
  box-shadow: 5px 0 0 #1a1a1a;
}

.passenger.cat-head-mini {
  width: 10px;
  height: 10px;
  position: relative;
}

.passenger.cat-head-mini.orange {
  background: linear-gradient(90deg, #fff 50%, #FF8C00 50%);
}

/* Cat ears */
.passenger.cat-head-mini.orange::before,
.passenger.cat-head-mini.gray::before {
  content: '';
  position: absolute;
  top: -3px;
  left: 0;
  width: 0;
  height: 0;
  border-left: 3px solid transparent;
  border-right: 3px solid transparent;
  border-bottom: 4px solid #FF8C00;
}

.passenger.cat-head-mini.gray::before {
  border-bottom-color: #6b6b6b;
}

.passenger.cat-head-mini.gray {
  background: #6b6b6b;
}

/* Hood */
.car-hood {
  position: absolute;
  left: -15px;
  top: 5px;
  width: 20px;
  height: 20px;
  background: linear-gradient(180deg, #e53935 0%, #c62828 100%);
  border-radius: 10px 0 5px 5px;
  border: 2px solid #7f1d1d;
  z-index: 9;
}

/* Trunk */
.car-trunk {
  position: absolute;
  right: -10px;
  top: 8px;
  width: 15px;
  height: 17px;
  background: linear-gradient(180deg, #c62828 0%, #b71c1c 100%);
  border-radius: 0 8px 5px 0;
  border: 2px solid #7f1d1d;
  border-left: none;
  z-index: 8;
}

/* Headlights */
.headlight {
  position: absolute;
  width: 6px;
  height: 6px;
  border-radius: 50%;
  z-index: 15;
}

.headlight.front {
  left: -18px;
  top: 18px;
  background: radial-gradient(circle, #fff9c4 0%, #ffeb3b 100%);
  box-shadow: 0 0 8px #ffeb3b;
}

.headlight.back {
  right: -8px;
  top: 18px;
  background: radial-gradient(circle, #ffcdd2 0%, #ef5350 100%);
  box-shadow: 0 0 5px #ef5350;
}

/* Wheels */
.wheel {
  position: absolute;
  bottom: -10px;
  width: 18px;
  height: 18px;
  background: radial-gradient(circle, #424242 0%, #212121 100%);
  border-radius: 50%;
  border: 2px solid #000;
  z-index: 20;
  display: flex;
  align-items: center;
  justify-content: center;
}

.wheel.front {
  left: 8px;
}

.wheel.back {
  right: 8px;
}

.wheel-rim {
  width: 8px;
  height: 8px;
  background: radial-gradient(circle, #bdbdbd 0%, #757575 100%);
  border-radius: 50%;
  border: 1px solid #424242;
}

/* Side Mirror */
.side-mirror {
  position: absolute;
  left: 20px;
  top: -8px;
  width: 5px;
  height: 4px;
  background: #7f1d1d;
  border-radius: 2px;
  z-index: 15;
}

/* Driving Animation */
.car.driving {
  animation: carBounce 0.3s ease-in-out infinite;
}

.car.driving .wheel {
  animation: wheelSpin 0.2s linear infinite;
}

@keyframes carBounce {
  0%, 100% { transform: translateY(0); }
  50% { transform: translateY(-2px); }
}

@keyframes wheelSpin {
  from { transform: rotate(0deg); }
  to { transform: rotate(360deg); }
}

/* Dust Trail */
.dust-trail {
  position: absolute;
  right: -40px;
  bottom: 0;
  display: flex;
  gap: 5px;
  align-items: flex-end;
}

.dust-puff {
  width: 12px;
  height: 12px;
  background: rgba(139, 119, 101, 0.6);
  border-radius: 50%;
  animation: dustFade 0.4s ease-out infinite;
}

.dust-puff.delay-1 {
  animation-delay: 0.1s;
  width: 10px;
  height: 10px;
}

.dust-puff.delay-2 {
  animation-delay: 0.2s;
  width: 8px;
  height: 8px;
}

@keyframes dustFade {
  0% { 
    opacity: 0.6; 
    transform: translateX(0) translateY(0) scale(1);
  }
  100% { 
    opacity: 0; 
    transform: translateX(20px) translateY(-10px) scale(0.5);
  }
}
</style>