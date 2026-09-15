# Data Model: Pie de cotización por ancho

Sin entidades de negocio. Comportamiento visual:

| Ancho | Hero | Buscador | `is-collapsed` |
|-------|------|----------|----------------|
| &lt;768px | `min-height: 100vh`, `height: auto` (crece al abrir) | Franja 011/012 + compositor 012 | Plega el compositor (013 intacto) |
| ≥768px | `height: 100vh` (primer pantallazo) | Barra siempre visible en `.hero-footer` | **Ignorado**: compositor abierto |

Estados 007 `is-quoted`: resumen en el pie en ambos anchos (009); 014 no cambia el card, solo **dónde** vive la barra en escritorio.
