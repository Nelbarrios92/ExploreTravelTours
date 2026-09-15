# Research: Buscador compacto en móvil

## Dónde aplicar (breakpoint)

**Decision**: Compactación y ocultar intercambio en **`max-width: 767px`**. A **768px** el grid ya pone origen | swap | destino en una fila; ahí el intercambio **sigue**.

**Rationale**: Spec: swap solo cuando los lugares comparten fila. El `max-width: 768px` actual **incluye** 768 y choca con `min-width: 768px`; 010 no debe apagar el swap en tablet.

**Alternatives considered**: `max-width: 768px` (ocultaría swap en el primer ancho de fila). Quitar el botón del HTML (rompe escritorio y JS).

## Ocultar swap sin hueco

**Decision**: En el CSS **base** (móvil-first), quitar `"swap"` de `grid-template-areas` de Transporte (solo ida e ida y vuelta) y `.swap-places { display: none }` bajo 767px. Los media **≥768px** ya reponen `origin swap dest` y muestran el botón.

**Rationale**: `display: none` dejando el área `swap` deja una pista vacía (el “sobrante” visual).

**Alternatives considered**: Solo `visibility: hidden` (reserva espacio). `position: absolute` (frágil).

## Escala moderada (clarificación A)

**Decision** (solo &lt;768px, `#hero-search` **sin** `.is-quoted`):

| Pieza | Hoy | 010 moderado |
|-------|-----|----------------|
| Padding card | 12–14px / 8px en max-768 | **8px 10px** |
| `.field` gap / panel gap | 6px / 10px | **4px / 8px** |
| Labels | 0.875rem | **0.8125rem** |
| Inputs | height **50px**, pad 12px 14px | height **44px**, pad **8px 12px**, tipo **0.875rem** |
| Tabs / pills viaje | min-height 40px | **36px** |
| `.search-submit` | 50px | **50px** (CTA principal) |
| Intercambio | fila propia ~50px | **no visible**, sin pista |

Suelo: MUST NOT 0.78rem ni CTA &lt;48px. MUST NOT tocar `.field` / `.search-submit` en ≥768px.

**Rationale**: Clarificación A. 44px campos + 50px CTA; Hero gana altura (~una fila de swap + ~6px×N campos).

**Alternatives considered**: Solo ocultar swap (C, rechazado). Achicar CTA a 42px (B, rechazado).

## Apilado a ancho completo (clarificaciones 2–3)

**Decision**: Bajo 767px, Transporte y Por horas: `grid-template-columns: 1fr`; **una** área por fila; CTA `width: 100%`. MUST NOT `fecha | hora` ni `origen | destino`. El 2-col de hourly a **768px** se conserva (tablet).

**Rationale**: Usuario eligió todo apilado. El 2-col de 768 no es teléfono.

**Alternatives considered**: Parejas fecha\|hora (rechazado). Origen\|destino sin swap (rechazado).

## JS / HTML / 009

**Decision**: Dejar `#swap-places` en `index.html` y el listener. No tocar `.is-quoted` ni `.quote-*`.

**Rationale**: El botón solo aplica en escritorio; 007/009 fuera de alcance.

**Alternatives considered**: `hidden` por JS al resize (innecesario si CSS lo cubre).
