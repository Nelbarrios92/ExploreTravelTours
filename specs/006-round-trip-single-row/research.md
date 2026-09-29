# Research: Ida y vuelta en una sola fila

## CSS Grid: una fila de 8 áreas vs dos filas 005

**Decision**: En `@media (min-width: 1280px)`, `.search-fields-transport.is-round-trip` usa una sola `grid-template-areas` con: `origin swap dest depart ret time pax cta`. Ocho columnas; `minmax` más estrechos que Solo ida donde haga falta (sobre todo fechas, hora, pasajeros, CTA).

**Rationale**: El wrap actual es deliberado en CSS (fila 2 `time time pax pax cta`), no un wrap accidental de `flex-wrap`. Quitar esa segunda fila cumple FR-001/clarificación A. La clase `.is-round-trip` sigue sirviendo para insertar `ret`.

**Alternatives considered**: Flex + `nowrap` (menos control de anchos); una fila solo desde 1440px (rechazado: clarificación A exige ~1280); scroll horizontal (`overflow-x: auto`) (rechazado por spec).

## Densidad vs caber

**Decision**: Conservar `font-size` de labels (~0.875rem) y `height` de inputs (~50px). Compactar **anchos** (`minmax(0, …)`, CTA `min-width` ~140–160px en ida-vuelta si 180px empuja wrap). `white-space` en labels: permitir wrap de 2 líneas del label, no recorte con ellipsis que oculte “Fecha de regreso”.

**Rationale**: Clarificación A: aire sí, textos ilegibles / labels ocultos / tipografía admin no.

**Alternatives considered**: Ocultar `.field-label` en ida-vuelta (rechazado); `font-size` &lt;14px (rechazado).

## Tablet y móvil

**Decision**: No cambiar `@media (min-width: 768px)` ni el stack de 1 columna. Ida y vuelta en tablet sigue 3 filas de reflujo intencional.

**Rationale**: Spec US2 / FR-004: no forzar la fila de escritorio en 375; tablet MAY refluir.

**Alternatives considered**: Una fila también a 768 (ilegible / overflow-x).

## HTML / JS

**Decision**: Cero cambios de markup o validación. `updateReturnVisibility` ya hace `transportFields.classList.toggle('is-round-trip', isRoundTrip)`.

**Rationale**: Orden DOM ya es origen → swap → destino → ida → regreso → hora → pasajeros → CTA.

**Alternatives considered**: Quitar `.is-round-trip` y usar `:has(.field-return:not([hidden]))` (más frágil; no hace falta).
