# Data Model: Alojamientos en el catálogo

Extiende el modelo de `specs/001-homepage-discovery-booking/data-model.md`. Sin persistencia.

## Category (enum ampliado)

| `id` | Chip visible | `filter` |
|------|----------------|----------|
| *(n/a)* | Todas | `todas` |
| `city-tours` | City tours | existente |
| `traslados` | Traslados | existente |
| `barcos-islas` | Barcos e islas | existente |
| `destinos-caribe` | Destinos Caribe | existente |
| **`alojamientos`** | **Alojamientos** | nuevo |

Estado inicial del filtro: `todas`.

## Experiencia (cards nuevas)

Mismos campos que 001: `id`, `title`, `description`, `image`, `category`, CTA.

| `id` | `title` | `category` | `image` (preferido) |
|------|---------|------------|---------------------|
| `apartamento-laguito` | Apartamento Laguito | `alojamientos` | `assets/apartamento-laguito.jpeg` |
| `apartamento-torices` | Apartamento Torices | `alojamientos` | `assets/apartamento-torices.jpeg` |

### Copy autorizado

**apartamento-laguito**  
Zona: El Laguito, Cartagena.  
Descripción: Apartamento cómodo y acogedor de 2 habitaciones, ubicado en el sector El Laguito, cerca de la playa, restaurantes, supermercados y principales atractivos turísticos de Cartagena. Ideal para familias, parejas o grupos que buscan comodidad y una excelente ubicación.

**apartamento-torices**  
Zona: Torices, Cartagena.  
Descripción: Apartamento de 2 habitaciones con capacidad para 5 personas, equipado con camas dobles, aire acondicionado, cocina equipada, comedor, TV, nevera y piscina. Ubicado estratégicamente cerca del Centro Histórico y otros sitios de interés de Cartagena.

## Validation

- Exactamente estas dos filas en `alojamientos` en este alcance.
- `category` de las 11 cards previas no cambia.
- Filtro `alojamientos` ⇒ 2 visibles; `todas` ⇒ 13.
- WhatsApp: mensaje `Hola, me interesa reservar: {title}.` con el `title` de la tabla.

## State

Sin transiciones propias. Mismo estado de filtro de catálogo (chip `aria-pressed`).
