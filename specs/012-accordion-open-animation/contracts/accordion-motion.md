# Contrato UI: movimiento de altura del acordeón

**012 manda** cómo se mueve `.search-composer` al toggle de la franja en **&lt;768px**. **011** manda cuándo hay acordeón.

## MUST

- Abrir/cerrar con `#search-accordion-toggle`: interpolar **altura** (~**320 ms**, `ease`, sin bounce).
- Un wrapper interno con `overflow: hidden`. Colapso por **`max-height: 0` / `100rem`** (~320 ms), no `display: none`.
- Al terminar de abrir: campos completos, sin recorte.
- `prefers-reduced-motion: reduce`: **0** transición de altura.
- `.is-quoted` y `hideQuote`: compositor / resumen **sin** esta transición.

## MUST NOT

- `display: none` como único medio de colapsar (rompe la interpolación).
- Animar opacidad como sustituto de altura.
- Animar escritorio, 009, o Modificar.
- Duración ≥ 500 ms o bounce.
