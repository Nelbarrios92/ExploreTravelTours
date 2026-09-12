# Feature Specification: Categoría de alojamientos en Experiencias

**Feature Branch**: `003-lodging-category`

**Created**: 2026-09-11

**Status**: Draft

**Input**: User description: "Implementar en Experiencias una nueva categoría de alojamientos o apartamentos, manteniendo el mismo estilo de card que ya se usa en experiencias."

## Clarifications

### Session 2026-09-11

- Q: ¿Etiqueta del chip de filtro? → A: **Alojamientos** (una sola categoría; cubre apartamentos y otros hospedajes).
- Q: ¿Qué ofertas publicar? → A: Lista suministrada por el negocio (nombre, zona, 1–2 frases, foto si existe).

### Session 2026-09-12

- Q: ¿Listado concreto de alojamientos? → A: Dos ofertas: **Apartamento Laguito** (El Laguito, Cartagena) y **Apartamento Torices** (Torices, Cartagena). Fotos: las que suba el negocio para cada inmueble; no reutilizar fotos de tours.

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Filtrar alojamientos en el catálogo (Priority: P1)

Un visitante en la homepage llega a Experiencias para ver qué ofrece Explore Travel Tours. Además de city tours, traslados, barcos e islas y destinos Caribe, ve un filtro de **alojamientos** (apartamentos u hospedaje que la agencia comercializa). Al pulsarlo, el catálogo muestra solo esas ofertas. Cada una se presenta con el **mismo tipo de tarjeta** que el resto: imagen, título, descripción breve y CTA para reservar por WhatsApp. En “Todas” esas tarjetas aparecen junto a las experiencias actuales. No hay una sección nueva aparte ni un diseño de card distinto.

**Why this priority**: Sin el filtro y las tarjetas visibles, la categoría no existe para el visitante. Es el incremento mínimo de valor.

**Independent Test**: En Experiencias, usar el nuevo chip, ver solo alojamientos, volver a Todas y reconocer las mismas cards que las demás categorías (misma estructura visual).

**Acceptance Scenarios**:

1. **Given** un visitante en la sección Experiencias, **When** mira los filtros, **Then** ve un chip con la etiqueta exacta **Alojamientos** además de Todas, City tours, Traslados, Barcos e islas y Destinos Caribe.
2. **Given** el chip Alojamientos, **When** el visitante lo activa, **Then** ve exactamente las cards **Apartamento Laguito** y **Apartamento Torices** (y ninguna experiencia de otra categoría); nunca “0 experiencias” ni “Próximamente”.
3. **Given** el filtro Todas, **When** el visitante lo activa, **Then** ve las experiencias ya publicadas y las nuevas cards de alojamiento en el mismo listado.
4. **Given** una card de alojamiento, **When** el visitante la compara con una card de city tour, **Then** comparte el mismo estilo: imagen, título, texto breve y botón de reserva por WhatsApp, sin un layout especial de “inmueble”.

---

### User Story 2 - Consultar un alojamiento por WhatsApp (Priority: P1)

Un visitante interesado en quedarse en Cartagena (o zona que Explore ofrezca) elige un alojamiento y usa el CTA de la card. Se abre el contacto por WhatsApp hacia el número comercial de Explore, con un mensaje en español que identifica ese alojamiento. No hay checkout, calendario de disponibilidad ni pago en el sitio.

**Why this priority**: La categoría solo convierte si el siguiente paso es el mismo modelo operativo que el resto del catálogo.

**Independent Test**: Pulsar el CTA de una card de alojamiento y comprobar que inicia WhatsApp con el nombre de esa oferta, igual que una experiencia existente.

**Acceptance Scenarios**:

1. **Given** una card de alojamiento, **When** el visitante usa Reservar por WhatsApp, **Then** inicia conversación con Explore (`+57 304 214 3149`) en una nueva vista, con un mensaje que nombra esa oferta.
2. **Given** ese flujo, **When** se completa, **Then** el sitio no pide tarjeta, fechas de check-in obligatorias ni un formulario enviado a un servidor.

---

### User Story 3 - Reconocer el catálogo unificado (Priority: P2)

