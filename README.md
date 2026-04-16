# PONG — P2P Multiplayer

A browser-based 1v1 Pong game using WebRTC P2P networking via **PeerJS**.

## 🎮 How to Play

1. Both players open `index.html` in a browser
2. **Player 1 (Host):** Enter your name → enter a room name → click **CREATE ROOM**
3. **Player 2 (Guest):** Enter your name → enter the same room name → click **JOIN ROOM**
4. Game starts automatically when both are connected!

**Controls:**
- `W` / `S` or `↑` / `↓` — move paddle
- Mobile: drag up/down on the canvas

**Win condition:** First to 7 points wins.

---

## 🌐 Networking Modes

### Cross-Device (Internet) — PeerJS Cloud
The game automatically loads PeerJS from CDN and uses the **PeerJS free cloud server** for WebRTC signaling. This lets players on **different computers / networks** play together. No server setup needed.

> ⚠️ PeerJS free tier has connection limits. For production, host your own PeerJS server or use [PeerServer Cloud](https://peerjs.com/peerserver.html).

### Same Device / Same Tab — BroadcastChannel fallback
If PeerJS fails to load, the game falls back to `BroadcastChannel` which only works within the same browser (useful for testing).

---

## 🚀 Deploy to GitHub Pages

```bash
# 1. Create a new repo on GitHub
# 2. Add index.html to the repo
git init
git add index.html README.md
git commit -m "Initial commit"
git remote add origin https://github.com/YOUR_USERNAME/YOUR_REPO.git
git push -u origin main

# 3. Go to repo Settings → Pages → Source: main branch → Save
# Your game will be live at: https://YOUR_USERNAME.github.io/YOUR_REPO/
```

Players can then share the GitHub Pages URL and just agree on a room name!

---

## 🏗️ Architecture

```
HOST (Player 1)              GUEST (Player 2)
──────────────               ───────────────
Creates PeerJS ID            Connects to Host's PeerJS ID
Runs ball physics            Receives ball state from Host
Sends: ball pos/vel          Sends: paddle position
       paddle pos                   paddle position
       score updates
```

- **Host** is authoritative for ball position and scoring
- Both players send their paddle Y position to each other in real-time
- ~60fps game loop with RequestAnimationFrame

---

## 🔧 Customization

Edit the constants at the top of the `<script>` tag in `index.html`:

```js
const SCORE_WIN = 7;       // Points to win
const BALL_SPEED_INIT = 5; // Starting ball speed
const PADDLE_H = 80;       // Paddle height
```
