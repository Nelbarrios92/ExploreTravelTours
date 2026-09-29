# Contract: Catálogo — delta Alojamientos

**Surface**: homepage `#experiences`  
**Extiende**: [catalog.md](../../001-homepage-discovery-booking/contracts/catalog.md)  
**Consumers**: visitante; `script.js` `initCatalog` / `setCatalogFilter`

## Markup (sin cambio de plantilla)

```html
<button type="button" class="filter-chip" data-filter="alojamientos" aria-pressed="false">Alojamientos</button>
```

```html
<article class="service-card fade-in-scroll" data-experience-id="{id}" data-category="alojamientos">
  <!-- imagen, h3, p, a.card-btn[data-wa-title] como el resto del catálogo -->
</article>
```

`{id}` ∈ `apartamento-laguito` | `apartamento-torices`.

## Filtros visibles (orden sugerido)

Todas → City tours → Traslados → Barcos e islas → Destinos Caribe → **Alojamientos**

(El chip nuevo al final evita reordenar hábitos; MAY intercalarse si el wrap queda mejor, pero la etiqueta MUST ser `Alojamientos`.)

## Filtro (comportamiento)

| Input | Output |
|-------|--------|
| `todas` | 13 cards (11 previas + 2 alojamientos) |
| `alojamientos` | Solo las 2 cards de esta categoría |
| categorías 001 | Igual que antes (sin las 2 nuevas) |

Cards ocultas: atributo `hidden` (implementación actual). No eliminar nodos.

Ancla `#destinations`: sigue siendo solo Destinos Caribe. MUST NOT activar Alojamientos.

## Card mínima (igual 001)

- Imagen propia del inmueble, `alt` no vacío (mencionar apartamento y zona)
- `h3` = título del data-model
- Párrafo = copy autorizado (data-model)
- CTA WhatsApp: [whatsapp.md](../../001-homepage-discovery-booking/contracts/whatsapp.md) mensaje de card `Hola, me interesa reservar: {title}.`

## Prohibido

- Chip sin las 2 cards
- Tercer inmueble
- “Próximamente” / recuento 0
- Foto de tour como foto del apartamento
- Precios, calendario, ficha tipo Airbnb
- Rediseñar `.service-card` o `.filter-chip` salvo wrap/overflow de chips

## Intro de sección

El subtítulo de `#experiences` MAY citar alojamientos. El `h2` se conserva.
