<script setup>
import { onMounted, ref } from 'vue';
import gsap from 'gsap';
import { ScrollTrigger } from 'gsap/ScrollTrigger';
import PlayerCharacter from './PlayerCharacter.vue';
import DialogueBox from './UI/DialogueBox.vue';
import ParallaxBackground from './ParallaxBackground.vue';
import FloatingElements from './FloatingElements.vue';
import PixelGround from './PixelGround.vue';
import { portfolioData } from '../data/portfolio';

gsap.registerPlugin(ScrollTrigger);

const worldTrack = ref(null);
const container = ref(null);
const isMoving = ref(false);
const currentLevel = ref(0);
const facingRight = ref(false);
let scrollTimeout = null;
let lastScrollY = 0;

// Visited levels tracking
const visitedLevels = ref(new Set([0])); // Level 0 visited by default

// Lifestyle gallery images
const lifestyleImages = [
  '023e6049-bf98-4b56-9d95-34e815620dc5.jpeg',
  '089b429e-817e-4431-8c4c-79be59fe71af.jpeg',
  '82b0106e-7111-44cb-bf74-718c076aace6.jpeg',
  'a2a36df6-238c-435a-aa26-5d92d553f8cc.jpeg',
  'cbb5f179-e2d1-4a17-811d-44a39adwqe846001.jpeg'
];

// Cat gallery images
const catImages = [
  '2db37770-969e-470a-bf7d-42c53a467a0b.jpeg',
  '983f2743-5bb8-41c2-90bb-0f64dcd0b70c.jpeg',
  'a0c6d223-974f-470f-bdc4-d3f6f87a4ff4.jpeg',
  'bf457aa7-8eab-4d47-b1e5-8969e35f6879.jpeg',
  'e2e58731-4da1-4a02-9007-a82af8ac5848.jpeg',
  'ee34716c-a4ea-435b-a17f-4d12f9238c97.jpeg'
];

// Relation gallery images
const relationImages = [
  '3ef58e0a-fa60-4652-96ec-43331ab342e5.jpeg',
  '68fc48e1-1ce5-46ec-aad7-9f87551abac8.jpeg',
  '6ae78126-2cf6-45e4-bb7a-f2db97a885de.jpeg',
  '99818099-a1c2-48b3-82be-1838aa4bdb38.jpeg',
  '9ab55c73-ccc5-4a86-91fd-83598f9f998d.jpeg',
  '9f877ff8-b5e7-4f86-bda4-f77b560e6664.jpeg',
  'd1d0315b-bfaa-45e3-aaf4-2885634c3ce8.jpeg',
  'fd4808bd-a178-4593-9c4e-dfcd191d18c2.jpeg'
];

const handleScroll = () => {
  const currentScrollY = window.scrollY;
  
  // Determine scroll direction
  if (currentScrollY > lastScrollY) {
    facingRight.value = false;  // Scrolling down = moving left
  } else if (currentScrollY < lastScrollY) {
    facingRight.value = true; // Scrolling up = moving right
  }
  lastScrollY = currentScrollY;
  
  isMoving.value = true;
  
  if (scrollTimeout) clearTimeout(scrollTimeout);
  
  scrollTimeout = setTimeout(() => {
    isMoving.value = false;
  }, 100);
};

const updateProgress = (progress) => {
  // 7 levels, so divide progress into 7 segments
  const level = Math.min(Math.floor(progress * 7), 6);
  currentLevel.value = level;
  
  // Animation Trigger logic
  if (!visitedLevels.value.has(level)) {
    visitedLevels.value.add(level);
    
    // Animate content for this level
    const content = document.querySelector(`.level:nth-child(${level + 1}) .content-layer`);
    if (content) {
      gsap.fromTo(content, 
        { y: -100, opacity: 0 },
        { 
          y: 0, 
          opacity: 1, 
          duration: 0.8, 
          ease: "bounce.out",
          overwrite: true
        }
      );
    }
  }

  // Scroll text
  const scrollText = document.querySelector('.helper-text');
  if (scrollText) {
    if (window.scrollY > 50) {
      scrollText.style.opacity = '0';
    } else {
      scrollText.style.opacity = '1';
    }
  }
};

// Mobile navigation
const moveLevel = (direction) => {
  const targetLevel = Math.max(0, Math.min(6, currentLevel.value + direction));
  const targetY = targetLevel * window.innerWidth;
  
  window.scrollTo({
    top: targetY,
    behavior: 'smooth'
  });
};

