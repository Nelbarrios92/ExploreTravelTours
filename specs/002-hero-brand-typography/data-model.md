# Data Model: Identidad tipográfica del Hero

No hay persistencia. El “modelo” es el bloque de contenido del Hero y sus reglas de presentación.

## Entities

### Identificador de marca

| Campo | Regla |
|-------|--------|
| `text` | Exacto `Explore Travel Tours` (nombre propio, no versales forzadas) |
| `role` | Eyebrow visual; **no** heading de documento |
| `markup` | Elemento no-heading (p. ej. `p.hero-brand`) |
| `font` | `var(--font-display)` (Fraunces) |
| `hierarchy` | Presencia alta; tamaño óptico menor que el H1 (~45–70% en desktop) |

### Titular principal

| Campo | Regla |
|-------|--------|
| `text` | Exacto `Tu viaje comienza con la forma de moverte.` |
| `role` | Único heading principal de la página (`h1.hero-title`) |
| `font` | `var(--font-sans)` (Montserrat) |
| `desktopLines` | Tres: `Tu viaje comienza` / `con la forma de` / `moverte.` |
| `mobileLines` | Reflujo libre; no forzar las tres líneas |

### Subtítulo de valor

| Campo | Regla |
|-------|--------|
| `text` | `Transporte privado y vehículos premium para moverte por Cartagena con confianza.` |
| `role` | Apoyo; menor que el H1 |
| `font` | `var(--font-sans)` |
| `forbidden` | Copy genérico de maravillas del Caribe; ofertas/precios/flota nuevas |

### Separación marca–H1

| Campo | Regla |
|-------|--------|
| `type` | Aire vertical + regla 1px sobria |
| `width` | Acotado al identificador (no full-bleed) |
| `emphasis` | No protagonista; sin degradado ni sombra extra |

### Bloque de contenido izquierdo

| Campo | Relación |
|-------|----------|
| Orden | identificador → separación → H1 → subtítulo → CTA → Instagram |
| `align` | Izquierda en desktop; `max-width` del bloque ~640px (existente) |
| `photo` | Fotografía y vehículo siguen visibles a la derecha / entre bloque y buscador |

### Acciones (sin cambio de comportamiento)

| Campo | Regla |
|-------|--------|
| CTA | Label `Explorar servicios`; destino `#experiences` |
| Instagram | URL autoritativa existente |
| Navbar / WhatsApp / buscador | Fuera de este modelo salvo no taparlos |

## Validation

- Un solo `h1` en la página cuyo texto es el mensaje de viaje.
- `--font-display` no aparece en selectores fuera de `.hero-brand` (y fallbacks directos del identificador).
- Playfair (`--font-serif`) no se asigna al identificador ni se retira de títulos de sección.
- El buscador `.hero-footer` no cambia de entidad ni de posición contractual (flush al pie, spec 001).

## State

Sin transiciones. El bloque es estático; el header scrolled y el menú móvil no dependen de este modelo.
