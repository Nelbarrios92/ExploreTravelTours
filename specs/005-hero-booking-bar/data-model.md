# Data Model: Booking bar (sin persistencia)

Negocio = modelo 001 (Solicitud de Transporte / Por horas). Este documento cubre **presentación y confirmación**.

## Modos

| Modo | Campos fila principal (~1280 solo ida / por horas) |
|------|-----------------------------------------------------|
| Transporte solo ida | origin, destination, depart-date, depart-time, passengers, CTA |
| Transporte ida-vuelta | Fila1: origin, destination, depart-date, return-date. Fila2: depart-time, passengers, CTA |
| Por horas | pickup, duration, date, time, passengers, CTA |

`name` JS **inmutables**: origin, destination, depart-date, return-date, depart-time, passengers, pickup, duration, date, time, trip-type.

## Confirmación

| Antes (incorrecto) | 005 |
|--------------------|-----|
| `.has-request` + nav “TU SOLICITUD”; `quote-summary` hidden | Solo `#quote-summary` visible; form sigue editable |

## Sugerencias de lugar (mínimo SC-007: ≥5)

Reutilizar y completar `#place-suggestions`: Cartagena, Barranquilla, Santa Marta, Aeropuerto (o Aeropuerto Rafael Núñez), Playa Blanca / Barú, Volcán del Totumo, Sincelejo, Montería. Texto libre permitido.

## FAB

Estado `visible` | `suppressed` según intersección de `#hero-search` con el viewport.

## Validation (sin cambio de significado)

Requeridos, pasajeros ≥1, fechas ≥ hoy, regreso ≥ ida, origen ≠ destino → prompt Por horas.
