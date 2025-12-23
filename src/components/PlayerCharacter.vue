<script setup>
defineProps({
  isMoving: {
    type: Boolean,
    default: false
  },
  facingRight: {
    type: Boolean,
    default: true
  }
})
</script>

<template>
  <div :class="['character-wrapper', { 'facing-left': !facingRight }]">
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
              <!-- Sword attached to hand -->
              <div class="hand-grip"></div>
              <div class="sword">
                <div class="sword-blade"></div>
                <div class="sword-guard"></div>
                <div class="sword-handle"></div>
              </div>
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
  transform: rotate(-15deg);
}

/* Sword attached to left hand */
.sword {
  position: absolute;
  bottom: -2px;
  left: -18px;
  transform: rotate(-50deg);
  z-index: 15;
}

.sword-blade {
  width: 6px;
  height: 30px;
  background: linear-gradient(90deg, #9ca3af 0%, #e5e7eb 50%, #9ca3af 100%);
  border-radius: 2px 2px 1px 1px;
  box-shadow: 0 0 8px rgba(135, 206, 235, 0.8);
}

.sword-guard {
  width: 14px;
  height: 4px;
  background: #fbbf24;
  margin-left: -4px;
  border-radius: 1px;
}

.sword-handle {
  width: 5px;
  height: 8px;
  background: #78350f;
  margin-left: 0px;
  border-radius: 0 0 2px 2px;
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
  animation: swingSwordArm 0.4s ease-in-out infinite alternate;
}

.hero.walking .arm.right {
  animation: swingArm 0.4s ease-in-out infinite alternate-reverse;
}

.hero.walking .leg.left {
  animation: walkLeg 0.4s ease-in-out infinite alternate;
}

.hero.walking .leg.right {
  animation: walkLeg 0.4s ease-in-out infinite alternate-reverse;
}

.hero.walking .pixel-character {
  animation: bounce 0.2s ease-in-out infinite;
}

@keyframes swingSwordArm {
  from { transform: rotate(-40deg); }
  to { transform: rotate(-20deg); }
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
  animation: walkLeg 0.3s ease-in-out infinite alternate;
}

.cat.walking .cat-leg:nth-child(2) {
  animation: walkLeg 0.3s ease-in-out infinite alternate-reverse;
}

.cat.walking .cat-leg:nth-child(3) {
  animation: walkLeg 0.3s ease-in-out infinite alternate-reverse;
}

.cat.walking .cat-leg:nth-child(4) {
  animation: walkLeg 0.3s ease-in-out infinite alternate;
}

.cat.walking .cat-tail {
  animation: wagTail 0.4s ease-in-out infinite alternate;
}

.cat.walking .pixel-cat {
  animation: catBounce 0.15s ease-in-out infinite;
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
  animation: walkLeg 0.3s ease-in-out infinite alternate;
}

.persian-cat.walking .persian-leg:nth-child(2) {
  animation: walkLeg 0.3s ease-in-out infinite alternate-reverse;
}

.persian-cat.walking .persian-leg:nth-child(3) {
  animation: walkLeg 0.3s ease-in-out infinite alternate-reverse;
}

.persian-cat.walking .persian-leg:nth-child(4) {
  animation: walkLeg 0.3s ease-in-out infinite alternate;
}

.persian-cat.walking .persian-tail {
  animation: wagTail 0.4s ease-in-out infinite alternate;
}

.persian-cat.walking .pixel-persian {
  animation: catBounce 0.15s ease-in-out infinite;
}
</style>