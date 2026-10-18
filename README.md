[ 🌐 عربي ](README.ar.md) | [ 🇩🇪 Deutsch ](README.de.md) | [ 🇫🇷 Français ](README.fr.md) | [ 🇳🇱 Nederlands ](README.nl.md) | [ 🇪🇸 Español ](README.sp.md) | [ 🇨🇳 中文 ](README.zh.md) | [ 🇬🇧 English ](README.md)
# 🚛 Universal 3D Cargo Loading Optimization Simulator

## ❓ Problem

When shipping, estimating "how many boxes fit in one container" from experience tends to go one of two ways: under-fill and waste freight cost, or overshoot capacity at the last minute and scramble to switch containers. Even when you have a number, you still don't know *how* to pack — which orientation to use against the wall, where to start loading, or whether cargo will shift and collide in transit.

---

## 🔍 Why It Happens

3D bin-packing is fundamentally an NP-hard problem. As the combination of box and container dimensions grows, the number of feasible layouts increases exponentially — exhaustive manual calculation is not viable. Even with a single product specification, a few centimetres of difference in how the box is oriented against the container's internal width can compound into a large dead zone at the rear.

Existing professional packing software either targets enterprise logistics clients at a prohibitive cost, or comes with a complex interface that isn't practical for fast pre-shipment estimation.

---

## 💰 Business Consequence

- A 5% drop in loading rate translates directly to a 5%–8% increase in effective freight cost for that shipment
- Lateral cargo movement and collision damage during transit are common in dry goods shipping, but tend to be written off as "normal wear and loss" without quantified tracking
- Without a clear loading figure, shippers default to ordering an extra container "just in case" — a habit that accumulates significant cost at scale

---

## 💡 Solution Logic

This simulator addresses these issues through four core mechanisms:

**① Zero-Gap Anti-Sway Algorithm**

Exhaustively tests both orientations (length × width) of the product to find the layout that perfectly matches the container's internal width, eliminating lateral play at the source.

**② Deep-First Loading Logic**

Loads from the back of the container forward, keeping the centre of gravity stable and making door-side unloading straightforward — consistent with standard field practice.

**③ Four-Side Buffer Management**

While maximising space utilisation, controls the gap distribution between cargo and all interior walls, reducing the risk of cargo impact from transit vibration.

**④ Physics-Based Centre-of-Gravity Stabilisation**

Strictly applies "bottom-first → back-first" sequencing, preventing cargo from floating loose and keeping the vehicle's centre of gravity forward, in compliance with road transport safety standards.

---

## 📋 Workbook

**Step 1: Open the Simulator**

[Click here to open the simulator →](https://hyvoid.github.io/Universal-3D-Cargo-Loading-Optimization-Simulator/)

**Step 2: Input Parameters** (unit: **cm**)

| Parameter | Description |
|-----------|-------------|
| 🚚 Container Dimensions | Actual usable internal length, width, and height of your truck or container |
| 📦 Product Dimensions | Outer carton length, width, and height (height is fixed upright; the algorithm only swaps length and width) |
| 🎯 Target Loading Count | Enter your order quantity; leave blank or set to `0` to calculate maximum container capacity |

**Step 3: Generate Plan**

Click the blue **「Generate Optimal 3D Plan」** button. The system runs the calculation and outputs a 3D visualisation automatically.

**Step 4: Interact & Review**

| Action | Function |
|--------|----------|
| 🖱️ Left-click & Drag | 360° panoramic rotation |
| 🖱️ Right-click & Drag | Pan the view |
| ⚙️ Mouse Wheel | Zoom in for detail or zoom out for overview |
| 📊 Stats Dashboard | Auto-appears after generation, showing capacity limit, gap widths, and remaining space near the door |

---

## 📌 Example

**Scenario**: A shipper plans to dispatch 800 boxes. Each carton measures 60×40×30 cm (outer dimensions). The intended container has internal dimensions of 1200×240×260 cm.

**Input**: Enter the above dimensions into the control panel, set Target Loading Count to `800`, and click 「Generate Optimal 3D Plan」.

**Output**: The system selects the orientation that best fits the container width, renders the full layout layer by layer in 3D, and outputs: actual loadable quantity, lateral gap per row, and longitudinal dead space at the rear.

**Decision reference**: If the optimal plan yields 780 boxes against a target of 800, the shipper can assess whether to split the shipment, adjust carton dimensions, or confirm an acceptable tolerance with the buyer.

---

## ⚠️ Limitations

- Supports **single product specification** only — mixed multi-SKU loading is not yet available
- The algorithm operates on absolute physical boundaries. For real operations, it is recommended to **subtract a 25 cm tolerance margin** from container dimensions to account for carton deformation, stacking deviation, and worker clearance
- Not suitable for cold-chain perishables, fragile goods, or cargo requiring specialised securing
- The 3D render is a planning illustration, not a formal loading instruction document

---

## 🔬 About The Method

This simulator uses a **deterministic exhaustive algorithm** — not heuristic search or AI generation. Identical inputs always produce identical outputs; the process is fully reproducible.

Technology stack: HTML5 / CSS3 / JavaScript (ES6), [Three.js](https://threejs.org/) (WebGL 3D rendering engine), [Tailwind CSS](https://tailwindcss.com/) (loaded via CDN). The entire tool is packaged as a **single `.html` file** — no Node.js, Python, or database required. Double-click and run in any modern browser.

**This tool is completely free for standard dry cargo planning. Not suitable for cold-chain perishables or fragile items.**

---

## 📄 License

This project is licensed under the **MIT License** — free to use, modify, and distribute with attribution.