Un visitante que ya conocía Experiencias no percibe un rediseño de la sección: mismos chips, misma grilla, mismo tono. El texto de apoyo de la sección puede mencionar alojamiento si hace falta, sin cambiar la navegación del sitio ni añadir un ítem de menú “Apartamentos”. El Hero, testimonios y FAQ no se rediseñan en esta feature (el FAQ MAY mencionar alojamiento más adelante; no es obligatorio aquí).

**Why this priority**: Reduce riesgo de romper el catálogo actual; aporta coherencia una vez que el filtro ya funciona.

**Independent Test**: Recorrer Experiencias: filtros previos siguen funcionando; no hay página ni menú nuevos.

**Acceptance Scenarios**:

1. **Given** los filtros City tours, Traslados, Barcos e islas y Destinos Caribe, **When** el visitante los usa, **Then** el comportamiento y las ofertas previas se conservan.
2. **Given** la navegación, **When** el visitante busca alojamientos, **Then** llega por Experiencias y el chip; MUST NOT aparecer un enlace de menú nuevo obligatorio.

---

### Edge Cases

- Categoría vacía: MUST NOT publicarse el chip si no hay al menos una oferta real de alojamiento.
- Filtro activo de alojamientos: no mostrar cards de otras categorías.
- Imagen ausente o pendiente de subida: MUST NOT usar la foto de un tour u otro destino como si fuera ese apartamento. Cada card MUST usar la imagen que el negocio asigne a ese inmueble.
- Capacidad, amenidades y zonas: MUST limitarse a lo indicado por el negocio para cada oferta (p. ej. Torices: 5 personas y el equipamiento descrito; Laguito: 2 habitaciones y ubicación). MUST NOT añadir tarifas ni check-in inventados.
- Nombres o precios inventados: MUST NOT publicar tarifas, cupos, amenidades de lujo no confirmadas ni edificios ficticios.
- “Todas”: incluye alojamientos y el resto; el recuento visible nunca es cero.
- Móvil: chips y cards usables; el menú no tapa el catálogo.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: El catálogo de Experiencias MUST incluir la categoría **Alojamientos** (apartamentos u otro hospedaje que Explore comercializa) como chip de filtro, al mismo nivel que las categorías actuales.
- **FR-002**: La etiqueta visible del chip MUST ser exactamente `Alojamientos`. MUST NOT usar un segundo chip “Apartamentos”.
- **FR-003**: Cada oferta de esta categoría MUST presentarse como card del mismo tipo que las experiencias actuales: imagen, título, descripción breve y CTA de reserva por WhatsApp.
- **FR-004**: El visitante MUST poder filtrar por Alojamientos y por Todas; el filtro MUST ocultar las cards que no correspondan, sin dejar la grilla vacía para una categoría publicada.
- **FR-005**: El catálogo MUST publicar exactamente estas dos ofertas de Alojamientos (ni más ni menos en este alcance), con el copy autorizado:

  1. **Apartamento Laguito** — zona El Laguito, Cartagena. Descripción: apartamento cómodo y acogedor de 2 habitaciones, en El Laguito, cerca de la playa, restaurantes, supermercados y principales atractivos turísticos de Cartagena; ideal para familias, parejas o grupos que buscan comodidad y una excelente ubicación. Imagen: la que suba el negocio para este inmueble.
  2. **Apartamento Torices** — zona Torices, Cartagena. Descripción: apartamento de 2 habitaciones con capacidad para 5 personas, con camas dobles, aire acondicionado, cocina equipada, comedor, TV, nevera y piscina; cerca del Centro Histórico y otros sitios de interés de Cartagena. Imagen: la que suba el negocio para este inmueble.

  MUST NOT añadir otros inmuebles ni inventar precios.
- **FR-006**: El CTA de cada card de alojamiento MUST abrir WhatsApp al número comercial de Explore con un mensaje en español que identifique esa oferta. MUST NOT añadir checkout ni pasarela.
- **FR-007**: Las categorías y cards ya publicadas (city tours, traslados, barcos/islas, destinos Caribe) MUST conservarse. MUST NOT rediseñar el sistema de cards ni crear una grilla paralela.
- **FR-008**: MUST NOT mostrar “Próximamente”, recuentos en cero, ni una sección de alojamientos fuera de Experiencias en este alcance.
- **FR-009**: La interfaz MUST permanecer en español. Copy de alojamiento MUST ser cercano y de servicio, sin inventar precios, horarios de check-in, capacidad o amenidades no indicadas por el negocio.
- **FR-010**: Esta feature MUST NOT cambiar la arquitectura de navegación, el Hero, testimonios ni el modelo de reserva (solo WhatsApp).