// Continuous movement logic
const movementInterval = ref(null);

const startMoving = (direction) => {
  // Move immediately once
  moveLevel(direction);
  
  // Clear any existing interval
  if (movementInterval.value) clearInterval(movementInterval.value);
  
  // Start continuous movement
  movementInterval.value = setInterval(() => {
    moveLevel(direction);
  }, 300); // 300ms delay between steps
};

const stopMoving = () => {
  if (movementInterval.value) {
    clearInterval(movementInterval.value);
    movementInterval.value = null;
  }
};

onMounted(() => {
  window.addEventListener('scroll', handleScroll);

  setTimeout(() => {
    const getScrollDistance = () => {
      if (!worldTrack.value) return 0;
      return worldTrack.value.scrollWidth - window.innerWidth;
    };

    gsap.to(worldTrack.value, {
      x: () => -getScrollDistance(),
      ease: "none",
      scrollTrigger: {
        trigger: container.value,
        start: "top top",
        end: () => `+=${getScrollDistance()}`,
        pin: true,
        scrub: 1,
        invalidateOnRefresh: true,
        anticipatePin: 1,
        onUpdate: (self) => {
          updateProgress(self.progress);
        }
      }
    });
    
    ScrollTrigger.refresh();
  }, 500);
});
</script>

<template>
  <div class="game-container" ref="container">
    
    <div class="world-track" ref="worldTrack">
      
      <!-- LEVEL 1: START -->
      <section class="level level-start">
        <ParallaxBackground theme="meadow" />
        <FloatingElements type="butterflies" :count="6" />
        
        <div class="content-layer">
          <div class="profile-logo">
            <img src="/profile.png" alt="Profile" class="pixel-avatar" />
          </div>
          <DialogueBox title="🎮 Welcome!" type="is-dark">
            <p>Hi! I'm <span class="nes-text is-success glow-text">{{ portfolioData.personal.name }}</span></p>
            <p><i class="nes-icon coin is-small"></i> {{ portfolioData.personal.role }}</p>
            <p class="helper-text blink">> Scroll to Start Adventure</p>
          </DialogueBox>
        </div>
        
        <div class="decorative-elements">
          <i class="nes-icon cloud is-large floating" style="position:absolute; top: 10%; left: 20%"></i>
          <i class="nes-icon cloud is-large floating delay-1" style="position:absolute; top: 20%; left: 80%"></i>
          <i class="nes-icon cloud is-medium floating delay-2" style="position:absolute; top: 8%; left: 50%"></i>
        </div>
      </section>

      <!-- LEVEL 2: BIO -->
      <section class="level level-bio">
        <ParallaxBackground theme="forest" />
        <FloatingElements type="flowers" :count="8" />
        
        <div class="content-layer content-wrapper">
          <h2 class="section-title nes-text is-success glow-title">
            <i class="nes-icon star is-small"></i> About Me
          </h2>
          <DialogueBox title="👋 Hello, I'm Warat Supaporn!" type="is-rounded">
            <p>{{ portfolioData.personal.bio }}</p>
            <p style="margin-top: 0.8rem; font-style: italic;">My favourite hobbies is {{ portfolioData.personal.hobbies }}</p>
          </DialogueBox>
        </div>
      </section>

      <!-- LEVEL 3: TECH STACK -->
      <section class="level level-skills">
        <ParallaxBackground theme="beach" />
        <FloatingElements type="stars" :count="8" />
        
        <div class="content-layer">
          <h2 class="section-title nes-text is-warning glow-title">
            <i class="nes-icon trophy is-small"></i> Tech Stack
          </h2>
          <div class="skills-block nes-container is-dark with-title glow-box">
             <p class="title">⚔️ My Skills</p>
             
             <!-- Languages -->
             <div class="skill-category">
               <p class="category-label nes-text is-warning">💻 Languages</p>
               <div class="skill-tags">
                 <span v-for="skill in portfolioData.skills.languages" :key="skill" class="skill-tag lang">
                   {{ skill }}
                 </span>
               </div>
             </div>
             
             <!-- Frameworks -->
             <div class="skill-category">
               <p class="category-label nes-text is-success">🚀 Frameworks</p>
               <div class="skill-tags">
                 <span v-for="skill in portfolioData.skills.frameworks" :key="skill" class="skill-tag framework">
                   {{ skill }}
                 </span>
               </div>
             </div>
             
             <!-- Tools -->
             <div class="skill-category">
               <p class="category-label nes-text is-primary">🛠️ Tools</p>
               <div class="skill-tags">
                 <span v-for="skill in portfolioData.skills.tools" :key="skill" class="skill-tag tool">
                   {{ skill }}
                 </span>
               </div>
             </div>
             
             <!-- OS -->
             <div class="skill-category">
               <p class="category-label nes-text is-error">🖥️ OS</p>
               <div class="skill-tags">
                 <span v-for="skill in portfolioData.skills.OS" :key="skill" class="skill-tag os">
                   {{ skill }}
                 </span>
               </div>
             </div>
             
             <!-- Design -->
             <div class="skill-category">
               <p class="category-label" style="color: #ff69b4;">🎨 Design</p>
               <div class="skill-tags">
                 <span v-for="skill in portfolioData.skills.Design" :key="skill" class="skill-tag design">
                   {{ skill }}
                 </span>
               </div>
             </div>
          </div>
        </div>
      </section>

      <!-- LEVEL 3: EXPERIENCE -->
      <section class="level level-exp">
        <ParallaxBackground theme="mountain" />
        <FloatingElements type="gems" :count="10" />
        
        <div class="content-layer">
          <h2 class="section-title nes-text is-warning glow-title">
            <i class="nes-icon trophy is-small"></i> Experience Quest
          </h2>
          <div class="timeline">
              <div v-for="(job, index) in portfolioData.experience" :key="job.id" class="exp-item" :style="{ animationDelay: index * 0.2 + 's' }">
                  <DialogueBox :withTitle="false" type="is-white">
                      <h4 class="nes-text is-primary">{{ job.period }}</h4>
                      <h5 class="nes-text is-success">{{ job.company }}</h5>
                      <p>{{ job.role }}</p>
                  </DialogueBox>
              </div>
          </div>
        </div>
      </section>

      <!-- LEVEL 4: PROJECTS -->
      <section class="level level-projects">
        <ParallaxBackground theme="sunset" />
        <FloatingElements type="coins" :count="12" />
        
        <div class="content-layer">
          <h2 class="section-title nes-text is-primary glow-title">
            <i class="nes-icon star is-small"></i> Projects Loot
          </h2>
          <div class="projects-grid">
             <div v-for="(proj, index) in portfolioData.projects" :key="proj.id" class="project-card" :style="{ animationDelay: index * 0.15 + 's' }">
                 <div class="nes-container is-rounded with-title is-centered project-container">
                     <p class="title">{{ proj.title }}</p>
                     <div class="tech-stack">
                       <div class="tech-badge frontend">
                         <span class="tech-label">🖥️ FE:</span>
                         <span class="nes-text is-primary">{{ proj.tech }}</span>
                       </div>
                       <div v-if="proj.techBack" class="tech-badge backend">
                         <span class="tech-label">⚙️ BE:</span>
                         <span class="nes-text is-error">{{ proj.techBack }}</span>
                       </div>
                     </div>
                     <p class="desc-text">{{ proj.desc }}</p>
                 </div>
             </div>
          </div>
        </div>
      </section>

      <!-- LEVEL 6: LIFESTYLE -->
      <section class="level level-lifestyle">
        <ParallaxBackground theme="desert" />
        <FloatingElements type="stars" :count="6" />
        
        <div class="content-layer">
          <h2 class="section-title nes-text is-warning glow-title">
            <i class="nes-icon heart is-small"></i> My Gallery
          </h2>
          
          <div class="gallery-container">
            <!-- My Lifestyle Section -->
            <div class="gallery-section">
              <h3 class="gallery-subtitle nes-text is-primary">My Lifestyle</h3>
              <div class="lifestyle-gallery">
                <div class="gallery-item" v-for="(img, index) in lifestyleImages" :key="`life-${index}`">
                  <img 
                    :src="`/lifestyle/${img}`" 
                    :alt="`Lifestyle ${index + 1}`"
                    class="gallery-img"
                    loading="lazy"
                  />
                </div>
              </div>
            </div>

            <!-- My Cats Section -->
            <div class="gallery-section">
              <h3 class="gallery-subtitle nes-text is-warning" style="margin-top: 20px;">My Cats 🐱</h3>
              <div class="lifestyle-gallery">
                <div class="gallery-item" v-for="(img, index) in catImages" :key="`cat-${index}`">
                  <img 
                    :src="`/lifestyle/cats/${img}`" 
                    :alt="`Cat ${index + 1}`"
                    class="gallery-img"
                    loading="lazy"
                  />
                </div>
              </div>
            </div>

            <!-- Relationships Section -->
            <div class="gallery-section">
              <h3 class="gallery-subtitle nes-text is-error" style="margin-top: 20px;">Relationships ❤️</h3>
              <div class="lifestyle-gallery">
                <div class="gallery-item" v-for="(img, index) in relationImages" :key="`rel-${index}`">
                  <img 
                    :src="`/lifestyle/relations/${img}`" 
                    :alt="`Relation ${index + 1}`"
                    class="gallery-img"
                    loading="lazy"
                  />
                </div>
              </div>
            </div>
          </div>
        </div>
      </section>

      <!-- LEVEL 7: CONTACT -->
      <section class="level level-contact">
        <ParallaxBackground theme="night" />
        <FloatingElements type="hearts" :count="8" />
        
        <div class="content-layer">
          <div class="final-castle">
            <i class="nes-icon trophy is-large victory-bounce"></i>
            <div class="confetti-container">
              <span v-for="n in 20" :key="n" class="confetti" :style="{ 
                left: Math.random() * 100 + '%',
                animationDelay: Math.random() * 2 + 's',
                backgroundColor: ['#ff6b6b', '#4ecdc4', '#ffe66d', '#a8e6cf', '#ff9ff3'][n % 5]
              }"></span>
            </div>
          </div>
          
          <DialogueBox title="🏆 The End!" type="is-dark">
              <p class="nes-text is-success" style = "text-align: center;">Know me more</p>
              <div class="social-links">
                  <a :href="portfolioData.contact.github" target="_blank" class="nes-icon github is-medium social-icon"></a>
                  <a :href="portfolioData.contact.linkedin" target="_blank" class="nes-icon linkedin is-medium social-icon"></a>
                  <a :href="'mailto:' + portfolioData.contact.email" target="_blank" class="nes-icon gmail is-medium social-icon"></a>
              </div>
              <p class="email-text">
                <i class="nes-icon is-small heart"></i> Mr.{{ portfolioData.personal.name }} ({{ portfolioData.personal.nickname }})
              </p>
          </DialogueBox>
        </div>
      </section>
      
      <!-- SPACER for smooth ending -->
      <div style="width: 50vw;"></div>

    </div>

    <div class="player-fixed">
      <PlayerCharacter :isMoving="isMoving" :facingRight="facingRight" />
    </div>
    
    <!-- Progress indicator -->
    <div class="progress-indicator">
      <div 
        v-for="n in 7" 
        :key="n" 
        :class="['progress-dot', { 'active': currentLevel >= n - 1 }]"
      ></div>
    </div>
    
    <!-- Mobile Controls -->
    <div class="mobile-controls">
      <button 
        class="nes-btn is-primary nav-btn prev" 
        @mousedown="startMoving(-1)"
        @touchstart.prevent="startMoving(-1)"
        @mouseup="stopMoving"
        @mouseleave="stopMoving"
        @touchend="stopMoving"
        :disabled="currentLevel === 0"
      >
        &lt;
      </button>
      <button 
        class="nes-btn is-primary nav-btn next" 
        @mousedown="startMoving(1)"
        @touchstart.prevent="startMoving(1)"
        @mouseup="stopMoving"
        @mouseleave="stopMoving"
        @touchend="stopMoving"
        :disabled="currentLevel === 6"
      >
        &gt;
      </button>
    </div>
  </div>
