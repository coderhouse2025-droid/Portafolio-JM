<img width="2239" height="1397" alt="Perfil_de_Juan_Manuel_Orellana" src="https://github.com/user-attachments/assets/59700793-5194-433f-91e4-18b30d959fa5" />



# 🌐 Juan Manuel Orellana — Portafolio Personal · Data Science & Analytics

[![Live Site](https://img.shields.io/badge/Live-Site-brightgreen?style=for-the-badge)](https://coderhouse2025-droid.github.io/tuusuario.github.io/)
[![GitHub Pages](https://img.shields.io/badge/Hosting-GitHub_Pages-181717?style=for-the-badge&logo=github)](https://pages.github.com/)
[![Vanilla JS](https://img.shields.io/badge/Stack-Vanilla_JS-F7DF1E?style=for-the-badge&logo=javascript)](https://developer.mozilla.org/en-US/docs/Web/JavaScript)

> Sitio web de portafolio personal desarrollado con HTML, CSS y JavaScript puro, alojado en GitHub Pages. Presenta mi perfil profesional, habilidades, proyectos de Data Science / Analytics y un formulario de contacto.

🔗 **Live site:** https://coderhouse2025-droid.github.io/Portafolio-JM/

---

## 📋 Índice

- [Descripción](#-descripción)
- [Objetivo del portafolio](#-objetivo-del-portafolio)
- [Decisiones técnicas y su justificación](#-decisiones-técnicas-y-su-justificación)
- [Arquitectura del sitio](#-arquitectura-del-sitio)
- [Pipeline de datos: de repositorios de GitHub a grilla de proyectos](#-pipeline-de-datos-de-repositorios-de-github-a-grilla-de-proyectos)
- [¿Por qué este camino y no otro?](#-por-qué-este-camino-y-no-otro)
- [Funcionalidades](#-funcionalidades)
- [Estructura del proyecto](#-estructura-del-proyecto)
- [Instalación local](#️-instalación-local)
- [Roadmap](#-roadmap)

---

## 📊 Descripción

Sitio web personal que centraliza mi trayectoria en Data Science, Machine Learning y Analítica de Negocios. Combina mi experiencia previa en **control de gestión y administración** con herramientas modernas de ciencia de datos.

Los proyectos se cargan dinámicamente desde la **API pública de GitHub**, lo que garantiza que el contenido siempre refleja el estado actual del perfil sin necesidad de actualizar el sitio manualmente.

---

## 🎯 Objetivo del portafolio

Vengo de una trayectoria en control de gestión y administración, y estoy transitando hacia Data Science y Analytics. Ese perfil es difícil de comunicar en un CV estándar: no soy desarrollador puro ni analista de negocio tradicional, y esa combinación es precisamente el valor que quiero mostrar.

Un portafolio en HTML propio me permite hacer exactamente eso — **mostrar el trabajo en lugar de describirlo**. Cada proyecto está vinculado a su repositorio real, con el código, las decisiones técnicas y el contexto del problema que resuelve. Quien lo visita puede verificar el nivel de trabajo directamente, sin intermediarios.

También es una decisión consciente frente a las alternativas: LinkedIn y Kaggle tienen un formato igual para todos. Un sitio propio me permite organizar el contenido según mi narrativa, destacar lo que considero relevante, y actualizar la disponibilidad laboral en tiempo real. Y construirlo en HTML/CSS/JS puro — sin frameworks — es en sí mismo parte de lo que quiero comunicar: que entiendo los fundamentos, no solo las abstracciones.

---

## 🧠 Decisiones técnicas y su justificación

### 1. HTML + CSS + JavaScript Vanilla — no React, no Next.js

**¿Por qué Vanilla?**

Un portafolio personal es fundamentalmente un sitio estático: el contenido no cambia entre visitas, no hay estado complejo, no hay múltiples rutas dinámicas. Introducir React hubiera significado: un paso de build obligatorio, un bundler que configurar, dependencias que mantener, y un bundle JavaScript más pesado para el visitante.

El argumento de rendimiento es directo: un sitio en HTML/CSS/JS puro carga en ~200-400ms. Un sitio equivalente en React con hidratación puede tardar 1-2 segundos en ser interactivo. Para un portafolio donde el reclutador decide en los primeros segundos si seguir leyendo, la velocidad de carga es parte de la impresión.

Además, un portafolio en Vanilla JS es en sí mismo una demostración de que el profesional conoce los fundamentos del desarrollo web sin depender de abstracciones — señal técnica relevante.

**¿Cuándo elegiría React en su lugar?**

Si el portafolio tuviera múltiples páginas con navegación SPA, un sistema de filtrado complejo con estado compartido entre componentes, o la necesidad de integrar librerías de componentes de UI sofisticadas. Para este scope, no aplica.

---

### 2. CSS Puro — no Tailwind, no Bootstrap

**¿Por qué CSS propio?**

La decisión tiene dos dimensiones: técnica y de diseño. Técnicamente, un portafolio sin framework CSS tiene cero dependencias externas de estilos — no hay CDN que pueda caer, no hay versión que deprecarse. El sitio funciona igual en 5 años.

En diseño, la motivación es más importante: un portafolio con estilos de Tailwind o Bootstrap *parece* hecho con Tailwind o Bootstrap. Los patrones visuales de estos frameworks son reconocibles. CSS propio permite construir una identidad visual genuinamente personal — las animaciones de blobs flotantes, el ring giratorio del avatar, los gradientes específicos — que no son posibles o naturales en frameworks utilitarios.

**¿Cuándo elegiría Tailwind?**

En un proyecto de equipo, donde la consistencia de convenciones CSS es más importante que la identidad visual individual. Para un portafolio personal, CSS propio es la elección correcta.

---

### 3. GitHub REST API v3 — proyectos cargados dinámicamente

**¿Por qué consumir la API de GitHub en lugar de hardcodear los proyectos?**

La alternativa obvia es escribir el HTML de cada proyecto directamente en el sitio. El problema: cada vez que se crea, actualiza o completa un proyecto en GitHub, habría que también actualizar el portafolio manualmente — dos fuentes de verdad que se desincronizarán inevitablemente.

La GitHub API convierte al repositorio en la **fuente única de verdad**. El portafolio la consulta en runtime y renderiza los proyectos según su estado actual: nombre, descripción, topics (usados como categorías), stars, y fecha de última actualización.

**Lógica de filtrado por topics:**

```javascript
// Solo se muestran repositorios etiquetados con topics relevantes
const CATEGORIAS_VISIBLES = ['machine-learning', 'data-analysis', 'bi', 'nlp', 'deep-learning'];

const proyectosFiltrados = repos.filter(repo =>
  repo.topics.some(topic => CATEGORIAS_VISIBLES.includes(topic))
);
```

Esto permite controlar qué proyectos aparecen en el portafolio simplemente administrando los topics en GitHub — sin tocar el código del sitio.

**¿Por qué no GraphQL API v4 de GitHub?**

La API v4 requiere autenticación para todas las llamadas. La API REST v3 permite consultas públicas sin token para repositorios públicos, lo que elimina la necesidad de gestionar secretos en un sitio estático desplegado en GitHub Pages.

---

### 4. EmailJS — formulario de contacto sin backend

**¿Por qué EmailJS?**

El problema clásico del formulario de contacto en un sitio estático: no hay servidor que procese el envío. Las alternativas son: crear un backend (infraestructura, costo, mantenimiento), usar Formspree o Netlify Forms (dependencia de terceros con límites en el tier gratuito), o EmailJS.

EmailJS ejecuta el envío desde el frontend llamando a su API con credenciales del servicio de email configurado. El email llega directamente a la casilla configurada, sin intermediarios adicionales ni pasos manuales.

**Trade-off aceptado:** las credenciales de EmailJS quedan expuestas en el código del cliente. Esto es una limitación conocida del servicio — está documentada y mitigada por el hecho de que un atacante solo podría *enviar emails desde el formulario*, no acceder a la bandeja de entrada. Para un formulario de contacto personal, este riesgo es aceptable.

---

### 5. GitHub Pages — no Vercel, no Netlify

**¿Por qué GitHub Pages?**

Para un sitio estático sin funciones serverless ni variables de entorno críticas, GitHub Pages es la opción que más reduce la fricción operativa: el deploy es automático con cada `git push`, no requiere cuenta en plataforma adicional, y la URL `usuario.github.io` es en sí misma una señal profesional reconocida en el mundo tech.

Comparado con Vercel: Vercel agrega valor concreto cuando hay serverless functions, edge middleware, o un framework como Next.js. Para HTML/CSS/JS puro sin lógica de servidor, es una capa innecesaria.

Comparado con Netlify: similar razonamiento. Netlify tiene ventajas para forms, functions y A/B testing. Ninguna aplica aquí.

---

### 6. Google Fonts (Playfair Display + DM Sans + Space Mono) — tipografía deliberada

**¿Por qué tres familias tipográficas?**

Cada familia cumple un rol semántico específico y comunica algo del perfil:

| Fuente | Uso | Por qué |
|--------|-----|---------|
| Playfair Display | Títulos principales, nombre | Serif elegante que comunica autoridad y trayectoria — conecta con el perfil de gestión y negocios |
| DM Sans | Texto de cuerpo, descripciones | Sans-serif moderna y legible — conecta con el perfil técnico y contemporáneo |
| Space Mono | Snippets de código, etiquetas técnicas | Monoespaciada que señala explícitamente competencia técnica |

Esta combinación no es estética arbitraria — es comunicación de marca personal. La tensión visual entre una serif clásica y una monoespaciada técnica refleja exactamente el perfil híbrido negocio + datos.

---

## 🏗️ Arquitectura del sitio

```
Visitante (browser)
      ↓
GitHub Pages (CDN global, HTTPS automático)
      ↓
index.html  ←── CSS propio (animaciones, grid, variables)
      ↓
JavaScript (ES6+ vanilla)
      ├── Fetch → GitHub REST API v3
      │   └── Repositorios públicos → filtrado por topics → render en grilla
      ├── EmailJS SDK
      │   └── Formulario de contacto → envío a email configurado
      └── DOM manipulation
          └── Modal CV, filtros de proyectos, animaciones de scroll
```

**Principio de diseño:** cero dependencias de servidor propio. Todo el sitio funciona desde archivos estáticos. Las únicas llamadas externas en runtime son a la GitHub API (datos de proyectos) y EmailJS (envío de contacto) — ambas con fallback visual si fallan.

---

## 🔄 Pipeline de datos: de repositorios de GitHub a grilla de proyectos

Este es el flujo de datos más técnico del sitio. Se documenta cada paso y las decisiones de transformación.

### El "dataset": repositorios públicos de GitHub

La fuente de datos son los repositorios públicos del perfil. Son datos semiestructurados — cada repo tiene campos predecibles (nombre, descripción, topics, stars, fechas) pero la calidad del contenido depende de cómo se documentaron.

---

#### Problema 1: Nombres de repositorios no son títulos legibles

Los nombres de repo siguen convenciones técnicas: `prediccion-churn-telecom`, `analisis-ventas-retail-2024`, `nlp-sentiment-reviews`. No son títulos para mostrar al público.

**Transformación aplicada:**

```javascript
function formatearNombreRepo(nombre) {
  return nombre
    .replace(/-/g, ' ')           // guiones → espacios
    .replace(/_/g, ' ')           // underscores → espacios
    .replace(/\b\w/g, l => l.toUpperCase()); // Title Case
}
// "prediccion-churn-telecom" → "Prediccion Churn Telecom"
```

**¿Por qué no usar el campo `name` directamente?**

Porque el nombre del repo es un identificador técnico, no un título de presentación. Un reclutador ve "Prediccion Churn Telecom" como título de tarjeta y entiende inmediatamente el tema. Ver `prediccion-churn-telecom` en formato slug rompe la experiencia visual.

---

#### Problema 2: Descripciones ausentes o inconsistentes

No todos los repositorios tienen descripción en GitHub. Algunos tienen descripciones técnicas pensadas para otros desarrolladores, no para reclutadores.

**Transformación aplicada:**

```javascript
const descripcion = repo.description
  ? repo.description.slice(0, 120) + (repo.description.length > 120 ? '...' : '')
  : 'Proyecto de Data Science — ver repositorio para más detalles.';
```

Dos decisiones aquí: truncado a 120 caracteres para mantener consistencia visual en la grilla (todas las tarjetas tienen la misma altura), y un fallback genérico que no deja tarjetas vacías.

---

#### Problema 3: Topics como sistema de categorización

Los topics de GitHub son strings libres — un repositorio puede tener `Machine-Learning`, `machine_learning`, `ml`, `Machine Learning` como variantes del mismo concepto.

**Transformación aplicada — normalización de topics:**

```javascript
const topicsNormalizados = repo.topics.map(t =>
  t.toLowerCase().replace(/\s+/g, '-')
);
```

Y un mapa de equivalencias para los casos más comunes:

```javascript
const TOPIC_ALIASES = {
  'ml': 'machine-learning',
  'deep-learning': 'machine-learning',
  'nlp': 'machine-learning',
  'data-science': 'data-analysis',
  'analytics': 'data-analysis',
  'tableau': 'bi',
  'power-bi': 'bi'
};
```

**¿Por qué este mapa y no filtrar exacto?**

Porque los topics se administran en GitHub de forma orgánica — no siempre se recuerda el exacto que usa el sitio. El mapa de aliases permite flexibilidad en el etiquetado sin romper la categorización del portafolio.

---

#### Problema 4: Ordenamiento — qué proyectos mostrar primero

La API de GitHub devuelve los repos ordenados por fecha de creación por defecto. Para un portafolio, el orden correcto no es cronológico sino por relevancia.

**Estrategia de ordenamiento:**

```javascript
const proyectosOrdenados = proyectosFiltrados.sort((a, b) => {
  // 1. Primero los que tienen descripción (más completos)
  const aDescripcion = a.description ? 1 : 0;
  const bDescripcion = b.description ? 1 : 0;
  if (bDescripcion !== aDescripcion) return bDescripcion - aDescripcion;

  // 2. Luego por stars (señal de calidad percibida)
  if (b.stargazers_count !== a.stargazers_count)
    return b.stargazers_count - a.stargazers_count;

  // 3. Finalmente por fecha de actualización (más reciente primero)
  return new Date(b.updated_at) - new Date(a.updated_at);
});
```

**Justificación:** un proyecto sin descripción visualmente incompleto no debería ser lo primero que ve el reclutador. La descripción es un proxy de qué tan bien documentado está el trabajo.

---

#### Problema 5: Rate limiting de la GitHub API

La API pública de GitHub permite 60 requests por hora por IP sin autenticación. Para un portafolio con tráfico normal, esto es suficiente. Para picos de visitas (compartir el link en una convocatoria laboral), puede ser limitante.

**Mitigación implementada:**

```javascript
// Cache en sessionStorage — una sola llamada por sesión de browser
const CACHE_KEY = 'github_repos_cache';
const cached = sessionStorage.getItem(CACHE_KEY);

if (cached) {
  renderProyectos(JSON.parse(cached));
} else {
  const repos = await fetchGitHubRepos();
  sessionStorage.setItem(CACHE_KEY, JSON.stringify(repos));
  renderProyectos(repos);
}
```

El sessionStorage vive mientras dura la pestaña del browser — un visitante que navega el sitio durante varios minutos no genera múltiples llamadas a la API.

---

## 🤔 ¿Por qué este camino y no otro?

### Alternativa descartada: Gatsby o Hugo (generadores de sitios estáticos)

Gatsby y Hugo permiten construir sitios estáticos con un sistema de componentes y contenido en Markdown. El trade-off: requieren un paso de build, una CLI instalada, y conocimiento del framework específico. Para hacer un cambio en el portafolio habría que: editar el archivo → build → deploy. Con HTML puro: editar el archivo → push → listo.

Para un sitio de una sola persona que actualiza contenido ocasionalmente, la fricción de un generador de sitios no se justifica.

### Alternativa descartada: Notion como portafolio público

Notion permite publicar páginas como sitios web de forma nativa. Es la solución de menor fricción posible. El problema: no es personalizable visualmente, la URL es un hash de Notion (`notion.site/abc123`), no transmite ninguna señal técnica, y está sujeta a los cambios de producto de Notion. Un portafolio en Notion dice "no sé hacer un sitio web". El contrario también suma.

### Alternativa descartada: Webflow / Squarespace

Plataformas no-code que generan sitios profesionales sin código. El problema en este contexto específico: un profesional que se postula a roles de Data Science con un portafolio en Webflow está perdiendo una oportunidad de demostrar que puede trabajar con tecnología. El sitio en sí es parte del portafolio.

---

## ✨ Funcionalidades

- **Hero dinámico** con animación de avatar, chips de habilidades y bio profesional
- **Sección "Sobre mí"** con datos de ubicación, formación y disponibilidad laboral
- **Grilla de habilidades** organizada por categorías (Lenguajes, ML/DL, Analítica de Negocios, Herramientas)
- **Proyectos desde GitHub API** — se cargan automáticamente y se filtran por categoría
- **Formulario de contacto** integrado con EmailJS (envío real sin backend)
- **Visor / descarga de CV** en modal sin salir del sitio
- Diseño **responsive** adaptado a móvil, tablet y desktop
- Animaciones CSS fluidas (blobs flotantes, ring giratorio en avatar, fade-in por scroll)

---

## 📁 Estructura del proyecto

```
/
├── index.html              # Estructura completa del sitio (semántica HTML5)
├── styles/
│   ├── main.css            # Variables globales, reset, tipografía
│   ├── layout.css          # Grid, flexbox, secciones
│   ├── components.css      # Tarjetas, botones, chips, modal
│   └── animations.css      # Keyframes: blobs, ring, fade-in, slide-up
├── scripts/
│   ├── github-api.js       # Fetch, transformaciones y render de proyectos
│   ├── contact.js          # Integración EmailJS + validación de formulario
│   └── ui.js               # Navegación, modal CV, scroll animations
├── CV/
│   └── JM_Orellana_CV.pdf  # CV descargable (actualizar con cada versión)
├── assets/
│   └── avatar.jpg          # Foto de perfil
└── README.md
```

---

## ⚙️ Instalación local

```bash
git clone https://coderhouse2025-droid.github.io/Portafolio-JM/
```

Abrir directamente en el browser:
```
index.html
```

O con live-server para hot reload:
```bash
npm install -g live-server
live-server
```

No requiere build step ni variables de entorno para visualización local. El formulario de contacto requiere credenciales de EmailJS configuradas en `scripts/contact.js`.

---

## 🧩 Roadmap

| Prioridad | Mejora | Justificación |
|-----------|--------|---------------|
| Alta | 📊 Sección de análisis exploratorio inline | Mostrar gráficos de proyectos directamente en el portafolio, sin redirigir a Jupyter |
| Alta | 🌙 Modo oscuro | Preferencia estándar en el mercado tech; reduce fatiga visual |
| Media | 🌎 Versión en inglés | Amplía el alcance a posiciones remotas internacionales |
| Media | 📈 Analytics de visitas | Entender qué proyectos atraen más atención para priorizar desarrollo |
| Baja | 🔗 Integración con LinkedIn API | Sincronizar experiencia laboral automáticamente |

---

## 👤 Autor

**Juan Manuel Orellana**
Data Science · ML · Analítica de Negocios · Control de Gestión

---

## 📄 Licencia

MIT License — libre para uso como referencia o inspiración para portafolios propios.
