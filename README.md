# andreu-marbor.github.io

Sitio de usuario de GitHub Pages: ocupa la **raíz** del dominio `https://andreu-marbor.github.io/`.

Contenido:

| Archivo | Para qué sirve |
|---|---|
| `.well-known/assetlinks.json` | **Digital Asset Links**: Chrome lo consulta en la raíz del dominio para comprobar si una APK TWA (Trusted Web Activity) es legítima. Si responde 200 con la huella correcta, la app se abre **a pantalla completa y sin barra de direcciones**; si no, cae en un Custom Tabs (navegador embebido con la URL arriba). |
| `index.html` | Landing mínima con enlace a los proyectos. |

> Los repos de proyecto (`tres-en-raya`, `catfoodcheck`, …) siguen publicando cada uno en su
> subcarpeta (`https://andreu-marbor.github.io/tres-en-raya/`, …). Este sitio **no los afecta**:
> conviven sin pisarse.

## Añadir una app Android nueva

Basta con añadir un objeto más al array de `.well-known/assetlinks.json`. Un bloque por app:

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
- Si cambia la **firma** (keystore nuevo o rotación de contraseña con clave nueva) → actualizar la huella.
  *Cambiar solo la contraseña del mismo keystore NO cambia la huella.*
- Si la app se publica en **otro dominio** → ese dominio necesita su propio `assetlinks.json`
  (a nivel de host, no de ruta).

## Verificación

- <https://andreu-marbor.github.io/.well-known/assetlinks.json>
- Validador oficial de Google: <https://developers.google.com/digital-asset-links/tools/generator>

> ⚠️ Chrome **cachea el resultado** de la comprobación (también los fallos). Tras publicar o
> cambiar la huella, si la app sigue mostrando la barra de direcciones: desinstalar la app,
> borrar los datos de Chrome en el móvil y volver a instalar la APK.
