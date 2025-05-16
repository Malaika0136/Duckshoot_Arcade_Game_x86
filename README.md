# DuckShoot Arcade Game (x86 Assembly - 8086)

DuckShoot is a classic arcade-style shooting game developed entirely in Intel 8086 Assembly Language using the `.asm` format. It runs in real mode via DOSBox and utilizes interrupt-based graphics (INT 10h) to display animated ducks, background objects, and interactive UI components such as a scoreboard, timer, and life counter.

Shoot as many ducks as possible before time or bullets run out!

---

##  Features

### 🎮 Two Game Modes

* **Mode 1 (Easy)** – One duck at a time with normal speed and unlimited bullets.
* **Mode 2 (Hard)** – Multiple ducks with faster movement and limited bullets.

###  Keyboard-Controlled Shooting

* You can move the duck up, right, left, down.
* To shoot you have to press enter.
* Ducks respond to shots using interrupt-driven mechanics.

###  Round Logic & Timer

* 3–4 game rounds.
* A countdown timer controls the pace of each round.

### 💾 File Handling

* Stores player names and high scores in a `.txt` file for persistent leaderboard tracking.

###  Graphics

Custom-drawn pixel art for:

* Ducks
* Grass
* Trees
* Bushes
* Title and logo

### ⏸ Pause & Resume Functionality

* Game can be paused and resumed mid-round.

###  Modular Architecture

Written across 4 modular `.asm` files:

* `nameinout.asm` – Takes username and manages score file.
* `mode.asm` – Provides mode selection screen.
* `resume.asm` – Handles game pause/resume functionality.
* `game.asm` – Core gameplay logic and visuals.

---

##  File Structure

```
DuckShoot/
 ┣ 📄 game.asm         # Main game logic (rendering, duck animation, backgrounds)
 ┣ 📄 nameinput.asm    # User input and file I/O for player scores
 ┣ 📄 mode.asm         # Mode selection logic (Easy / Hard)
 ┣ 📄 resume.asm       # Pause and resume implementation
 ┣ 📄 SCORES.txt       # (Generated) Stores names and high scores
 ┣ 📄 README.md        # Game documentation
```

---

##  How It Works

### Game Flow

#### Startup

* Game loads into video mode 13h (320x200, 256 colors).
* Displays `title_logo` and welcome screen.
* Prompts player for their name.

#### Mode Selection

* `mode.asm` allows player to choose between Easy or Hard.

#### Gameplay

* `game_page` (in `game.asm`) sets up graphics:

  * Sky background
  * Duck sprite
  * Ground with grass and bushes
  * Scoreboard and lives
* Ducks are drawn with `draw` procedure using pixel-by-pixel rendering (INT 10h, AH=0Ch).
* Ducks fly across the screen; player must shoot them before timer/lives run out.

#### Pause / Resume

* `resume.asm` allows pausing the game mid-round.

#### Score Tracking

* At the end of a game, scores are written to `SCORES.txt` using file I/O in `nameinput.asm`.

---

##  Technical Highlights

| Feature      | Implementation                                     |
| ------------ | -------------------------------------------------- |
| Graphics     | INT 10h - Mode 13h, pixel draw via AH=0Ch          |
| Video Memory | No direct access – uses BIOS interrupts            |
| User Input   | Handled via keyboard/cursor (via interrupts)       |
| File I/O     | INT 21h DOS file services (open/write/read)        |
| Modular Code | Procedures used for draw, mode selection, file I/O |
| Game Data    | Stored as byte arrays (e.g., duck, bush, grass)    |

---

##  How to Run (DOSBox)

 **Ensure all `.asm` files are assembled and linked.**

### Step 1: Assemble using MASM

```bash
masm nameinout.asm;
masm resume.asm;
masm mode.asm;
masm game.asm;
```

### Step 2: Link using LINK (MASM default linker)

```bash
link game.obj + nameinout.obj + resume.obj + mode.obj;
```

### Step 3: Run in DOSBox

```bash
mount c .
c:
game.exe
```

---



## 📊 Scoring System

* +1 Point per Duck Hit
* Score shown in real-time on the scoreboard.
* Final high score saved to `SCORES.txt` alongside player's name.

---

##  Bonus Features

*  Title and intro screens styled with pixel logos
*  Creativity in scene layout (grass, trees, ducks, moving objects)
*  Persistent Score Saving

---

##  Author

* **Project By:** Malaika Nasir
* **Platform:** x86 Assembly Language (MASM)
* **Environment:** DOSBox Emulator

---

## License

This project is academic and non-commercial. All graphics and code are handcrafted for educational purposes only.
