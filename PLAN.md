# PLAN.md — andreu-marbor.github.io

Este sitio está **terminado y en mantenimiento** — no es un proyecto por fases como los
juegos. Este plan documenta el estado y el mantenimiento previsto.

## Estado

- ✅ Portfolio publicado en la raíz del dominio (ES/EN, estático, sin build).
- ✅ `.well-known/assetlinks.json` sirviendo para 3 apps Android (tresenraya, sudoku,
  quizophistoria).
- ✅ Validado: W3C Nu 0 mensajes · csstree 0 errores · axe-core 0 violaciones · sin overflow
  horizontal de 320 a 1440 px.

## Mantenimiento previsto

1. **Contenido:** mantener paridad ES/EN en cada edición (mismas secciones/id en `index.html`
   y `en.html`); verificar `hreflang`/`canonical` y enlaces externos (ver README).
2. **assetlinks de nuevas TWAs:** al publicar en Play Store `trencadis`, `triunfo` y
   `rompeolas` (y cualquier futura TWA), añadir su bloque a `.well-known/assetlinks.json`
   (huella `AA:BB:…` mayúsculas) y verificar con el validador de Google.
3. **Portfolio con los proyectos nuevos:** cuando los juegos nuevos estén publicados,
   añadirlos a la sección 03 (Proyectos) en ambos idiomas, con el mismo patrón
   (problema/arquitectura/decisiones).
4. **Certificaciones/enlaces:** si aparecen enlaces de verificación de las credenciales,
   añadirlos (el README indica que hoy no los hay).

## Fuera de alcance

Build, frameworks, JavaScript, CMS, analytics — el sitio es deliberadamente mínimo.
