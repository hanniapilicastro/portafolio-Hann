---
layout: default
title: Estilos y personalización visual
nav_order: 7
---

# Estilos y personalización visual

Esta sección explica **cómo funciona la personalización visual** en este repositorio y qué debes modificar para poner el sitio con tu identidad (logo, colores, footer, etc.) **sin romper la estructura**.

> [FIGURA: Captura del sitio ya publicado (antes/después de cambiar logo y colores).]

---

## 1) ¿Qué archivos controlan el estilo?

En este repositorio, el estilo y algunos elementos visuales se controlan con **tres piezas**:

1) **CSS** con los colores y ajustes visuales:  
   - `assets/css/custom.css`

2) **Head** (carga el CSS, favicon y agrega el logo en el título):  
   - `_includes/head_custom.html`

3) **Footer** (tu footer “propio”, con licencia y “Last modified”):  
   - `_includes/footer_custom.html`

Estructura típica:

```text
.
├─ _includes/
│  ├─ head_custom.html
│  └─ footer_custom.html
├─ assets/
│  ├─ css/
│  │  └─ custom.css
│  └─ img/
│     ├─ logotipo.png
│     └─ favicon.ico
└─ ...
```

> [FIGURA: Captura de la estructura en GitHub o Codespaces.]

---

## 2) “Lo mínimo” para poner tu identidad (sin complicarte)

Si solo quieres “poner tu marca” y seguir avanzando con el curso, haz esto:

### Paso A — Cambia el logo
Reemplaza el archivo:

- `assets/img/logotipo.png`

**Regla importante:** conserva **exactamente** el nombre `logotipo.png` para no tener que cambiar rutas.

> [FIGURA: Captura del archivo `logotipo.png` en la carpeta assets/img.]

### Paso B — Cambia el favicon
Reemplaza el archivo:

- `assets/img/favicon.ico`

> [FIGURA: Captura del favicon en pestaña del navegador.]

### Paso C — Ajusta colores (si lo necesitas)
Edita:

- `assets/css/custom.css`

Más abajo tienes una guía de “qué tocar” sin perderte.

---

## 3) Cómo funciona `head_custom.html` (logo + favicon + CSS)

Este archivo se inserta en el `<head>` del sitio y hace 3 cosas:

1) Carga `custom.css`.
2) Define el favicon.
3) Inserta el logo **antes del texto** del título del sitio (en la barra lateral / encabezado, según el tema).

Código relevante (simplificado):

```html
<link rel="stylesheet" href="{{ '/assets/css/custom.css' | relative_url }}">
<link rel="icon" href="{{ '/assets/img/favicon.ico' | relative_url }}" sizes="any">

<script>
  document.addEventListener('DOMContentLoaded', () => {
    const titleLink = document.querySelector('.site-title');
    if (!titleLink || titleLink.querySelector('img')) return;

    const img = document.createElement('img');
    img.src = "{{ '/assets/img/logotipo.png' | relative_url }}";
    img.alt = "Logo";
    img.className = "site-logo";
    titleLink.prepend(img);
  });
</script>
```

**Qué modificar aquí:**
- Normalmente **no necesitas cambiar nada** si mantienes:
  - `assets/css/custom.css`
  - `assets/img/logotipo.png`
  - `assets/img/favicon.ico`

**Cuándo sí lo cambiarías:**
- Si decides renombrar archivos (no recomendado en un curso).
- Si quieres insertar otro elemento adicional en el `<head>` (por ejemplo: analytics, meta tags especiales, etc.).

> [FIGURA: Captura del archivo `_includes/head_custom.html` abierto en Codespaces.]

---

## 4) Cómo funciona `custom.css` (qué tocar y qué NO tocar)

`assets/css/custom.css` contiene reglas para:

- Colores del header y sidebar.
- Colores de enlaces (y quitar el morado/azul por defecto).
- Estados hover/active del menú.
- Jerarquía visual del menú (nivel 1, 2, 3).
- Ajustes del botón hamburguesa en móvil.
- Ocultar el footer original del tema y mostrar tu footer personalizado.
- Tamaño del logo en el título.

### 4.1 Paleta rápida (qué buscar)

En este CSS verás repetidos estos colores:

- **Rojo principal:** `#E00034`
- **Rosa claro/acento:** `#FFD5DE`
- **Rojo oscuro hover:** `#b00028`

Recomendación práctica:
- Para cambiar la “marca”, normalmente te basta con cambiar:
  - `#E00034` (color principal)
  - `#FFD5DE` (acento)
  - y la variable `--link-color`.

Ejemplo de variable de enlaces:

