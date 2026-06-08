# 412 — El Programa de Fútbol ⚽

Sitio web oficial de **412**, el programa de streaming de debate de fútbol y entretenimiento.

📺 **Emisión:** Lunes y Viernes a las 22:00 hs (Argentina) en [Kick](https://kick.com)
📹 **VODs:** [YouTube @programa412](https://youtube.com/@programa412)

## Conductores

- **Davo Xeneize** — [@davoxeneize](https://kick.com/davoxeneize)
- **La Cobra** — [@lacobraaa](https://kick.com/lacobraaa)
- **Teo D'Elia**
- **Benito SDR**
- **Agusneta**

## Stack

- [Astro](https://astro.build) — Framework SSG con islands architecture
- [Tailwind CSS v4](https://tailwindcss.com) — Utilidades CSS
- [GSAP](https://gsap.com) — Animaciones de alto rendimiento y scroll-driven

## Desarrollo

```bash
# Instalar dependencias
bun install

# Dev server (localhost:4321)
bun run dev

# Build de producción
bun run build

# Preview del build
bun run preview

# Formatear código
bun run format

# Linting
bun run lint
```

## Estructura

```
src/
├── assets/images/    # Imágenes de conductores y logo
├── components/       # Componentes Astro (futuro)
├── layouts/          # Layout base
├── pages/            # Páginas (index.astro)
└── styles/           # Tailwind CSS global
```

Para más detalle técnico, ver [PROJECT_BLUEPRINT.md](./PROJECT_BLUEPRINT.md).

## Licencia

[MIT](./LICENSE)