</template>

<style scoped>
.game-container {
  width: 100%;
  height: 100vh;
  overflow: hidden;
  position: relative;
  font-family: 'Press Start 2P', cursive;
  background-color: #87CEEB;
}

.player-fixed {
  position: absolute;
  bottom: 120px;
  left: 15%;
  z-index: 1000;
  pointer-events: none;
  filter: drop-shadow(0 4px 8px rgba(0,0,0,0.3));
}

.world-track {
  display: flex;
  height: 100%;
}

.level {
  min-width: 100vw;
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  position: relative;
  box-sizing: border-box;
  padding: 20px;
  overflow: hidden;
}

.content-layer {
  position: relative;
  z-index: 20;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  opacity: 0; /* Hidden initially for animation */
}

/* First level visible by default */
.level:first-child .content-layer {
  opacity: 1;
}

.decorative-elements {
  position: absolute;
  inset: 0;
  z-index: 5;
  pointer-events: none;
}

/* === FLOATING ANIMATION === */
.floating {
  animation: float 4s ease-in-out infinite;
}

.floating.delay-1 {
  animation-delay: 1s;
}

.floating.delay-2 {
  animation-delay: 2s;
}

@keyframes float {
  0%, 100% { transform: translateY(0); }
  50% { transform: translateY(-15px); }
}

