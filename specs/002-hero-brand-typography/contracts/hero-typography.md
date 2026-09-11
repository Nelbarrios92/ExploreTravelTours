# Contract: Tipografía y composición del Hero

Superficie: `.hero-content` dentro de `.hero-section`. No aplica a `.hero-search`.

## Tokens

| Token | Valor |
|-------|--------|
| `--font-sans` | `'Montserrat', sans-serif` (existente) |
| `--font-serif` | `'Playfair Display', serif` (existente; **no** identificador) |
| `--font-display` | `'Fraunces', serif` (**solo** identificador) |

Google Fonts: un único `link` que incluye Montserrat, Playfair Display y Fraunces (`display=swap`).

## Mapa de clases

| Clase | Elemento | Fuente | Notas de escala |
|-------|----------|--------|-----------------|
| `.hero-brand` | no-heading | `--font-display` | `clamp` intermedio; peso 400–600; letter-spacing ligero; color blanco; text-shadow existente o equivalente |
| `.hero-brand-rule` | `hr` o `span` decorativo | n/a | 1px, opacidad ~0.55–0.75, ancho ≤ identificador, `aria-hidden="true"` |
| `.hero-title` | `h1` | `--font-sans` | `clamp` **mayor** que `.hero-brand`; line-height ~1.05–1.15; peso 600–700 |
| `.hero-subtitle` | `p` | `--font-sans` | `clamp` menor que el H1 (orden de magnitud actual ~1–1.5rem) |
| `.lets-go-btn` | CTA | `--font-sans` | Estilo existente; solo label |

Relación de tamaño desktop (1280): óptico H1 > marca > subtítulo. Marca visible “a distancia de primer pantallazo” sin igualar al H1.

## Saltos del H1

- Desktop `min-width: 1024px`: tres líneas fijas (contrato de copy).
- `< 1024px`: sin saltos forzados; wrap natural.
- Implementación sugerida: `span.hero-title-line { display: block }` solo desde 1024px, o `br.hero-title-break` ocultos bajo 1024px.

## Layout

- `.hero-content`: `align-items: flex-start`, `text-align: left`, `max-width` ~640px (conservar).
- Fotografía: no nueva capa que tape el vehículo; overlay existente.
- `.hero-footer` / `.hero-search`: sin cambios de contrato 001 (flush al pie).

## Responsive

| Ancho | Marca | H1 |
|-------|--------|-----|
| ~1280 | Considerable, subordinada | Tres líneas, dominante |
| ~768 | Reducción proporcional vía `clamp` | Reflujo; jerarquía intacta |
| ~375 | Más pequeña; 1–2 líneas naturales | Sin tres líneas forzadas |

Prohibido: `font-size` mágico solo a 1440px; sombras extra; degradados decorativos; `text-transform: uppercase` en el identificador.

## Accesibilidad

- Un `h1` cuyo texto accesible es el mensaje de viaje (los `span` de línea no añaden puntuación extra rara).
- Contraste de texto blanco sobre overlay: no empeorar respecto al Hero actual.
- Zoom de texto del sistema: el bloque no se solapa de forma ilegible; el hero MAY crecer (ya permitido en móvil).
- La regla es puramente visual (`aria-hidden`).
