# Data Model: Composición del Hero móvil

Sin entidades de negocio. Zonas de layout:

| Zona | Contenido | Móvil (&lt;768px), acordeón cerrado | Móvil, acordeón abierto (solo ida) |
|------|-----------|-------------------------------------|-------------------------------------|
| **Mensaje** `.hero-message` | `.hero-brand`, regla, `.hero-subtitle` | Arriba, bajo el nav | Misma posición percibida (Δ &lt; ~8 px) |
| **Aire** | `margin-top: auto` de `.hero-actions` | Visible entre descripción y botón | Se reduce; absorbe el crecimiento del pie |
| **Acción** `.hero-actions` | `.lets-go-btn`, `.hero-social` | Baja, cerca del pie | Más arriba si hace falta; botón completo y tocable encima del buscador |
| **Pie** `.hero-footer` | `#hero-search` | Franja 011/012 | Formulario 010/012; MUST NOT tapar el botón |

Escritorio: las zonas existen en el DOM pero **no** aplican el ancla ni el `margin-top: auto`.
