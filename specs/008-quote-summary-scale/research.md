# Research: Escala unificada del resumen

## Caja interior vs padding del card

**Decision**: `.quote-summary` sin `background`, `border` ni padding extra (o padding 0). El aire lo da `.hero-search` (`padding: 12px 14px 14px`). Con `#hero-search.is-quoted` el resumen es el único hijo visible y llena el blanco.

**Rationale**: Clarificación A. El recuadro `#f8fafc` + padding 8px es lo que se siente “caja chica dentro del card”.

**Alternatives considered**: Solo subir `font-size` dejando el inset (rechazado).

## Escala numérica (alineada al buscador)

**Decision**:

| Pieza | Valor |
|-------|--------|
| Título h2 | Playfair, ~1.125rem, `--brand-blue` |
| `.quote-lines` / relacionados | 0.875rem (igual `.field-label`) |
| `dd` | 0.9375rem (igual input del buscador) |
| `.quote-wa-btn` y `.quote-modify` | height/min-height **50px**, font-size 0.9375rem, border-radius 10px, width 100% |

**Rationale**: FR-001/FR-004. Hoy líneas 0.78rem y WA 0.82rem / padding 9px vs Modificar 44px.

**Alternatives considered**: Todo a 16px (rompe paridad con labels 14px del form).

## Media 1280

**Decision**: Borrar o no compactar `.quote-summary` / `.quote-lines` en `@media (min-width: 1280px)` (hoy `font-size: 0.85rem` en líneas).

**Rationale**: US2: no “modo admin” solo en escritorio.

**Alternatives considered**: Compactar más en desktop (rechazado por spec).
