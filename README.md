# andreu-marbor.github.io

Sitio personal y de GitHub Pages: ocupa la **raíz** del dominio
`https://andreu-marbor.github.io/`.

Es un portfolio estático en dos idiomas (español + inglés) **sin build, sin
dependencias y sin JavaScript**: HTML y CSS publicados tal cual.

## Contenido

| Archivo | Para qué sirve |
|---|---|
| `index.html` | Portfolio en **español** (idioma por defecto de la raíz). |
| `en.html` | Misma página en **inglés**. Enlace de cambio de idioma en la cabecera y en el pie. |
| `styles.css` | Hoja de estilos única compartida por ambos idiomas. Tokens de color con soporte de modo claro/oscuro (`prefers-color-scheme`). |
| `images/avatar.jpg` | Retrato profesional (448×448): hero, Open Graph y origen de los favicons. |
| `favicon.ico`, `images/favicon.png`, `images/apple-touch-icon.png` | Iconos del dominio. |
| `.nojekyll` | Impide que GitHub Pages procese el sitio con Jekyll (necesario para servir `.well-known/`). |
| `.well-known/assetlinks.json` | **Digital Asset Links** para las apps Android/TWA (ver más abajo). |

> Los repos de proyecto (`tres-en-raya`, `quiz-historia`, …) publican cada uno
> en su subcarpeta (`https://andreu-marbor.github.io/tres-en-raya/`, …). Este
> sitio no los afecta: conviven sin pisarse.

## Estructura del sitio

Secciones, en este orden y con esta jerarquía de encabezados:

1. **Hero** (`h1`): nombre, `Lead Software Engineer`, posicionamiento (experiencia
   profesional en backend, frontend, sistemas enterprise y desarrollo asistido
   por IA, más la exploración agéntica fuera del trabajo), meta de
   ubicación/experiencia y CTAs a proyectos, GitHub y LinkedIn.
2. **01 · Perfil** (`h2`): once años repartidos entre backend y frontend
   enterprise, interés por el diseño de sistemas y liderazgo técnico, Codex y
   la adopción de IA en los equipos en el trabajo, y experimentación con
   agentes fuera de él.
3. **02 · Enfoque**: seis áreas de competencia e interés (arquitectura,
   backend, APIs e integraciones, frontend y aplicaciones cliente, desarrollo
   asistido por IA, productividad).
4. **03 · Proyectos**: CatFoodCheck (API + app), 3 en raya, Quiz Historia y
   este sitio, presentados como **proyectos personales**. Cada uno con
   problema, arquitectura, decisiones y —en `<details>`— límites/incidencias.
5. **04 · Práctica y experimentación**: desarrollo asistido por IA como
   pregunta de ingeniería, separando **práctica profesional (Codex y adopción
   de IA en los equipos)** de **experimentación personal (OpenCode, agentes,
   subagents)**.
6. **05 · Trayectoria**: **experiencia profesional** en tres bloques
   (ingeniería y arquitectura · frontend y aplicaciones cliente · desarrollo
   asistido por IA) y, al final, **credenciales** (4 certificaciones OpenAI,
   Scrum Fundamentals Certified de ScrumStudy y Elements of AI de la
   Universidad de Helsinki, sin enlaces de verificación).
7. **06 · Exploración**: áreas de investigación actual (ingeniería agéntica,
   OpenCode, automatización del ciclo de desarrollo, otras tecnologías).
8. **CTA de GitHub** y **pie** (nombre, copyright, GitHub, LinkedIn, idioma).

### Decisiones técnicas

- **Cero JavaScript.** Navegación por anclas, cambio de idioma por enlace y
  notas desplegables con `<details>` nativo.
- **Un solo CSS** para los dos idiomas: la estructura no puede divergir.
- **SEO**: `title` y `description` localizados, `canonical` + `hreflang`
  (`es`, `en`, `x-default`), Open Graph, Twitter Card y JSON-LD de tipo
  `Person` (mismo contenido en ambos idiomas).
