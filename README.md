<div align="center">

# 🌍 Vue Combos 3D

### Combos encadenados de 3 niveles con Vue 3 + Vite

Un selector de ubicación en cascada — **País → Estado/Provincia → Ciudad** — donde cada desplegable se activa y se rellena en función del anterior.

<br>

![Vue](https://img.shields.io/badge/Vue.js-3.4-42b883?style=for-the-badge&logo=vuedotjs&logoColor=white)
![Vite](https://img.shields.io/badge/Vite-5.4-646CFF?style=for-the-badge&logo=vite&logoColor=white)
![Tailwind](https://img.shields.io/badge/Tailwind_CSS-3.4-38BDF8?style=for-the-badge&logo=tailwindcss&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-ES2022-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)

</div>

---

## 📋 Tabla de contenidos

- [¿Qué es esto?](#-qué-es-esto)
- [¿Qué significa "3D"?](#-qué-significa-3d)
- [Demostración visual](#-demostración-visual)
- [Características](#-características)
- [Stack tecnológico](#-stack-tecnológico)
- [Estructura del proyecto](#-estructura-del-proyecto)
- [Puesta en marcha](#-puesta-en-marcha)
- [Cómo funciona por dentro](#-cómo-funciona-por-dentro)
- [Personalización](#-personalización)
- [Conectar con un backend real](#-conectar-con-un-backend-real)
- [Documentación adicional](#-documentación-adicional)
- [Licencia](#-licencia)

---

## 🎯 ¿Qué es esto?

**Vue Combos 3D** es una aplicación de demostración que implementa el patrón clásico de **combos encadenados** (o *dependientes*) usando **Vue 3 con la Composition API** y `<script setup>`.

El usuario elige un **país** y, automáticamente, se cargan sus **estados/provincias**. Al elegir uno, se rellenan sus **ciudades**. Cuando los tres desplegables están completos, la app muestra la selección final formateada.

Es un ejemplo ideal para aprender:

- Reactividad con `ref` y `computed`
- Gestión de estado dependiente entre varios `<select>`
- Reseteo en cascada cuando cambia un nivel superior
- Habilitar/deshabilitar controles según el flujo de selección
- Estilado limpio y responsive con Tailwind CSS

> **Nota:** en la versión actual, los datos (países, estados y ciudades) están **simulados dentro del propio componente**. En el código hay un comentario indicando que, en una aplicación real, vendrían de una API. Consulta la sección [Conectar con un backend real](#-conectar-con-un-backend-real).

---

## 🧩 ¿Qué significa "3D"?

El "3D" del nombre hace referencia a los **3 niveles Dependientes** de la cascada, **no** a gráficos tridimensionales:

```
Nivel 1          Nivel 2                 Nivel 3
┌─────────┐      ┌──────────────────┐    ┌──────────┐
│  País   │ ───▶ │ Estado/Provincia │ ──▶│  Ciudad  │
└─────────┘      └──────────────────┘    └──────────┘
```

Cada nivel depende del anterior: sin país no hay estado, y sin estado no hay ciudad.

---

## 🖼️ Demostración visual

```
┌───────────────────────────────────────┐
│         Selección de Ubicación         │
│                                        │
│  País                                  │
│  ┌──────────────────────────────────┐ │
│  │ España                        ▼  │ │
│  └──────────────────────────────────┘ │
│                                        │
│  Estado/Provincia                      │
│  ┌──────────────────────────────────┐ │
│  │ Euskadi                       ▼  │ │
│  └──────────────────────────────────┘ │
│                                        │
│  Ciudad                                │
│  ┌──────────────────────────────────┐ │
│  │ Donostia                      ▼  │ │
│  └──────────────────────────────────┘ │
│                                        │
│  ┌──────────────────────────────────┐ │
│  │ Has seleccionado:                │ │
│  │ Donostia, Euskadi, España        │ │
│  └──────────────────────────────────┘ │
└───────────────────────────────────────┘
```

Los datos de ejemplo incluyen 3 países (España, Francia, Italia), cada uno con 3 estados/regiones, y cada estado con 3 ciudades.

---

## ✨ Características

| | Característica | Descripción |
|---|---|---|
| 🔗 | **Cascada de 3 niveles** | País → Estado/Provincia → Ciudad, totalmente dependientes |
| 🔄 | **Reseteo automático** | Al cambiar un nivel superior, los inferiores se limpian solos |
| 🚫 | **Controles bloqueados** | Cada `<select>` se deshabilita hasta que su nivel padre tenga valor |
| ⚡ | **Reactividad Vue 3** | Estado gestionado con `ref` y valores derivados con `computed` |
| 🎨 | **Estilo con Tailwind** | Interfaz limpia, centrada y responsive |
| ✅ | **Resultado formateado** | Muestra la selección completa solo cuando los 3 niveles están elegidos |
| 📦 | **Cero configuración compleja** | Proyecto ligero basado en la plantilla oficial Vue + Vite |

---

## 🛠️ Stack tecnológico

| Tecnología | Versión | Uso |
|---|---|---|
| [Vue 3](https://vuejs.org/) | `^3.4.37` | Framework principal (Composition API, `<script setup>`) |
| [Vite](https://vitejs.dev/) | `^5.4.1` | Bundler y servidor de desarrollo |
| [Tailwind CSS](https://tailwindcss.com/) | `^3.4.13` | Framework de utilidades CSS |
| [PostCSS](https://postcss.org/) | `^8.4.47` | Procesado de CSS |
| [Autoprefixer](https://github.com/postcss/autoprefixer) | `^10.4.20` | Prefijos de navegador automáticos |
| [Express](https://expressjs.com/) | `^4.21.0` | Presente como dependencia (pensado para un backend; ver notas) |

> El paquete `express` figura en las dependencias, pero **el componente actual no lo usa**: la demo funciona 100% en el cliente con datos simulados.

---

## 📁 Estructura del proyecto

```
vue-combos-3d/
├── public/
│   └── vite.svg
├── src/
│   ├── assets/
│   │   └── vue.svg
│   ├── components/
│   │   └── CombosEncadenados.vue    ← ⭐ Componente principal (toda la lógica)
│   ├── App.vue                      ← Monta el componente de combos
│   ├── main.js                      ← Punto de entrada (createApp)
│   └── style.css                    ← Estilos globales
├── index.html
├── package.json
├── vite.config.js                   ← Configuración de Vite + plugin Vue
├── tailwind.config.js               ← Configuración de Tailwind
├── postcss.config.js                ← Tailwind + Autoprefixer
├── paso a paso 3D.docx              ← Guía paso a paso del proyecto
└── README.md
```

El corazón de la aplicación es **`src/components/CombosEncadenados.vue`**: un único Single File Component que contiene la plantilla, la lógica reactiva y los datos de ejemplo.

---

## 🚀 Puesta en marcha

### Requisitos previos

- **Node.js** (recomendado 18 o superior)
- **npm** (incluido con Node)

### Instalación

```bash
# 1. Clonar el repositorio
git clone https://github.com/jsersan/vue-combos-3d.git

# 2. Entrar en la carpeta
cd vue-combos-3d

# 3. Instalar dependencias
npm install
```

### Comandos disponibles

```bash
# Servidor de desarrollo con recarga en caliente
npm run dev

# Compilar para producción (genera la carpeta dist/)
npm run build

# Previsualizar la build de producción
npm run preview
```

Tras `npm run dev`, abre la URL que muestra Vite en la terminal (por defecto `http://localhost:5173`).

---

## 🔍 Cómo funciona por dentro

Toda la lógica vive en `CombosEncadenados.vue`. El flujo es el siguiente:

### 1. Estado reactivo

```js
const paisSeleccionado   = ref('')
const estadoSeleccionado = ref('')
const ciudadSeleccionada = ref('')

const estados  = ref([])   // opciones que se rellenan dinámicamente
const ciudades = ref([])
```

### 2. Carga en cascada

Cuando cambia el país (`@change="cargarEstados"`), se cargan sus estados y se **resetean** los niveles inferiores:

```js
const cargarEstados = () => {
  estados.value = estadosPorPais[paisSeleccionado.value] || []
  estadoSeleccionado.value = ''   // limpia estado
  ciudadSeleccionada.value = ''   // limpia ciudad
  ciudades.value = []
}
```

Lo mismo ocurre al elegir estado, que carga sus ciudades.

### 3. Bloqueo de niveles

Cada desplegable usa `:disabled` para no dejar avanzar hasta completar el anterior:

```html
<select :disabled="!paisSeleccionado">   <!-- Estado -->
<select :disabled="!estadoSeleccionado"> <!-- Ciudad -->
```

### 4. Resultado calculado

Una propiedad `computed` construye el texto final solo cuando los tres niveles tienen valor:

```js
const seleccionCompleta = computed(() =>
  paisSeleccionado.value && estadoSeleccionado.value && ciudadSeleccionada.value
)
```

---

## 🎨 Personalización

### Cambiar los datos

Edita los objetos al inicio del `<script setup>` de `CombosEncadenados.vue`:

```js
const paises = [
  { id: 1, nombre: 'España' },
  // añade los tuyos...
]

const estadosPorPais = {
  1: [{ id: 1, nombre: 'Euskadi' }, /* ... */],
}

const ciudadesPorEstado = {
  1: [{ id: 1, nombre: 'Vitoria' }, /* ... */],
}
```

La clave numérica de `estadosPorPais` es el `id` del país, y la de `ciudadesPorEstado` es el `id` del estado. Respeta esa correspondencia para que la cascada funcione.

### Cambiar el aspecto

Al usar Tailwind, basta con modificar las clases de utilidad en la plantilla (colores, espaciado, bordes…). También puedes extender el tema en `tailwind.config.js`.

---

## 🔌 Conectar con un backend real

Actualmente los datos están **codificados en el componente**. Para hacerlo dinámico, sustituye los objetos simulados por llamadas a una API. Un esquema posible con `fetch`:

```js
const cargarEstados = async () => {
  const res = await fetch(`/api/estados?pais=${paisSeleccionado.value}`)
  estados.value = await res.json()
  estadoSeleccionado.value = ''
  ciudadSeleccionada.value = ''
  ciudades.value = []
}
```

Dado que `express` ya figura en las dependencias, encaja bien crear un pequeño servidor Node/Express que exponga endpoints como `/api/paises`, `/api/estados` y `/api/ciudades`.

---

## 📚 Documentación adicional

El repositorio incluye el documento **`paso a paso 3D.docx`**, una guía que explica la construcción del proyecto paso a paso.

---

## 📄 Licencia

Este proyecto no incluye actualmente un archivo de licencia. Si quieres permitir su reutilización, considera añadir una licencia (por ejemplo, MIT).

---

<div align="center">

Hecho con 💚 usando **Vue 3** + **Vite** + **Tailwind CSS**

</div>
