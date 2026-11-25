# Prism Stack // Kinetic Glass

> **Built With:** **Three.js (r128)** · **MediaPipe Hands** · **WebGL (`MeshPhysicalMaterial`)** · **One-Euro Adaptive Filtering** · **HTML5 Canvas 2D HUD** · **Tailwind CSS** · **Vanilla ES6+**

An interactive 3D WebGL kinetic glass stacking playground set against an architectural slate stage. **Prism Stack** combines physically based refractive glass polyhedra, deterministic vertical stacking and balance physics, and surgical computer-vision hand tracking—allowing you to pinch, lift, align, and stack translucent glass prisms using natural hand gestures or cursor/touch controls.

---

## 🛠 Technologies Used

| Technology | Role in Application |
| :--- | :--- |
| **Three.js (`r128`)** | 3D WebGL scene graph, shadow mapping, raycasting, and procedural `PMREMGenerator` studio environment reflections. |
| **`MeshPhysicalMaterial`** | Real-time optical glass refraction (`transmission: 0.94`), adjustable Index of Refraction (`IOR`), surface frost roughness, and edge/core wireframe highlights. |
| **MediaPipe Hands (`@mediapipe/hands`)** | Real-time 21-landmark GPU hand tracking via webcam (`getUserMedia`) with a Picture-in-Picture hand cam preview. |
| **One-Euro Velocity-Adaptive Filter** | Custom low-latency signal filter applied to the 3D thumb-index pinch midpoint—suppressing micro-tremor during delicate stacking while preserving zero-lag response during fast hand movements. |
| **HTML5 2D HUD Canvas** | Synchronized full-viewport overlay rendering the 21-point hand skeleton, thumb-to-index bridge, surgical crosshair reticle, and closing pinch-distance gauge. |
| **Tailwind CSS & Vanilla JavaScript** | Zero-build-step, single-file glassmorphic UI, live stack telemetry, and rigid-body vertical stacking physics. |

---

## 🚀 Getting Started

**Prism Stack** is packaged in a single, self-contained HTML file (`index.html`) with no bundler or `npm install` step required.

> **Important Note on Webcam Permissions:** Modern browsers require a secure context (`https://` or `http://localhost`) to grant webcam access (`getUserMedia`) for MediaPipe hand tracking. Serve the folder over a local HTTP server rather than opening `index.html` directly via `file://`.

```bash
# Option 1: Python 3
python3 -m http.server 8080

# Option 2: Node.js (npx)
npx serve .
```

Then open **`http://localhost:8080`** in Chrome, Edge, Safari, or Firefox. *(Mouse and touch controls work immediately even without enabling a camera.)*

---

## 🕹 How to Use It

### 1. Hand Gesture Controls (Camera Mode)
Click **Enable Hand Tracking** in the top-right corner and allow webcam access:

* **Target a Prism (Open Hand):** Move your hand across the frame to steer the surgical crosshair reticle. When the reticle hovers over a glass prism, a glowing cyan target halo illuminates beneath it and the top-left badge displays `TARGET // <PRISM NAME>`.
* **Grab & Lift (Thumb-Index Pinch or Closed Fist):** Bring your thumb tip and index finger tip together (watch the circular pinch gauge around the crosshair close) or curl your fingers into a fist. The reticle locks onto the prism with zero positional jump.
* **Align with the Plumb-Line:** While holding a prism, a dashed vertical plumb-line and ghost landing ring appear directly underneath it—turning bright sky-blue when centered over another prism's balance zone.
* **Release to Stack (Open Fingers):** Open your thumb and index finger (or uncurl your fist) to drop the prism. Centered drops magnetically snap onto the tower and trigger a glowing seam pulse ring; off-center drops tip and slide naturally onto the slate floor.

### 2. Mouse & Touch Controls (Works Anytime)
* **Click & Drag / Touch Drag:** Click or tap directly on any glass prism to lift it, align the vertical plumb-line over your tower, and release to stack.

### 3. Floating Control Dock & Telemetry
* **Top-Left Telemetry Pill:** Tracks live **STACKED** prism count (`1 / 5` up to `8`) and **TOWER HEIGHT** in meters (`0.68m`+), alongside active gesture state.
* **Mode: Micro-Precision / Standard:** Toggles between damped `0.62×` high-precision hand sensitivity (ideal for tall, delicate stacks) and `1.0×` full-range hand movement.
* **Add Prism (`5/8`):** Spawns additional glass prisms onto the slate stage (up to 8 total).
* **Optical IOR (`1.10` – `2.20`):** Adjusts the refractive index of every glass prism in real time.
* **Glass Frost (`0.01` – `0.48`):** Transitions the glass surface from polished crystal to frosted architectural glass.
* **Hand HUD: ON/OFF & Reset Stack:** Toggle the 2D hand wireframe/PIP camera preview or reset all prisms back to their starting positions.

---

## 🧠 Precision Hand-Tracking Architecture

1. **Exact Pinch Midpoint & Zero-Jump Anchoring:** Tracks the midpoint between thumb tip (`landmark 4`) and index tip (`landmark 8`) rather than palm center, recording the initial grab offset vector so prisms never snap or jump when pinched.
2. **Schmitt-Trigger Pinch Hysteresis:** Uses separate thresholds to engage (`0.28` normalized distance) and release (`0.47`) a grab so minor finger tremor never causes accidental mid-air drops.
3. **Deterministic Stacking & Balance Physics:** Evaluates vertical support surfaces, radial overlap tolerances, and center-of-mass balance thresholds on every frame—allowing multi-tier towers to rise cleanly while tipping unstable placements.

## 📄 License

Free to use, modify, and build upon for personal and creative projects.
