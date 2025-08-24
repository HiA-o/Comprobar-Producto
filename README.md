# 🥗 Analizador de Saludabilidad de Productos - Open Food Facts

Aplicación web que permite analizar la saludabilidad de productos alimenticios utilizando la **API de Open Food Facts**.  
Introduce un **código de barras (EAN)** o una **URL de producto**, y la app generará una **nota de saludabilidad (1 a 10)** basada en diversos factores nutricionales.
> Puedes probar la herramienta en vivo aquí:  
> **[🔗 Comprobar Producto - Demo en Vivo](https://hia-o.github.io/Comprobar-Producto/)**

---

## 🚀 Características
- 🔢 **Entrada flexible**: acepta códigos de barras (EAN de 8 a 14 dígitos) o URLs de Open Food Facts.  
- 🧠 **Nota de saludabilidad**: calcula una puntuación personalizada basada en una heurística que considera:
  - Nutri-Score (opcional, activado por defecto).  
  - NOVA (nivel de procesamiento, penaliza ultraprocesados).  
  - Aditivos (penaliza según cantidad y controversia).  
  - Azúcares, grasas saturadas, sal, fibra, proteína y frutas/verduras.  
- ⚠️ **Modo estricto (opcional)**: penaliza más el azúcar y los productos NOVA 4.  
- 🧼 **Interfaz limpia**: muestra ingredientes, nutrientes, aditivos y los motivos de la puntuación.  
- 🧪 **Demos incluidas**: botones para probar con productos de ejemplo (yogur, natillas, galletas).  
- 📋 **Copia rápida**: botón para copiar un resumen del producto al portapapeles.  
- 🔧 **Depuración**: sección técnica con datos en bruto (JSON).  
- 🗂 **Sin almacenamiento**: todo se procesa en el cliente. No se guardan datos.  

---

## 🛠 Tecnologías utilizadas
- 🌐 **HTML5 & CSS3** → diseño responsive con grid y media queries.  
- ⚙️ **JavaScript (ES6+)** → lógica de análisis, consultas a API y generación de puntuaciones.  
- 📡 **Open Food Facts API** → fuente de datos y taxonomías de aditivos.  
- ❌ **Sin dependencias externas** → código puro, sin frameworks ni librerías externas.

---

## 📦 Instalación y uso

1. Clona el repositorio
`git clone https://github.com/<tu-usuario>/<nombre-del-repositorio>.git`

2. Abre la aplicación
Abre el archivo index.html en un navegador.<br>
💡 Opcional: Si prefieres un servidor local:
`python -m http.server 8000`

3. Luego abre en tu navegador: http://localhost:8000

---

## ⚙️ Uso
1. Introduce un **código de barras** (ej. `8410100082930`) o una **URL de Open Food Facts** (ej. `https://es.openfoodfacts.org/producto/8410100082930`).  
2. Haz clic en **"Analizar"** para obtener el resumen y la puntuación.  
3. Usa los **botones de demo** para probar con productos predefinidos.  
4. Activa/desactiva:  
- ✅ **Modo estricto**  
- ✅ **Usar Nutri-Score**  
5. Haz clic en **"Copiar resumen"** para copiar los datos.  

---

## 🧠 Notas técnicas
### 📡 API utilizada
- Producto:  
  `https://world.openfoodfacts.org/api/v2/product/<código>.json`  
- Taxonomía de aditivos:  
  `https://static.openfoodfacts.org/data/taxonomies/additives.json`

### 🔐 CORS
Consultas con `mode: "cors"` para compatibilidad con navegadores.  

### 📈 Heurística de puntuación
- **Puntuación base**: 10  
- **Penalizaciones**:  
  - NOVA (grado de procesado) → hasta -3.0
  - Nutri-Score D/E → hasta -3.0
  - Azúcares → hasta -3.5 
  - Grasas saturadas → hasta -2.5
  - Grasas trans → -4.0 (si las contiene)
  - Sal → hasta -2.5
  - Aditivos → penalización por cantidad y riesgo.
  - Aromas sin fruta → hasta -0.8
  - Alto valor calórico → hasta -1.5
  - 0% de fruta/verdura/nueces → -0.8
  - Alcohol → -2.0
  - Cafeína → -1.0
- **Bonificaciones**:  
  - Nutri-Score A/B → hasta +1.2
  - Energía muy baja (≤50 kcal) → +0.5
  - Fibra → hasta +1.0
  - Proteína → hasta +0.5
  - Buena proporción de FVH (frutas, verduras, frutos secos) → +0.6
  - Sin azúcares → +0.4
  - Grasas saturadas muy bajas (<1g) → +0.2
  - Micronutrientes (Calcio, Hierro, Vitamina C/D) → hasta +0.8

👉 **Rango final**: de 1 a 10  

---

## ⚠️ Limitaciones
- Depende de la **calidad de los datos** en Open Food Facts.  
- Los **códigos de demo** pueden no estar disponibles en todas las regiones.  
- La **taxonomía de aditivos** puede fallar si la API no responde (fallback vacío).  

---
## 📝 Licencia
Este proyecto está bajo la **licencia MIT**.  
Consulta el archivo [LICENSE](LICENSE) para más información.  

---

## 🙌 Créditos
- **Open Food Facts** → Base de datos abierta de productos alimenticios.  
