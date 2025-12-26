# 🎮 Pixel Art Portfolio

> ✨ **This portfolio was created with AI prompting assistance** - demonstrating the power of human-AI collaboration in web development!

A retro-style pixel art portfolio website featuring a horizontal scrolling game world with animated characters, parallax backgrounds, and interactive elements.

## 🖥️ Live Demo

[View Portfolio](https://warat-supaporn.vercel.app) _(Update with your deployed URL)_

## 📸 Preview

The portfolio features:

- 🎮 Side-scrolling game world with multiple themed sections
- 🏀 Animated pixel art basketball player character with sword
- 🐱 Two cats: Orange tabby and Gray Persian
- ✨ Parallax backgrounds and floating decorative elements
- 📱 Responsive design for all devices

## 🛠️ Tech Stack

### Frontend Framework

| Technology   | Version | Description                                           |
| ------------ | ------- | ----------------------------------------------------- |
| **Vue.js 3** | ^3.5.13 | Progressive JavaScript framework with Composition API |
| **Vite**     | ^7.2.4  | Next-generation frontend build tool                   |

### Styling & UI

| Library     | Version | Description                           |
| ----------- | ------- | ------------------------------------- |
| **NES.css** | ^2.2.1  | Retro 8-bit style CSS framework       |
| **SASS**    | ^1.83.0 | CSS preprocessor for advanced styling |

### Animation

| Library           | Version       | Description                          |
| ----------------- | ------------- | ------------------------------------ |
| **GSAP**          | ^3.14.2       | Professional-grade animation library |
| **ScrollTrigger** | (GSAP plugin) | Scroll-based animations              |

### Development Tools

| Tool                   | Purpose                |
| ---------------------- | ---------------------- |
| **@vitejs/plugin-vue** | Vue 3 support for Vite |
| **ESLint**             | Code linting           |

## 📂 Project Structure

```
my-pixel-portfolio/
├── src/
│   ├── components/
│   │   ├── GameWorld.vue          # Main game world component
│   │   ├── PlayerCharacter.vue    # Animated pixel characters
│   │   ├── ParallaxBackground.vue # Parallax effect backgrounds
│   │   ├── FloatingElements.vue   # Decorative floating items
│   │   ├── PixelGround.vue        # Themed ground layers
│   │   └── UI/
│   │       └── DialogueBox.vue    # Dialogue box component
│   ├── data/
│   │   └── portfolio.js           # Portfolio data (experience, skills, etc.)
│   ├── assets/                    # Images and styles
│   ├── App.vue                    # Root component
│   ├── main.js                    # App entry point
│   └── style.css                  # Global styles
├── index.html
├── vite.config.js
└── package.json
```

## ✨ Features

- **🎨 Pure CSS Pixel Art Characters** - No sprite images needed
- **🔄 Scroll-based Direction** - Characters face different directions based on scroll
- **🏆 Multiple Themed Sections**:
  - 🏠 Welcome Level
  - 🌳 About Me (Forest theme)
  - 🏜️ Tech Stack (Desert theme)
  - 🏔️ Experience (Cave theme)
  - 💎 Projects (Dungeon theme)
  - 👋 Contact (Night theme)
- **📱 Fully Responsive** - Works on desktop, tablet, and mobile
- **✨ Smooth Animations** - GSAP-powered scroll animations

## 🚀 Getting Started

### Prerequisites

- Node.js 18+
- npm or yarn

### Installation

```bash
# Clone the repository
git clone https://github.com/sanookdev/pixel-art-profile.git

# Navigate to project directory
cd pixel-art-profile

# Install dependencies
npm install

# Start development server
npm run dev
```

### Build for Production

```bash
npm run build
```

## 🤖 AI-Assisted Development

This portfolio was created through collaborative prompting with **AI assistance**, demonstrating:

- 🎨 CSS pixel art character design
- 🎮 Complex animation implementations
- 📱 Responsive design patterns
- ⚡ Performance optimization
- 🏗️ Component architecture

The entire development process utilized natural language prompts to iteratively build and refine the portfolio features.

## 📝 Customization

### Update Your Information

Edit `src/data/portfolio.js` to update:

- Personal details
- Experience/work history
- Projects
- Skills & tools
- Contact information

### Change Character Appearance

Modify `src/components/PlayerCharacter.vue` to customize:

- Character colors (jersey, hair, etc.)
- Cat colors
- Animation styles

## 📄 License

MIT License - feel free to use this as a template for your own portfolio!

## 👤 Author

**Warat Supaporn (Sanooker)**

- GitHub: [@sanookdev](https://github.com/sanookdev)
- LinkedIn: [Warat Supaporn](https://www.linkedin.com/in/warat-supaporn-622b101b0/)

---

⭐ If you like this project, please give it a star!
