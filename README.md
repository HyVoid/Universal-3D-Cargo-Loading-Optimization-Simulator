通用 3D 货柜装载优化模拟器

Universal 3D Cargo Loading Optimization Simulator

这是一个基于 WebGL (Three.js) 的轻量级、实时 3D 货柜装载模拟器。它专为物流从业者、仓库规划人员和算法爱好者设计，用于在无需任何后端服务器或本地环境配置的情况下，快速验证和生成最优的货物空间排布方案。

This is a lightweight, real-time 3D cargo loading simulator based on WebGL (Three.js). Designed for logistics professionals, warehouse planners, and algorithm enthusiasts, it allows you to quickly verify and generate optimal cargo spatial layout plans without needing any backend server or local environment configuration.

🌟 核心亮点 | Key Features

零部署，即开即用 (Zero Deployment, Out of the Box):
整个模拟器仅包含一个单独的 .html 文件。无需安装 Node.js、Python 或任何数据库。只需双击文件，即可在任何现代浏览器中畅快运行。
The entire simulator consists of a single .html file. No need to install Node.js, Python, or any database. Just double-click the file to run it smoothly in any modern browser.

宽度零间隙防晃动算法 (Zero-Gap Anti-Sway Algorithm):
这是本模拟器的核心逻辑。算法会穷举产品的长、宽维度组合，寻找一种能够完美贴合货柜内径宽度（或者缝隙最小）的铺排方案。这在现实运输中能极大程度减少因车辆变道、急刹车带来的货物横向位移和破损。
This is the core logic of the simulator. The algorithm exhaustively explores combinations of the product's length and width dimensions to find a layout that perfectly fits (or has the smallest gap) the internal width of the container. In real-world transportation, this significantly reduces lateral movement and damage to goods caused by lane changes and sudden braking.

物理重心自稳排序 (Physics-Based Center of Gravity Stabilization):
当目标装载数量小于货柜极限容量时，算法严格遵循“底层优先铺满”、“深处（车头）优先铺满”的原则。这确保了散货不会飘在空中，且车辆重心始终靠前，符合交通安全规范。
When the target loading quantity is less than the container's maximum capacity, the algorithm strictly follows the principles of "bottom layer first" and "deepest part (front of the truck) first." This ensures that loose cargo doesn't float in the air and the vehicle's center of gravity remains forward, complying with traffic safety regulations.

实时精细单体渲染 (Real-time Detailed Individual Rendering):
得益于 Three.js 的底层优化，即使是生成上万个带有独立描边线框的纸箱，也能保持极高的帧率。你可以拉近视角，清晰地看到每一个箱体的摆放姿态和拼接缝隙。
Thanks to the underlying optimization of Three.js, a high frame rate is maintained even when generating tens of thousands of cartons with independent stroke wireframes. You can zoom in to clearly see the placement posture and splicing gaps of each individual box.

🚀 如何使用 | How to Use

打开文件 (Open File):
下载并使用 Chrome、Edge 或 Safari 等现代浏览器打开 cargo_simulator.html 文件。
Download and open the cargo_simulator.html file using a modern browser like Chrome, Edge, or Safari.

输入参数 (Input Parameters):
在屏幕左侧的控制面板中，修改相应的尺寸数据（单位：厘米 cm）：
Modify the corresponding dimension data (Unit: cm) in the control panel on the left side of the screen:

🚚 货柜内径尺寸 (Container Dimensions): 输入你的车厢或集装箱的内部实际可用长、宽、高。
(Enter the actual usable internal length, width, and height of your truck or container.)

📦 单一产品尺寸 (Product Dimensions): 输入纸箱的外径长、宽、高。注意： 模拟器目前设定高度方向是固定朝上的（例如带有“向上”箭头的纸箱），算法只会自动互换和平移长和宽。
(Enter the outer length, width, and height of the carton. Note: The simulator currently assumes the height direction is fixed upwards (e.g., cartons with an "up" arrow), and the algorithm will only automatically swap and translate length and width.)

🎯 目标装箱总数 (Target Loading Count): 如果你有特定的订单数量，填入这里。模拟器会优先在底层深处排布。如果你想知道这个货柜“最多能塞多少箱”，请将此处留空或设置为 0。
(If you have a specific order quantity, enter it here. The simulator will prioritize placing them at the bottom and front. If you want to know the "maximum capacity" of this container, leave this blank or set it to 0.)

生成方案 (Generate Plan):
点击蓝色的 "生成最优 3D 方案 (Generate Optimal 3D Plan)" 按钮。
Click the blue button.

交互与查看 (Interact & View):

🖱️ 鼠标左键拖拽 (Left-click & Drag): 360度旋转全景视角。 (Rotate 360° panoramic view)

🖱️ 鼠标右键拖拽 (Right-click & Drag): 在同一平面内平移视角。 (Pan the view within the same plane)

⚙️ 鼠标滚轮 (Mouse Wheel): 缩放，拉近查看局部细节或推远查看全局。 (Zoom in for local details or zoom out for the global view)

📊 查看看板 (Check Dashboard): 生成后，控制面板下方会弹出详细的统计数据，包括理论极限数量、缝隙宽度、距离车门剩余空间等。 (After generation, a detailed statistics dashboard will pop up below the control panel, including the theoretical limit, gap width, remaining space near the door, etc.)

🛠️ 技术栈 | Technology Stack

HTML5 / CSS3 / JavaScript (ES6)

Three.js (WebGL 3D 渲染引擎 | WebGL 3D rendering engine)

Tailwind CSS (通过 CDN 引入，用于快速构建现代 UI | Loaded via CDN for rapid UI building)

💡 注意事项 | Disclaimers

本模拟器目前针对单一产品规格 (Single Product Specification) 的装载进行了深度优化。
(This simulator is currently deeply optimized for the loading of a single product specification.)

空间算法计算的是绝对物理边界。在实际装载作业中，考虑到纸箱的轻微形变、堆垛偏差以及工人的操作空间，建议在输入货柜内径尺寸时，适当减去 2~5 cm 的容错余量 (Tolerance margin)，以确保生成的方案在现实中 100% 可行。
(The spatial algorithm calculates absolute physical boundaries. In actual loading operations, considering slight carton deformation, stacking deviations, and workers' operating space, it is recommended to subtract a tolerance margin of 2~5 cm when inputting the container's internal dimensions to ensure the generated plan is 100% feasible in reality.)
