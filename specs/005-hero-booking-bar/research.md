# Research: Booking bar premium del Hero

## 1. Relación con 004

**Decision**: Implementar contra spec **005**. Reutilizar labels estáticos y CTA-en-grid de 004 si siguen en el DOM; **no** conservar chrome vacío, “Buscar / Continuar”, ni `activateRequestState`.

**Rationale**: 005 es la fuente vigente. Embellecer 004 no corrige orden DOM, dual feedback ni overlap.

**Alternatives considered**: Solo CSS sobre 004 — rechazado por el brief.

## 2. Confirmación post-submit

**Decision**: Dejar de llamar `activateRequestState`. `renderQuote` MUST mostrar `#quote-summary` (`hidden = false`) y **no** añadir `.has-request`. Eliminar markup `.nav-request` / botones `request-action` del header (o dejarlos `hidden` permanentes y CSS muerto fuera). Formulario editable debajo del resumen (comportamiento 001).

**Rationale**: Clarificación A + FR-007. Hoy el JS **oculta** el resumen y salta al navbar.

**Alternatives considered**: Barra sticky — rechazada (preferencia inline). Mantener ambos — prohibido.

## 3. Copy de CTAs

**Decision**: `.search-submit` texto **Pedir cotización**. `#quote-wa-btn` **Continuar por WhatsApp**. `preventDefault` en submit se conserva.

**Rationale**: Clarificación A. Naranja no abre WhatsApp.

## 4. Orden Ida y vuelta (~1280px)

**Decision**: En HTML, `.field-return` **después** de fecha de ida (no primer hijo). CSS ≥1280:  
- Solo ida: `grid-template-columns: repeat(5, minmax(0,1fr)) auto` (origen destino fecha hora pasajeros + CTA).  
- `.search-fields.is-round-trip` (clase togglada por JS al elegir ida-vuelta): fila 1 cuatro campos de ruta/fechas; fila 2 hora, pasajeros, CTA `justify-self: end` / `grid-column: 3 / -1` o equivalente de 3 columnas.

**Rationale**: Clarificación B. Evita 7 columnas y el wrap roto.

**Alternatives considered**: Una fila de 7 — rechazada. Fecha de regreso sola en fila 2 — peor orden mental.

## 5. Altura estable entre modos

**Decision**: Misma receta de `.search-fields` (5 slots + CTA) en Por horas y Transporte solo ida. Pills de viaje **en la misma fila que los tabs** o como segmented hermano de altura fija **solo visualmente ocupada en Transporte** sin un bloque vacío enorme: usar `visibility`/`grid` de una sola línea de pills **siempre presente**; en Por horas las pills `visibility: hidden` + `pointer-events: none` **o** tabs+pills en un `display:grid` de dos áreas donde Por horas muestra solo tabs y el área de pills tiene `min-height: 0` si las pills se integran **dentro** de Transporte como primer row del grid de campos (tipo de viaje como pills compactas encima de origen, y Por horas tiene un título/slot equivalente “Servicio por horas” de una línea). Preferencia de implementación: **pills dentro del form Transporte** con altura ~40px; Por horas usa una línea de contexto de la misma altura (“Duración del servicio” o simple `min-height` en `.search-panel` igualando `minmax` del grid de 2 rows de campos, no un chrome vacío).

Patrón limpio elegido: **no `.search-chrome` vacío**. Por horas y Transporte solo ida = una fila de campos. Ida y vuelta = dos filas (extra justificada). El salto Transporte↔Por horas en solo ida es ~0. El salto al activar ida-vuelta es intencional (segunda fila).

**Rationale**: 005 reemplaza la franja vacía de 004.

## 6. FAB vs CTA

**Decision**: `IntersectionObserver` sobre `#hero-search`. Si `isIntersecting` y ratio &gt; 0, añadir `.is-fab-suppressed` a `body` o `.floating-wa` (`opacity: 0; pointer-events: none; visibility: hidden`). Al salir, quitar. Fallback: `bottom` + padding-safe si Observer falta.

**Rationale**: Spec: ocultar mientras el cotizador está en vista.

## 7. Densidad y paleta

**Decision**: Labels `font-size: 0.875rem` (14px); inputs `height: 48px`–`52px`; padding interno ≥12px. Tabs segmented; trip pills. Sombra suave. CTA naranja; WA verde.

**Rationale**: FR-009/011/016.

## 8. Locale y lugares

**Decision**: `lang="es"` ya en `html`. Inputs `date` con `lang="es-CO"` donde el motor lo respete; labels “Fecha de ida / Fecha de regreso”; placeholders de texto “Cartagena”, “Aeropuerto Rafael Núñez…”. Ampliar `#place-suggestions` con los destinos del catálogo (sin inventar).

**Rationale**: FR-012/013. Datalist nativo = vanilla.

## 9. Swap

**Decision**: Botón `type="button"` entre origen y destino; JS intercambia `.value`. `aria-label="Intercambiar origen y destino"`.

**Rationale**: FR-013. No requiere librería.

## 10. Competencia visual Hero

**Decision**: Bajar peso de `.lets-go-btn` (outline/ghost) y compactar `.hero-social`; no tocar `.hero-brand` / H1.

**Rationale**: FR-015 mínimo.

## 11. script.js validaciones

**Decision**: Conservar mensajes, `minDate`, origen=destino, `relatedSuggestions`, `buildWhatsAppUrl`. Sustituir llamadas `activateRequestState` por `renderQuote(...)` visible. Quitar listeners de `requestModifyBtn` si se elimina el nodo.
