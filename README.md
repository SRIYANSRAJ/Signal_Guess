# Signal Lock — Number Tracking Protocol

A modern, interactive number-guessing game with a sleek radar/signal-tracking aesthetic. Built with vanilla HTML, CSS, and JavaScript — no dependencies, no build step.

![Signal Lock](https://img.shields.io/badge/Status-Active-brightgreen) ![License](https://img.shields.io/badge/License-MIT-blue) ![Size](https://img.shields.io/badge/Size-~28KB-orange)

---

## 🎯 Overview

**Signal Lock** transforms the classic "guess the number" game into an immersive signal-tracking experience. Instead of simple "higher/lower" feedback, players get real-time proximity visualization, a color-coded signal-strength meter, and a detailed ping log of every attempt.

Perfect for:
- Quick brain teasers during breaks
- Learning number estimation skills
- UI/UX design reference for interactive games
- A foundation for educational number-guessing exercises

---

## ✨ Features

### Core Gameplay
- **4 Difficulty Levels**: Easy (1–100), Medium (1–1,000), Hard (1–10,000), Extreme (1–100,000)
- **Custom Range Mode**: Pick your own starting point and end point for completely personalized challenges
- **Unbiased Randomization**: Uses `crypto.getRandomValues()` with rejection sampling for cryptographically secure random numbers
- **Real-Time Feedback**: Signal strength meter, status labels (FREEZING → COLD → COOL → WARM → HOT → BURNING → LOCKED), and directional hints

### Visual Feedback
- **Color-Coded Meter**: Gradient from cold blue → amber → hot red based on guess proximity
- **Ping Log**: Scrollable history of all attempts with proximity percentage and direction
- **Direction Tag**: Animated "too low ↑ go higher" or "too high ↓ go lower" indicator
- **Win Screen**: Celebratory locked-ring animation with stats (attempts, range size, elapsed time)

### Dark & Light Mode
- **Auto-Detection**: Respects system color scheme preference on first load
- **Instant Toggle**: Smooth theme switch with animated toggle button
- **Full Coverage**: Every UI element adapts to the theme without harsh transitions

### UX Polish
- **Keyboard Support**: Press Enter to submit a guess
- **Input Validation**: Prevents invalid entries with visual shake feedback
- **Ordinal Counter**: Displays guesses as "1st attempt," "2nd attempt," "21st attempt" (correctly formatted)
- **Responsive Design**: Works seamlessly on desktop, tablet, and mobile
- **Accessibility**: Proper ARIA labels, focus states, and reduced-motion support
- **No Dependencies**: Single HTML file, runs anywhere

---

## 🚀 Getting Started

### Installation
No build step, no npm, no setup needed. Just download or clone:

```bash
git clone https://github.com/yourusername/signal-lock.git
cd signal-lock
```

### Usage
Open `signal-lock.html` directly in any modern web browser:
```bash
open signal-lock.html
# or
firefox signal-lock.html
# or drag the file into your browser
```

That's it. The game is ready to play.

---

## 🎮 How to Play

### Standard Mode
1. **Choose a difficulty** by clicking one of the four cards (Easy, Medium, Hard, Extreme)
2. **Click "Begin Tracking"** to start the game with a randomly selected target
3. **Enter your guess** in the input field and press Enter or click "Lock In"
4. **Watch the meter fill** — it shows your proximity to the target:
   - **FREEZING** (0–10%): Nowhere close
   - **COLD** (10–25%): Pretty far
   - **COOL** (25–45%): Getting warmer
   - **WARM** (45–65%): Close
   - **HOT** (65–85%): Very close
   - **BURNING** (85–97%): Extremely close
   - **LOCKED** (97–100%): You got it!
5. **Read the direction tag** — "TOO LOW ↑ go higher" or "TOO HIGH ↓ go lower"
6. **Check the ping log** — every guess is recorded with proximity and direction
7. **Win** when you find the exact number
8. **Play again** with the "Track Another Signal" button

### Custom Mode
1. **Toggle "Custom range"** to activate personalized settings
2. **Set the starting point** (default: 1) — can be any number
3. **Set the end point** (required) — must be greater than the start
4. **Click "Begin Tracking"** with your custom range
5. **Play as normal** — the game works exactly the same, just with your chosen range

#### Custom Range Examples
- **1 to 50**: Tight training range for quick games
- **100 to 500**: Mid-range challenge
- **0 to 10,000**: Extended exploration
- **1000 to 1100**: Laser-focused precision test

---

## 🎨 Design & Aesthetics

### Theme
**Signal Lock** uses a radar/military signal-tracking theme:
- Rotating radar icon in the header
- "Ping log" terminology instead of "guess history"
- "Signal strength" meter instead of "progress bar"
- Status labels inspired by radio signal quality (COLD, WARM, HOT, LOCKED)
- Color palette: cool blues (cold), warm ambers (medium), hot reds (close)

### Dark Mode
- Deep navy background (#080d18) with subtle grid pattern
- Teal accent (#5eead4) for interactive elements
- Precise contrast ratios for readability
- Smooth 500ms transitions when toggling

### Light Mode
- Soft gray background (#eef1f7) with grid texture
- Teal accent (#0f9488) adapted for light backgrounds
- Clean, minimal aesthetic with high contrast
- Responsive to the same transitions

### Typography
- **Display**: JetBrains Mono (monospace, all headings and numbers)
- **Body**: Manrope (humanist sans-serif, readable and friendly)
- Intentional type scale: 11px labels → 22px input → 30px win number

---

## 🔐 Technical Details

### Randomization
Instead of `Math.random()` (which is predictable for games), Signal Lock uses:
```javascript
crypto.getRandomValues() + rejection sampling
```
This ensures:
- **Unbiased**: Every number in the range has equal probability
- **Cryptographically secure**: Suitable for competitive scenarios
- **No patterns**: Truly random, not pseudo-random

### File Structure
- **Single HTML file** (~28KB): Everything embedded (HTML, CSS, JavaScript)
- **No external dependencies**: Works offline, no CDN required
- **Responsive CSS Grid**: Mobile-first layout that scales up
- **Vanilla JavaScript**: ES6+, no frameworks, ~500 lines total

### Browser Support
- ✅ Chrome/Chromium (90+)
- ✅ Firefox (88+)
- ✅ Safari (14+)
- ✅ Edge (90+)
- ✅ Mobile browsers (iOS Safari, Chrome Mobile)

**Note**: Requires `crypto.getRandomValues()` support (available in all modern browsers).

---

## 🎯 Gameplay Statistics

### Metrics Tracked
- **Attempts**: Total guesses to find the target
- **Range Size**: Total numbers in the playing range
- **Elapsed Time**: Seconds from start to completion
- **Proximity**: Real-time % closeness to target

### Algorithm Complexity
- **Best case** (lucky guess): 1 attempt, 0 seconds
- **Average case** (binary search-like): ~log₂(range) attempts
- **Worst case** (systematic trial): Range size attempts

---

## 🛠 Customization

### Adjusting Difficulty Levels
Edit the `data-min` and `data-max` attributes in the difficulty cards:
```html
<button class="diff-card" data-min="1" data-max="100">
  <div class="name">Easy</div>
  <div class="range">1 – 100</div>
</button>
```

### Changing Colors
Modify CSS variables in `:root[data-theme]`:
```css
--cold: #38bdf8;      /* Blue (far from target) */
--hot: #fb7185;       /* Red (close to target) */
--lock: #34d399;      /* Green (found it!) */
--accent: #5eead4;    /* Teal (interactive elements) */
```

### Adjusting Animations
Update timing in keyframes:
```css
@keyframes sweep { to { transform: rotate(360deg); } } /* Radar spin speed */
@keyframes pulseRing { /* Win screen ring animation */ }
@keyframes shimmer { /* Meter fill glow */ }
```

---

## 📱 Responsive Behavior

| Breakpoint | Layout |
|------------|--------|
| Desktop (420px+) | Full-width cards, 2-column difficulty grid, horizontal layout |
| Mobile (<420px) | Stacked layout, vertical difficulty grid, single-column guess row |
| Tablets | Optimized 1-column layout with scaled typography |

---

## ♿ Accessibility

- **Keyboard Navigation**: Tab through all controls, Enter to submit
- **Screen Reader Support**: ARIA labels on dynamic updates, proper heading hierarchy
- **Focus States**: All interactive elements have visible keyboard focus
- **Color Blind Friendly**: Doesn't rely solely on color (includes icons, patterns, and text)
- **Reduced Motion**: Respects `prefers-reduced-motion` media query, disables animations for users who request it
- **High Contrast**: WCAG AA compliant contrast ratios (4.5:1+)

---

## 🔧 Development

### Project Structure
```
signal-lock.html       # Everything in one file
├─ <head>              # Meta tags, fonts, styles
│  ├─ CSS Variables    # Theme system (light/dark)
│  ├─ Grid/Flexbox     # Responsive layout
│  └─ Animations       # Keyframes, transitions
└─ <body>              # HTML structure
   ├─ Header           # Logo, theme toggle
   ├─ Setup Panel      # Difficulty & custom range
   ├─ Game Panel       # Guess input, meter, log
   ├─ Win Panel        # Results screen
   ├─ Footer           # Credit to creator
   └─ <script>         # Game logic, state management
```

### State Management
The game maintains:
```javascript
{
  target: number,        // Random number to find
  min: number,           // Minimum of range
  max: number,           // Maximum of range
  attempts: number,      // Total guesses so far
  startTime: timestamp,  // When game started
  history: [             // Log of all guesses
    { guess, proximity, direction }
  ]
}
```

### Key Functions
- `randomInt(min, max)` — Cryptographically secure random integer
- `ordinal(n)` — Converts number to ordinal string (1 → "1st", 21 → "21st")
- `lerpColor(a, b, t)` — Interpolates between two hex colors
- `proximityColor(p)` — Returns color based on proximity %
- `statusLabel(p)` — Returns status name based on proximity %
- `submitGuess()` — Main game logic for processing a guess
- `finishGame()` — Displays win screen with stats

---

## 🎓 Learning Value

This project is useful for learning:
- **Vanilla JavaScript**: No frameworks, just clean ES6+ code
- **CSS Grid/Flexbox**: Responsive layout without Bootstrap
- **CSS Variables**: Theme switching without rewriting selectors
- **Animation**: Keyframes, transitions, and orchestration
- **State Management**: Single-file state handling
- **UX Design**: Micro-interactions, feedback loops, visual hierarchy
- **Accessibility**: ARIA, keyboard support, color contrast
- **Cryptography**: Real random number generation
- **Game Design**: Feedback systems, difficulty curves, win conditions

---

## 📄 License

MIT License — Use, modify, and distribute freely. See LICENSE file for details.

---

## 👨‍💻 Credits

**Built by**: Sriyans Raj  
**Version**: 2.0  
**Last Updated**: 2026  

Inspired by classic number-guessing games, reimagined with modern UI/UX principles and a signal-tracking aesthetic.

---

## 🚀 Future Enhancements

Potential features for future versions:
- 🎵 **Sound Effects**: Beeps for too-high/low, chime for win (optional, toggleable)
- 📊 **Leaderboard**: localStorage-based personal best tracking
- 💡 **Hints System**: "Is it odd or even?", "Is it greater than X?"
- ⏱️ **Time Attacks**: Win within a set time limit
- 🏆 **Achievements**: Unlock badges ("Got it in 1 guess!", "Found 100 numbers!")
- 🎮 **Multiplayer**: Competitive mode where players take turns guessing
- 📈 **Statistics**: Track average attempts, best time, games played
- 🔊 **Difficulty Curve**: Auto-adjust range based on performance

---

## 🐛 Known Issues & Workarounds

| Issue | Workaround |
|-------|-----------|
| Custom range > 100M numbers | Game remains responsive but randomization slower | Avoid ranges larger than this |
| Rapid clicks on submit | Button has debounce delay built-in | Just wait for feedback |
| Theme doesn't persist | Single-session file (no localStorage) | Refresh loads system preference again |

---

## 📧 Feedback & Contribution

Found a bug? Have a feature idea?  
- Open an issue with details
- Include browser version and reproduction steps
- Suggest improvements to code or UX

---

## 🎉 Play Now!

Download `signal-lock.html` and open in your browser. No installation, no setup—just instant fun.

**Start tracking signals. Find the number. Lock in. Repeat.**

---

*Signal Lock v2.0 — Built with precision, designed for delight.*
