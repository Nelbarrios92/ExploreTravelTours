# Data Model: Escala del resumen (presentación)

Negocio inmutable. Solo tokens visuales del resumen.

## Superficie

| Estado | Padding efectivo | Fondo |
|--------|------------------|--------|
| Componer (buscador) | `.hero-search` 12–14px | Blanco del card |
| Cotizado (resumen) | El mismo (resumen sin inset) | El mismo |

## Jerarquía de tipo (una familia)

1. Título del resumen (un paso sobre el cuerpo, no display)
2. Cuerpo: etiquetas, valores, relacionados (≥ labels del buscador)
3. Controles: WA y Modificar, **misma altura**

Sin persistencia ni campos nuevos.
