# 412 — Project Blueprint

## Visión General

Plataforma web oficial del programa de streaming de fútbol **"412"**.
Emisión: Lunes y Viernes 22:00 hs (Argentina) en Kick. VODs en YouTube (`@programa412`).
Conductores: Davo Xeneize, La Cobra, Teo D'Elia, Benito SDR, Agusneta.

---

## Stack Tecnológico

| Capa         | Tecnología                       | Versión |
| ------------ | -------------------------------- | ------- |
| Framework    | Astro (SSG, islands)             | ^6.4.4  |
| Estilos      | Tailwind CSS v4 + Scoped CSS     | ^4.3.0  |
| Animaciones  | GSAP + ScrollTrigger             | ^3.15.0 |
| Video Player | lite-youtube-embed               | ^0.3.4  |
| Runtime      | Bun                              | ^1.3.5  |
| Linting      | ESLint + eslint-plugin-astro     | ^10.4.1 |
| Formateo     | Prettier + prettier-plugin-astro | —       |

---

## Estructura de Carpetas

```
412/
├── .agents/                  # Skills y configuración del agente de IA
│   └── skills/               # GSAP, Tailwind, Astro, SEO, A11Y, etc.
├── public/
│   ├── favicon.ico
│   └── favicon.webp
├── src/
│   ├── assets/
│   │   └── images/
│   │       ├── agus0.webp    # Recorte PNG/WebP de Agusneta
│   │       ├── teo0.webp     # Recorte PNG/WebP de Teo
│   │       ├── davo0.webp    # Recorte PNG/WebP de Davo
│   │       ├── nine0.webp    # Recorte PNG/WebP de La Cobra
│   │       ├── beno0.webp    # Recorte PNG/WebP de Benito
│   │       ├── logo.webp     # Logo 412 (con transparencia)
│   │       └── cuatrodo.webp # Asset adicional
│   ├── components/
│   │   ├── Header.astro      # Header tipo cristal animado con GSAP
│   │   ├── Footer.astro      # Footer tipo cristal con borde superior neón animado
│   │   ├── HeroSection.astro # Nueva sección Hero modular (Muchachos, Canvas, GSAP)
│   │   ├── PartidosSection.astro # Nueva sección Partidos modular (Tabs, Video, Fuego/Chispas)
│   │   ├── InfoSection.astro # Nueva sección Info modular (Kick, Próximo programa, Aura)
│   │   └── HistoriaSection.astro # Nueva sección Historia modular (Línea de tiempo animada, GSAP)
│   ├── layouts/
│   │   └── Layout.astro      # Shell HTML base (head, meta, slots, JSON-LD Schema)
│   ├── pages/
│   │   └── index.astro       # Landing page principal (Ensamblador de secciones)
│   └── styles/
│       └── global.css        # Tailwind CSS v4 import
├── AGENTS.md                 # Contexto para asistentes de IA
├── PROJECT_BLUEPRINT.md      # Este archivo
├── astro.config.mjs          # Config Astro + Tailwind Vite plugin
├── eslint.config.js          # ESLint flat config
├── .prettierrc               # Prettier config + Astro plugin
├── tsconfig.json             # TypeScript config
└── package.json
```

---

## Arquitectura de la Landing Page (`index.astro`)

### Componentes y Secciones

#### Header (`Header.astro`)

- **Estilo**: Cristal de alta calidad (Glassmorphism con `backdrop-filter: blur(12px)` y fondo `rgba(0,0,0,0.4)`).
- **Contenido**: Logo miniatura 412, enlaces de navegación con efectos hover en verde Kick (`#00E701`) y botones rápidos a redes sociales / Kick en vivo.
- **Animación**: Oculto al inicio (translateY(-100%) y opacity: 0). Se activa al pasar la sección de los muchachos con GSAP ScrollTrigger (`trigger: '.hero-section', start: 'bottom top'`), entrando suavemente con opacidad y traslación.

