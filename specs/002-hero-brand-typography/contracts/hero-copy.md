# Contract: Copy del bloque de marca del Hero

Idioma: español. No anglicismos nuevos.

## Textos autoritativos

| Superficie | Texto | Inmutable |
|------------|--------|-----------|
| Identificador | `Explore Travel Tours` | Sí |
| H1 | `Tu viaje comienza con la forma de moverte.` | Sí |
| H1 línea 1 (desktop) | `Tu viaje comienza` | Sí (partición visual) |
| H1 línea 2 (desktop) | `con la forma de` | Sí |
| H1 línea 3 (desktop) | `moverte.` | Sí (incluir el punto) |
| Subtítulo | `Transporte privado y vehículos premium para moverte por Cartagena con confianza.` | Sí para esta feature |
| CTA | `Explorar servicios` | Sí (reemplaza “Ver Servicios” en este botón) |

## SEO (no cambiar en esta feature)

| Campo | Conservar |
|-------|-----------|
| `<title>` | Actual (agencia / Caribe) |
| `meta description` | Actual |
| `canonical` | `https://www.exploretours.co/` |
| JSON-LD `TravelAgency.name` | Explore Travel Tours (o el valor ya publicado) |
| `og:*` | Actual |

El cambio de H1 visible **no** autoriza vaciar Schema.org ni el nombre en metadatos.

## Prohibido

- Restaurar “Descubre las incomparables maravillas del Caribe…” como subtítulo del Hero.
- Alterar el H1.
- Versales completas en el identificador.
- Nuevos bullets de beneficios, destinos o precios en este bloque.

## Acciones (comportamiento)

| Control | Destino |
|---------|---------|
| Explorar servicios | `#experiences` (igual que el CTA actual) |
| Instagram | `https://www.instagram.com/exploretraveltoursco` |
| WhatsApp header/flotante | Contrato [whatsapp.md](../../001-homepage-discovery-booking/contracts/whatsapp.md) |
