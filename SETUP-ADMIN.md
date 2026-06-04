# Guía de Setup — Admin CMS

Esta guía te lleva paso a paso para activar el admin de fotos en `tusitio.netlify.app/admin`.

## Requisitos previos

- Cuenta en Netlify ✓ (ya tienes el sitio deployed)
- Cuenta en GitHub (gratis si no tienes — github.com/signup)
- 20 minutos

---

## Paso 1 — Sube el código a GitHub

El CMS necesita un repo de Git para guardar los cambios.

1. En github.com crea un nuevo repo (privado o público, da igual). Sugerencia de nombre: `sister-cities-gdl-sjc`.
2. **NO** lo inicialices con README, .gitignore ni licencia (lo dejas vacío).
3. En tu compu, en la carpeta donde tienes los archivos del sitio:

```bash
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/TU-USUARIO/sister-cities-gdl-sjc.git
git push -u origin main
```

Si no usas terminal: la app de **GitHub Desktop** (desktop.github.com) hace todo esto con clicks.

---

## Paso 2 — Conecta Netlify al repo

Si ya tienes el sitio deployed por drag-and-drop, vamos a re-conectarlo a GitHub para que se actualice automáticamente.

1. Entra a Netlify → tu sitio → **Site configuration** → **Build & deploy** → **Continuous deployment**
2. Click **"Link site to Git"** (o "Link repository")
3. Elige **GitHub** → autoriza Netlify → selecciona el repo `sister-cities-gdl-sjc`
4. Branch: `main`
5. Build command: déjalo vacío (es sitio estático)
6. Publish directory: `/` (raíz)
7. **Deploy**

Ya cada `git push` triggerea un deploy automático. 🚀

---

## Paso 3 — Activa Netlify Identity

Esto da el login para entrar al admin.

1. En Netlify → tu sitio → **Site configuration** → **Identity** (en el menú lateral)
2. Click **"Enable Identity"**
3. En **Registration preferences**: elige **"Invite only"** (recomendado — solo tú y tu equipo)
4. En **External providers** (opcional): puedes activar login con Google/GitHub

---

## Paso 4 — Activa Git Gateway

Esto permite que el CMS escriba en el repo sin que el usuario tenga cuenta de GitHub.

1. En el mismo panel de Identity, baja a **Services**
2. Bajo **Git Gateway**, click **"Enable Git Gateway"**

---

## Paso 5 — Invítate al admin

1. En el panel de Identity, click **"Invite users"**
2. Pon tu email → enviar
3. Revisa tu correo y haz click en el link de invitación
4. Crea tu contraseña

---

## Paso 6 — Entra al admin 🎉

Ve a: **`https://tusitio.netlify.app/admin/`**

Login con el email y contraseña que creaste.

Verás la sección **📷 Galería** → click → **Photos** → click **+ Add Foto** → arrastra una imagen, llena los campos, **Publish**.

En 1-2 minutos (lo que tarda el redeploy de Netlify) la foto aparece en tu sitio.

---

## Cómo invitar a más miembros del equipo

Identity → **Invite users** → pones su email → ellos crean su contraseña → tienen acceso al admin.

Útil para que Fernando, Samuel u otros puedan subir fotos sin tocar código.

---

## Troubleshooting

**"No autoriza el login"** → revisa que activaste Git Gateway en el paso 4.

**"El admin se queda en blanco"** → abre la consola del navegador (F12). Probablemente falta el step de Git Gateway, o el sitio no está conectado a Git todavía.

**"Subí una foto pero no aparece en el sitio"** → espera 1-2 min para el redeploy. Mira en Netlify → Deploys que se haya completado el build. Refresca con Ctrl+Shift+R (limpia caché).

**"No quiero invitar gente, solo yo"** → mantén "Invite only" en Registration preferences (paso 3).

---

## Estructura final de archivos

```
sister-cities/
├── index.html
├── hub.html
├── gallery.json          ← El CMS escribe aquí
├── admin/
│   ├── index.html        ← Decap CMS UI
│   └── config.yml        ← Campos del formulario
└── img/
    ├── logo.png, sj.jpg, gdl.webp, ...
    └── gallery/          ← El CMS sube fotos aquí
        └── (las fotos que subas)
```