#### Footer (`Footer.astro`)

- **Estilo**: Cristal coincidente con el Header (Glassmorphism con `backdrop-filter: blur(12px)` y fondo `rgba(0,0,0,0.4)`).
- **Borde Superior**: Borde decorativo de 2px con gradiente neón verde Kick (`#00E701`) en movimiento horizontal continuo que emula el efecto de aura del logo.
- **Contenido**: Créditos de imágenes a Doxen Management y David Quint; créditos de desarrollo a GenaDeev con enlaces a GitHub y LinkedIn; enlaces de navegación.

#### Hero Section (`HeroSection.astro`)

- **Logo 412** con efecto de aura neón rotativa (conic-gradient + mask-image + drop-shadow).
- **Indicador de scroll** animado con neón verde.
- **Personajes** en formación V (Davo centro, flanqueado por Teo/Cobra, Agus/Beno en los extremos).
- Timeline GSAP con ScrollTrigger (`scrub: 1`, `pin: true`):
  1. Logo desaparece (blur + scale + opacity).
  2. Personajes entran desde offscreen con stagger desde el centro.
- **Hover Pixel-Perfect**: Canvas 1x1 lee el alpha del pixel bajo el cursor para ignorar zonas transparentes de los PNG. Ordena por z-index para detectar al personaje más frontal.
- **Player Cards**: Tarjetas glassmorphism con datos de cada conductor. Aparecen/desaparecen con CSS transitions controladas por JS.
- **Salida suave**: Al scrollear fuera de la zona interactiva, las cards se desvanecen y los inline styles se limpian con un delay de 400ms para que GSAP retome el control sin conflictos.

#### Partidos Section (`PartidosSection.astro`)

- **Temática de crisis**: Fondo de pared carbonizada/con cenizas (`#140d0d` a `#000000`) con graffitis de la barra ("FUERA VENDIDOS $", etc.) con tipografía `Rubik Spray Paint` y opacidades y tamaños adaptativos visibles en todas las pantallas.
- **Grietas SVG**: Dos sobrecapas vectoriales de roturas de vidrio blancas con brillo neón y opacidades reducidas (`opacity-25` y `opacity-20` respectivamente).
- **Match Card**: Tarjeta de partido con un efecto de fuego ardiendo (`fire-glow`) en su contorno muy intenso (glows compuestos rojos, naranjas y amarillos) envolviendo escudos de 412 y Luzu con drop-shadows y el marcador `6 - 6` (penales Luzu 3-2).
- **Chispas/Brasas de Fuego**: Sistema de 10 partículas ascendentes (`spark`) con trayectorias staggered, de mayor frecuencia y opacidades neón vibrantes (`radial-gradient` amarillo-naranja con filtros `drop-shadow`), simulando un incendio constante en el estudio tras la derrota.
- **Resumen en Video**: Reproductor de YouTube embebido directamente debajo de la match-card utilizando `lite-youtube-embed` para una carga ultrarrápida.
- **Tabs de Detalle**: Selector responsivo para alternar entre la línea de tiempo vertical de los goles y la grilla de penales.
- **Remoción de Placa de Crisis**: Se removió el banner metálico de crisis para limpiar el diseño y enfocarse en la visual del partido.

#### Info Section (`InfoSection.astro`)

- Logo 412 grande con aura neón rotativa (mismo efecto).
- `<h1>` con `sr-only` para SEO: "412 - EL PROGRAMA DE FÚTBOL".
- **Botón Kick** dinámico (client-side):
  - Color oficial `#00E701`, SVG oficial de Kick.
  - Calcula automáticamente si el próximo programa es Lunes (→ canal de Davo) o Viernes (→ canal de La Cobra).
- Entrada animada con GSAP `.to()` + `.animate-up` class.

#### Historia Section (`HistoriaSection.astro`)