- **Accesibilidad**: enlace de salto, landmarks, jerarquía `h1 → h2 → h3`,
  `focus-visible`, `prefers-reduced-motion` y axe-core con **0 incumplimientos**.

## Mantenimiento

### Cambiar contenido

Cualquier texto o sección hay que tocarla en **los dos ficheros**:
`index.html` (español) e `en.html` (inglés). La estructura y los `id` son
idénticos a propósito para que comparar ambos archivos sea directo.

Comprobaciones rápidas tras editar:

1. Los dos idiomas tienen las mismas secciones y el mismo orden.
2. `hreflang` y `canonical` siguen apuntando a las URLs correctas.
3. Ningún enlace roto (todos los externos están verificados).

### Datos personales

- Perfil público: <https://github.com/andreu-marbor>
- LinkedIn: <https://www.linkedin.com/in/andreu-martinez/>
- No se publica ningún email personal.

### Añadir una app Android nueva

Basta con añadir un objeto más al array de `.well-known/assetlinks.json`. Un
bloque por app:

```json
{
  "relation": ["delegate_permission/common.handle_all_urls"],
  "target": {
    "namespace": "android_app",
    "package_name": "com.andreumarbor.miaplicacion",
    "sha256_cert_fingerprints": [
      "huella_sha256_del_keystore_en_minusculas_sin_dos_puntos"
    ]
  }
}
```

Obtener la huella de un keystore:

```bash
keytool -list -v -keystore android.keystore -alias android   # campo SHA256
```

**Cuándo hay que tocar este archivo:**

- Al crear una **app Android nueva** → añadir su bloque.
- Si cambia la **firma** (keystore nuevo o rotación de contraseña con clave
  nueva) → actualizar la huella. *Cambiar solo la contraseña del mismo keystore
  NO cambia la huella.*
- Si la app se publica en **otro dominio** → ese dominio necesita su propio
  `assetlinks.json` (a nivel de host, no de ruta).

Verificación:

- <https://andreu-marbor.github.io/.well-known/assetlinks.json>
- Validador oficial de Google: <https://developers.google.com/digital-asset-links/tools/generator>

> ⚠️ Chrome **cachea el resultado** de la comprobación (también los fallos).
> Tras publicar o cambiar la huella, si la app sigue mostrando la barra de
> direcciones: desinstalar la app, borrar los datos de Chrome en el móvil y
> volver a instalar la APK.

## Despliegue

GitHub Pages publica la **rama `main`** de este repositorio desde la raíz. No
hay workflow de CI: basta con hacer push.

La rama local puede llamarse `master`; para desplegar:

```bash
git push origin HEAD:main
```

## Validación

Comandos usados durante el rediseño (todos pasaron):

```bash
# HTML: W3C Nu checker (0 mensajes en index.html y en.html)
curl -H "Content-Type: text/html; charset=utf-8" --data-binary @index.html \
  "https://validator.w3.org/nu/?out=json"

# CSS: sintaxis
npx --yes csstree-validator styles.css

# Accesibilidad y responsive: axe-core (0 violaciones) y comprobación de
# overflow horizontal de 320 a 1440 px, vía Chrome DevTools Protocol.
```

Comprobaciones adicionales que se repiten tras cada cambio de contenido:

- **Paridad ES/EN**: ambos ficheros deben tener la misma secuencia de
  etiquetas, los mismos `id` y las mismas anclas (`href="#…"` resolubles).
  Difieren solo en el texto y en el enlace de idioma.
- **Enlaces externos**: todos devuelven 200 (LinkedIn responde `999` a las
  peticiones automatizadas, es su bloqueo habitual).
- **Rejillas**: `Enfoque` 2×3, `Experiencia` 3 columnas y `Explorando` 2×2 a
  partir de ~860 px de ancho; por debajo pasan a 2 y a 1 columna.