### Key Entities

- **Categoría Alojamientos**: Agrupación nueva del catálogo. Un chip; al menos una oferta real; mismo mecanismo de filtro que el resto.
- **Oferta de alojamiento**: Card vendible. En este alcance, exactamente dos:

  | Título | Zona | Notas de contenido |
  |--------|------|---------------------|
  | Apartamento Laguito | El Laguito, Cartagena | 2 habitaciones; playa y servicios cercanos; familias, parejas o grupos |
  | Apartamento Torices | Torices, Cartagena | 2 habitaciones; 5 personas; equipamiento y piscina indicados por el negocio; cerca del Centro Histórico |

  Atributos de card: título, descripción breve (la autorizada), imagen propia con `alt` descriptivo, categoría Alojamientos, CTA WhatsApp.
- **Card de experiencia (tipo existente)**: Plantilla visual a reutilizar (no una plantilla nueva de ficha inmobiliaria).

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Un visitante nuevo localiza el chip **Alojamientos** y ve las dos ofertas (Laguito y Torices) en menos de 30 segundos desde que llega a Experiencias.
- **SC-007**: Un revisor confirma que no hay una tercera card de alojamiento no listada en FR-005 y que el copy visible coincide con el autorizado (sin precios inventados).
- **SC-002**: El 100% de las cards de alojamiento usan el mismo tipo de tarjeta (imagen + título + texto + CTA WhatsApp) que las experiencias actuales; un revisor no identifica un diseño de card distinto.
- **SC-003**: Con el filtro de alojamientos activo, el 100% de las cards visibles pertenecen a esa categoría; con Todas, alojamientos y ofertas previas coexisten.
- **SC-004**: El 100% de los CTA de alojamiento inician WhatsApp con el contexto de esa oferta, sin pago en el sitio.
- **SC-005**: Tras el cambio, un revisor confirma que city tours, traslados, barcos e islas y destinos Caribe siguen filtrables y visibles como antes.
- **SC-006**: 0 categorías publicadas con listado vacío o etiqueta “Próximamente”.

## Assumptions

- Una sola categoría **Alojamientos** cubre apartamentos y otros hospedajes (no dos chips).
- El inventario de este alcance es **Apartamento Laguito** y **Apartamento Torices**. Cualquier otro inmueble queda fuera hasta una nueva instrucción.
- Las fotografías las aporta el negocio (una por apartamento). La implementación no sustituye con fotos de city tours u otros destinos.
- Explore ya ofrece o quiere ofrecer hospedaje; esta instrucción de negocio autoriza **añadir el tipo de oferta** al catálogo, no inventar inmuebles.
- El CTA de las cards nuevas sigue el mismo patrón de mensaje que el catálogo actual (interés/reserva por nombre de la oferta).
- No hay motor de disponibilidad: el valor es descubrir y consultar por WhatsApp.
- Fotos: una imagen por card, con `alt` descriptivo; no reutilizar una foto de tour como si fuera el apartamento.
- El copy introductorio de la sección Experiencias MAY mencionar alojamientos de forma breve; no es un rediseño de la sección.
- Responsive: mismos anchos de referencia del sitio (375 / 768 / 1280).

## Out of Scope

- Calendario de disponibilidad, motor de reservas, pasarela o precios publicados.
- Ficha larga tipo Airbnb, mapa, galería compleja o comparación de inmuebles.
- Nueva página o ítem de menú “Apartamentos”.
- Rediseño de las cards existentes o de otras secciones (Hero, FAQ obligatorio, testimonios).
- Dos categorías simultáneas (p. ej. un chip Hoteles y otro Apartamentos).
- Inventar edificios, barrios, tarifas o amenidades no confirmados por el negocio.
