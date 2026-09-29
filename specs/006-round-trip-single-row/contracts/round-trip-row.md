# Contrato UI: fila única Ida y vuelta

**006 manda** sobre el bloque “Grid ≥1280px / Ida y vuelta” de `specs/005-hero-booking-bar/contracts/booking-bar.md`. El resto de ese contrato (copy, FAB, pills, swap, ids) sigue vigente.

## Selectores

- Grid: `.search-fields.search-fields-transport`
- Ida y vuelta: `.search-fields-transport.is-round-trip` (JS existente)
- Áreas: `origin`, `swap`, `dest`, `depart`, `ret`, `time`, `pax`, `cta`

## Grid ≥1280px — Ida y vuelta

Una sola fila:

```text
origin | swap | dest | depart | ret | time | pax | cta
```

MUST NOT:

- `grid-template-areas` de dos filas (`depart ret` arriba y `time pax cta` abajo)
- `overflow-x` del panel o del `body` por esta fila
- `font-size` de labels/controles por debajo de ~14px para “hacer caber”
- `hidden` en labels

MAY: `minmax` y `min-width` del CTA más compactos que en Solo ida.

## Grid ≥1280px — Solo ida (sin cambio)

```text
origin | swap | dest | depart | time | pax | cta
```

## &lt;1280px

Reflujo 005 (stack / 768). MUST NOT aplicar la fila de 8 columnas en 375px.
