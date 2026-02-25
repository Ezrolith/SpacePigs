# Claude Project Knowledge

## Workflow Rules
- **ALWAYS bump the version number** in both the game (`index.html` footer) AND CLAUDE.md before pushing changes
- **ALWAYS commit to GitHub AND deploy to Firebase** after changes — they must stay in sync
- **GitHub is the source of truth** — pull/clone fresh when starting a new session
- **Deploy command** must set PATH first (see below)

## SpacePigs - Pig-Themed Space Invaders Game

### What It Is
A pig-themed Space Invaders game, built as a single-page web app (PWA). Styled to look like a retro "SPACE PIGS" branded phone device. Companion game to HannaPig. Created by Ezrolith.

### GitHub Access
- **Repo:** https://github.com/Ezrolith/SpacePigs
- **GitHub CLI:** installed at `"C:\Program Files\GitHub CLI\gh.exe"`, authenticated as **Ezrolith**
- **Clone:** `"/c/Program Files/GitHub CLI/gh.exe" repo clone Ezrolith/SpacePigs`
- **View:** `"/c/Program Files/GitHub CLI/gh.exe" repo view Ezrolith/SpacePigs`

### Firebase Hosting & Deployment
- **Live URL:** https://spacepigs-game.web.app
- **Firebase Project ID:** `spacepigs-game`
- **Firebase CI Token:** stored locally (see root CLAUDE.md — not committed to repo)
- **Node.js:** `C:\Program Files\nodejs`
- **Firebase CLI:** `C:\Users\Peter\AppData\Roaming\npm`
- **Deploy command:** See root `C:\Users\Peter\CLAUDE.md` for full command with token
- **Deploy rules/indexes:** Remove `--only hosting` to deploy Firestore rules + indexes too

### Local Copy
- **Working repo:** `D:\Claude Visual Studio\SpacePigs\`

### Tech Stack
- **Single file app:** Everything in `index.html` (~2500 lines)
- **Vanilla HTML/CSS/JS** — no frameworks, no build step
- **Firebase Firestore** for leaderboard (per-difficulty)
- **PWA:** `manifest.json` + `sw.js` for offline/installable support
- **Hosted on Firebase Hosting**

### File Structure
```
SpacePigs/
  firebase.json          - Firebase hosting + Firestore config
  firestore.rules        - Firestore security rules (validates name, score, wave, difficulty, ts)
  firestore.indexes.json - Composite index: difficulty + score desc
  icon.svg               - App icon (pig themed)
  index.html             - THE ENTIRE GAME (~2500 lines: CSS + HTML + JS)
  manifest.json          - PWA manifest
  sw.js                  - Service worker (network-first strategy)
```

### Game Features
- **Phone brand:** "SPACE PIGS" displayed at top of device
- **Pig ship** (player) with ears-as-antenna, snout cockpit, eye shine — drawn on canvas
- **3 enemy types:** Wolves (top rows, 30pts, grey with red eyes), Foxes (mid rows, 20pts, orange), Farmers (bottom rows, 10pts, hat + angry eyebrows)
- **Boss waves** every N waves: cats named **Pepsi** (black cat, green eyes) and **Cherry** (white cat, blue eyes) that alternate — HP bar, spread-shot, slit pupils, whiskers, fangs
- **Destructible shields** (mud-pile style, 3x3 grid, 3 HP per cell)
- **4 power-ups** (10% drop from killed enemies):
  - Truffle Shot: triple spread fire (8s)
  - Mud Shield: absorbs all hits (3s)
  - Oink Bomb: instant screen-clear + 5 boss damage
  - Speed Trot: 1.5x movement speed (10s)
- **Wave system** with increasing difficulty (faster enemies, faster shooting)
- **3 difficulty levels:** Easy (4 lives, 3x5 grid, boss every 5), Normal (3 lives, 4x5, boss every 5), Hard (2 lives, 5x5, boss every 3)
- **Per-difficulty high scores:** stored in localStorage as `spacePigsHighScore_easy/normal/hard`
- **Per-difficulty Firestore leaderboard:** scores include `difficulty` + `wave` fields
- **All Champs display:** start screen shows #1 pilot for all 3 difficulties
- **Live target during gameplay:** current leader shown in screen header
- **"NEW TOP PIG!" banner:** golden flash with particles when you overtake the leader mid-game
- **Per-difficulty music** (procedural Web Audio API):
  - Easy: "Piglet's Patrol" — 90 BPM, gentle bouncy march (square lead, triangle bass)
  - Normal: "Hog Squadron" — 130 BPM, energetic driving march (square lead, sawtooth bass)
  - Hard: "The Last Sow" — 160 BPM, intense urgent minor key (sawtooth lead, driving bass)
- **Sound effects:** pew laser, enemy pop (noise burst + squeal), player hit, power-up arpeggio, boss appear (sawtooth rumble), boss explode (filtered noise), wave complete fanfare, game over descending notes
- **Screen shake** on player hit + red flash overlay
- **Touch controls:** drag on canvas to move + auto-fire, plus button strip (Left/Fire/Right)
- **Keyboard controls:** Arrow keys / WASD + Space to fire + P to pause
- **Fullscreen support**
- **Player bullets:** acorn-shaped projectiles (max 3 on screen)
- **Enemy bullets:** pitchfork-shaped projectiles
- **Starfield background** (seeded, static)

### Version
Current version: **v1.6** (shown in screen footer + sw.js cache name)