/* === GLOW EFFECTS === */
.glow-text {
  text-shadow: 
    0 0 10px currentColor,
    0 0 20px currentColor,
    0 0 30px currentColor;
  animation: glow 2s ease-in-out infinite alternate;
}

@keyframes glow {
  from { text-shadow: 0 0 5px currentColor, 0 0 10px currentColor; }
  to { text-shadow: 0 0 15px currentColor, 0 0 25px currentColor, 0 0 35px currentColor; }
}

.glow-box {
  box-shadow: 
    0 0 20px rgba(255, 255, 255, 0.3),
    inset 0 0 20px rgba(255, 255, 255, 0.1);
  animation: boxGlow 3s ease-in-out infinite alternate;
}

@keyframes boxGlow {
  from { box-shadow: 0 0 10px rgba(255, 255, 255, 0.2); }
  to { box-shadow: 0 0 30px rgba(255, 255, 255, 0.4), 0 0 60px rgba(138, 43, 226, 0.2); }
}

.glow-title {
  text-shadow: 0 0 20px currentColor;
}

/* === PULSE ANIMATION === */
.pulse {
  animation: pulse 2s ease-in-out infinite;
}

.pulse.delay-1 {
  animation-delay: 0.5s;
}

.pulse.delay-2 {
  animation-delay: 1s;
}

