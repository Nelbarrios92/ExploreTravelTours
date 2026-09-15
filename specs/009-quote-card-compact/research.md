# Research: Card de resumen compacta (moderada)

## Dónde aplicar la compactación

**Decision**: Tokens más bajos en `.quote-summary` / CTAs del resumen (solo existen en estado cotizado). Además `#hero-search.is-quoted { padding: 8px 12px; }` (el card al componer sigue 12–14px). MUST NOT cambiar `.search-submit` ni `.field`.

**Rationale**: FR-005. Compactar el card entero en `.is-quoted` baja la placa blanca sin tocar el formulario.

**Alternatives considered**: Compactar todo `#hero-search` siempre (rompería 006).

## Escala moderada (un paso bajo 008)

**Decision**:

| Pieza | 008 (actual) | 009 moderado |
|-------|----------------|--------------|
| h2 | 1.125rem | **1rem** |
| dt / relacionados | 0.875rem | **0.8125rem** (13px) |
| dd | 0.9375rem | **0.875rem** |
| WA / Modificar | 50px / 0.9375rem | **42px** / **0.8125rem** |
| gaps líneas | 8px 16px | **4px 12px** |
| margen h2 / CTAs | 12px / 10px | **8px / 6px** |

Suelo: MUST NOT 0.78rem ni padding 8px de caja gris 007-era.

**Rationale**: Clarificación A. 13px sigue ≥ “legible”; 42px &lt; 50px y ≥ ~40px táctil.

**Alternatives considered**: Solo padding (C, rechazado); 36px/0.7rem (B, rechazado).

## Relacionados

**Decision**: Misma escala de cuerpo; `margin-top` 8px. No ocultar (fuera de spec).

**Rationale**: Edge case: no inflar; no quitar valor de 001.
