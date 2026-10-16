# AGENTS.md — andreu-marbor.github.io

## Qué es esto

Portfolio **estático en la raíz del dominio** `https://andreu-marbor.github.io/` — HTML + CSS
tal cual, **sin build, sin dependencias y sin JavaScript**. Aloja además el
`.well-known/assetlinks.json` (Digital Asset Links) de **todas** las apps Android/TWA de la
carpeta. Este `AGENTS.md` resume; el **`README.md` de este repo es detallado y está
actualizado** (ficha por fichero, decisiones técnicas, validaciones) — léelo antes de editar.

- **Ficheros:** `index.html` (español, idioma por defecto) · `en.html` (inglés, misma
  estructura) · `styles.css` único con modo claro/oscuro (`prefers-color-scheme`) ·
  `images/` (avatar + favicons) · `.nojekyll` · `.well-known/assetlinks.json`.
- **Idioma del código y documentación:** español.

## Reglas duras

- **Paridad ES/EN obligatoria:** `index.html` y `en.html` deben tener las **mismas secciones,
  el mismo orden y los mismos `id`** — difieren solo en texto y en el enlace de idioma.
  Cualquier cambio de contenido se aplica **en los dos ficheros**.
- **Cero JavaScript** (navegación por anclas, `<details>` nativo) y **un solo CSS** — si un
  cambio requiere romper esto, es una decisión de proyecto, no un detalle.
- **`.nojekyll` no se borra nunca** — sin él, Pages procesa con Jekyll y `.well-known/` deja
  de servirse → las apps Android pierden el modo inmersivo (muestran la barra de URL).
- **`assetlinks.json` es crítico para los TWAs hermanos** (acoplado a sus keystores):

  | Paquete | Proyecto hermano |
  |---|---|
  | `com.andreumarbor.tresenraya` | `tres-en-raya/` |
  | `com.andreumarbor.sudoku` | `sudoku/` |
  | `com.andreumarbor.quizophistoria` | `quiz-historia/` |

  Reglas (detalladas en el README): huella en formato **`AA:BB:…` mayúsculas** (Google rechaza
  hex plano), una sentencia por app (admitidas varias), añadir bloque al publicar una TWA
  nueva, actualizar huella si cambia el keystore (cambiar solo la contraseña **no** cambia la
  huella). **Pendiente de futuras TWAs** (`trencadis`, `triunfo`, `rompeolas`): añadir su
  bloque al publicarlas en Play Store.
- Si el contenido cambia, verificar paridad ES/EN y `hreflang`/`canonical`; validaciones
  completas (W3C Nu, csstree, axe-core 0 violaciones, overflow 320–1440 px) en el README.

## Comandos / despliegue

- **Sin build y sin CI:** GitHub Pages publica la rama `main` desde la raíz; desplegar es
  `git push origin HEAD:main` (la rama local es `master`, sin upstream — misma discrepancia
  que `tres-en-raya`; ver `Repositorios/AGENTS.md` padre).

## Conexiones con los hermanos

- **Este repo es el dueño del dominio**: los proyectos (`tres-en-raya`, `sudoku`,
  `quiz-historia`, futuros...) publican en subcarpetas del mismo dominio y no se ven
  afectados por él; conviven sin pisarse.
- Tras cada push de Pages, el cacheo de Chrome puede retener un `assetlinks.json` antiguo:
  el README documenta el workaround (desinstalar app, limpiar datos de Chrome, reinstalar).

## ⚠️ Seguridad: datos sensibles — NUNCA al repo

- **Prohibido subir a git**: claves privadas, tokens, credenciales y `.env` — este repo es público en la raíz del dominio, así que cualquier secreto aquí es **instantáneamente visible**.
- **Dato especial: `assetlinks.json` no es sensible** — al revés, es público por diseño (solo contiene la huella SHA-256 pública del certificado de firma, no el keystore ni la contraseña). El keystore y sus contraseñas viven en `tres-en-raya/`/`sudoku/` (gitignored) y en `%USERPROFILE%\.bubblewrap\`.
- **Antes de cada commit:** `git status` + `git ls-files | Select-String -Pattern '(keystore|\.env|secret|passw|token|key)'` → debe salir vacío. El avatar y las imágenes sí son públicas intencionadamente.
- **Si algo se sube por error:** rotar la credencial **inmediatamente** — borrar el commit no basta (el historial conserva el dato y el repo es público).
- Auditoría recurrente: `git log --all --diff-filter=A --name-only` (auditoría 2026-10-16: los 10 proyectos de la carpeta, limpios).

## Memoria y plan

- **[MEMORY.md](./MEMORY.md)** — registro **solo aditivo** de cambios e incidencias.
  Tras cada cambio relevante, **añadir** una entrada (fecha, descripción, solución); nunca
  borrar ni reescribir entradas anteriores.
- **[PLAN.md](./PLAN.md)** — estado y mantenimiento previsto (contenido y assetlinks).
- Si cambian las secciones o las reglas de este fichero, actualizarlo.
