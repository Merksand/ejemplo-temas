# CLAUDE.md — Guía para crear visuales HTML

Este archivo le indica a Claude cómo crear correctamente un nuevo visual HTML para el repo `apuntes-visuales`, desplegado en Vercel.

---

## Estructura del repo

```
apuntes-visuales/
├── index.html                        ← Dashboard principal (NO tocar la estructura, solo agregar topics)
├── assets/
│   └── shared.css                    ← Estilos globales compartidos — SIEMPRE importar esto
├── README.md
└── 1er-semestre/
    ├── inf110-sf/                    ← Sistemas informáticos
    │   └── compuertas-logicas.html   ← Ejemplo de referencia
    ├── fis100/                       ← Física (puede contener subcarpeta mapas/)
    └── mat100/                       ← Matemáticas (puede contener subcarpeta mapas/)
```

---

## Paso 1 — Crear el archivo HTML

Ubicación: `1er-semestre/<materia>/<nombre-en-kebab-case>.html`

Ejemplos válidos:
- `1er-semestre/inf110-sf/algebra-boole.html`
- `1er-semestre/fis100/cinematica.html`
- `1er-semestre/mat100/limites.html`

**Regla de nombres: siempre kebab-case, sin espacios, sin mayúsculas.**

---

## Paso 2 — Template base obligatorio

Todo HTML nuevo debe usar esta estructura. Copiar y adaptar:

```html
<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>[Nombre del tema] — [Código materia]</title>
<link rel="stylesheet" href="../../assets/shared.css">
<style>
  /* Estilos propios del visual van aquí */
  body { padding-bottom: 4rem; }
</style>
</head>
<body>

<nav class="nav">
  <div class="nav-logo">apuntes<span>/</span>visuales</div>
  <a href="../../index.html" class="nav-back">← volver al dashboard</a>
</nav>

<div class="container">

  <!-- HERO (siempre incluir) -->
  <div class="hero">
    <p class="eyebrow">[Código materia] — [Nombre materia]</p>
    <h1>[Título principal] <span>[Palabra destacada]</span></h1>
    <p class="subtitle">[Descripción breve del visual]</p>
  </div>

  <!-- CONTENIDO INTERACTIVO AQUÍ -->

</div>

</body>
</html>
```

El `../../` en el `href` del CSS y del botón "volver" es correcto para archivos dentro de `1er-semestre/<materia>/`. No cambiarlo.

---

## Paso 3 — Variables CSS disponibles (shared.css)

No redefinir estos colores, usarlos directamente:

```css
/* Fondos */
--bg       #0d0d0f   (fondo principal)
--bg2      #141417   (cards, superficies)
--bg3      #1c1c21   (hover de cards)
--border   rgba(255,255,255,0.08)
--border-h rgba(255,255,255,0.18)  (hover)

/* Texto */
--text     #e8e8ec   (texto principal)
--muted    #888896   (texto secundario)
--dim      #555562   (texto apagado)

/* Colores de acento */
--teal     #1D9E75
--teal-l   #5DCAA5   (teal claro — usar para highlights)
--teal-bg  rgba(29,158,117,0.12)
--teal-bg2 rgba(29,158,117,0.22)
--amber    #EF9F27
--amber-bg rgba(239,159,39,0.12)
--red      #E24B4A
--red-bg   rgba(226,75,74,0.12)
--purple   #7F77DD
--purple-bg rgba(127,119,221,0.12)
--blue     #378ADD
--blue-bg  rgba(55,138,221,0.12)

/* Tipografía */
--mono     'JetBrains Mono', monospace
--sans     'Syne', sans-serif

/* Border radius */
--radius    12px
--radius-sm 8px
```

### Clases utilitarias ya disponibles

```css
.nav          → barra de navegación sticky (ya tiene estilos)
.nav-logo     → logo "apuntes/visuales"
.nav-back     → botón "← volver al dashboard"
.container    → max-width 960px centrado con padding
.badge        → pastilla de texto pequeña
.badge-teal / .badge-amber / .badge-purple / .badge-blue / .badge-dim
.mono         → font-family monospace
.muted        → color --muted
```

