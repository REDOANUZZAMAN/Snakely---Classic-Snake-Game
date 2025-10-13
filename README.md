# 🐍 Snakely - Classic Snake Game

A modern, minimalist implementation of the classic Snake game built with pure vanilla JavaScript. Features smooth animations, responsive design, and a beautiful glowing aesthetic with no dependencies required.

![Status](https://img.shields.io/badge/status-active-success.svg)
![HTML5](https://img.shields.io/badge/html5-%23E34F26.svg?style=flat&logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/css3-%231572B6.svg?style=flat&logo=css3&logoColor=white)
![JavaScript](https://img.shields.io/badge/javascript-%23323330.svg?style=flat&logo=javascript&logoColor=white)

## ✨ Features

- **Pure Vanilla JavaScript** - No frameworks or libraries required
- **Responsive Grid System** - Adapts to any screen size (28x16 or 16x28)
- **Smooth Animations** - 60 FPS gameplay with requestAnimationFrame
- **Visual Path Indicators** - Directional arrows show path to food
- **Glowing Effects** - Beautiful animated glow on snake head and food
- **Progressive Difficulty** - Speed increases as you eat more food
- **Wall Wrapping** - Snake wraps around edges of the board
- **Keyboard Controls** - Arrow keys or WASD for movement
- **Score Tracking** - Real-time score display
- **Single File** - Everything contained in one HTML file

## 🎮 How to Play

### Controls

| Key | Action |
|-----|--------|
| ↑ or W | Move Up |
| ↓ or S | Move Down |
| → or D | Move Right |
| ← or A | Move Left |

### Objective

- Guide the snake to eat the glowing food
- Each food eaten increases your score by 1
- Snake grows longer with each food consumed
- Speed increases slightly after eating
- Avoid running into yourself
- Walls wrap around - use them strategically!

### Tips

- Plan your path ahead using the directional indicators on tiles
- Use wall wrapping to escape tight situations
- The snake speeds up gradually, so be ready for faster gameplay
- Don't corner yourself - always leave an escape route

## 🚀 Quick Start

### Option 1: Direct Download

```bash
# Download the HTML file
# Open directly in your browser
open snake-game.html
```

### Option 2: Local Server

```bash
# Using Python 3
python -m http.server 8000

# Using Node.js (http-server)
npx http-server

# Then open: http://localhost:8000/snake-game.html
```

### Option 3: Online Hosting

Upload to any web hosting service:
- GitHub Pages
- Netlify
- Vercel
- Surge.sh

No build process needed!

## 📁 File Structure

```
snake-game/
├── snake-game.html     # Complete game (HTML + CSS + JS)
└── README.md          # Documentation
```

## 🎨 Customization

### Change Colors

```css
/* In the <style> section */

/* Background gradient */
body {
  background: radial-gradient(#333, #111); /* Dark theme */
}

/* Snake color */
backgroundColor: 'rgba(255, 255, 255, ' + this.alpha + ')'; /* White */

/* Food color */
backgroundColor: 'hsla(' + this.hue + ', 100%, 60%, 1)'; /* Rainbow hue */
```

### Adjust Grid Size

```javascript
// In StatePlay.prototype.init
this.dimLong = 28;  // Change for longer dimension
this.dimShort = 16; // Change for shorter dimension
```

### Modify Game Speed

```javascript
// In g.Snake constructor
this.updateTick = 10;          // Starting speed (lower = faster)
this.updateTickLimit = 3;      // Maximum speed limit
this.updateTickChange = 0.2;   // Speed increase per food
```

### Change Snake Length

```javascript
// In g.Snake constructor
for( var i = 0; i < 5; i++ ) {  // Change 5 to desired length
  this.tiles.push( new g.SnakeTile({...}));
}
```

### Disable Wall Wrapping

```javascript
// In g.Snake.prototype.update, replace wrap logic with:
if( this.tiles[0].col >= this.parentState.cols ||
    this.tiles[0].col < 0 ||
    this.tiles[0].row >= this.parentState.rows ||
    this.tiles[0].row < 0 ) {
  this.deathFlag = 1;
}
```

### Adjust Visual Effects

```javascript
// Snake head glow intensity
this.blur = this.parentState.dimAvg * 0.03; // Increase for more glow

// Food pulse animation
this.scale = 0.8 + Math.sin(...) * 0.2; // Adjust multiplier

// Snake eating animation rotation
this.rotation = (...) * 90; // Change angle
```

## 🛠️ Technical Details

### Architecture

The game uses a modular entity-component system:

| Component | Purpose |
|-----------|---------|
| **Grid** | Tracks board state (empty/snake/food) |
| **BoardTile** | Visual grid tiles with path indicators |
| **SnakeTile** | Individual snake segment |
| **FoodTile** | Animated food item |
| **Snake** | Snake logic and movement |
| **Food** | Food spawning and management |
| **StatePlay** | Game state management |

### Performance Features

- **RequestAnimationFrame** - Smooth 60 FPS rendering
- **Delta Time Calculation** - Consistent speed across devices
- **DOM Reuse** - Tiles rotate through object pool
- **CSS Transforms** - Hardware-accelerated animations
- **Efficient Grid Updates** - Only modified cells tracked

### Polyfills Included

- RequestAnimationFrame for older browsers
- DOM manipulation utilities (addClass, removeClass, etc.)

## 🌐 Browser Support

| Browser | Support |
|---------|---------|
| Chrome | ✅ Full support |
| Firefox | ✅ Full support |
| Safari | ✅ Full support |
| Edge | ✅ Full support |
| Opera | ✅ Full support |
| IE11 | ⚠️ Limited (polyfills included) |

### Mobile Support

- Touch controls not implemented
- Playable on mobile with external keyboard
- Responsive grid adapts to portrait/landscape

## 🐛 Troubleshooting

### Game Runs Too Fast/Slow

```javascript
// Adjust in g.Snake constructor
this.updateTick = 10; // Increase to slow down, decrease to speed up
```

### Path Indicators Not Showing

```javascript
// Check in g.BoardTile.prototype.update
// Ensure food.tile.col and food.tile.row are valid
```

### Snake Not Responding to Keys

```javascript
// Verify event listener is attached
// Check browser console for errors
// Try pressing keys after clicking on the page
```

### Visual Glitches on Resize

```javascript
// Window resize recalculates all dimensions
// Refresh page if issues persist
```

## 📊 Game Mechanics

### Scoring System

- **Base Score**: +1 per food eaten
- **No Penalties**: Death resets game but not score tracking
- **Speed Bonus**: Implicit - faster gameplay challenges skill

### Difficulty Progression

```javascript
Initial Speed: 10 ticks (16.67ms per tick at 60 FPS)
Speed Decrease: 0.2 ticks per food
Minimum Speed: 3 ticks (max difficulty)
Growth Rate: +1 segment per food
```

### Collision Detection

- **Self-collision**: Game over and restart
- **Food collision**: Eat food, grow, speed up
- **Wall collision**: Wrap to opposite side

## 💡 Enhancement Ideas

- [ ] Add touch controls for mobile devices
- [ ] Implement high score persistence (localStorage)
- [ ] Add sound effects and background music
- [ ] Create multiple difficulty levels
- [ ] Add power-ups (slow down, extra points, invincibility)
- [ ] Implement obstacle tiles
- [ ] Add multiplayer mode
- [ ] Create level progression system
- [ ] Add particle effects on food consumption
- [ ] Implement game pause functionality
- [ ] Add color themes selector
- [ ] Create tutorial/instructions overlay

## 🎯 Code Quality Features

- **No Global Pollution** - All code in IIFE modules
- **Namespace Pattern** - Single global `g` object
- **Prototype Pattern** - Efficient object creation
- **State Machine** - Clean state management
- **Separation of Concerns** - Update/render split
- **Commented Code** - Clear section markers

## 📝 License

This project is open source and available under the [MIT License](LICENSE).

## 🤝 Contributing

Contributions, issues, and feature requests are welcome!

1. Fork the project
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add touch controls'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 👨‍💻 Author

**Redoanuzzaman**
- GitHub: [@redoanuzzaman](https://github.com/redoanuzzaman)
- Email: redoanuzzaman707@gmail.com
- Website: [redoan.dev](https://redoan.dev)

## 🙏 Acknowledgments

- Classic Snake game by Nokia (1997)
- Modern web game development community
- Vanilla JavaScript enthusiasts

## 💖 Show Your Support

Give a ⭐️ if you enjoyed playing this game!

## 🎮 Play Online

[Live Demo](https://redoanuzzaman.github.io/Snakely---Classic-Snake-Game/) - Deploy and add your link here

---

Made with 🐍 and Vanilla JavaScript

**Last Updated:** October 2025
