# 🚛 通用 3D 货柜装载优化模拟器
### Universal 3D Cargo Loading Optimization Simulator | محاكي تحميل الحاويات ثلاثي الأبعاد

Read this in other languages: [简体中文](#-简体中文) | [English](#-english) | [العربية](#-العربية)

---

## 🇨🇳 简体中文

**本工具为完全免费的公益性软件**，适用于普通干货的装车规划场景。用户输入货物与货柜的体积参数及目标装载量，系统自动计算最优排布方案并生成实时 3D 可视化效果。

**典型使用场景：**
- 与货运公司沟通装载方案，评估并议定装货成本
- 出货方预先估算所需订购的货柜数量，优化采购决策
- 仓储规划与装车作业前的方案预演

> 🚫 **适用货物范围：** 普通干货。不适用于冷链生鲜产品及易碎品。

---

### 🌟 核心功能

#### 📦 零部署，即开即用
整个模拟器仅为**一个单独的 `.html` 文件**。无需安装 Node.js、Python 或任何数据库，双击即可在任何现代浏览器中运行。

#### 📐 宽度零间隙防晃动算法
算法穷举产品长、宽维度组合，寻找**完美贴合货柜内径宽度**的排布方案，从根源上减少运输途中货物的横向位移与碰撞破损风险。

#### 📥 深进优先装载逻辑
装载时优先填满货柜内侧，确保重心前移稳定，同时便于卸货时从车门侧逐层取出，符合实际作业习惯。

#### 🛡️ 四面缓冲余量管理
在保证体积利用率最优的前提下，合理控制货物与货柜四壁及顶部的空隙分布，降低运输颠簸时货物与壁面的撞击风险，兼顾装载效率与货物保护。

#### ⚖️ 物理重心自稳排序
严格遵循 **"底层优先 → 深处优先"** 的装载原则，确保货物不飘空，车辆重心始终靠前，符合道路运输安全规范。

#### 🎮 实时精细单体渲染
基于 Three.js 底层优化，即使渲染**上万个独立线框纸箱**也能保持流畅帧率。可拉近视角，清晰查看每一个箱体的摆放姿态与拼接缝隙。

---

### 🚀 使用步骤

**第一步 — 打开模拟器**

[点击此处打开模拟器](https://hyvoid.github.io/Universal-3D-Cargo-Loading-Optimization-Simulator/)

**第二步 — 输入参数**

在左侧控制面板中填写以下数据（单位：**cm**）：

| 参数 | 说明 |
|------|------|
| 🚚 货柜内径尺寸 | 车厢或集装箱的实际可用内部长、宽、高 |
| 📦 单一产品尺寸 | 纸箱外径长、宽、高（高度方向固定朝上，算法仅自动互换长宽） |
| 🎯 目标装箱总数 | 填入订单数量；留空或填 `0` 则计算货柜最大理论容量 |

**第三步 — 生成方案**

点击蓝色按钮 **「生成最优 3D 方案」**。

**第四步 — 交互查看**

| 操作 | 功能 |
|------|------|
| 🖱️ 左键拖拽 | 360° 全景旋转视角 |
| 🖱️ 右键拖拽 | 平移视角 |
| ⚙️ 滚轮 | 缩放，拉近局部或推远全局 |
| 📊 统计看板 | 生成后自动弹出，显示极限容量、缝隙宽度、距车门剩余空间等 |

---

### 🛠️ 技术栈

- **HTML5 / CSS3 / JavaScript** (ES6)
- **[Three.js](https://threejs.org/)** — WebGL 3D 渲染引擎
- **[Tailwind CSS](https://tailwindcss.com/)** — 通过 CDN 引入，快速构建现代 UI

---

### 💡 注意事项

> ⚠️ 本模拟器目前针对**单一产品规格**的装载进行了深度优化，暂不支持多规格货物混装。

> 📏 算法计算的是绝对物理边界。实际作业中，建议在输入货柜内径时**减去 25 cm 容错余量**，以应对纸箱轻微形变、堆垛偏差及工人操作空间。

---

## 🇬🇧 English

**This is a free, open-access tool** for planning standard dry cargo loading. Input your cargo dimensions, container dimensions, and target quantity — the system automatically calculates the optimal arrangement and generates a real-time 3D visualization.

**Typical use cases:**
- Communicating loading plans with freight carriers and negotiating shipping costs
- Pre-estimating the number of containers needed before placing orders
- Pre-planning warehouse operations and loading procedures

> 🚫 **Applicable cargo types:** Standard dry goods only. Not suitable for cold-chain perishables or fragile items.

---

### 🌟 Key Features

#### 📦 Zero Deployment, Out of the Box
The entire simulator is a **single `.html` file**. No Node.js, Python, or database required — just double-click and run in any modern browser.

#### 📐 Zero-Gap Anti-Sway Algorithm
The algorithm exhaustively explores product dimension combinations to find a layout that **perfectly fits the container's internal width**, significantly reducing lateral cargo movement and collision damage during transit.

#### 📥 Deep-First Loading Logic
Cargo is loaded from the back of the container forward, keeping the center of gravity stable and making unloading from the door side straightforward — consistent with standard loading practice.

#### 🛡️ Four-Side Buffer Management
While maximizing volumetric efficiency, the algorithm manages gap distribution between cargo and all interior walls, reducing collision risk from transit vibration and striking a balance between space utilization and cargo protection.

#### ⚖️ Physics-Based Center of Gravity Stabilization
Strictly follows a **"bottom-first → back-first"** loading principle, preventing cargo from floating loose, keeping the vehicle's center of gravity forward, and complying with road transport safety standards.

#### 🎮 Real-Time Detailed Individual Rendering
Powered by Three.js optimizations, the simulator maintains smooth frame rates even with **tens of thousands of individual wireframe cartons**. Zoom in to inspect the exact placement and gap of every single box.

---

### 🚀 How to Use

**Step 1 — Open the Simulator**

[Click here to open the simulator](https://hyvoid.github.io/Universal-3D-Cargo-Loading-Optimization-Simulator/)

**Step 2 — Input Parameters**

Fill in the following data (unit: **cm**) in the left control panel:

| Parameter | Description |
|-----------|-------------|
| 🚚 Container Dimensions | Actual usable internal length, width, and height of your truck or container |
| 📦 Product Dimensions | Outer length, width, and height of the carton (height is fixed upright; the algorithm only swaps length and width automatically) |
| 🎯 Target Loading Count | Enter your order quantity; leave blank or set to `0` to calculate maximum container capacity |

**Step 3 — Generate Plan**

Click the blue **「Generate Optimal 3D Plan」** button.

**Step 4 — Interact & View**

| Action | Function |
|--------|----------|
| 🖱️ Left-click & Drag | Rotate 360° panoramic view |
| 🖱️ Right-click & Drag | Pan the view |
| ⚙️ Mouse Wheel | Zoom in for local detail or zoom out for overview |
| 📊 Stats Dashboard | Auto-appears after generation, showing capacity limit, gap widths, remaining space near the door, etc. |

---

### 🛠️ Technology Stack

- **HTML5 / CSS3 / JavaScript** (ES6)
- **[Three.js](https://threejs.org/)** — WebGL 3D rendering engine
- **[Tailwind CSS](https://tailwindcss.com/)** — Loaded via CDN for rapid modern UI building

---

### 💡 Disclaimers

> ⚠️ This simulator is currently optimized for **single product specification** loading. Mixed multi-SKU loading is not yet supported.

> 📏 The algorithm calculates absolute physical boundaries. In practice, it is recommended to **subtract a 25 cm tolerance margin** from container dimensions to account for carton deformation, stacking deviation, and worker clearance.

---

## 🇸🇦 العربية

**هذه أداة مجانية ومفتوحة للعموم** لتخطيط تحميل البضائع الجافة العادية. أدخل أبعاد البضاعة والحاوية والكمية المستهدفة، وسيحسب النظام تلقائيًا أفضل ترتيب ممكن ويولّد تصورًا ثلاثي الأبعاد في الوقت الفعلي.

**حالات الاستخدام الرئيسية:**
- التواصل مع شركات الشحن لمناقشة خطط التحميل والتفاوض على تكاليف الشحن
- تقدير عدد الحاويات اللازمة مسبقًا قبل إصدار أوامر الشراء
- التخطيط المسبق لعمليات المستودعات وإجراءات التحميل

> 🚫 **أنواع البضائع المدعومة:** البضائع الجافة العادية فقط. غير مناسب للبضائع المبردة أو القابلة للتلف أو الهشة.

---

### 🌟 الميزات الرئيسية

#### 📦 بدون تثبيت، جاهز للاستخدام الفوري
يتكون المحاكي بالكامل من **ملف `.html` واحد فقط**. لا يتطلب تثبيت Node.js أو Python أو أي قاعدة بيانات — فقط انقر نقرًا مزدوجًا وشغّله في أي متصفح حديث.

#### 📐 خوارزمية التثبيت بالتلاصق الصفري
تستعرض الخوارزمية جميع تركيبات أبعاد المنتج للعثور على ترتيب **يتطابق تمامًا مع العرض الداخلي للحاوية**، مما يقلل بشكل جوهري من الحركة الجانبية للبضاعة وأضرار الاصطدام أثناء النقل.

#### 📥 منطق التحميل من الداخل إلى الخارج
يُحمَّل البضاعة بدءًا من الجزء الخلفي للحاوية نحو الأمام، مما يحافظ على ثبات مركز الثقل ويجعل التفريغ من جانب الباب سهلًا ومتسقًا مع الممارسات المعتادة.

#### 🛡️ إدارة هوامش التخمة الأربعة
مع الحفاظ على أقصى كفاءة في استخدام الحجم، تتحكم الخوارزمية في توزيع الفجوات بين البضائع وجميع الجدران الداخلية، مما يقلل من مخاطر الاصطدام الناجمة عن اهتزازات النقل ويحقق توازنًا بين كفاءة الاستخدام وحماية البضاعة.

#### ⚖️ ترتيب تثبيت مركز الثقل الفيزيائي
يتبع صرامًا مبدأ **"الطبقات السفلية أولًا ← العمق أولًا"** في التحميل، مما يمنع البضائع من الطفو، ويبقي مركز ثقل المركبة في المقدمة، ويتوافق مع معايير سلامة النقل البري.

#### 🎮 عرض فردي تفصيلي في الوقت الفعلي
مدعوم بتحسينات Three.js، يحافظ المحاكي على معدلات إطارات سلسة حتى مع **عشرات الآلاف من صناديق الكرتون المنفردة**. كبّر الصورة لفحص الموضع الدقيق والفجوة لكل صندوق على حدة.

---

### 🚀 طريقة الاستخدام

**الخطوة الأولى — فتح المحاكي**

[اضغط هنا لفتح المحاكي](https://hyvoid.github.io/Universal-3D-Cargo-Loading-Optimization-Simulator/)

**الخطوة الثانية — إدخال المعطيات**

أدخل البيانات التالية (الوحدة: **سم**) في لوحة التحكم اليسرى:

| المعامل | الوصف |
|---------|-------|
| 🚚 أبعاد الحاوية | الطول والعرض والارتفاع الداخلي الفعلي القابل للاستخدام |
| 📦 أبعاد المنتج | الطول والعرض والارتفاع الخارجي لصندوق الكرتون (الارتفاع ثابت لأعلى، والخوارزمية تبادل الطول والعرض تلقائيًا فقط) |
| 🎯 الكمية المستهدفة | أدخل كمية الطلب؛ اتركها فارغة أو اكتب `0` لحساب الطاقة الاستيعابية القصوى للحاوية |

**الخطوة الثالثة — توليد الخطة**

اضغط على الزر الأزرق **「توليد الخطة الثلاثية الأبعاد المثلى」**.

**الخطوة الرابعة — التفاعل والعرض**

| الإجراء | الوظيفة |
|---------|---------|
| 🖱️ سحب بالزر الأيسر | تدوير 360° بزاوية بانورامية |
| 🖱️ سحب بالزر الأيمن | تحريك زاوية العرض |
| ⚙️ عجلة الفأرة | تكبير للتفاصيل أو تصغير للنظرة الشاملة |
| 📊 لوحة الإحصاءات | تظهر تلقائيًا بعد التوليد، وتعرض الطاقة الاستيعابية القصوى وعرض الفجوات والمساحة المتبقية قرب الباب |

---

### 🛠️ التقنيات المستخدمة

- **HTML5 / CSS3 / JavaScript** (ES6)
- **[Three.js](https://threejs.org/)** — محرك العرض ثلاثي الأبعاد WebGL
- **[Tailwind CSS](https://tailwindcss.com/)** — محمّل عبر CDN لبناء واجهة مستخدم حديثة بسرعة

---

### 💡 تنبيهات

> ⚠️ هذا المحاكي محسَّن حاليًا لتحميل **مواصفة منتج واحدة**. التحميل المختلط لمنتجات متعددة المقاسات غير مدعوم حتى الآن.

> 📏 تحسب الخوارزمية الحدود الفيزيائية المطلقة. في التطبيق الفعلي، يُوصى **بطرح 25 سم كهامش تسامح** من أبعاد الحاوية لمراعاة تشوه الكرتون وانحراف التكديس ومساحة حركة العمال.

---

## 📄 License

This project is licensed under the **MIT License** — free to use, modify, and distribute with attribution.
