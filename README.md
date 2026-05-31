# 🚛 通用 3D 货柜装载优化模拟器
### Universal 3D Cargo Loading Optimization Simulator | محاكي تحميل الحاويات ثلاثي الأبعاد

Read this in other languages: [简体中文](#-简体中文) | [English](#-english) | [العربية](#-العربية)

---

## 🇨🇳 简体中文

### ❓ 问题

出货时凭经验估算"一个货柜能装多少箱"，结果往往要么装不满浪费运费，要么临时超柜打乱发货节奏。即使有了数量，仍然不知道怎么摆——用哪个朝向贴墙、从哪里开始装、货物在途中会不会晃动碰撞。

---

### 🔍 为何如此

三维装箱本质上是 NP-hard 问题：随着箱型与货柜尺寸的组合增加，可行排布的数量呈指数级增长，人工计算无法穷举。即便只有单一规格货物，长宽两种摆向与货柜内径的匹配关系，几厘米的偏差就会在货柜末端累积成大量无效空间。

现有专业装箱软件，要么面向物流企业定制、收费门槛高，要么操作界面复杂，难以用于出货前的快速估算。

---

### 💰 商业影响

- 装载率每下降 5%，等效该次运输成本额外上浮 5%–8%
- 货物横向位移导致的途中碰撞破损在干货运输中普遍存在，但往往以"正常损耗"归档，未被量化追踪
- 在装载量不明确的情况下，出货方倾向于"多订一柜保险"——这一决策惯性在批量出货中长期累积的成本相当显著

---

### 💡 方案逻辑

针对以上问题，本模拟器采用四项核心机制：

**① 宽度零间隙防晃动算法**
穷举产品长、宽两种摆向，寻找与货柜内径宽度完美贴合的排布，从根源上减少货物横向位移与碰撞破损。

**② 深进优先装载逻辑**
优先填满货柜内侧，确保重心靠前稳定，同时便于从车门侧逐层取出，符合实际作业习惯。

**③ 四面缓冲余量管理**
在空间利用率最优的前提下，合理控制货物与货柜四壁及顶部的空隙分布，降低颠簸时货物撞壁风险。

**④ 物理重心自稳排序**
严格遵循"底层优先 → 深处优先"原则，确保货物不飘空，车辆重心始终靠前，符合道路运输安全规范。

---

### 📋 操作手册

**第一步：打开模拟器**

[点击此处打开模拟器 →](https://hyvoid.github.io/Universal-3D-Cargo-Loading-Optimization-Simulator/)

**第二步：输入参数**（单位：**cm**）

| 参数 | 说明 |
|------|------|
| 🚚 货柜内径尺寸 | 车厢或集装箱的实际可用内部长、宽、高 |
| 📦 单一产品尺寸 | 纸箱外径长、宽、高（高度固定朝上，算法仅自动互换长宽） |
| 🎯 目标装箱总数 | 填入订单数量；留空或填 `0` 则计算货柜最大理论容量 |

**第三步：生成方案**

点击蓝色按钮 **「生成最优 3D 方案」**，系统自动完成运算并输出 3D 可视化结果。

**第四步：交互查看**

| 操作 | 功能 |
|------|------|
| 🖱️ 左键拖拽 | 360° 全景旋转视角 |
| 🖱️ 右键拖拽 | 平移视角 |
| ⚙️ 滚轮 | 缩放，拉近局部或推远全局 |
| 📊 统计看板 | 生成后自动弹出，显示极限容量、缝隙宽度、距车门剩余空间 |

---

### 📌 场景示例

**背景**：出货方计划发运 800 箱，单箱外径 60×40×30 cm，拟用货柜内径 1200×240×260 cm。

**操作**：将上述参数填入控制面板，目标装箱数填 `800`，点击「生成最优 3D 方案」。

**输出**：系统自动选出贴合内径宽度最优的摆向组合，3D 视图逐层呈现排布，统计看板输出实际可装量、每行横向间隙、纵向末端剩余空间。

**决策参考**：若最优方案实际可装 780 箱，与目标相差 20 箱，出货方可据此判断是否拆批出货、调整包装尺寸，或与采购方确认允差范围。

---

### ⚠️ 当前局限

- 仅支持**单一规格**货物，不支持多 SKU 混装
- 算法基于绝对物理边界计算——实际作业建议输入货柜内径时**减去 25 cm 容错余量**，以应对纸箱轻微形变、堆垛偏差及工人操作空间
- 不适用于冷链生鲜、易碎品或需特殊固定的货物
- 3D 渲染为方案示意，不等同于正式作业指导书

---

### 🔬 关于这个方法

本模拟器采用**确定性穷举算法**，非启发式搜索或 AI 生成，相同输入始终输出相同结果，过程可完整复现。

技术栈：HTML5 / CSS3 / JavaScript（ES6）、[Three.js](https://threejs.org/)（WebGL 3D 渲染引擎）、[Tailwind CSS](https://tailwindcss.com/)（CDN 引入）。整体打包为**单一 `.html` 文件**，无需安装 Node.js、Python 或任何数据库，双击即可在任何现代浏览器中运行。

**本工具完全免费，适用于普通干货装车规划场景。不适用于冷链生鲜产品及易碎品。**

---

## 🇬🇧 English

### ❓ Problem

When shipping, estimating "how many boxes fit in one container" from experience tends to go one of two ways: under-fill and waste freight cost, or overshoot capacity at the last minute and scramble to switch containers. Even when you have a number, you still don't know *how* to pack — which orientation to use against the wall, where to start loading, or whether cargo will shift and collide in transit.

---

### 🔍 Why It Happens

3D bin-packing is fundamentally an NP-hard problem. As the combination of box and container dimensions grows, the number of feasible layouts increases exponentially — exhaustive manual calculation is not viable. Even with a single product specification, a few centimetres of difference in how the box is oriented against the container's internal width can compound into a large dead zone at the rear.

Existing professional packing software either targets enterprise logistics clients at a prohibitive cost, or comes with a complex interface that isn't practical for fast pre-shipment estimation.

---

### 💰 Business Consequence

- A 5% drop in loading rate translates directly to a 5%–8% increase in effective freight cost for that shipment
- Lateral cargo movement and collision damage during transit are common in dry goods shipping, but tend to be written off as "normal wear and loss" without quantified tracking
- Without a clear loading figure, shippers default to ordering an extra container "just in case" — a habit that accumulates significant cost at scale

---

### 💡 Solution Logic

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

### 📋 Workbook

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

### 📌 Example

**Scenario**: A shipper plans to dispatch 800 boxes. Each carton measures 60×40×30 cm (outer dimensions). The intended container has internal dimensions of 1200×240×260 cm.

**Input**: Enter the above dimensions into the control panel, set Target Loading Count to `800`, and click 「Generate Optimal 3D Plan」.

**Output**: The system selects the orientation that best fits the container width, renders the full layout layer by layer in 3D, and outputs: actual loadable quantity, lateral gap per row, and longitudinal dead space at the rear.

**Decision reference**: If the optimal plan yields 780 boxes against a target of 800, the shipper can assess whether to split the shipment, adjust carton dimensions, or confirm an acceptable tolerance with the buyer.

---

### ⚠️ Limitations

- Supports **single product specification** only — mixed multi-SKU loading is not yet available
- The algorithm operates on absolute physical boundaries. For real operations, it is recommended to **subtract a 25 cm tolerance margin** from container dimensions to account for carton deformation, stacking deviation, and worker clearance
- Not suitable for cold-chain perishables, fragile goods, or cargo requiring specialised securing
- The 3D render is a planning illustration, not a formal loading instruction document

---

### 🔬 About The Method

This simulator uses a **deterministic exhaustive algorithm** — not heuristic search or AI generation. Identical inputs always produce identical outputs; the process is fully reproducible.

Technology stack: HTML5 / CSS3 / JavaScript (ES6), [Three.js](https://threejs.org/) (WebGL 3D rendering engine), [Tailwind CSS](https://tailwindcss.com/) (loaded via CDN). The entire tool is packaged as a **single `.html` file** — no Node.js, Python, or database required. Double-click and run in any modern browser.

**This tool is completely free for standard dry cargo planning. Not suitable for cold-chain perishables or fragile items.**

---

## 🇸🇦 العربية

### ❓ المشكلة

عند الشحن، يعتمد كثير من المُصدِّرين على الخبرة الشخصية لتقدير "كم صندوقاً يسع الحاوية"، فتكون النتيجة إما حاوية غير ممتلئة يضيع معها جزء من تكلفة الشحن، أو تجاوزاً للسعة في اللحظة الأخيرة يُربك جدول الشحن. وحتى حين تتوفر أرقام، يظل السؤال قائماً: ما الاتجاه الصحيح لوضع الصناديق؟ ومن أين يبدأ التحميل؟ وهل ستظل البضاعة ثابتة دون اهتزاز أثناء النقل؟

---

### 🔍 لماذا يحدث هذا؟

تُصنَّف مشكلة التعبئة ثلاثية الأبعاد ضمن مسائل NP-hard، مما يعني أن عدد الترتيبات الممكنة يتضاعف أسياً مع زيادة تنوع الأبعاد — فالحسابات اليدوية الشاملة غير قابلة للتطبيق عملياً. حتى مع منتج وحيد الحجم، يمكن لبضعة سنتيمترات في اتجاه وضع الصناديق داخل الحاوية أن تتراكم لتصنع منطقة ميتة كبيرة في نهايتها.

أما برامج التعبئة الاحترافية المتاحة، فإما موجَّهة لشركات اللوجستيات الكبرى بتكاليف باهظة، أو بواجهات معقدة تجعل الاستخدام السريع قبل الشحن أمراً غير عملي.

---

### 💰 الأثر التجاري

- انخفاض معدل التحميل بنسبة 5% يعادل ارتفاعاً فعلياً في تكلفة الشحن بنسبة 5%–8%
- أضرار الاصطدام الناجمة عن حركة البضائع الجانبية شائعة في شحن البضائع الجافة، لكنها غالباً تُدرج تحت "الهالك الطبيعي" دون تتبع كمّي
- في غياب رقم تحميل واضح، يلجأ المُصدِّرون تلقائياً إلى "طلب حاوية إضافية احتياطاً" — وهذه العادة تُراكم تكاليف ملموسة عند الشحن بكميات كبيرة

---

### 💡 منطق الحل

يعالج هذا المحاكي المشكلات السابقة عبر أربع آليات أساسية:

**① خوارزمية التثبيت بالتلاصق الصفري لمنع الاهتزاز**
تختبر الخوارزمية كلا اتجاهَي المنتج (طول × عرض) بشكل استنفادي للعثور على الترتيب الذي يتطابق تماماً مع العرض الداخلي للحاوية، مما يُزيل الحركة الجانبية من جذورها.

**② منطق التحميل من الداخل للخارج**
يبدأ التحميل من الجزء الخلفي للحاوية نحو الباب، مما يحافظ على ثبات مركز الثقل ويجعل التفريغ من جانب الباب سهلاً ومنسجماً مع الممارسات الميدانية المعتادة.

**③ إدارة هوامش التخزين الأربعة**
مع الحفاظ على أقصى استخدام للمساحة، تتحكم الخوارزمية في توزيع الفجوات بين البضاعة وجميع الجدران الداخلية، مما يقلل من مخاطر الاصطدام الناجمة عن اهتزازات النقل.

**④ ترتيب تثبيت مركز الثقل الفيزيائي**
يتبع صرامًا تسلسل "الطبقات السفلى أولاً ← العمق أولاً"، مما يمنع البضائع من الطفو ويبقي مركز ثقل المركبة نحو الأمام، وفق معايير سلامة النقل البري.

---

### 📋 دليل التشغيل

**الخطوة الأولى: فتح المحاكي**

[اضغط هنا لفتح المحاكي ←](https://hyvoid.github.io/Universal-3D-Cargo-Loading-Optimization-Simulator/)

**الخطوة الثانية: إدخال المعطيات** (الوحدة: **سم**)

| المعامل | الوصف |
|---------|-------|
| 🚚 أبعاد الحاوية | الطول والعرض والارتفاع الداخلي الفعلي القابل للاستخدام |
| 📦 أبعاد المنتج | الطول والعرض والارتفاع الخارجي للصندوق (الارتفاع ثابت لأعلى، والخوارزمية تبادل الطول والعرض فقط) |
| 🎯 الكمية المستهدفة | أدخل كمية الطلب؛ اتركها فارغة أو اكتب `0` لحساب الطاقة الاستيعابية القصوى |

**الخطوة الثالثة: توليد الخطة**

اضغط الزر الأزرق **「توليد الخطة الثلاثية الأبعاد المثلى」**. يُكمل النظام الحسابات تلقائياً ويعرض النتائج المرئية ثلاثية الأبعاد.

**الخطوة الرابعة: التفاعل والمراجعة**

| الإجراء | الوظيفة |
|---------|---------|
| 🖱️ سحب بالزر الأيسر | تدوير 360° بزاوية بانورامية |
| 🖱️ سحب بالزر الأيمن | تحريك زاوية العرض |
| ⚙️ عجلة الفأرة | تكبير للتفاصيل أو تصغير للنظرة الشاملة |
| 📊 لوحة الإحصاءات | تظهر تلقائياً بعد التوليد، وتعرض الطاقة الاستيعابية القصوى وعرض الفجوات والمساحة المتبقية |

---

### 📌 مثال تطبيقي

**السيناريو**: يخطط أحد المُصدِّرين لشحن 800 صندوق، بأبعاد خارجية لكل صندوق 60×40×30 سم، باستخدام حاوية بأبعاد داخلية 1200×240×260 سم.

**الإدخال**: أدخل الأبعاد أعلاه في لوحة التحكم، واضبط الكمية المستهدفة على `800`، ثم اضغط 「توليد الخطة الثلاثية الأبعاد المثلى」.

**المخرجات**: يختار النظام تلقائياً الاتجاه الأمثل الذي يناسب عرض الحاوية، ويعرض الترتيب طبقة بطبقة في العرض ثلاثي الأبعاد، ويُخرج: الكمية الفعلية القابلة للتحميل، والفجوة الجانبية لكل صف، والمساحة المتبقية في نهاية الحاوية.

**مرجع القرار**: إذا أظهر المخطط الأمثل إمكانية تحميل 780 صندوقاً مقارنة بالهدف البالغ 800، يمكن للمُصدِّر تقييم ما إذا كان سيقسّم الشحنة، أو يعدّل أبعاد التغليف، أو يتحقق من نطاق التسامح المقبول مع المشتري.

---

### ⚠️ القيود الحالية

- يدعم **مواصفة منتج واحدة** فقط — التحميل المختلط لمنتجات متعددة الأحجام غير مدعوم حتى الآن
- تحسب الخوارزمية الحدود الفيزيائية المطلقة. في التطبيق الفعلي، يُوصى **بطرح 25 سم كهامش تسامح** من أبعاد الحاوية لمراعاة تشوه الكرتون وانحراف التكديس ومساحة حركة العمال
- غير مناسب للبضائع المبردة أو الهشة أو التي تستلزم تثبيتاً خاصاً
- العرض ثلاثي الأبعاد هو توضيح للخطة، وليس وثيقة تعليمات تحميل رسمية

---

### 🔬 عن المنهجية

يعتمد هذا المحاكي على **خوارزمية استنفادية حتمية** — لا بحث استدلالي ولا توليد بالذكاء الاصطناعي. المدخلات المتطابقة تُنتج دائماً مخرجات متطابقة، والعملية قابلة للتحقق والاستنساخ الكامل.

المكدس التقني: HTML5 / CSS3 / JavaScript (ES6)، [Three.js](https://threejs.org/) لعرض WebGL ثلاثي الأبعاد، و[Tailwind CSS](https://tailwindcss.com/) محمَّل عبر CDN. يُجمَّع كل ذلك في **ملف `.html` واحد** — لا يتطلب تثبيت Node.js أو Python أو أي قاعدة بيانات. انقر نقراً مزدوجاً وشغّله في أي متصفح حديث.

**هذه الأداة مجانية تماماً لتخطيط شحن البضائع الجافة العادية. غير مناسبة للبضائع المبردة أو الهشة.**

---

## 📄 License

This project is licensed under the **MIT License** — free to use, modify, and distribute with attribution.
