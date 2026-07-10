# UtilEs — Landing Page

Sitio estático de una sola página para `apputiles.com`, listo para GitHub Pages.

## Estructura
```
utiles-landing/
├── index.html          # todo el sitio (HTML + CSS + JS inline)
├── CNAME                # apunta a apputiles.com
└── assets/
    └── utiles-screenshot.jpg
```

## Publicar en GitHub Pages

1. Crea un repositorio nuevo en GitHub (público), por ejemplo `utiles-landing`.
2. Sube estos archivos a la raíz del repo:
   ```bash
   cd utiles-landing
   git init
   git add .
   git commit -m "Landing page UtilEs"
   git branch -M main
   git remote add origin https://github.com/TU_USUARIO/utiles-landing.git
   git push -u origin main
   ```
3. En GitHub: **Settings → Pages → Build and deployment → Source: Deploy from a branch**, elige `main` y carpeta `/ (root)`.
4. Cada `git push` a `main` vuelve a publicar el sitio automáticamente (30s–2min).

## Conectar `apputiles.com` (Namecheap)

En Namecheap → Domain List → `apputiles.com` → **Advanced DNS**, agrega:

| Tipo | Host | Valor |
|------|------|-------|
| A | @ | 185.199.108.153 |
| A | @ | 185.199.109.153 |
| A | @ | 185.199.110.153 |
| A | @ | 185.199.111.153 |
| CNAME | www | TU_USUARIO.github.io |

Luego en GitHub → Settings → Pages → **Custom domain**: escribe `apputiles.com` y guarda (esto reescribe el archivo `CNAME`, ya incluido aquí). Activa **Enforce HTTPS** una vez el certificado se emita (puede tardar hasta un par de horas).

## Botón de descarga manual (.apk)

El sitio incluye dos botones que apuntan a `assets/UtilEs.apk` (uno en el hero, otro en la sección final). Ese archivo **no está incluido** — antes de publicar, copia tu APK firmado ahí:

```bash
cp /ruta/a/tu/app-direct-release.apk utiles-landing/assets/UtilEs.apk
```

Actualiza también la versión, el tamaño y el requisito de Android en los dos bloques `.btn-meta` de `index.html` (busca `v1.2.7 · 8.4 MB`) cada vez que subas una nueva build. Si prefieres no alojar el binario en el repo (GitHub limita archivos a 100 MB y recomienda evitar binarios grandes en Pages), sube el APK como asset de un [GitHub Release](https://docs.github.com/en/repositories/releasing-projects-on-github) y cambia el `href` de ambos botones a esa URL — el resto del sitio sigue igual.

## Editar contenido

Todo vive en `index.html`:
- Copy y textos: dentro de las secciones `<section>`.
- Colores y tipografía: variables `:root` al inicio del `<style>`.
- La demo animada de "SMS → saldo activado": al final, dentro de `<script>`.

No hay build step — es HTML/CSS/JS puro, así que cualquier cambio se refleja con solo hacer push.
