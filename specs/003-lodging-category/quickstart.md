# Quickstart: Alojamientos en Experiencias

Validación manual. Contratos: [catalog-alojamientos.md](./contracts/catalog-alojamientos.md), [data-model.md](./data-model.md).

## Prerrequisitos

- Servir la raíz del repo con `assets/apartamento-laguito.jpeg` y `assets/apartamento-torices.jpeg` presentes.
- No sustituir con fotos de otros destinos.

## Recorrido

1. Abrir la homepage y ir a Experiencias (`#experiences` o nav).
2. Ver chip **Alojamientos** junto a los filtros existentes.
3. Pulsar Alojamientos: solo **Apartamento Laguito** y **Apartamento Torices**; mismo aspecto que un city tour (imagen, título, texto, WhatsApp).
4. Pulsar Todas: 13 cards; las dos de alojamiento siguen en la grilla.
5. Pulsar City tours / Traslados / Barcos e islas / Destinos Caribe: comportamiento previo; las cards de apartamento no aparecen.
6. CTA de Laguito y de Torices: WhatsApp al número comercial con `Hola, me interesa reservar: {título}.`
7. Nav, Hero, buscador, testimonios, FAQ: sin ítem de menú nuevo ni sección paralela.
8. 375px y 768px: chips usables (wrap/scroll existente); cards apiladas; menú no tapa el CTA.

## Esperado

- 0 “Próximamente” / grilla vacía en Alojamientos.
- Copy alineado al data-model (2 hab. Laguito; 5 personas y equipamiento en Torices).
- `alt` de cada foto describe ese apartamento/zona.

## Fuera de esta prueba

- Disponibilidad, precios, mapa.
- Sugerencias del buscador del Hero apuntando a apartamentos.
