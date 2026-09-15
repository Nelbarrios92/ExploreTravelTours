# Data Model: Buscador (sin persistencia)

El modelo de negocio **no cambia** respecto a `specs/001-homepage-discovery-booking/data-model.md`. Este documento describe el **esqueleto visual** y los campos ya existentes.

## Modos

| `data-mode` | Form `id` | Campos de la fila principal |
|-------------|-----------|-----------------------------|
| `transporte` | `search-form-transporte` | origin, destination, depart-date, depart-time, passengers + submit |
| `por-horas` | `search-form-hourly` | pickup, duration, date, time, passengers + submit |

## Chrome compartido

| Zona | Transporte | Por horas |
|------|------------|-----------|
| Tabs | Transporte \| Por horas | igual |
| `.search-chrome` | Solo ida / Ida y vuelta (`trip-type`) | vacío, misma `min-height` |
| Resumen | `#quote-summary` encima (ambos) | igual |

## Campos (nombres JS inmutables)

| `name` | Modo | Etiqueta visible |
|--------|------|------------------|
| origin | Transporte | Origen |
| destination | Transporte | Destino |
| depart-date | Transporte | Fecha |
| return-date | Transporte si ida-vuelta | Fecha de regreso |
| depart-time | Transporte | Hora |
| passengers | ambos | Pasajeros |
| pickup | Por horas | Lugar de recogida |
| duration | Por horas | Duración (1–12; vacío = Selecciona) |
| date | Por horas | Fecha |
| time | Por horas | Hora |

## Validation (sin cambio)

- Requeridos, pasajeros ≥ 1, fechas ≥ hoy, regreso ≥ ida, origen ≠ destino.
- Origen = destino: no cotizar; prompt `#same-place-prompt`.

## State

Filtro de modo: tab `aria-selected` + `form.hidden`. Tipo de viaje: radio checked. Resumen: `hidden` en `#quote-summary`.