### Estilos del hero (definir en cada página)

```css
.hero { padding: 2.5rem 0 2rem; margin-bottom: 2rem; border-bottom: 1px solid var(--border); }
.eyebrow { font-family: var(--mono); font-size: 11px; letter-spacing: 0.15em; color: var(--teal-l); text-transform: uppercase; margin-bottom: 10px; }
h1 { font-size: clamp(26px, 5vw, 42px); font-weight: 800; letter-spacing: -0.03em; line-height: 1.1; margin-bottom: 10px; }
h1 span { color: var(--teal-l); }
.subtitle { font-family: var(--mono); font-size: 13px; color: var(--muted); }
```

---

## Paso 4 — Patrones de componentes reutilizables

### Card estándar

```html
<style>
  .card { background: var(--bg2); border: 1px solid var(--border); border-radius: var(--radius); padding: 16px 18px; transition: border-color .2s, background .2s; }
  .card:hover { border-color: var(--border-h); background: var(--bg3); }
</style>
<div class="card">...</div>
```

### Info box

```html
<style>
  .info-box { background: var(--bg2); border: 1px solid var(--border); border-left: 3px solid var(--teal); border-radius: var(--radius); padding: 16px 20px; margin-bottom: 1rem; }
  .info-title { font-size: 13px; font-weight: 700; color: var(--teal-l); margin-bottom: 8px; font-family: var(--mono); }
  .info-body { font-family: var(--mono); font-size: 12px; color: var(--muted); line-height: 1.8; }
  .info-body code { color: var(--amber); background: var(--amber-bg); padding: 1px 6px; border-radius: 4px; }
</style>

<!-- teal = info, cambiar border-left-color y color del title para otros acentos -->
<div class="info-box">
  <div class="info-title">Título</div>
  <div class="info-body">Texto. <code>código inline</code></div>
</div>
```

### Grid responsive

```html
<style>
  .grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(270px, 1fr)); gap: 12px; }
</style>
<div class="grid">
  <div class="card">...</div>
</div>
```

### Tabla interactiva

```css
.tt { width: 100%; border-collapse: collapse; font-family: var(--mono); font-size: 12px; }
.tt th { color: var(--dim); font-weight: 500; padding: 3px 8px; text-align: center; border-bottom: 1px solid var(--border); }
.tt td { padding: 4px 8px; text-align: center; color: var(--muted); cursor: pointer; border-radius: 4px; }
.tt tr.active td { background: rgba(255,255,255,0.06); color: var(--text); }
.tt tr.active td.out-1 { background: var(--teal-bg2); color: var(--teal-l); font-weight: 700; }
.tt tr.active td.out-0 { background: var(--red-bg); color: var(--red); font-weight: 700; }
```

---

## Paso 5 — Registrar el visual en index.html

Abrir `index.html` y dentro del subject card correspondiente, cambiar el `<div>` del tema por un `<a>`:

```html
<!-- ANTES -->
<div class="topic-item">
  <span class="topic-name">Álgebra de Boole</span>
  <span class="topic-status">próximamente</span>
</div>

<!-- DESPUÉS -->
<a href="1er-semestre/inf110-sf/algebra-boole.html" class="topic-item has-visual">
  <span class="topic-name">Álgebra de Boole</span>
  <span class="topic-status">● visual</span>
</a>
```

El contador de "Visuales disponibles" en el dashboard se actualiza solo.

---

## Reglas de diseño — no romper

1. **Dark mode siempre** — nunca fondos blancos ni claros.
2. **Fuentes**: `var(--sans)` para títulos y UI, `var(--mono)` para código, datos y labels.
3. **Sin colores hardcodeados** — usar siempre las variables de shared.css.
4. **Interactividad obligatoria** — clicks, sliders, toggles. Nada completamente estático.
5. **Responsive** — grids con `auto-fill` + `minmax`. Sin widths fijos.
6. **Siempre actualizar index.html** al agregar un nuevo visual.

---

## Referencia

Ver `1er-semestre/inf110-sf/compuertas-logicas.html` como ejemplo completo de todos los patrones aplicados.