@keyframes pulse {
  0%, 100% { transform: scale(1); }
  50% { transform: scale(1.2); }
}

/* === BLINK ANIMATION === */
.helper-text {
  margin-top: 20px;
  font-size: 0.8rem;
  color: #888;
}

.blink {
  animation: blinker 1.5s linear infinite;
}

@keyframes blinker {
  50% { opacity: 0; }
}

/* === CONTENT WRAPPER === */
.content-wrapper {
  display: flex;
  gap: 30px;
  align-items: center;
  flex-wrap: wrap;
  justify-content: center;
}

/* === SKILLS === */
.skills-block {
  max-width: 550px;
  padding: 15px;
}

.skill-category {
  margin-bottom: 18px;
}

.category-label {
  font-size: 0.85rem;
  margin-bottom: 10px;
  font-weight: bold;
}

.skill-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
}

.skill-tag {
  font-size: 0.7rem;
  padding: 8px 14px;
  border-radius: 6px;
  background: rgba(255,255,255,0.15);
  border: 2px solid rgba(255,255,255,0.3);
  transition: all 0.2s ease;
  font-weight: 500;
}

.skill-tag:hover {
  transform: scale(1.1);
  background: rgba(255,255,255,0.25);
}

.skill-tag.lang {
  border-color: #f7d51d;
  color: #f7d51d;
}

.skill-tag.framework {
  border-color: #92cc41;
  color: #92cc41;
}

.skill-tag.tool {
  border-color: #209cee;
  color: #209cee;
}

.skill-tag.os {
  border-color: #e85151;
  color: #e85151;
}

.skill-tag.design {
  border-color: #ff69b4;
  color: #ff69b4;
}

/* === PROFILE LOGO === */
.profile-logo {
  margin-bottom: -10px;
  display: flex;
  justify-content: center;
  z-index: 10;
  position: relative;
}

.pixel-avatar {
  width: 180px;
  height: 180px;
  border-radius: 50%;
  image-rendering: pixelated;
  image-rendering: -moz-crisp-edges;
  image-rendering: crisp-edges;
  border: 4px solid #fff;
  box-shadow: 
    0 0 0 3px #333,
    0 0 15px rgba(0, 200, 255, 0.6),
    0 0 30px rgba(0, 200, 255, 0.4);
  filter: contrast(1.1) saturate(0.8);
  object-fit: cover;
  animation: avatarGlow 2s ease-in-out infinite alternate;
}

