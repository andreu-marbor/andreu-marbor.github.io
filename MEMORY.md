# MEMORY.md — andreu-marbor.github.io

Registro de cambios, incidencias y estado. **Solo aditivo**: nunca borrar ni reescribir
entradas anteriores; corregir añadiendo una entrada nueva.

---

## 2026-10-16 — Creación de MEMORY.md y PLAN.md

**Qué:** el sitio nace con un README exhaustivo pero sin MEMORY/PLAN; se crean ambos ficheros
para alinearlo con el patrón de la carpeta (AGENTS.md + MEMORY.md + PLAN.md en todo proyecto).

**Historial resumido (del log de git, hasta hoy):**

- Rediseño del portfolio como sitio estático ES/EN sin build (cero JS, un CSS, axe-core 0
  incumplimientos, W3C Nu 0 mensajes) — decisiones detalladas en el `README.md`.
- `assetlinks.json`: sentencia de `com.andreumarbor.quizophistoria` añadida; huella de
  `com.andreumarbor.tresenraya` actualizada (keystore nuevo); **todas las huellas pasadas a
  formato `AA:BB:…` mayúsculas** (Google rechazaba hex plano con `ERROR_CODE_MALFORMED_CONTENT`).
- Sentencia de `com.andreumarbor.sudoku` añadida (keystore compartido con tresenraya).
- Sección de proyectos del portfolio ampliada (CatFoodCheck, 3 en raya, Quiz Historia,
  Sudoku) y posicionamiento como Lead Software Engineer.

**Estado git:** rama local `master`, remota `main`, mismo commit, sin upstream — push con
`git push origin HEAD:main`. Sin cambios pendientes en el working tree.

**Pendiente (cuando toque):** añadir las sentencias de `com.andreumarbor.trencadis`,
`com.andreumarbor.triunfo` y `com.andreumarbor.rompeolas` cuando esas TWAs se publiquen;
valorar si el portfolio añade esos proyectos a la sección "Proyectos".
