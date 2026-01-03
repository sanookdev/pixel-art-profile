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
    
    <!-- DRIVING MODE - Luxury Gray Sedan -->
    <template v-else>
      <div :class="['car', { 'driving': isMoving }]">
        <div class="pixel-car">
          <!-- Car Roof/Cabin -->
          <div class="car-roof"></div>
          
          <!-- Large Windows with detailed passengers -->
          <div class="car-cabin">
            <!-- Front Window (Driver) -->
            <div class="car-window driver-window">
              <div class="driver-seat">
                <!-- Human Head -->
                <div class="driver-head">
                  <div class="driver-hair"></div>
                  <div class="driver-face">
                    <div class="driver-eyes"></div>
                  </div>
                </div>
              </div>
            </div>
            
            <!-- Back Window (Cats) -->
            <div class="car-window passenger-window">
              <div class="back-seats">
                <!-- Orange Cat Head -->
                <div class="cat-passenger orange">
                  <div class="cat-ear-left"></div>
                  <div class="cat-ear-right"></div>
                  <div class="cat-face"></div>
                </div>
                <!-- Gray Cat Head -->
                <div class="cat-passenger gray">
                  <div class="cat-ear-left"></div>
                  <div class="cat-ear-right"></div>
                  <div class="cat-face"></div>
                </div>
              </div>
            </div>
          </div>
          
          <!-- Car Body -->
          <div class="car-body">
            <div class="car-hood"></div>
            <div class="car-trunk"></div>
            <div class="door-line"></div>
          </div>
          
          <!-- Headlights -->
          <div class="headlight front"></div>
          <div class="headlight back"></div>
          
          <!-- Premium Wheels -->
          <div class="wheel front">
            <div class="wheel-rim">
              <div class="rim-spoke"></div>
            </div>
          </div>
          <div class="wheel back">
            <div class="wheel-rim">
              <div class="rim-spoke"></div>
            </div>
          </div>
          
          <!-- Side Mirror -->
          <div class="side-mirror"></div>
          
          <!-- Door Handle -->
          <div class="door-handle"></div>
        </div>
        
        <!-- Dust effect when driving -->
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
  transition: transform 0.3s ease, opacity 0.3s ease;
}

.character-wrapper.facing-left {
  transform: scaleX(-1);
}

/* Smooth mode transition - only on initial mount */
.hero, .cat, .persian-cat, .car {
  /* No infinite animation - just static now */
}

/* Only animate on first appearance, not on re-renders */

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

/* ============ LUXURY GRAY SEDAN ============ */
.car {
  position: relative;
  filter: drop-shadow(4px 6px 10px rgba(0,0,0,0.5));
}

.pixel-car {
  position: relative;
  transform: scale(2);
  transform-origin: bottom center;
}

