# Contrato UI: acordeón encima de Explorar

**015 manda** el orden vertical en **&lt;768px**. **014** manda **≥768px**.

## MUST

- En `max-width: 767px`: `.hero-content { display: contents }`.
- `order`: `.hero-message` 1, `.hero-footer` 2, `.hero-actions` 3.
- `.hero-footer { margin-top: auto }` (aire 013 sobre el par). MUST NOT `margin-top: auto` en `.hero-actions` en este ancho.
- Franja / form / resumen **encima** de `.lets-go-btn`. Título Δ &lt; ~8 px al abrir.
- ≥768px: sin `contents`/`order` de 015; pie 014.

## MUST NOT

- Superponer el acordeón sobre Explorar (`position` absoluto).
- Pegar el footer a la descripción.
- Cambiar 012, `script.js`, o el árbol de escritorio percibido.