@keyframes avatarGlow {
  0% {
    box-shadow: 
      0 0 0 3px #333,
      0 0 15px rgba(0, 200, 255, 0.6),
      0 0 30px rgba(0, 200, 255, 0.4);
  }
  100% {
    box-shadow: 
      0 0 0 3px #333,
      0 0 20px rgba(0, 200, 255, 0.8),
      0 0 40px rgba(0, 200, 255, 0.6);
  }
}

/* === LIFESTYLE GALLERY === */
.gallery-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 95vw;
  max-height: 80vh;
  padding: 10px;
}

.gallery-section {
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-bottom: 5px;
}

.gallery-subtitle {
  font-size: 1.2rem;
  margin-bottom: 10px;
  text-shadow: 2px 2px 0 #000;
  background: rgba(0,0,0,0.5);
  padding: 5px 15px;
  border-radius: 4px;
}

.lifestyle-gallery {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  gap: 15px;
  width: 100%;
}

.lifestyle-gallery .gallery-item {
  width: 140px; 
  height: 140px;
}

.gallery-item {
  position: relative;
  border-radius: 8px;
  overflow: hidden;
  border: 3px solid #fff;
  box-shadow: 0 4px 15px rgba(0,0,0,0.3);
  transition: all 0.3s ease;
  aspect-ratio: 1;
}

.gallery-item:nth-child(odd) {
  transform: rotate(-2deg);
}

.gallery-item:nth-child(even) {
  transform: rotate(2deg);
}

.gallery-item:hover {
  transform: scale(1.1) rotate(0deg);
  z-index: 10;
  box-shadow: 
    0 8px 30px rgba(0,0,0,0.4),
    0 0 20px rgba(255, 215, 0, 0.5);
}

.gallery-img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  image-rendering: pixelated;
  image-rendering: -moz-crisp-edges;
  filter: contrast(1.1) saturate(0.9);
  transition: filter 0.3s ease;
}

.gallery-item:hover .gallery-img {
  filter: contrast(1.2) saturate(1.1);
}

/* === CAT BACKGROUND === */
.cat-background {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  display: flex;
  z-index: 1;
  opacity: 0.4;
}

.cat-half {
  width: 50%;
  height: 100%;
  overflow: hidden;
  position: relative;
}

.cat-half::after {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.3);
  z-index: 1;
}

.cat-bg-img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  image-rendering: pixelated;
  image-rendering: -moz-crisp-edges;
  image-rendering: crisp-edges;
  filter: contrast(1.2) saturate(0.7) brightness(0.9);
}

.cat-half.right .cat-bg-img {
  transform: scaleX(-1);
}

/* === EXPERIENCE === */
.timeline {
  display: flex;
  gap: 30px;
  margin-top: 30px;
  overflow-x: visible;
}

.exp-item {
  animation: fadeInUp 0.6s ease forwards;
  opacity: 0;
  transform: translateY(30px);
}

