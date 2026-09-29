# Data Model: Movimiento del acordeón

Sin entidades de negocio. Mismos flags 011:

| Flag | Efecto visual 012 |
|------|-------------------|
| `is-collapsed` (móvil, no cotizado) | `grid-template-rows: 0fr` (plegado; transiciona si el compositor está en pantalla) |
| sin `is-collapsed` | `1fr` (desplegado) |
| `is-quoted` | compositor `display: none` **sin** transición de altura |

`prefers-reduced-motion: reduce`: mismas filas, **sin** transición.