- **Diseño**: Línea de tiempo interactiva con diseño de alternancia izquierda/derecha.
- **Contenido**: Relato histórico de aproximadamente 800 palabras estructurado en 4 hitos:
  1. *El Origen en Pandemia* (con imágenes de Davo y Teo).
  2. *El porqué del nombre* (con el logotipo oficial).
  3. *La expansión del elenco* (con imagen grupal).
  4. *El duelo con Luzu TV* (con los dos escudos en combate visual).
- **Animaciones GSAP**:
  - ScrollTrigger para la línea central de progreso, animando su altura del 0% al 100% de forma proporcional al scroll.
  - ScrollTrigger de entrada suavizada para cada tarjeta y contenedor multimedia (desplazamientos de izquierda y derecha, y escalado en los puntos de la línea de tiempo).
- **Efectos interactivos**: Efecto de brillo de vidrio interactivo en las tarjetas (`timeline-card`) que sigue la posición del cursor (`mousemove` en CSS/JS).
- **SEO integrado**: Redactado estratégicamente para responder a las preguntas más frecuentes sobre la historia, integrantes y origen del nombre.

#### Estructura SEO y Metadatos (`Layout.astro`)

- **Metadatos Avanzados**: Incorporación de etiquetas Open Graph y Twitter Cards para mejorar las previsualizaciones al compartir en redes.
- **Canonical Links**: Configurado en la dirección oficial para evitar contenido duplicado.
- **Structured Data (Schema.org)**: Implementación de script JSON-LD en el `<head>` que define las entidades principales:
  - `WebSite` para la información y descripción del sitio.
  - `CreativeWorkSeries` (Serie/Programa) con el listado oficial de actores/conductores (Davo, Teo, La Cobra, Agusneta, Beno) y productora (Doxen Management).
  - `FAQPage` con preguntas y respuestas optimizadas para Rich Results de Google sobre el origen, emisión e integrantes del programa.

---

## Decisiones Técnicas Clave

### FOUC Prevention

Los personajes tienen `visibility: hidden` in CSS y son revelados por `gsap.set()` en el `<script>`. Esto evita un flash de contenido al recargar la página.

### Hover con `style.setProperty('...', 'important')`

GSAP manipula inline styles. Para que el hover manual (grayscale, scale, z-index) tenga prioridad, se usa `!important` vía JS. La clase `.interactive` solo se agrega cuando la animación GSAP termina al 100%, evitando conflictos con el scrub.

### Tailwind CSS v4 + Scoped CSS

Se usa Tailwind para layout/spacing/flex simples. Los estilos complejos (animaciones, pseudo-elements, masks, gradientes, shadows compuestos) se mantienen en `<style>` scoped de Astro para máxima legibilidad y control.

### Aura Neón del Logo y Borde del Footer

Al ser una imagen raster (.webp), no se puede trazar el borde vectorialmente en el logo. Se usa una capa `.logo-aura` con `mask-image` y conic-gradient rotativo. En el caso del Footer, se implementa una barra superior con `linear-gradient` y brillo neón que se desplaza horizontalmente usando un keyframe de `background-position`.

---

## Scripts Disponibles

| Comando           | Acción                           |
| ----------------- | -------------------------------- |
| `bun run dev`     | Dev server en `localhost:4321`   |
| `bun run build`   | Build de producción en `./dist/` |
| `bun run preview` | Preview del build                |
| `bun run format`  | Prettier en todo el proyecto     |
| `bun run lint`    | ESLint en todo el proyecto       |

---

## Configuración de Colores

| Uso                  | Color                  | Notas                     |
| -------------------- | ---------------------- | ------------------------- |
| Kick Green (oficial) | `#00E701`              | Botón, auras, indicadores |
| Fondo principal      | `#000`                 | Dark mode nativo          |
| Fondo info-section   | `#0a120a`              | Radial gradient sutil     |
| Card border active   | `#00E701`              | Borde neón al hover       |
| Card glow            | `rgba(0, 231, 1, 0.2)` | Box-shadow inset          |
