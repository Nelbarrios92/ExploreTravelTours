# Contrato UI: buscador compacto en móvil

**010 manda** sobre `#hero-search` **sin** `.is-quoted` cuando el viewport es **&lt;768px**. **006 manda** el grid ≥1280. **009 manda** `.is-quoted`.

## Layout &lt;768px (MUST)

- `.search-fields-transport` y `.search-fields-hourly`: una columna; cada campo y Pedir cotización a **ancho completo**.
- `grid-template-areas` de Transporte **sin** fila `swap` (ida y ida-vuelta).
- `#swap-places` / `.swap-places`: **no visible** (p. ej. `display: none`).
- MUST NOT `origen | destino` ni `fecha | hora`.

## Escala &lt;768px (MUST)

- Inputs/selects del buscador: height **44px** (±2px); labels ≥ **0.8125rem**.
- `.search-submit`: height **50px** (±2px); sigue el CTA principal.
- Padding del card de búsqueda **menor** que escritorio (p. ej. 8px 10px).
- MUST NOT tipo ≤0.78rem.

## ≥768px (MUST NOT romper)

- Intercambiar origen/destino **visible** y usable.
- Ida y vuelta ~1280: **una fila** (006).
- `.search-submit` e inputs del formulario vuelven a densidad de barra (~50px).

## MUST NOT

- Cambiar `script.js`, copy, `wa.me`, 007, `.quote-*`, `.is-quoted`.
- Emparejar campos en teléfono.
- Quitar `#swap-places` del HTML.
