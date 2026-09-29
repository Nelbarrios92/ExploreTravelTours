# Data Model: Vista cotizada (sin persistencia)

Negocio de solicitud = 001/005. Este documento describe **qué superficie está activa**.

## Estados del card `#hero-search`

| Estado | Buscador (tabs + forms) | `#quote-summary` | Clase |
|--------|-------------------------|------------------|-------|
| Componer | Visible | `hidden` | (ninguna / no `.is-quoted`) |
| Cotizado | Oculto | Visible | `.is-quoted` |

Transiciones:

- Componer → Cotizado: submit válido → `renderQuote`.
- Cotizado → Componer: click **Modificar** → `hideQuote` + quitar `.is-quoted`. Valores de campos **sin reset**.
- Componer + error: permanece Componer.

## Campos

`name` inmutables. Al Modificar no se llama `form.reset()`.

## Validation

Sin cambio de significado (005).
