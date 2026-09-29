# Research: Categoría de alojamientos en Experiencias

## 1. Mecanismo de filtro

**Decision**: Reutilizar `setCatalogFilter` / `initCatalog` en `script.js`. Chip `data-filter="alojamientos"` y cards `data-category="alojamientos"`.

**Rationale**: El código ya muestra la card si `filter === 'todas' || category === filter`. Un chip extra en el DOM basta. YAGNI.

**Alternatives considered**: Rama JS por categoría — innecesaria. Segunda grilla — viola FR-007.

## 2. Identificadores y etiqueta

**Decision**: Categoría `alojamientos`. IDs: `apartamento-laguito`, `apartamento-torices`. Chip visible: `Alojamientos`.

**Rationale**: Spec FR-002; slugs alineados al data-model 001 (`kebab-case`).

**Alternatives considered**: `apartamentos` como id — rechazado (etiqueta de negocio es Alojamientos).

## 3. Markup de card

**Decision**: Copiar la estructura de una card existente (`article.service-card.fade-in-scroll`, `card-image-wrapper`, `card-content`, `card-btn` + `data-wa-title`). CTA pintado por el bucle existente `Hola, me interesa reservar: {title}.`

**Rationale**: SC-002 / mismo estilo. `initCatalog` ya asigna `href` a todos `.card-btn[data-wa-title]`.

**Alternatives considered**: Ficha con mapa, galería o precio — fuera de alcance.

## 4. Imágenes

**Decision**: Una foto por inmueble en `assets/`, nombres preferidos `apartamento-laguito` y `apartamento-torices` (extensión la del archivo subido: png/jpg/webp). `alt` descriptivo (zona + tipo). MUST NOT usar `cartagena.png` ni otras fotos de tours.

**Rationale**: Spec y constitución. Si al implementar aún no están los archivos, la tarea de assets queda bloqueada hasta que el negocio los deposite; no se publica el chip con imagen ajena.

**Alternatives considered**: Placeholder genérico de stock — rechazado (puede parecer otro destino).

## 5. Intro de sección

**Decision**: Actualizar el párrafo de `.section-header` para mencionar alojamientos de forma breve, p. ej. incluir “alojamientos” junto a city tours, traslados, barcos e islas y destinos. No cambiar el `h2`.

**Rationale**: Spec MAY; el visitante entiende que el catálogo creció. Un h2 nuevo o sección extra está fuera de alcance.

**Alternatives considered**: Dejar el subtítulo igual — válido pero menos claro.

## 6. Sugerencias del buscador del Hero

**Decision**: No añadir Laguito/Torices a `relatedSuggestions` en esta feature.

**Rationale**: El flujo de cotización es transporte/por horas; mezclar apartamentos ahí cambia alcance. Spec FR-010.

**Alternatives considered**: Sugerir alojamiento si el destino es Cartagena — pospuesto.

## 7. Constitución / inventario 001

**Decision**: No enmendar constitución. El catálogo 001 sigue siendo el mínimo; 003 añade dos ofertas documentadas. El contrato 001 decía “11 cards / cuatro categorías”: este plan lo **extiende** (13 cards / cinco categorías visibles + Todas) en el contrato de esta feature, sin reescribir 001 entero.

**Rationale**: Evitar drift silencioso: el contrato 003 es la fuente para Alojamientos.

**Alternatives considered**: Parchear catalog.md de 001 — se puede alinear después; no bloquea.
