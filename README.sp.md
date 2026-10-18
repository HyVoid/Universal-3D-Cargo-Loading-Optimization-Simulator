[ 🌐 عربي ](README.ar.md) | [ 🇩🇪 Deutsch ](README.de.md) | [ 🇫🇷 Français ](README.fr.md) | [ 🇳🇱 Nederlands ](README.nl.md) | [ 🇪🇸 Español ](README.sp.md) | [ 🇨🇳 中文 ](README.zh.md) | [ 🇬🇧 English ](README.md)
# 🚛 Simulador universal de optimización de carga de contenedores 3D

## ❓ Problema

Al enviar mercancía, estimar «cuántas cajas caben en un contenedor» por experiencia suele tener uno de dos resultados: subllenado y desperdicio de costo de flete, o exceso de capacidad en el último momento y cambio apresurado de contenedor. Incluso con una cifra, a menudo no se sabe *cómo* cargar — qué orientación usar contra la pared, por dónde empezar la carga, o si la mercancía se desplazará y colisionará en tránsito.

---

## 🔍 Por qué ocurre

El empaquetado 3D (bin-packing) es fundamentalmente un problema NP-hard. A medida que crece la combinación de dimensiones de caja y contenedor, el número de disposiciones viables aumenta exponencialmente — el cálculo manual exhaustivo no es viable. Incluso con una sola especificación de producto, unos pocos centímetros de diferencia en la orientación de la caja contra el ancho interno del contenedor pueden acumularse en una gran zona muerta en la parte trasera.

El software profesional de empaquetado existente se dirige a clientes de logística empresarial a un costo prohibitivo, o viene con una interfaz compleja que no es práctica para la estimación rápida previa al envío.

---

## 💰 Consecuencia comercial

- Una caída del 5 % en la tasa de carga se traduce directamente en un aumento del 5 %–8 % del costo de flete efectivo de ese envío
- El movimiento lateral de la carga y los daños por colisión en tránsito son comunes en el transporte de mercancía seca, pero suelen archivarse como «desgaste y pérdida normales» sin seguimiento cuantificado
- Sin una cifra de carga clara, los embarcadores piden por defecto un contenedor adicional «por si acaso» — un hábito que acumula costos significativos a escala

---

## 💡 Lógica de la solución

Este simulador aborda estos problemas mediante cuatro mecanismos centrales:

**① Algoritmo antioscilación de holgura cero**

Prueba exhaustivamente ambas orientaciones (largo × ancho) del producto para encontrar la disposición que coincide exactamente con el ancho interno del contenedor, eliminando el juego lateral en su origen.

**② Lógica de carga profunda primero**

Carga desde la parte trasera del contenedor hacia adelante, mantiene el centro de gravedad estable y hace sencilla la descarga por el lado de la puerta — coherente con la práctica de campo estándar.

**③ Gestión de amortiguación en cuatro lados**

Al maximizar el aprovechamiento del espacio, controla la distribución de holguras entre la carga y todas las paredes interiores, reduciendo el riesgo de impacto de la carga por vibraciones del transporte.

**④ Estabilización del centro de gravedad basada en física**

Aplica estrictamente la secuencia «abajo primero → atrás primero», evitando que la carga quede suelta y manteniendo el centro de gravedad del vehículo hacia adelante, conforme a las normas de seguridad del transporte por carretera.

---

## 📋 Manual de operación

**Paso 1: Abrir el simulador**

[Haz clic aquí para abrir el simulador →](https://hyvoid.github.io/Universal-3D-Cargo-Loading-Optimization-Simulator/)

**Paso 2: Introducir parámetros** (unidad: **cm**)

| Parámetro | Descripción |
|-----------|-------------|
| 🚚 Dimensiones del contenedor | Largo, ancho y alto internos realmente utilizables de su camión o contenedor |
| 📦 Dimensiones del producto | Largo, ancho y alto exteriores de la caja de cartón (la altura queda fija hacia arriba; el algoritmo solo intercambia largo y ancho) |
| 🎯 Cantidad objetivo de carga | Introduzca su cantidad de pedido; déjelo vacío o ponga `0` para calcular la capacidad máxima del contenedor |

**Paso 3: Generar plan**

Haga clic en el botón azul **«Generar plan 3D óptimo»**. El sistema ejecuta el cálculo y produce automáticamente una visualización 3D.

**Paso 4: Interactuar y revisar**

| Acción | Función |
|--------|----------|
| 🖱️ Clic izquierdo y arrastrar | Rotación panorámica de 360° |
| 🖱️ Clic derecho y arrastrar | Desplazar la vista |
| ⚙️ Rueda del ratón | Acercar para detalle o alejar para vista general |
| 📊 Panel de estadísticas | Aparece automáticamente tras la generación y muestra el límite de capacidad, las anchuras de holgura y el espacio restante cerca de la puerta |

---

## 📌 Ejemplo

**Escenario**: Un embarcador planea despachar 800 cajas. Cada caja de cartón mide 60×40×30 cm (dimensiones exteriores). El contenedor previsto tiene dimensiones internas de 1200×240×260 cm.

**Entrada**: Introduzca las dimensiones anteriores en el panel de control, ajuste la cantidad objetivo de carga en `800` y haga clic en «Generar plan 3D óptimo».

**Salida**: El sistema selecciona la orientación que mejor se ajusta al ancho del contenedor, renderiza la disposición completa capa por capa en 3D y produce: cantidad realmente cargable, holgura lateral por fila y espacio muerto longitudinal en la parte trasera.

**Referencia de decisión**: Si el plan óptimo produce 780 cajas contra un objetivo de 800, el embarcador puede evaluar si divide el envío, ajusta las dimensiones del cartón o confirma una tolerancia aceptable con el comprador.

---

## ⚠️ Limitaciones

- Admite **una sola especificación de producto** — la carga mixta multi-SKU aún no está disponible
- El algoritmo opera sobre fronteras físicas absolutas. Para operaciones reales, se recomienda **restar un margen de tolerancia de 25 cm** a las dimensiones del contenedor para contemplar la deformación del cartón, la desviación de apilado y el espacio de trabajo
- No apto para perecederos de cadena de frío, mercancía frágil o carga que requiera sujeción especializada
- El render 3D es una ilustración de planificación, no un documento formal de instrucciones de carga

---

## 🔬 Acerca del método

Este simulador usa un **algoritmo exhaustivo determinista** — no búsqueda heurística ni generación por IA. Entradas idénticas producen siempre salidas idénticas; el proceso es completamente reproducible.

Pila tecnológica: HTML5 / CSS3 / JavaScript (ES6), [Three.js](https://threejs.org/) (motor de renderizado 3D WebGL), [Tailwind CSS](https://tailwindcss.com/) (cargado vía CDN). Toda la herramienta está empaquetada como un **único archivo `.html`** — no requiere Node.js, Python ni base de datos. Haga doble clic y ejecútelo en cualquier navegador moderno.

**Esta herramienta es completamente gratuita para la planificación de carga seca estándar. No apta para perecederos de cadena de frío ni artículos frágiles.**

---

## 📄 Licencia

Este proyecto está licenciado bajo la **MIT License** — libre de usar, modificar y distribuir con atribución.
