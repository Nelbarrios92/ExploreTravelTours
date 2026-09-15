# Research: Acordeón encima de Explorar

## No mover el footer en el DOM

**Decision**: `.hero-footer` permanece **hermano** de `.hero-content` (014). En `max-width: 767px`, `.hero-content { display: contents }` para que mensaje, acciones y footer sean ítems del mismo flex (`.hero-layout`). `order`: mensaje 1, footer 2, acciones 3. `margin-top: auto` en `.hero-footer` (no en `.hero-actions`).

**Rationale**: Clarificación A (par abajo, aire sobre el par). Mover el footer en HTML rompería el pie de escritorio. `order` sin `contents` no puede meter el footer entre los hijos de `.hero-content`.

**Alternatives considered**: Duplicar `#hero-search` (rechazado). Grid en el layout con áreas distintas por breakpoint (más CSS). JS `insertBefore` al resize (G5).

## Aire y apertura 012

**Decision**: El auto-margen en el footer hace de aire. Al crecer el compositor (012), el par baja o el aire se come; `.hero-message` sigue `order: 1` arriba (013 / SC-002). Explorar (`order: 3`) queda bajo el form.

**Rationale**: US2. MUST NOT `position: absolute` del acordeón sobre Explorar.

**Alternatives considered**: Pegar footer a `.hero-message` (rechazado, clarificación A).

## Desktop

**Decision**: ≥768px sin `display: contents` ni `order`. `.hero-actions` sin el `margin-top: auto` de 013 (ese auto solo 767, ahora en footer).

**Rationale**: FR-005 / 014.

**Alternatives considered**: `order` también en desktop (innecesario).
