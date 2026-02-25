# ⭕ Perfect Circle

> **Can you draw a perfect circle by hand?**
> Draw one stroke, release, and find out instantly — scored on circularity, symmetry, and closure.

**Created and owned by [Anthroberc](https://x.com/anthroberc)**

> ⚠️ **This is exclusive property of Anthroberc. Not licensed for personal or commercial use. All rights reserved.**

---

## 📖 Table of Contents

- [What is Perfect Circle?](#what-is-perfect-circle)
- [How to Use It](#how-to-use-it)
- [Understanding Your Score](#understanding-your-score)
- [How the Scoring Works (Under the Hood)](#how-the-scoring-works-under-the-hood)
- [UI Breakdown](#ui-breakdown)
- [Tips to Score Higher](#tips-to-score-higher)
- [Running the File Locally](#running-the-file-locally)
- [Technical Details](#technical-details)
- [License](#license)
- [Credits](#credits)

---

## What is Perfect Circle?

Perfect Circle is a **single-file web app** that challenges you to draw the most perfect circle you can — using just your mouse or finger. The moment you lift your finger or release the mouse, it scores your circle from **0.0% to 99.9%** based on how geometrically accurate it is.

It's inspired by the classic "can you draw a perfect circle?" challenge. It works on **desktop** (mouse) and **mobile** (touch), requires no internet connection after the page loads, and has no ads, accounts, or downloads.

---

## How to Use It

Using Perfect Circle is as simple as it gets. Here's a step-by-step:

**Step 1 — Open the file**
Open `index.html` in your browser (Chrome, Firefox, Safari, Edge all work).

**Step 2 — Draw your circle**
Click and hold (or press and hold on mobile), then drag to draw a circle shape anywhere on the screen. The app will trace your stroke in real time.

**Step 3 — Release to score**
Let go of the mouse button (or lift your finger). The app instantly calculates your score and displays it in large text at the center of the screen.

**Step 4 — Try again**
Just click/tap anywhere on the screen to start a new stroke. Your previous drawing clears and you can go again.

> ⚠️ **Important:** You must draw in **one continuous stroke**. Lifting midway and restarting counts as a new drawing.

---

## Understanding Your Score

Your score is shown as a percentage — the closer to **99.9%**, the more perfect your circle.

| Score | Rating | What it means |
|-------|--------|---------------|
| 95% – 99.9% | ⭐ Extraordinary | Near-perfect. Extremely rare. |
| 88% – 94.9% | ✅ Excellent | Very circular. Great job. |
| 75% – 87.9% | 👍 Great Shape | Solid circle, minor wobbles. |
| 55% – 74.9% | 🟡 Getting There | Recognizable but imperfect. |
| 30% – 54.9% | 🔴 Keep Practicing | Noticeable irregularities. |
| 0% – 29.9% | ❌ Not a Circle | Might be a square or squiggle. |

### The Streak Counter
The bottom-left shows your **Streak** — how many circles in a row you've scored **80% or higher**. It resets to 0 the moment you score below 80%.

### The Best Score
The top-right corner tracks your **personal best** for the current session. It updates every time you beat your previous high score. (Resets when you refresh the page.)

### The Score Ring
After you draw, a faint circular ring appears around your drawing. This is a **radial accuracy meter** — it animates and fills based on your score, giving you a visual sense of how circular your stroke was.

---

## How the Scoring Works (Under the Hood)

Don't worry if math isn't your thing — here's a plain-English breakdown of how the app decides your score.

### 1. Finding the Center
The app first calculates the **centroid** of all the points you drew — basically the average position of every dot in your stroke. This becomes the "center" of your attempted circle.

### 2. Measuring Radial Consistency
From that center, it measures the distance to every point you drew. In a perfect circle, **all those distances would be identical**. The app measures how much each distance deviates from the average — this is called **Mean Absolute Deviation (MAD)**. The smaller the deviation, the better.

### 3. Checking the Shape (Aspect Ratio)
It looks at the bounding box of your drawing — the smallest rectangle that fits around it. A perfect circle's bounding box is a **square** (equal width and height). If your shape is more like an oval or egg, you get penalized.

### 4. Checking Closure (Did You Close the Loop?)
The app measures the gap between where you **started** drawing and where you **ended**. A perfect circle loops back to the start. The bigger the gap, the bigger the penalty.

### 5. Checking Angular Coverage (Did You Go All the Way Around?)
It checks that your stroke actually sweeps through a **full 360 degrees**. If you only drew a three-quarter circle or a curved line, you'll lose significant points.

### 6. Final Score Calculation
All the penalties are combined:

```
Score = 100
  − (radial deviation penalty)
  − (oval/aspect ratio penalty)
  − (loop closure penalty)
  − (incomplete rotation penalty)
```

If your radial deviation is extremely high (like a square or scribble), the score is hard-capped at **15%** regardless.

The final score is clamped between **0.0%** and **99.9%** — it can never reach 100%, because perfection is impossible.

---

## UI Breakdown

Here's what everything on the screen means:

```
┌─────────────────────────────────────────┐
│  App                          Best       │  ← Top bar
│  Perfect Circle               —          │
│                                          │
│                                          │
│              87.3%                       │  ← Your score (giant text)
│           GREAT SHAPE                    │  ← Status label                  
│                                          │
│                                          │
│  Streak                  One continuous  │  ← Bottom bar
│  3                       Release to score│
│                                          │
│       Powered by Anthroberc              │  ← Footer
└─────────────────────────────────────────┘
```

| Element | Location | Description |
|---------|----------|-------------|
| **App title** | Top left | The app name |
| **Best** | Top right | Your highest score this session |
| **Score** | Center | Your latest circle accuracy percentage |
| **Status** | Below score | A word rating (Excellent, Great Shape, etc.) |
| **Score ring** | Behind score | SVG ring that fills to match your score |
| **Streak** | Bottom left | Consecutive 80%+ circles in a row |
| **Hint** | Bottom right | Reminder of how to draw |
| **Footer** | Very bottom | Credit link to Anthroberc |

---

## Tips to Score Higher

Getting a high score is harder than it looks. Here are some tips:

- **Go slow.** Rushing makes your hand shake and creates wobbly edges.
- **Use your whole arm**, not just your wrist. Bigger circles made with arm movement tend to be more consistent.
- **Draw a medium-large circle.** Tiny circles are harder to control; huge ones leave more room for error.
- **Close the loop.** Try to end your stroke exactly where you started — the closure penalty is significant.
- **Stay on the same radius.** The most common mistake is drifting inward or outward partway through.
- **On mobile**, use a single finger and draw slowly and deliberately.
- **Breathe out** as you draw — seriously, it steadies your hand.

---

## Running the File Locally

The app is entirely self-contained in one HTML file. To run it:

**Option 1 — Just double-click it**
Find `index.html` in your file explorer and double-click. It will open in your default browser.

**Option 2 — Drag into browser**
Open your browser and drag the file into the browser window.

**Option 3 — Via terminal**
```bash
# Mac
open index.html

# Windows
start index.html

# Linux
xdg-open index.html
```

> 💡 You need an internet connection the first time to load the fonts (Bebas Neue + DM Mono from Google Fonts). After that it works fully offline.

---

## Technical Details

| Property | Value |
|----------|-------|
| **File name** | `index.html` |
| **File type** | Single HTML file |
| **File size** | ~11 KB (minified) |
| **Dependencies** | Google Fonts (Bebas Neue, DM Mono) |
| **Frameworks** | None — vanilla HTML, CSS, JavaScript |
| **Canvas API** | Used for real-time stroke rendering |
| **Input handling** | Pointer Events API (works for mouse + touch + stylus) |
| **DPR support** | Yes — crisp on Retina / HiDPI screens |
| **Browsers** | Chrome, Firefox, Safari, Edge (all modern versions) |
| **Mobile** | Yes — iOS Safari, Android Chrome |
| **Data stored** | Nothing — no cookies, no localStorage, no tracking |

### Why is the code on one line?
The source code is **minified** — all whitespace and line breaks have been removed. This makes the file slightly smaller and harder to casually copy. The app functions identically to a readable version.

---

## License

**© Anthroberc. All rights reserved.**

This project is the **exclusive property of [Anthroberc](https://x.com/anthroberc)**.

- ❌ You may **not** use, copy, modify, or distribute this project for **personal use**
- ❌ You may **not** use, copy, modify, or distribute this project for **commercial use**
- ❌ You may **not** host, republish, or claim ownership of this project
- ❌ No license is granted to any individual or organization

Any unauthorized use is strictly prohibited.

---

## Credits

**Created and owned by [Anthroberc](https://x.com/anthroberc)**

Follow on X: [@anthroberc](https://x.com/anthroberc)

---

*Perfect Circle — because 99.9% is as close as you'll ever get.*
