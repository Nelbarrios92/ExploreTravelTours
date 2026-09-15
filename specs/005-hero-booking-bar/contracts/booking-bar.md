# Contract: Booking bar del Hero

**Surface**: `#hero-search`  
**Supersede visual**: `specs/004-search-form-consistency/contracts/search-layout.md`  
**Negocio**: `specs/001-homepage-discovery-booking/contracts/search-quote.md` (validar + resumen + WhatsApp; **no** el layout 004 del CTA “Buscar”)

## Copy

| Control | Texto |
|---------|--------|
| Submit naranja | `Pedir cotización` |
| CTA resumen | `Continuar por WhatsApp` |
| Tabs | Transporte \| Por horas |
| Pills | Solo ida \| Ida y vuelta |
| Swap | `aria-label="Intercambiar origen y destino"` |

MUST NOT: “Buscar”, “Buscar / Continuar” en el naranja.

## Orden DOM Transporte `.search-fields`

1. Origen  
2. Botón swap (opcional como hermano entre origen y destino)  
3. Destino  
4. Fecha de ida  
5. Fecha de regreso (`.field-return`, `hidden` si solo ida)  
6. Hora  
7. Pasajeros  
8. Submit  

MUST NOT colocar `.field-return` como primer campo.

## Grid ≥1280px

**Solo ida / Por horas:** una fila, 5 campos + CTA (`align-self: end`, altura = input ~48–52px).

**Ida y vuelta** (clase `.is-round-trip` en `.search-fields`):

```
[Origen] [Destino] [Fecha ida] [Fecha regreso]
[Hora]   [Pasajeros]           [Pedir cotización]
```

CTA `grid-column` al final de la fila 2. MUST NOT 7 columnas en una fila.

## Densidad

- Labels ≥14px  
- Control height 48–52px  
- Contraste AA sobre fondo del card  

## Tabs / pills

- Segmented: activo `--brand-blue` + texto blanco; inactivo neutro.  
- Pills viaje: no radio nativo crudo (radio + span estilizado aceptable).  
- Sin `.search-chrome` vacío en Por horas.

## Post-submit

1. `preventDefault`  
2. Validar (contratos 001)  
3. Pintar `#quote-summary` **visible** encima del form  
4. `#quote-wa-btn` con `buildWhatsAppUrl`  
5. MUST NOT `mainHeader.classList.add('has-request')`  
6. MUST NOT `quoteSummary.hidden = true` en el éxito  

## FAB

`.floating-wa` `visibility: hidden` (y sin clics) mientras `#hero-search` intersecta el viewport. Restaurar al hacer scroll al catálogo.

## Header

Eliminar o no usar `.nav-request` y `.request-action` como UI de confirmación. Conservar Contactar Ya.

## Hero (mínimo)

`.lets-go-btn` visualmente secundario respecto a la booking bar. No cambiar `.hero-brand` / titular.

## Selectores JS de negocio a conservar

`#search-form-transporte`, `#search-form-hourly`, `input[name="trip-type"]`, nombres de campo, `#errors-*`, `#same-place-prompt`, `#switch-to-hourly`, `#quote-summary`, `#quote-wa-btn`.

## Prohibido

npm, datepicker, precios, mapas, copiar Uber/Airbnb, dual feedback, chrome vacío tipo 004.
