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
  // 5 levels, so divide progress into 5 segments
  const level = Math.min(Math.floor(progress * 6), 5);
  currentLevel.value = level;
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
        <ParallaxBackground theme="sky" />
        <FloatingElements type="butterflies" :count="6" />
        <PixelGround theme="grass" />
        
        <div class="content-layer">
          <DialogueBox title="🎮 Welcome!" type="is-dark">
            <p>Hi! I'm <span class="nes-text is-primary glow-text">{{ portfolioData.personal.name }}</span></p>
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
        <PixelGround theme="grass" />
        
        <div class="content-layer content-wrapper">
          <DialogueBox title="👋 Hello, I'm Warat Supaporn!" type="is-rounded">
            <p>{{ portfolioData.personal.bio }}</p>
            <p style="margin-top: 0.8rem;">{{ portfolioData.personal.bio2 }}</p>
            <p style="margin-top: 0.8rem; font-style: italic;">My favourite hobbies is {{ portfolioData.personal.hobbies }}</p>
          </DialogueBox>
        </div>
      </section>

      <!-- LEVEL 3: TECH STACK -->
      <section class="level level-skills">
        <ParallaxBackground theme="desert" />
        <FloatingElements type="stars" :count="8" />
        <PixelGround theme="sand" />
        
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
          </div>
        </div>
      </section>

      <!-- LEVEL 3: EXPERIENCE -->
      <section class="level level-exp">
        <ParallaxBackground theme="cave" />
        <FloatingElements type="gems" :count="10" />
        <PixelGround theme="stone" />
        
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
        <ParallaxBackground theme="night" />
        <FloatingElements type="stars" :count="12" />
        <PixelGround theme="stone" />
        
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

      <!-- LEVEL 5: CONTACT -->
      <section class="level level-contact">
        <ParallaxBackground theme="sunset" />
        <FloatingElements type="hearts" :count="8" />
        <PixelGround theme="castle" />
        
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
          
          <DialogueBox title="🏆 Quest Complete!" type="is-dark">
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
        v-for="n in 6" 
        :key="n" 
        :class="['progress-dot', { 'active': currentLevel >= n - 1 }]"
      ></div>
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
  margin-top: -20px;
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
  0%, 100% { transform: translateY(0) rotate(-5deg); }
  50% { transform: translateY(-20px) rotate(5deg); }
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
  
  /* DialogueBox */
  .nes-container {
    max-width: 90vw !important;
    padding: 12px !important;
    font-size: 0.6rem;
  }
  
  .nes-container .title {
    font-size: 0.7rem !important;
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
    transform: scale(0.6);
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
}
</style>