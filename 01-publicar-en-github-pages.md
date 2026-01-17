---
layout: default
title: Publicar en GitHub Pages
nav_order: 2
---

# Publicar tu sitio en GitHub Pages (solo GitHub Pages)

En este curso vamos a publicar tu documentación como un **sitio web** usando:

- **GitHub** (para guardar el repositorio y el historial)
- **GitHub Pages** (para convertir el repositorio en una URL pública)
- **Codespaces** (para editar desde el navegador, sin instalar nada)

---

## 1) Conceptos mínimos (5 minutos)

- **GitHub**: plataforma para alojar proyectos (repositorios) y colaborar.
- **Repositorio (repo)**: carpeta de proyecto con archivos + historial.
- **Commit**: “guardar un cambio” en el historial con un mensaje.
- **Push**: enviar tus commits a GitHub (a la nube).
- **GitHub Pages**: servicio que publica tu repo como sitio web.
- **Pipeline (Actions)**: proceso automático que construye y publica el sitio cuando haces *push*.

**Figura 1 (pendiente):** Página principal de GitHub.
<!-- ![Figura 1 — GitHub](assets/img/fig01-github-home.png) -->

---

## 2) Crear tu proyecto en GitHub

Vas a partir del repo plantilla que te entrega el profesor (este repositorio).

### Ruta A (recomendada): Fork del repo del profesor

1. Abre el repositorio del profesor en GitHub.
2. Clic en **Fork**.
3. Configura:
   - **Owner**: tu usuario (o la organización de tu equipo)
   - **Repository name**: por ejemplo `documentacion-equipo-3`
4. Clic en **Create fork**.

**Figura 2 (pendiente):** Botón *Fork* y pantalla de creación.
<!-- ![Figura 2 — Fork](assets/img/fig02-fork.png) -->

> Ventaja: no necesitas “subir archivos” manualmente; ya tienes el proyecto completo en tu cuenta.

### Ruta B (alternativa): Crear un repo nuevo y subir los archivos

Úsala solo si tu profesor te pide explícitamente “crear repo desde cero”.

1. Abre GitHub → **New repository**.
2. Nombre: `documentacion-equipo-3`.
3. Crea el repo.
4. Descarga el repo del profesor en tu computadora:
   - **Code → Download ZIP** (o descarga el `.zip` que te entregó el profesor).
5. Sube el contenido a tu repo:
   - **Add file → Upload files**
   - Arrastra los archivos (descomprimidos) a la ventana
   - Clic en **Commit changes**

**Figura 3 (pendiente):** Crear repositorio nuevo.
<!-- ![Figura 3 — New repo](assets/img/fig03-new-repo.png) -->

**Figura 4 (pendiente):** Descargar ZIP / subir archivos.
<!-- ![Figura 4 — Download ZIP + Upload files](assets/img/fig04-zip-upload.png) -->

---

## 3) Abrir el proyecto con Codespaces (sin instalar nada)

1. En tu repo (tu fork o tu repo nuevo):
   - Clic en **Code → Codespaces → Create codespace on main**
2. Se abre un VS Code en el navegador.

**Figura 5 (pendiente):** Crear Codespace.
<!-- ![Figura 5 — Codespaces](assets/img/fig05-codespaces.png) -->

> Nota: Codespaces puede tardar 1–3 minutos en iniciar la primera vez.

---

## 4) Configurar `_config.yml` para que funcione tu URL

En el explorador de archivos abre `_config.yml` y ajusta **solo**:

```yml
url: "https://TU_USUARIO.github.io"
baseurl: "/TU_REPO"
```

Ejemplo típico:
- Usuario: `ana-ibero`
- Repo: `documentacion-equipo-3`

Entonces:

```yml
url: "https://ana-ibero.github.io"
baseurl: "/documentacion-equipo-3"
```

**Figura 6 (pendiente):** Editando `_config.yml` en Codespaces.
<!-- ![Figura 6 — Edit config](assets/img/fig06-config.png) -->

> Si `baseurl` no coincide con el nombre del repo, los links y estilos suelen “romperse”.

---

## 5) Hacer tu primer cambio (commit) y subirlo (push)

En Codespaces:

1. Modifica un archivo sencillo, por ejemplo `index.md`.
2. Ve a la pestaña **Source Control** (ícono de rama).
3. En **Message**, escribe un mensaje de commit, por ejemplo:
   - `Actualiza portada`
4. Clic en **Commit**.
5. Clic en **Sync Changes** (o **Push**).

**Figura 7 (pendiente):** Source Control → Commit → Sync Changes.
<!-- ![Figura 7 — Commit y Push](assets/img/fig07-commit-push.png) -->

### ¿Qué pasó en realidad?

Cuando haces **push**:

1. Tus archivos se guardan en GitHub.
2. Se dispara un **pipeline (GitHub Actions)**.
3. GitHub construye el sitio (Jekyll + Just the Docs).
4. GitHub publica la versión nueva en **GitHub Pages**.

---

## 6) Activar GitHub Pages y obtener tu URL

En tu repositorio (en GitHub, no en Codespaces):

1. **Settings → Pages**
2. En **Build and deployment**:
   - Source: **Deploy from a branch**
   - Branch: `main`
   - Folder: `/ (root)`
3. Guarda.

GitHub te mostrará tu URL con este formato:

- `https://TU_USUARIO.github.io/TU_REPO/`

**Figura 8 (pendiente):** Settings → Pages (branch y folder).
<!-- ![Figura 8 — Pages settings](assets/img/fig08-pages.png) -->

---

## 7) Verificar que el sitio ya está publicado

### Verificación rápida (lo mínimo)

1. En el repo, abre la pestaña **Actions**.
2. Busca el workflow que dice algo como **pages build and deployment**.
3. Espera a que salga en **verde (success)**.
4. Regresa a **Settings → Pages** y abre la URL.

**Figura 9 (pendiente):** Actions con ejecución exitosa.
<!-- ![Figura 9 — Actions success](assets/img/fig09-actions-success.png) -->

### Señales típicas

- Si **Actions** sigue corriendo: espera (es normal).
- Si falla (rojo): abre el job y lee el error (a veces es un YAML mal indentado o un archivo faltante).

---

## Checklist antes de entregar

- [ ] Ya hiciste **commit** y **push** (desde Codespaces).
- [ ] Ajustaste `url` y `baseurl` en `_config.yml`.
- [ ] Activaste **Settings → Pages** con `main` y `/ (root)`.
- [ ] En **Actions** la ejecución está en verde.
- [ ] Tu URL abre y el menú lateral aparece.

