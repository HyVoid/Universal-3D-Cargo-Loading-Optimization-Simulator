# 🚛 通用 3D 货柜装载优化模拟器
### Universal 3D Cargo Loading Optimization Simulator

这是一个基于 **WebGL (Three.js)** 的轻量级、实时 3D 货柜装载模拟器。专为物流从业者、仓库规划人员和算法爱好者设计，无需任何后端服务器或本地环境配置，即可快速验证并生成最优货物空间排布方案。

> A lightweight, real-time 3D cargo loading simulator based on **WebGL (Three.js)**. Designed for logistics professionals, warehouse planners, and algorithm enthusiasts — no backend server or local setup required.

Read this in other languages: [简体中文](#核心亮点--key-features) | [English](#核心亮点--key-features)

---

## 🌟 核心亮点 | Key Features

### 📦 零部署，即开即用 | Zero Deployment, Out of the Box
整个模拟器仅包含**一个单独的 `.html` 文件**。无需安装 Node.js、Python 或任何数据库，双击即可在任何现代浏览器中运行。

The entire simulator is a **single `.html` file**. No Node.js, Python, or database required — just double-click and run in any modern browser.

---

### 📐 宽度零间隙防晃动算法 | Zero-Gap Anti-Sway Algorithm
算法穷举产品长、宽维度组合，寻找**完美贴合货柜内径宽度**的铺排方案，极大程度减少运输途中货物的横向位移与破损风险。

The algorithm exhaustively explores product dimension combinations to find a layout that **perfectly fits the container's internal width**, significantly reducing lateral cargo movement and damage during transit.

---

### ⚖️ 物理重心自稳排序 | Physics-Based Center of Gravity Stabilization
严格遵循 **"底层优先 → 深处优先"** 的装载原则，确保散货不飘空，车辆重心始终靠前，符合交通安全规范。

Strictly follows a **"bottom-first → front-first"** loading principle, keeping the vehicle's center of gravity forward and complying with traffic safety regulations.

---

### 🎮 实时精细单体渲染 | Real-time Detailed Individual Rendering
基于 Three.js 底层优化，即使生成**上万个独立线框纸箱**也能保持极高帧率。可拉近视角，清晰查看每一个箱体的摆放姿态与拼接缝隙。

Powered by Three.js, maintains high frame rates even with **tens of thousands of individual wireframe cartons**. Zoom in to inspect the exact placement and gap of every single box.

---

## 🚀 快速开始 | How to Use

**第一步 | Step 1 — 打开文件 | Open File**

下载并使用 Chrome、Edge 或 Safari 打开 `cargo_simulator.html` 文件。

Download and open `cargo_simulator.html` in Chrome, Edge, or Safari.

---

**第二步 | Step 2 — 输入参数 | Input Parameters**

在左侧控制面板中填写以下数据（单位：**cm**）：

| 参数 | 说明 |
|------|------|
| 🚚 货柜内径尺寸 | 车厢或集装箱的实际可用内部长、宽、高 |
| 📦 单一产品尺寸 | 纸箱外径长、宽、高（高度方向固定朝上，算法仅自动互换长宽） |
| 🎯 目标装箱总数 | 填入订单数量；留空或填 `0` 则计算货柜最大理论容量 |

---

**第三步 | Step 3 — 生成方案 | Generate Plan**

点击蓝色按钮 **「生成最优 3D 方案 | Generate Optimal 3D Plan」**。

---

**第四步 | Step 4 — 交互查看 | Interact & View**

| 操作 | 功能 |
|------|------|
| 🖱️ 左键拖拽 | 360° 全景旋转视角 |
| 🖱️ 右键拖拽 | 平移视角 |
| ⚙️ 滚轮 | 缩放，拉近局部或推远全局 |
| 📊 统计看板 | 生成后自动弹出，显示极限容量、缝隙宽度、距车门剩余空间等 |

---

## 🛠️ 技术栈 | Technology Stack

- **HTML5 / CSS3 / JavaScript** (ES6)
- **[Three.js](https://threejs.org/)** — WebGL 3D 渲染引擎
- **[Tailwind CSS](https://tailwindcss.com/)** — 通过 CDN 引入，快速构建现代 UI

---

## 💡 注意事项 | Disclaimers

> ⚠️ 本模拟器目前针对**单一产品规格**的装载进行了深度优化。
> This simulator is currently optimized for **single product specification** loading.

> 📏 空间算法计算的是绝对物理边界。实际作业中，建议在输入货柜内径时**减去 25 cm 容错余量**，以应对纸箱轻微形变、堆垛偏差及工人操作空间。
> The algorithm calculates absolute physical boundaries. In practice, it is recommended to **subtract a 25 cm tolerance margin** from container dimensions to account for carton deformation, stacking deviation, and worker clearance.

---

## 📄 License

This project is licensed under the **MIT License** — feel free to use, modify, and distribute with attribution.
