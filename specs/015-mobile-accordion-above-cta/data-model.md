# Data Model: Orden Hero móvil

Sin entidades de negocio. Orden visual **&lt;768px**:

| Orden | Bloque | Aire |
|-------|--------|------|
| 1 | `.hero-message` | Arriba (013) |
| — | margen automático | Entre mensaje y el par |
| 2 | `.hero-footer` (acordeón / 009) | Justo encima de Explorar |
| 3 | `.hero-actions` (Explorar + redes) | Debajo del cotizador |

**≥768px**: mensaje+acciones agrupados; footer al pie (014). `is-collapsed` / `is-quoted` no cambian de significado.
