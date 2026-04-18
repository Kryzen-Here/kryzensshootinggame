# 🎮 Stickman FPS 3D — Ultimate Edition

A fully featured browser-based 3D First-Person Shooter built with **Three.js**, playable on both **PC and Mobile** browsers. No downloads, no installs — just open `index.html` and play!

---

## 📋 Table of Contents

- [Features](#features)
- [How to Play](#how-to-play)
- [Controls](#controls)
- [Weapons](#weapons)
- [Game Systems](#game-systems)
- [Enemy AI](#enemy-ai)
- [Leaderboard & Name System](#leaderboard--name-system)
- [Technical Stack](#technical-stack)
- [Installation](#installation)
- [Browser Compatibility](#browser-compatibility)
- [Known Issues](#known-issues)
- [Credits](#credits)

---

## ✨ Features

### 🎯 Core Gameplay
- Full 3D First-Person Shooter experience in a single HTML file
- Wave-based survival — enemies get harder every round
- 3 unique weapons with distinct playstyles
- Slide, sprint, and jump mechanics
- Health system with screen flash on damage
- Auto-reload when magazine is empty

### 🧠 Advanced Enemy AI
- 7 distinct AI states: Approach, Flank, Strafe, Rush, Retreat, Attack, Dodge
- Enemies dodge when shot at
- Enemies retreat when low on health
- Enemies rush at the player unpredictably
- Crowd avoidance — enemies don't stack on each other
- Health bars above each enemy that face the camera
- Scales in difficulty each wave

### 🔫 3 Unique Weapons
- **AK-47** — Full-auto rifle with heavy recoil
- **Glock-18** — Semi-auto pistol, fast reload
- **Karambit** — Melee knife, one-hit heavy damage

### 🏆 Leaderboard System
- Persistent leaderboard saved to browser localStorage
- Top 20 scores tracked with name, kills, wave, and date
- 🥇🥈🥉 Medal system for top 3
- Rank announcement on game over
- Clear leaderboard option

### 👤 Player Name System
- Custom player name input on main menu
- Name saved between sessions via localStorage
- Name displayed in HUD during gameplay

### 📱 Full Mobile Support
- Virtual joystick for movement
- Touch look zone for aiming
- On-screen buttons: FIRE, RELOAD, JUMP, SLIDE, SPRINT, SWITCH
- Responsive layout for all screen sizes

### 🎚️ Sensitivity System
- Separate X and Y sensitivity sliders
- Adjustable from the main menu and in-game settings panel
- Settings sync between both panels in real time

### 🗺️ Minimap
- Live minimap in the top-left corner
- Player arrow rotates with your view direction
- Enemy dots color-coded by AI state:
  - 🔴 Red — Normal
  - 🔥 Bright Red — Rushing
  - 🟠 Orange — Retreating
- Building markers shown on minimap

### 🌍 3D Environment
- Fully 3D world with buildings, crates, barrels, and street lamps
- Dynamic vertex-displaced terrain
- Animated moon and stars
- Atmospheric fog and night sky shader
- Blood pools that stay on the ground
- Bullet trail effects
- Muzzle flash with dynamic point light

### 🔊 Synthesized Audio
- All sounds generated in real-time using the Web Audio API
- No external audio files required
- Unique sounds for: AK shoot, Glock shoot, Knife slash, Reload, Footsteps, Slide, Hit, Kill, Hurt, Empty mag

---

## 🚀 How to Play

1. Open `index.html` in any modern browser
2. Enter your player name
3. Adjust sensitivity if needed
4. Click **START GAME**
5. On PC: Click the screen to lock your mouse pointer
6. Survive as many waves as possible
7. When you die, your score is saved to the leaderboard
8. Click **PLAY AGAIN** to retry or **MAIN MENU** to go back

---

## 🎮 Controls

### PC Controls

| Key / Input | Action |
|-------------|--------|
| `W` `A` `S` `D` | Move |
| `SHIFT` | Sprint |
| `SPACE` | Jump |
| `C` | Slide (while moving) |
| `Mouse Move` | Aim / Look |
| `Left Click` | Shoot / Slash |
| `R` | Reload |
| `Q` | Cycle to next weapon |
| `1` | Switch to AK-47 |
| `2` | Switch to Glock-18 |
| `3` | Switch to Karambit |
| `ESC` | Release mouse pointer |

### Mobile Controls

| Button | Action |
|--------|--------|
| Left Joystick | Move |
| Right Touch Zone | Look / Aim |
| `FIRE` | Shoot / Slash |
| `RELOAD` | Reload weapon |
| `JUMP` | Jump |
| `RUN` | Toggle sprint |
| `SLIDE` | Slide |
| `SWITCH` | Cycle weapon |

---

## 🔫 Weapons

### AK-47
- **Type:** Automatic Rifle
- **Magazine:** 30 rounds
- **Fire Rate:** Fast (auto)
- **Damage:** 25 per bullet
- **Reload Time:** 2 seconds
- **Range:** Long
- **Recoil:** High
- **Best For:** Sustained fire, clearing groups

### Glock-18
- **Type:** Semi-Automatic Pistol
- **Magazine:** 15 rounds
- **Fire Rate:** Medium (semi-auto)
- **Damage:** 20 per bullet
- **Reload Time:** 1.5 seconds
- **Range:** Medium
- **Recoil:** Low
- **Best For:** Precision shots, conserving ammo

### Karambit
- **Type:** Melee Knife
- **Ammo:** Unlimited
- **Attack Rate:** Moderate
- **Damage:** 55 per slash
- **Reload Time:** None
- **Range:** Very short (melee only)
- **Recoil:** None
- **Best For:** Close quarters, saving ammo, silent kills

---

## ⚙️ Game Systems

### Wave System
- Each wave spawns a set number of enemies
- Enemies per wave increases with each round: `5 + wave × 3`
- Between waves, you receive **+25 HP** (up to max)
- Enemy speed, health, and damage scale each wave
- Maximum 15 enemies active at once

### Health System
- Player starts with 100 HP
- Screen flashes red when taking damage
- Red vignette damage overlay effect
- Health bar changes color: Green → Yellow → Red
- Death triggers game over and leaderboard save

### Slide Mechanic
- Press `C` (PC) or `SLIDE` (mobile) while moving
- Camera drops low for a fast ground slide
- Weapon tilts during slide animation
- 1.2 second cooldown between slides
- Great for dodging enemy attacks

### View Bobbing
- Camera bobs when walking or running
- Sprint increases bob intensity
- Weapon model sways with movement

### Camera Shake & Recoil
- Each shot applies recoil to the camera
- Camera shakes on taking damage
- Recoil gradually recovers after shooting
- AK has strongest recoil, Glock lighter, Knife has none

---

## 🤖 Enemy AI

Enemies use a **state machine** with 7 states:

| State | Behaviour |
|-------|-----------|
| **Approach** | Walk directly toward the player's last known position |
| **Flank** | Circle around to attack from the player's side |
| **Strafe** | Sidestep while slowly closing the distance |
| **Rush** | Sprint at 1.8× speed directly at the player |
| **Retreat** | Run away when HP drops below 30% |
| **Attack** | Melee the player when within close range |
| **Dodge** | Quick lateral dodge when shot (35% chance) |

### AI Reactions to Damage
- **35% chance** to dodge sideways when hit
- **50% chance** to retreat when below 40% HP
- **30% chance** to rage-rush at the player when hit
- Enemies become more aggressive on higher waves

---

## 🏆 Leaderboard & Name System

### Player Name
- Entered on the main menu before starting
- Saved automatically to `localStorage`
- Remembered on your next visit
- Displayed in the HUD during gameplay
- Shown on the game over screen

### Leaderboard
- Automatically saves your score when you die
- Stores up to **20 entries** in `localStorage`
- Sorted by **kills** (wave used as tiebreaker)
- Visible on both the **main menu** and **game over screen**
- Shows: Rank, Name, Kills, Wave, Date

### Ranking Rewards
| Rank | Display |
|------|---------|
| 1st | 🥇 NEW HIGH SCORE! |
| 2nd | 🥈 2nd Place! |
| 3rd | 🥉 3rd Place! |
| 4th–10th | Top 10! Rank #N |
| 11th+ | Rank #N |

### Clearing the Leaderboard
- Click **"Clear Leaderboard"** on the main menu
- A confirmation dialog will appear before clearing

---

## 🛠️ Technical Stack

| Technology | Usage |
|------------|-------|
| **HTML5** | Structure and layout |
| **CSS3** | UI styling, animations, mobile layout |
| **JavaScript (ES5/ES6)** | Game logic, AI, controls |
| **Three.js r128** | 3D rendering engine |
| **Web Audio API** | Procedural sound generation |
| **localStorage** | Leaderboard and name persistence |
| **Pointer Lock API** | PC mouse control |
| **Touch Events API** | Mobile controls |

### Architecture
- Single `index.html` file — no build tools, no dependencies to install
- Three.js loaded via CDN
- All assets generated procedurally (no image or audio files)
- IIFE-wrapped JavaScript to prevent global scope pollution

---

## 📦 Installation

### Option 1 — Direct Open
```bash
# Just double-click index.html
# Or drag it into your browser
