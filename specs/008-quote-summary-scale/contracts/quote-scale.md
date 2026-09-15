# Contrato UI: escala del resumen

**008 manda** sobre tipografía/caja de `#quote-summary`. 007 manda visibilidad (`.is-quoted`).

## Caja

`.quote-summary` MUST NOT usar un recuadro interior más apretado que `.hero-search` (no `padding` 8px + `background` `#f8fafc` + `border` como bloque anidado).

## Escala MUST

- Labels/valores/relacionados: ≥ **0.875rem**
- Valores (`dd`): **0.9375rem** preferido
- `.quote-wa-btn` y `.quote-modify`: **50px** de alto, `width: 100%`, `border-radius: 10px`
- Título: ≤ ~1.25rem; MUST NOT Fraunces

## MUST NOT

- Compactar `.quote-lines` por debajo de 0.875rem en ≥1280px
- Alturas distintas entre verde y Modificar
- Cambiar ids, copy, `wa.me`, grid 006, clase `.is-quoted`
