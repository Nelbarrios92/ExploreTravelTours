# Research: Animación de altura del acordeón

## Técnica: grid `0fr` / `1fr`, no `display: none`

**Decision**: Un hijo `.search-composer-body` con `overflow: hidden`. En &lt;768px, `.search-composer` usa `max-height: 100rem` abierto y `max-height: 0` colapsado, `transition: max-height 320ms ease`. Quitar `display: none` del colapso (impide interpolar). `.is-quoted` sigue `display: none !important`.

**Rationale**: `display: none` no anima. `grid-template-rows: 0fr`/`1fr` abre bien en Chromium pero **no pliega** (`1fr` → `0fr`). `max-height` interpola ambos sentidos; 100rem cubre ida y vuelta apilada.

**Alternatives considered**: Solo opacity (rechazado). `0fr`/`1fr` (cierre roto). Medir `scrollHeight` en JS (más código en Modificar).

## Duración y easing

**Decision**: **320 ms**, `ease` (o `ease-in-out`), sin bounce. Chevron de la franja MAY usar la misma duración en `transform`.

**Rationale**: &lt; 0,5 s (FR-003). Misma familia abrir/cerrar.

**Alternatives considered**: 500 ms (límite, se siente lento). Spring/bounce (spec lo prohíbe).

## Toggle vs cotizar / Modificar

**Decision**: La transición CSS solo aplica cuando el compositor **está visible** (no `.is-quoted`). `renderQuote` / `hideQuote` no añaden clases de animación; al cotizar el compositor se oculta al instante; al Modificar reaparece ya a `1fr`.

**Rationale**: Clarificación A (solo franja).

**Alternatives considered**: Animar hideQuote (rechazado).

## Reduced motion

**Decision**: `@media (prefers-reduced-motion: reduce)` → `transition: none` en compositor y chevron. El snap 0fr/1fr equivale a 011.

**Rationale**: FR-005 / constitución (movimiento no forzado).

**Alternatives considered**: Ignorar la preferencia (rechazado).

## Toques rápidos

**Decision**: Confiar en la interpolación CSS hacia la última clase `is-collapsed`. MUST NOT bloquear el botón durante 320 ms.

**Rationale**: SC-004: acaba abierto o cerrado; bloquear retrasaría el gesto.