/* Car Body - Luxury Gray */
.car-body {
  width: 110px;
  height: 28px;
  background: linear-gradient(180deg, #9e9e9e 0%, #757575 40%, #616161 100%);
  border-radius: 5px 12px 4px 4px;
  position: relative;
  border: 2px solid #424242;
  z-index: 10;
}

/* Car Roof - Gray */
.car-roof {
  position: absolute;
  top: -32px;
  left: 18px;
  width: 75px;
  height: 35px;
  background: linear-gradient(180deg, #9e9e9e 0%, #757575 100%);
  border-radius: 15px 15px 0 0;
  border: 2px solid #424242;
  border-bottom: none;
  z-index: 5;
}

/* Cabin - Window Container */
.car-cabin {
  position: absolute;
  top: -30px;
  left: 20px;
  display: flex;
  gap: 3px;
  z-index: 20;
}

/* Windows */
.car-window {
  height: 28px;
  background: linear-gradient(180deg, #e1f5fe 0%, #81d4fa 50%, #4fc3f7 100%);
  border-radius: 8px 8px 0 0;
  border: 2px solid #0288d1;
  display: flex;
  align-items: flex-end;
  justify-content: center;
  padding-bottom: 2px;
  overflow: visible;
}

.driver-window {
  width: 30px;
}

.passenger-window {
  width: 38px;
}

/* Driver Seat */
.driver-seat {
  display: flex;
  justify-content: center;
}

/* Driver Head */
.driver-head {
  position: relative;
  width: 16px;
  height: 16px;
}

.driver-hair {
  position: absolute;
  top: 0;
  left: 1px;
  width: 14px;
  height: 8px;
  background: #1a1a1a;
  border-radius: 7px 7px 0 0;
  z-index: 2;
}

.driver-face {
  position: absolute;
  top: 5px;
  left: 2px;
  width: 12px;
  height: 11px;
  background: #fcd8b5;
  border-radius: 3px 3px 6px 6px;
  z-index: 1;
}

.driver-eyes {
  position: absolute;
  top: 3px;
  left: 2px;
  width: 3px;
  height: 2px;
  background: #1a1a1a;
  border-radius: 50%;
  box-shadow: 5px 0 0 #1a1a1a;
}

/* Back Seats - Cats */
.back-seats {
  display: flex;
  gap: 4px;
  padding: 0 2px;
}

/* Cat Passengers */
.cat-passenger {
  position: relative;
  width: 14px;
  height: 14px;
}

.cat-passenger .cat-face {
  position: absolute;
  bottom: 0;
  left: 2px;
  width: 10px;
  height: 10px;
  border-radius: 50%;
  z-index: 1;
}

.cat-passenger.orange .cat-face {
  background: linear-gradient(90deg, #fff 50%, #FF8C00 50%);
}

.cat-passenger.gray .cat-face {
  background: #6b6b6b;
}

/* Cat Ears */
.cat-passenger .cat-ear-left,
.cat-passenger .cat-ear-right {
  position: absolute;
  top: 0;
  width: 0;
  height: 0;
  border-left: 4px solid transparent;
  border-right: 4px solid transparent;
  z-index: 2;
}

.cat-passenger .cat-ear-left {
  left: 0;
}

.cat-passenger .cat-ear-right {
  right: 0;
}

.cat-passenger.orange .cat-ear-left,
.cat-passenger.orange .cat-ear-right {
  border-bottom: 6px solid #FF8C00;
}

.cat-passenger.gray .cat-ear-left,
.cat-passenger.gray .cat-ear-right {
  border-bottom: 6px solid #6b6b6b;
}

/* Car Hood */
.car-hood {
  position: absolute;
  left: -18px;
  top: 4px;
  width: 24px;
  height: 20px;
  background: linear-gradient(180deg, #9e9e9e 0%, #757575 100%);
  border-radius: 12px 0 5px 5px;
  border: 2px solid #424242;
  z-index: 9;
}

/* Car Trunk */
.car-trunk {
  position: absolute;
  right: -12px;
  top: 6px;
  width: 18px;
  height: 18px;
  background: linear-gradient(180deg, #757575 0%, #616161 100%);
  border-radius: 0 10px 5px 0;
  border: 2px solid #424242;
  border-left: none;
  z-index: 8;
}

/* Door Line */
.door-line {
  position: absolute;
  left: 45px;
  top: 2px;
  width: 2px;
  height: 22px;
  background: #424242;
  z-index: 11;
}

/* Door Handle */
.door-handle {
  position: absolute;
  left: 50px;
  top: 10px;
  width: 8px;
  height: 3px;
  background: #bdbdbd;
  border-radius: 2px;
  border: 1px solid #424242;
  z-index: 12;
}

/* Headlights */
.headlight {
  position: absolute;
  border-radius: 50%;
  z-index: 15;
}

.headlight.front {
  left: -22px;
  top: 16px;
  width: 8px;
  height: 6px;
  background: radial-gradient(ellipse, #fffde7 0%, #ffeb3b 100%);
  box-shadow: 0 0 10px #ffeb3b, 0 0 20px rgba(255,235,59,0.5);
  border-radius: 3px;
}

.headlight.back {
  right: -10px;
  top: 16px;
  width: 6px;
  height: 5px;
  background: radial-gradient(circle, #ffcdd2 0%, #e53935 100%);
  box-shadow: 0 0 6px #e53935;
}

/* Premium Wheels */
.wheel {
  position: absolute;
  bottom: -10px;
  width: 20px;
  height: 20px;
  background: radial-gradient(circle, #424242 0%, #1a1a1a 100%);
  border-radius: 50%;
  border: 2px solid #000;
  z-index: 25;
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
  width: 12px;
  height: 12px;
  background: radial-gradient(circle, #e0e0e0 0%, #9e9e9e 100%);
  border-radius: 50%;
  border: 1px solid #616161;
  display: flex;
  align-items: center;
  justify-content: center;
}

.rim-spoke {
  width: 6px;
  height: 6px;
  background: #424242;
  border-radius: 50%;
}

/* Side Mirror */
.side-mirror {
  position: absolute;
  left: 15px;
  top: -12px;
  width: 6px;
  height: 5px;
  background: linear-gradient(180deg, #616161 0%, #424242 100%);
  border-radius: 2px;
  border: 1px solid #212121;
  z-index: 25;
}

/* Driving Animation */
.car.driving {
  animation: carBounce 0.25s ease-in-out infinite;
}

.car.driving .wheel {
  animation: wheelSpin 0.15s linear infinite;
}

.car.driving .wheel-rim {
  animation: wheelSpin 0.15s linear infinite reverse;
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
  right: -50px;
  bottom: 5px;
  display: flex;
  gap: 6px;
  align-items: flex-end;
}

.dust-puff {
  width: 14px;
  height: 14px;
  background: rgba(158, 158, 158, 0.5);
  border-radius: 50%;
  animation: dustFade 0.5s ease-out infinite;
}

.dust-puff.delay-1 {
  animation-delay: 0.15s;
  width: 11px;
  height: 11px;
}

.dust-puff.delay-2 {
  animation-delay: 0.3s;
  width: 8px;
  height: 8px;
}

@keyframes dustFade {
  0% { 
    opacity: 0.5; 
    transform: translateX(0) translateY(0) scale(1);
  }
  100% { 
    opacity: 0; 
    transform: translateX(25px) translateY(-8px) scale(0.4);
  }
}
</style>