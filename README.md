# SmartBudget — Landing page (Módulo 3)

## Cómo ejecutarlo
Instala SASS de forma global (una sola vez) y compila:
```bash
npm install -g sass
sass scss/main.scss css/main.css           # compila una vez
sass --watch scss/main.scss css/main.css   # recompila al guardar
```
Abre `index.html` en el navegador (Bootstrap 4.6 se carga por CDN). El archivo `css/main.css` ya viene compilado.

## Lección 1 — Del diseño a la implementación
- HTML5 semántico: `header`, `nav`, `main`, `section` (con `aria-labelledby`), `article`, `aside`, `ol`, `footer`.
- Un solo `h1`; jerarquía `h2` → `h3` sin saltos.
- Los comentarios `<!-- COMPONENTE: ... -->` y `<!-- SECCIÓN: ... -->` marcan cada pieza del diseño.
- **Prototipo:** el boceto en Figma queda por tu cuenta. Orden sugerido de secciones: header, hero + medidor, funciones, pasos, CTA final, footer.
- **Reflexión (ejemplo para adaptar):** el front-end traduce el diseño en una interfaz que funciona, se ve bien en cualquier pantalla y es accesible. También detecta casos que el prototipo no cubre (estados vacíos, pantallas pequeñas, foco de teclado) y los devuelve al equipo de diseño.

## Lección 2 — Metodología: BEM
Elegí **BEM** (`bloque__elemento--modificador`) porque:
- El nombre de la clase explica su función (`budget-meter__bar--housing`).
- Mantiene baja la especificidad: casi todo son selectores de una sola clase, sin conflictos entre secciones.
- Cada bloque es un componente independiente y se puede reutilizar en la app completa.

Bloques: `site-header`, `section`, `hero`, `budget-meter`, `feature-card`, `steps`, `cta`, `signup-modal`, `final-cta`, `site-footer`.

## Lección 3 — SASS y patrón 7-1
```
scss/
├─ abstracts/   variables (tokens), mixins (up, flex-center, focus-ring)
├─ base/        reset (box-sizing), tipografía
├─ components/  cta, budget-meter, feature-card, steps, signup-modal
├─ layout/      header, section, footer
├─ pages/       home (hero, final-cta)
├─ themes/      tema por defecto
├─ vendors/     ajustes mínimos sobre Bootstrap
└─ main.scss    único punto de entrada
```
Cada carpeta tiene un `_index.scss` que reexporta sus parciales (`@forward`), y `main.scss` los une con `@use`.
Se usan variables (`$color-mint`), mapas (`$categories` con `@each`), mixins y anidamiento con `&__elemento`.

## Lección 4 — Modelo de cajas y layout
- `box-sizing: border-box` global; `padding`, `margin` y `border` definidos con `$space` (múltiplos de 8 px).
- `position: sticky` en el header.
- **Grid:** hero (1 → 2 columnas) y `steps` (1 → 3 columnas).
- **Flexbox:** footer, acciones del hero, etiquetas del medidor.
- Mobile-first con el mixin `up(md|lg)`. Valida con DevTools: pestaña *Computed* → diagrama de la caja, y modo dispositivo para probar móvil, tablet y escritorio.

## Lección 5 — Bootstrap 4
Componentes: navbar colapsable, cards, modal, form-control, grilla `row`/`col-md-4` y utilidades (`ml-auto`, `mb-4`, `mb-0`, `align-items-md-center`, `border-0`).
Los estilos propios se cargan después y se aplican con clases BEM; solo hay una regla de ajuste en `vendors/`.
