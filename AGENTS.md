# PROMPT DE CONTEXTO DE AGENTE: PROYECTO WEB "412"

## 1. OBJETIVO DEL SISTEMA

Estás asistiendo en el desarrollo de la plataforma web oficial para el programa de streaming de fútbol **"412"** (conducido por Davo Xeneize, La Cobra, Teo D'Elia, Benito SDR y Agusneta). El objetivo de la web es centralizar el contenido on-demand, el estado de las transmisiones en vivo, secciones interactivas para la comunidad y la identidad visual del show.

---

## 2. STACK TECNOLÓGICO OBLIGATORIO

El proyecto se construye estrictamente bajo las siguientes tecnologías. No propongas alternativas fuera de este stack:

- **Framework:** Astro (orientado a rendimiento, arquitectura de islas para componentes interactivos).
- **Estilos:** Tailwind CSS (diseño responsivo, utilidades nativas, consistencia visual rápida).
- **Animaciones:** GSAP - GreenSock Animation Platform (para transiciones de interfaz de alto rendimiento, efectos de scroll y micro-interacciones dinámicas).

---

## 3. PROTOCOLO DE HERRAMIENTAS Y SKILLS (`.agents`)

- **Ubicación de Herramientas:** En el mismo directorio raíz donde se encuentra este archivo Markdown, existe una carpeta denominada `.agents/`.
- **Instrucción Operativa:** Debes escanear, cargar y utilizar activamente las habilidades, scripts o prompts de comportamiento almacenados dentro de la carpeta `.agents` para ejecutar tareas de generación de código, formateo o despliegue. No asumas flujos de trabajo sin consultar primero los archivos de esa carpeta.

---

## 4. PROTOCOLO OBLIGATORIO DE FLUJO DE TRABAJO: PROJECT BLUEPRINT

Para garantizar la consistencia de la arquitectura de la app, debes implementar el siguiente ciclo en **cada consulta del usuario**:

1.  **Verificación Inicial (Cada Consulta):** Antes de responder o generar código, revisa el estado actual del _Project Blueprint_ (Mapa/Planos del Proyecto) para asegurarte de que tus sugerencias no rompan la estructura existente.
2.  **Creación del Blueprint:** Si aún no existe, debes definir un _Project Blueprint_ inicial que detalle la estructura de carpetas, componentes clave de Astro, configuración de Tailwind y los timelines principales de GSAP.
3.  **Adaptación por Cambios Mayores:** Cada vez que el usuario solicite un cambio estructural importante (ej. agregar un sistema de votaciones en tiempo real, cambiar la API de Kick/YouTube, reestructurar layouts nativos de Astro), debes **actualizar el Project Blueprint primero** y mostrar la versión modificada antes de proceder con el código detallado.

---

## 5. ENTIDAD DEL PROYECTO ("412")

Para tu contexto de generación de contenido y componentes:

- **Qué es:** Programa de streaming de debate de fútbol y entretenimiento.
- **Emisión:** Lunes y Viernes 22:00 hs (Arg) en Kick. VODs en YouTube (`@programa412`).
- **Conductores:** Davo Xeneize, La Cobra, Teo D'Elia, Benito SDR, Agusneta.
- **Estética sugerida para código:** Identidad futbolística, moderna, oscura (dark mode nativo ideal para audiencias de streaming), con secciones dinámicas (widgets de "en vivo", contadores, tiers de ligas, etc.).

---

## 6. CONFIRMACIÓN DE ENTRADA

Si has procesado correctamente este archivo de contexto, responde al usuario confirmando:

1. La lectura del stack (Astro + Tailwind + GSAP).
2. La detección de la carpeta `.agents`.
3. El despliegue o estado actual del **Project Blueprint** inicial para comenzar a trabajar.

---

## 7. REGLAS TÉCNICAS ESPECÍFICAS

- **Evitar `overflow-x: hidden` Global:** No apliques `overflow-x: hidden` a todo el documento (`html` o `body`), ya que interfiere y rompe el cálculo de dimensiones y la posición de scroll de GSAP ScrollTrigger. Para solucionar desbordamientos horizontales, aplicalo localmente al contenedor específico que los genera.
