# Research: Solo el resumen tras cotizar

## Cómo ocultar el buscador

**Decision**: Clase `#hero-search.is-quoted`. CSS oculta `.search-tabs`, `.search-panel` (ambos forms), `.search-errors` y `#same-place-prompt`. JS pone/quita la clase en `renderQuote` / `hideQuote`. Los `value` de los campos permanecen en el DOM (`hidden` en el form padre no los borra).

**Rationale**: Un wrapper extra no es obligatorio; la clase en el card ya existente evita romper ids. `display: none` en paneles es coherente con `[hidden]` de tabs.

**Alternatives considered**: Borrar/recrear el form (perdería valores); `has-request` en el header (prohibido por 005/007); recargar (rechazado en clarify).

## Modificar

**Decision**: `<button type="button" class="quote-modify" id="quote-modify">Modificar</button>` debajo del CTA verde (secundario visual: borde/azul, no naranja ni verde WhatsApp). Click → `hideQuote()` + `heroSearch.classList.remove('is-quoted')`. No `preventDefault` de submit.

**Rationale**: Clarificación A. Debajo del verde para no competir con conversión.

**Alternatives considered**: Enlace “Volver a cotizar”; botón en el navbar (005 lo quitó).

## Errores de validación

**Decision**: Los `return` actuales de submit que llaman `hideQuote()` **no** añaden `.is-quoted`. Si un éxito previo dejó `.is-quoted`, un nuevo intento inválido no aplica (el buscador ya está visible solo tras Modificar). Tras éxito no se puede reenviar el form oculto.

**Rationale**: FR-005.

**Alternatives considered**: Resetear is-quoted en cada submit al inicio (innecesario si el form está hidden).
