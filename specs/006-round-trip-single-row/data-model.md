# Data Model: Fila de Ida y vuelta (presentación)

Negocio inmutable (001/005). Este documento solo describe **layout**.

## Tipo de viaje → filas en viewport

| Viewport | Solo ida | Ida y vuelta |
|----------|----------|----------------|
| ~375px | 1 columna (stack) | 1 columna + fecha de regreso en el stack |
| ~768px | Reflujo 2–3 filas (005) | Reflujo 2–3 filas **intencional** (no el salto de escritorio) |
| ~1280px | 1 fila: origin, swap, dest, depart, time, pax, CTA | **1 fila**: origin, swap, dest, depart, **return**, time, pax, CTA |

`name` JS **inmutables**: origin, destination, depart-date, return-date, depart-time, passengers, trip-type.

## Estado de layout

| Clase | Significado |
|-------|-------------|
| `.search-fields-transport` | Grid de traslado |
| `.is-round-trip` | Fecha de regreso visible; a ≥1280px **misma fila** que el resto, no segunda banda |

## Validation

Sin cambio de significado respecto a 005.
