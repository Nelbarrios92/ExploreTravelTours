# Contract: Layout del buscador del Hero

**Surface**: `#hero-search` (pie de `.hero-section`)  
**Lógica**: [search-quote.md](../../001-homepage-discovery-booking/contracts/search-quote.md) (sin cambio de comportamiento)  
**Consumers**: visitante; `initSearch` en `script.js`

## Esqueleto (ambos modos)

```
#hero-search
  #quote-summary (slim, hidden hasta buscar)
  .search-tabs (dos .search-tab flex iguales)
  form.search-panel
    .search-chrome          /* min-height fija */
    .search-fields          /* grid; último hijo = .search-submit */
    .search-errors
    [#same-place-prompt]    /* solo transporte */
    /* NO .search-submit aquí fuera del grid */
```

## Campo

```html
<label class="field">
  <span class="field-label">Origen</span>
  <input …>
</label>
```

- Label **no** `position: absolute` sobre el input.
- Duración: `<select>` con `<option value="" disabled selected>Selecciona</option>` y `.field-label` “Duración”.
- `.field-return` conserva clase e `input[name="return-date"]`.

## Tabs

| Estado | Fondo | Texto | Borde |
|--------|--------|-------|-------|
| Activo | `--brand-blue` | blanco | `--brand-blue` |
| Inactivo | `#f1f5f9` o equivalente neutro | `#64748b` | `#e2e8f0` |

`flex: 1 1 0`; misma altura (`min-height` ~36–40px).

## Grid `.search-fields`

| Viewport | Columnas | Submit |
|----------|----------|--------|
| &lt;768 | 1 | última fila, `width: 100%`, min-height táctil ≥44px |
| 768–1023 | 2 | full width al cierre |
| 1024–1279 | 3 | al cierre (full width si no cabe en la fila) |
| ≥1280 | `5fr + auto` | misma fila, `height` = input, `align-self: end` |

Ida y vuelta (≥1280): `.field-return` segunda fila; `.search-submit { grid-row: 1; grid-column: 6; }`.

## Paleta

- CTA Buscar: `--brand-orange` (no verde).
- WhatsApp del resumen: `--whatsapp-green`.
- Superficie panel: blanco / `rgba(255,255,255,0.96)`.
- Sombra del panel: más contenida que `0 -8px 40px` actual.

## Selectores JS que MUST seguir existiendo

`#search-form-transporte`, `#search-form-hourly`, `.search-tab[data-mode]`, `.field-return`, `input[name="trip-type"]`, campos `name` del data-model, `#errors-transporte`, `#errors-hourly`, `#same-place-prompt`, `#switch-to-hourly`, `#quote-summary`.

## Prohibido

- Floating label mixto.
- Submit hermano fuera de `.search-fields`.
- Radio falso en Por horas.
- Datepicker de terceros / npm.
- Rediseñar `#quote-summary` más allá de márgenes para alinearlo al panel.
