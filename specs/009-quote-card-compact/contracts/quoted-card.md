# Contrato UI: card cotizado compacto

**009 manda** sobre talla de `#hero-search.is-quoted` y `.quote-*`. 007 manda visibilidad. 006 manda el grid al componer.

## Card

`#hero-search.is-quoted`: padding **menor** que el modo buscador (p. ej. 8px 12px). MUST NOT `background`/`border` extra en `.quote-summary`.

## Resumen (MUST)

- h2 ≈ **1rem**
- dt / relacionados ≥ **0.8125rem** (MUST NOT ≤0.78rem)
- dd ≈ **0.875rem**
- `.quote-wa-btn` y `.quote-modify`: **misma** height **42px** (±2px), font-size **0.8125rem**
- MUST NOT height 50px en esos CTAs

## MUST NOT

- Cambiar `.search-submit`, `.field`, `.is-round-trip` ≥1280
- Cambiar JS 007 / copy / `wa.me`
