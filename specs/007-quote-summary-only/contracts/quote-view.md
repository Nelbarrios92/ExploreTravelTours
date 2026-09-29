# Contrato UI: vista solo resumen

**007 manda** sobre “formulario visible bajo el resumen” de 005. Ids de negocio (`#search-form-transporte`, `#search-form-hourly`, `#quote-summary`, `#quote-wa-btn`, `#same-place-prompt`) se conservan.

## Estado cotizado

- Contenedor: `#hero-search` con clase `is-quoted`.
- Visible: `#quote-summary` (`hidden` false), `#quote-wa-btn`, `#quote-related` si hay sugerencias, `#quote-modify`.
- Oculto: `.search-tabs`, `#search-form-transporte`, `#search-form-hourly`, `#errors-transporte`, `#errors-hourly`, `#same-place-prompt`.

## Control Modificar

- `id="quote-modify"`
- `type="button"` (MUST NOT submit)
- Texto exacto: **Modificar**
- MUST NOT estar en `.main-header`

## JS

- `renderQuote`: `quoteSummary.hidden = false`; `#hero-search.classList.add('is-quoted')`.
- `#quote-modify` click: `quoteSummary.hidden = true`; `classList.remove('is-quoted')`; limpiar relacionados como `hideQuote`.
- MUST NOT `form.reset()` en Modificar.
- MUST NOT `quoteSummary.hidden = true` en el camino de submit **válido**.

## Copy / WhatsApp

- Naranja **Pedir cotización** no abre WA.
- Verde **Continuar por WhatsApp** → `wa.me/573042143149`.