```css
:root { --link-color: #E00034; }
a, a:visited { color: var(--link-color); }
```

> [FIGURA: Captura de búsqueda “#E00034” dentro de `custom.css`.]

### 4.2 Sidebar y navegación (menú lateral)

El CSS fuerza el sidebar en rojo y los links en blanco:

```css
.side-bar,
.side-bar .site-nav,
.side-bar .nav-list { background-color: #E00034 !important; }

.nav-list .nav-list-link,
.nav-list .nav-list-link:visited { color: #ffffff !important; }
```

Y define estados activos/hover más visibles.

> [FIGURA: Captura del menú lateral con un ítem activo.]

### 4.3 “Navbar fix”: si te salen símbolos raros en el menú

El archivo incluye un bloque comentado como “NAVBAR FIX (Just the Docs)”. Su intención es neutralizar pseudo-elementos que, en algunas combinaciones, generan caracteres raros en el sidebar y luego dibujar un bullet limpio para el nivel 2.

Si alguna vez ves cosas extrañas (por ejemplo símbolos repetidos), revisa ese bloque.

> [FIGURA: Captura del problema (si aparece) + captura del bloque “NAVBAR FIX”.]

### 4.4 Footer: ocultar el del tema y usar el tuyo

El CSS oculta el footer del tema:

```css
footer.site-footer { display: none !important; }
```

Y define estilos para tu footer:

```css
.custom-footer { ... }
.custom-footer a { ... }
```

Esto funciona en conjunto con `_includes/footer_custom.html`.

---

## 5) Footer personalizado (`footer_custom.html`)

Tu footer actual:

- Muestra copyright.
- Enlaza a tu perfil.
- Enlaza a la licencia CC BY 4.0.
- Enlaza a la página “Uso de IA”.
- Muestra “Last modified” con fecha/hora.

Ejemplo (simplificado):

```html
<footer class="custom-footer">
  <p class="custom-footer__copy">
    Copyright © 2026 IBERO.
    <a href="...">Huber Giron</a>.
    <a href="...">CC BY 4.0</a>.
    <a href="{{ '/uso-ia/' | relative_url }}">Uso de IA</a>
  </p>

  <p class="custom-footer__modified">
    <strong>Last modified:</strong>
    {{ modified | date: "%A, %B %-d, %Y at %H:%M" }}
  </p>
</footer>
```

### Qué cambiar aquí (típicamente)
- El texto “Copyright © 2026 …”.
- Tu nombre y enlace.
- La licencia (si aplica).
- El enlace “Uso de IA” (si quieres ocultarlo o moverlo).

> [FIGURA: Captura del footer al final de una página.]

---

## 6) Estilos útiles para el curso (recomendados)

### 6.1 Video responsivo (iframe de YouTube/Vimeo)

Si quieres que los iframes sean responsivos (se ajusten en móvil), agrega esto a `custom.css`:

```css
.responsive-embed {
  position: relative;
  width: 100%;
  padding-top: 56.25%; /* 16:9 */
  overflow: hidden;
  border-radius: 12px; /* opcional */
}

.responsive-embed iframe {
  position: absolute;
  inset: 0;
  width: 100%;
  height: 100%;
  border: 0;
}
```

Y en Markdown/HTML úsalo así:

```html
<div class="responsive-embed">
  <iframe
    src="https://www.youtube.com/embed/ID_DEL_VIDEO"
    title="Video"
    allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
    allowfullscreen></iframe>
</div>
```

> [FIGURA: Captura de un video incrustado en desktop y móvil.]

### 6.2 Video MP4 (archivo local) más “amigable” en móvil

Para que el MP4 no “se salga” en pantallas pequeñas, agrega:

```css
video {
  max-width: 100%;
  height: auto;
}
```

---

## 7) Checklist rápido cuando “no se ve” el cambio

1) **Guardaste el archivo** (en Codespaces o en tu editor).
2) Hiciste **commit** y **push** al repositorio.
3) Esperaste a que **GitHub Actions** termine (verde).
4) Abriste tu sitio y forzaste recarga:
   - Windows: `Ctrl + F5`
   - macOS: `Cmd + Shift + R`

Tip de diagnóstico:
- Abre directamente el CSS en el navegador:  
  `TU_URL/assets/css/custom.css`  
  Si no carga, el problema es de ruta o de build.

> [FIGURA: Captura de GitHub Actions en verde + captura de recarga dura en el navegador.]

---

## Siguiente sección

Este es el último tema de personalización. Puedes volver a:

- [Inicio](index.md)
- [Publicar en GitHub Pages](01-publicar-en-github-pages.md)
