# apuntes-visuales

Visualizaciones interactivas de temas universitarios — Sistemas Informáticos, 1er Semestre.

## Estructura

```
apuntes-visuales/
├── index.html                              ← Dashboard principal
├── assets/
│   └── shared.css                          ← Estilos compartidos
└── 1er-semestre/
    ├── inf110-sf/
    │   └── compuertas-logicas.html         ✅ disponible
    ├── fisica/                             (próximamente)
    └── matematicas/                        (próximamente)
```

## Deploy en Vercel

1. Subir este repo a GitHub
2. Entrar a [vercel.com](https://vercel.com) → New Project → importar el repo
3. Framework Preset: **Other** (es HTML estático puro)
4. Click en Deploy — listo ✅

Cada visual tiene su URL automáticamente:
```
tu-proyecto.vercel.app/
tu-proyecto.vercel.app/1er-semestre/inf110-sf/compuertas-logicas.html
```

## Agregar un nuevo visual

1. Crear el archivo en la carpeta de la materia:
   ```
   1er-semestre/inf110-sf/nuevo-tema.html
   ```
2. Usar el template de la página (copiar `compuertas-logicas.html` como base)
3. Agregar el link en `index.html` dentro del subject card correspondiente:
   ```html
   <a href="1er-semestre/inf110-sf/nuevo-tema.html" class="topic-item has-visual">
     <span class="topic-name">Nombre del tema</span>
     <span class="topic-status">● visual</span>
   </a>
   ```
4. Push al repo → Vercel redespliega automáticamente 🚀

## Convención de nombres

- Siempre `kebab-case` → `compuertas-logicas.html`, no `Compuertas Logicas.html`
- Carpetas por materia en minúsculas: `inf110-sf/`, `fisica/`, `matematicas/`
