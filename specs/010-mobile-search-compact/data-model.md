# Data Model: Buscador compacto en móvil

Negocio inmutable (campos, validación, WhatsApp). Solo **presentación** del estado **Componer** en vista estrecha.

| Viewport / estado | Densidad | Intercambio origen/destino |
|-------------------|----------|----------------------------|
| &lt;768px Componer | Compactación **moderada** 010 (inputs ~44px, CTA ~50px, todo apilado) | **Oculto**, sin pista de grid |
| ≥768px Componer | 005/006 (inputs ~50px; a 1280 una fila ida-vuelta) | **Visible** y operativo |
| Cualquier ancho Cotizado | Compactación **moderada** 009 | N/A (formulario oculto) |

Transiciones 007 sin cambio. Al **Modificar** en 375px: vuelve Componer 010 (apilado, sin swap).
