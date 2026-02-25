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
- **Single file app:** Everything in `index.html` (~3000+ lines)
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
  index.html             - THE ENTIRE GAME (~3000+ lines: CSS + HTML + JS)
  scores.html            - "Ezrolith Arcade" combined leaderboard page (HannaPig + SpacePigs)
  manifest.json          - PWA manifest
  sw.js                  - Service worker (network-first strategy)
```

### Game Features
- **Phone brand:** "SPACE PIGS" displayed at top of device
- **Pig ship** (player) with ears-as-antenna, snout cockpit, eye shine — drawn on canvas
- **3 enemy types:** Wolves (top rows, 30pts, grey with red eyes), Foxes (mid rows, 20pts, orange), Farmers (bottom rows, 10pts, hat + angry eyebrows)
- **4 bosses** cycling every N waves: PEPSI → CHERRY → HARRY → JAKE
  - **Pepsi** (black cat, lime green eyes) — slit pupils, whiskers, fangs
  - **Cherry** (white cat, cyan eyes) — same cat style, lighter palette
  - **Harry** (black cat, orange eyes) — like Pepsi with different eye colour
  - **Jake** (friendly black dog) — floppy ears, round eyes, tongue out, wagging tail
- **Boss special attacks** with taunts (text appears before attack):
  - Cherry: "CLAW!" (diagonal bullet lines + scratch marks), "HISSS!" (mirrored claw), "GOTCHA!" (targeted burst)
  - Pepsi/Harry: "PURRRR..." (expanding sonic rings with gaps), "NAP TIME..." (sleep cloud), "MEOW!" (circle burst)
  - Jake: "JUMP!" (paw prints rain down + shockwave), "FETCH!" (bouncy balls off walls), "WOOF!" (bark shockwave arc)
- **Specials trigger** every 6-9 seconds + at HP thresholds (75%/50%/25%)
- **Destructible shields** (cyan energy style, 3x3 grid, 3 HP per cell, pulsing glow)
- **5 power-ups** (10% drop from killed enemies):
  - Truffle Shot: triple spread fire (8s)
  - Mud Shield: absorbs all hits (3s)
  - Oink Bomb: instant screen-clear + 5 boss damage
  - Speed Trot: 1.5x movement speed (10s)
  - Extra Life Mushroom: grants +1 life, capped at starting+1 (~6% of drops, red & white toadstool)
- **Giant Pig bonus event** (ultra-rare, wave 3+): golden crowned pig bounces around screen for 5 seconds, takes 8 hits to destroy. If destroyed, activates **Super Pig Mode** (15s invulnerability + 500% fire rate + spread shot + golden visual effects). If missed, it escapes.
- **Summon Super Pig button:** spend 100 credits during gameplay to manually activate Super Pig Mode — player ship grows 5x, invulnerable, 500% fire rate, spread shot. Gold button below controls. Once per round only; duration scales by wave (8s at waves 1-5, -1s per 5 waves, min 4s). Natural Giant Pig (15s) unaffected by these limits.
- **Permanent upgrades shop** (start screen): Extra Life (+1 starting life, 250 credits, non-stackable) and Attack Speed (+10% fire rate per level, stackable 3x for 30%, 250 credits each). Stored in Firestore `users` doc `upgrades` field, persist forever.
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
- **Player bullets:** acorn-shaped projectiles with golden glow + trail (max 3 on screen)
- **Enemy bullets:** pitchfork-shaped with red-orange glow + trail; special types: paw prints (Jake), bouncy balls (Jake), sleep clouds (Pepsi/Harry)
- **3-layer parallax background:** distant dim stars, drifting nebula clouds (purple/blue/pink), bright twinkling foreground stars (multi-coloured)
- **Colour-coded flash messages:** per enemy type, per power-up, cyan wave banners, red boss warnings
- **Death effects:** white+red flash, expanding colour rings on enemy death, boss hit flash
- **Power-up screen-edge glow:** coloured border glow when timed power active

### Version
Current version: **v1.14** (shown in screen footer + sw.js cache name)
