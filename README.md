# GEO-SHOOTER: Battle Arena

A multiplayer battle arena where players use their **smartphones as motion controllers** (gyroscope/accelerometer) to navigate and fight on a central PC screen via WebSockets.

> 📄 Academic project for *Web Technologies* — FEUP, University of Porto (Jan 2026)

docs/demo_video_g05.mov

> ⬆️ Replace this line with your demo video: edit the README on GitHub, drag & drop `demo.mp4`, and GitHub will generate the embed link automatically.

---

## How It Works

1. **PC** runs the game server and displays the arena on screen
2. **Players** scan a QR code to open the controller on their phones
3. **Tilt your phone** to move, tap to shoot and use abilities
4. All communication happens over **WebSockets** on the local Wi-Fi network
5. HTTPS is required for mobile motion sensor access

---

## Features

- **5 Character Classes** — Tank (Shield), Sniper (Pierce), Runner (Dash), Balanced (Heal), Assault (Bullet Storm), each with unique stats and abilities
- **6 Dynamic Maps** — Training Ground, Classic Arena, Urban Warfare, Crossfire, The Pit, Death Zone — featuring hazards like toxic zones, moving walls, and gravity anomalies
- **Motion Calibration** — per-axis sensitivity tuning and axis inversion for any device orientation
- **Room-based Matchmaking** — multiple games can run simultaneously
- **Immersive Audio** — background music and SFX for gunfire, power-ups, and respawns

---

## Tech Stack

| Layer | Technology |
|-------|-----------|
| Backend | Node.js, Express |
| Communication | WebSockets (`ws`) — low-latency input and game state sync |
| Frontend | HTML5 Canvas, Vanilla JavaScript, CSS3 |
| Libraries | Chart.js (controller UI), qrcode.min.js (QR join codes) |

---

## Project Structure

```
geo-shooter/
├── server.js                  # Node.js backend (HTTPS + WebSocket)
├── package.json
├── public/
│   ├── landing.html           # Entry point (CRT power-on effect)
│   ├── game.html              # Game arena (PC screen)
│   ├── controller.html        # Mobile controller interface
│   ├── scripts/
│   │   ├── landing.js         # Landing page animations & audio
│   │   ├── game.js            # Game engine, physics, rendering
│   │   └── controller.js      # Motion sensing, calibration, input
│   ├── styles/
│   │   ├── landing.css
│   │   ├── game.css
│   │   └── controller.css
│   ├── fonts/
│   │   └── LostEntity-8OmW2.otf
│   ├── vendor/
│   │   └── qrcode.min.js
│   └── sounds/                # Audio files (.mp3)
├── docs/
│   └── demo.mp4               # Gameplay demo video
└── README.md
```

---

## Getting Started

### Prerequisites

- Node.js (v14+)
- PC and phones on the **same Wi-Fi network**

### Installation

```bash
git clone https://github.com/paolopasca/geo-shooter.git
cd geo-shooter
npm install
```

### Generate SSL Certificates

Mobile browsers require HTTPS for motion sensor access. Generate self-signed certificates:

```bash
mkdir -p certs

# Find your local IP
# macOS: ipconfig getifaddr en0
# Linux: hostname -I

openssl req -x509 -newkey rsa:2048 -nodes \
  -keyout certs/key.pem \
  -out certs/cert.pem \
  -days 365 \
  -subj "/CN=YOUR-LOCAL-IP"
```

Replace `YOUR-LOCAL-IP` with your actual IP (e.g., `192.168.1.25`).

### Run

```bash
node server.js
```

The server starts on `https://localhost:8443`. Open it on the PC, then scan the QR code with your phone to join.

---

## How to Play

1. **PC** — open `https://<YOUR-IP>:8443`, create a room
2. **Phone** — scan the QR code or visit `https://<YOUR-IP>:8443/phone`
3. **Join** the same Room ID on both devices
4. **Select** your character on the phone
5. **Calibrate** your phone's motion sensors
6. **Tilt** to move, tap **FIRE** to shoot, tap **ABILITY** for your special power

---

## Troubleshooting (iOS)

- Motion sensors are **blocked on HTTP** — always use HTTPS
- Accept the self-signed certificate warning when it appears
- Ensure "Motion & Orientation Access" is enabled in Safari settings

---

## Authors

- **Paolo Pascarelli** — [GitHub](https://github.com/paolopasca)
- **Alessandro Zocchi**
- **Dayo Ashaolu**

## License

This project was developed for educational purposes at FEUP, University of Porto. The LostEntity font is freeware, non-commercial ([source](https://www.fontspace.com/lost-entity-font-f148345)).