@keyframes fadeInUp {
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.exp-badge {
  position: absolute;
  top: -15px;
  right: -10px;
  background: linear-gradient(135deg, #FFD700 0%, #FFA500 100%);
  color: #000;
  padding: 5px 10px;
  font-size: 0.6rem;
  border-radius: 4px;
  font-weight: bold;
  box-shadow: 0 2px 10px rgba(255, 215, 0, 0.5);
  animation: badgeShine 2s ease-in-out infinite;
}

@keyframes badgeShine {
  0%, 100% { box-shadow: 0 2px 10px rgba(255, 215, 0, 0.5); }
  50% { box-shadow: 0 2px 20px rgba(255, 215, 0, 0.8), 0 0 30px rgba(255, 215, 0, 0.4); }
}

/* === PROJECTS === */
.projects-grid {
  display: flex;
  gap: 25px;
  flex-wrap: wrap;
  justify-content: center;
  max-width: 85vw;
  align-items: flex-start;
}

.project-card {
  width: 320px;
  flex-shrink: 0;
  animation: fadeInUp 0.6s ease forwards;
  opacity: 0;
  transform: translateY(30px);
}

.project-container {
  transition: transform 0.3s ease, box-shadow 0.3s ease;
  background: rgba(255,255,255,0.95);
  padding: 12px;
}

.project-container .title {
  font-size: 0.8rem !important;
}

.project-container:hover {
  transform: translateY(-10px) scale(1.02);
  box-shadow: 0 15px 40px rgba(0,0,0,0.3);
}

.tech-stack {
  margin: 10px 0;
}

.tech-badge {
  background: rgba(0,0,0,0.08);
  padding: 6px 10px;
  border-radius: 4px;
  margin: 5px 0;
  display: block;
  text-align: left;
  font-size: 0.65rem;
}

.tech-badge.frontend {
  border-left: 3px solid #209cee;
}

.tech-badge.backend {
  border-left: 3px solid #92cc41;
}

.tech-label {
  font-weight: bold;
  margin-right: 6px;
  font-size: 0.7rem;
}

.desc-text {
  font-size: 0.7rem;
  line-height: 1.7;
  margin: 12px 0;
  min-height: 45px;
  color: #333;
}

.btn-glow {
  animation: btnGlow 2s ease-in-out infinite;
  transition: all 0.3s ease;
}

.btn-glow:hover {
  transform: scale(1.1);
  box-shadow: 0 0 20px rgba(138, 43, 226, 0.6);
}

@keyframes btnGlow {
  0%, 100% { box-shadow: 0 0 5px rgba(138, 43, 226, 0.3); }
  50% { box-shadow: 0 0 15px rgba(138, 43, 226, 0.5); }
}

/* === SECTION TITLE === */
.section-title {
  background: rgba(0,0,0,0.85);
  padding: 15px 30px;
  border: 4px solid #fff;
  margin-bottom: 25px;
  border-radius: 8px;
  box-shadow: 0 5px 20px rgba(0,0,0,0.3);
}

/* === SOCIAL LINKS === */
.social-links {
  margin-top: 20px;
  display: flex;
  gap: 25px;
  justify-content: center;
}

.social-icon {
  transition: transform 0.3s ease, filter 0.3s ease;
  cursor: pointer;
  display: inline-block;
}

.social-icon:hover {
  transform: scale(3) rotate(10deg) !important;
  filter: drop-shadow(0 0 15px rgba(255,255,255,1)) drop-shadow(0 0 25px rgba(255,100,100,0.8));
}

.email-text {
  margin-top: 20px;
  font-size: 0.7rem;
  opacity: 0.8;
}

/* === VICTORY EFFECTS === */
.final-castle {
  position: relative;
  margin-bottom: 30px;
}

.victory-bounce {
  animation: victoryBounce 1s ease-in-out infinite;
  filter: drop-shadow(0 0 20px rgba(255, 215, 0, 0.8));
}

@keyframes victoryBounce {
  0%, 100% { transform: scale(2.5) translateY(0) rotate(-5deg); }
  50% { transform: scale(2.5) translateY(-20px) rotate(5deg); }
}

/* === CONFETTI === */
.confetti-container {
  position: absolute;
  top: -100px;
  left: 50%;
  transform: translateX(-50%);
  width: 200px;
  height: 200px;
  pointer-events: none;
}

.confetti {
  position: absolute;
  width: 10px;
  height: 10px;
  animation: confettiFall 3s linear infinite;
}

@keyframes confettiFall {
  0% {
    transform: translateY(-100px) rotate(0deg);
    opacity: 1;
  }
  100% {
    transform: translateY(200px) rotate(720deg);
    opacity: 0;
  }
}

/* === PROGRESS INDICATOR === */
.progress-indicator {
  position: fixed;
  bottom: 30px;
  left: 50%;
  transform: translateX(-50%);
  display: flex;
  gap: 15px;
  z-index: 1500;
  background: rgba(0,0,0,0.6);
  padding: 10px 20px;
  border-radius: 30px;
  backdrop-filter: blur(5px);
}

.progress-dot {
  width: 12px;
  height: 12px;
  border-radius: 50%;
  background: rgba(255,255,255,0.3);
  border: 2px solid rgba(255,255,255,0.5);
  transition: all 0.3s ease;
}

.progress-dot.active {
  background: #4CAF50;
  box-shadow: 0 0 10px #4CAF50;
  border-color: #4CAF50;
}

/* ============================================ */
/* ============ RESPONSIVE STYLES ============ */
/* ============================================ */

/* Tablet */
@media (max-width: 1024px) {
  .level {
    min-width: 100vw;
    padding: 15px;
  }
  
  .content-wrapper {
    flex-direction: column;
    gap: 20px;
  }
  
  .projects-grid {
    max-width: 95vw;
  }
  
  .project-card {
    width: 280px;
  }
  
  .timeline {
    flex-wrap: wrap;
    justify-content: center;
  }
}

/* Mobile */
@media (max-width: 768px) {
  .game-container {
    font-size: 0.7rem;
  }
  
  .level {
    padding: 10px;
    min-width: 100vw;
    padding-bottom: 120px; /* Space for character and ground */
  }
  
  .content-layer {
    padding: 0 10px;
    margin-bottom: 60px; /* Keep content above character */
    max-height: calc(100vh - 180px);
    overflow-y: auto;
  }
  
  .player-fixed {
    bottom: 80px;
    left: 10%;
    transform: scale(0.8);
    transform-origin: bottom left;
  }

  /* Welcome Screen Fixes */
  .pixel-avatar {
    width: 140px;
    height: 140px;
    margin-bottom: 20px !important; /* Fix overlap */
  }
  
  /* DialogueBox */
  .nes-container {
    max-width: 90vw !important;
    padding: 12px !important;
    font-size: 0.8rem; /* Increase text size further */
    line-height: 1.6;
  }
  
  .nes-container .title {
    font-size: 1rem !important; /* Larger title */
  }

  .helper-text {
    font-size: 0.6rem !important; /* Smaller scroll text to fit one line */
  }
  
  /* Section titles */
  .section-title {
    font-size: 0.8rem;
    padding: 10px 15px;
  }
  
  /* Skills */
  .skills-block {
    max-width: 90vw;
  }
  
  /* Timeline */
  .timeline {
    flex-direction: column;
    gap: 15px;
    align-items: center;
  }
  
  .exp-item {
    width: 90vw;
  }
  
  .exp-badge {
    font-size: 0.5rem;
    padding: 3px 6px;
  }
  
  /* Projects */
  .projects-grid {
    flex-direction: column;
    align-items: center;
    max-width: 100vw;
    gap: 15px;
  }
  
  .project-card {
    width: 90vw;
    max-width: 320px;
  }
  
  .tech-badge {
    font-size: 0.5rem;
    padding: 3px 6px;
  }
  
  .desc-text {
    font-size: 0.55rem;
    min-height: 30px;
  }
  
  /* Social links */
  .social-links {
    gap: 15px;
    flex-wrap: wrap;
  }
  
  .social-links .nes-icon {
    transform: scale(0.8);
  }
  
  /* Progress indicator */
  .progress-indicator {
    bottom: 15px;
    padding: 8px 15px;
    gap: 10px;
  }
  
  .progress-dot {
    width: 10px;
    height: 10px;
  }
  
  /* Floating elements - reduce for mobile */
  .decorative-elements {
    display: none;
  }
  
  /* Ground */
  .ground-layer {
    height: 80px;
  }
}

/* Small Mobile */
@media (max-width: 480px) {
  .game-container {
    font-size: 0.6rem;
  }
  
  .player-fixed {
    bottom: 60px;
    left: 5%;
    transform: scale(0.6);
  }
  
  .nes-container {
    padding: 10px !important;
    font-size: 0.55rem;
  }
  
  .section-title {
    font-size: 0.7rem;
    padding: 8px 12px;
  }
  
  .project-card {
    width: 95vw;
  }
  
  .social-links .nes-icon {
    transform: scale(2);
  }
  
  .progress-indicator {
    bottom: 10px;
    padding: 6px 12px;
    gap: 8px;
  }
  
  .progress-dot {
    width: 8px;
    height: 8px;
  }
  
  .email-text {
    font-size: 0.5rem;
  }
  
  /* Mobile Layout Fixes */
  .level-skills .content-layer,
  .level-projects .content-layer,
  .level-lifestyle .content-layer {
    padding-top: 80px;
    align-items: center;
    justify-content: flex-start;
  }
  
  .skills-block,
  .projects-container,
  .gallery-container {
    max-height: calc(100vh - 120px);
    overflow-y: auto;
    padding-bottom: 60px; /* Space for controls */
  }
  
  /* Mobile Controls */
  .mobile-controls {
    display: flex;
    justify-content: space-between;
    position: fixed;
    bottom: 20px;
    left: 20px;
    right: 20px;
    z-index: 2000;
  }
  
  .nav-btn {
    width: 50px;
    height: 50px;
    padding: 0;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 1.2rem;
    opacity: 0.8;
    touch-action: manipulation; /* Disable double-tap zoom */
    user-select: none; /* Prevent text selection */
  }
  
  .nav-btn:disabled {
    opacity: 0.3;
    cursor: not-allowed;
  }
}

/* Desktop: Hide mobile controls */
@media (min-width: 481px) {
  .mobile-controls {
    display: none;
  }
}
</style>