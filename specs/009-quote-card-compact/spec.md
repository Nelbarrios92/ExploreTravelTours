# Feature Specification: Card de resumen más compacta

**Feature Branch**: `009-quote-card-compact`

**Created**: 2026-09-15

**Status**: Draft

**Input**: User description: "el resumen sigue viendose grande, la card rompe visualmente el hero, reduce la parte de la card del resumen"

## Relación con las features 007–008

`007` sigue vigente: tras Pedir cotización solo se ve el resumen; **Modificar** recupera el buscador. **009 es la fuente vigente para el tamaño del card en estado cotizado.**

| Tema | Estado en 009 |
|------|----------------|
| 008: resumen a la misma escala “grande” que el buscador (cuerpo y botones como Pedir cotización) y llenando el card | **Reemplazado en estado cotizado**: el bloque del resumen MUST ser **más compacto** para no romper el Hero (marca, foto y primer pantallazo). |
| 008: sin caja gris anidada (mismo aire que el card blanco) | **Se conserva** el no-anidar una cajita distinta; se **reduce** padding, tipo y altura de controles del resumen, no se vuelve a un recuadro gris desconectado. |
| Buscador al componer (006 densidad / una fila ida-vuelta) | **Se conserva**; no se pide achicar el formulario. |
| Copy, WhatsApp, Modificar | **Se conservan**. |

## Clarifications

### Session 2026-09-15

- Q: ¿Cuánto se compacta el card cotizado? → A: **Moderada**: más bajo que el buscador; tipo y CTAs un poco más chicos que 008, aún legibles. MUST NOT letra de administración ni conservar botones a la altura de Pedir cotización (~50px). MUST NOT solo recortar padding dejando la escala 008.

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Cotizar sin que el card se coma el Hero (Priority: P1)

El visitante pide cotización y el card blanco del pie del Hero se vuelve solo resumen. Hoy ese bloque se siente **demasiado alto y pesado**: empuja o tapa la composición del Hero (marca, subtítulo, foto). Quiere un resumen **más chico en conjunto**: se lee y se actúa (WhatsApp / Modificar), pero el Hero sigue siendo el primer pantallazo, no un formulario-gigante de confirmación.

**Why this priority**: El usuario reporta que la card rompe el Hero; es un defecto de primera impresión.

**Independent Test**: En ~1280px y ~375px, tras un envío válido, el card de resumen ocupa claramente menos altura visual que el buscador completo; marca/foto del Hero siguen percibiéndose.

**Acceptance Scenarios**:

1. **Given** un Pedir cotización válido, **When** el visitante mira el primer pantallazo, **Then** el card de resumen es un bloque **compacto** al pie (o en su zona actual), no una placa que domine o parta el Hero. NEVER la misma “talla” percibida que el buscador de muchos campos.
2. **Given** ese resumen compacto, **When** lee datos y usa Continuar por WhatsApp y Modificar, **Then** todo sigue legible (compactación **moderada**, no microscópica). Los dos CTAs siguen la **misma** altura entre sí, **menor** que Pedir cotización del buscador.
3. **Given** el Hero (marca, regla, subtítulo), **When** el resumen está visible, **Then** esos elementos de marca no se perciben aplastados ni desplazados fuera de sentido por un card excesivo.

---

### User Story 2 - Compacto también en móvil (Priority: P2)

En 375px el resumen no debe ocupar casi todo el viewport ni empujar todo el Hero fuera de vista. Puede apilar CTAs; debe ser más bajo en conjunto que el buscador de Transporte.

**Why this priority**: En móvil un card alto rompe aún más el primer pantallazo.

**Independent Test**: 375px cotizado: card más bajo que el formulario; CTAs usables; 0 overflow-x.

**Acceptance Scenarios**:

1. **Given** 375px y resumen visible, **When** compara mentalmente con el buscador, **Then** el card cotizado es más bajo; WhatsApp y Modificar siguen pulsables.
2. **Given** 1280px, **When** compara con 375, **Then** la compactación es del mismo sistema (no un desktop enorme y un móvil minúsculo).

---

### Edge Cases

- Ida y vuelta (más filas de datos): MAY crecer un poco en altura; MUST NOT volver al tamaño del buscador de 8 controles.
- Relacionados: si hay enlaces, MUST NOT inflar el card de forma desproporcionada (pueden ir más apretados, misma escala que el cuerpo del resumen).
- Al pulsar Modificar, el buscador recupera su densidad 005/006 (no hereda la compactación del resumen).
- MUST NOT reintroducir “TU SOLICITUD” en el header.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: En estado cotizado, el card del resumen MUST ser **visualmente más compacto** (menos altura percibida) que el buscador de Transporte/Por horas, de modo que **no rompa** la composición del Hero.
- **FR-002**: Esta regla MUST sustituir, solo para el estado cotizado, la de 008 que igualaba el resumen a la talla de campos/botones del buscador.
- **FR-003**: Título, datos, relacionados y CTAs del resumen MUST compartir **una** escala compacta **moderada** (un paso por debajo del buscador 008, no densidad admin). MUST NOT dejar los CTAs del resumen a la misma altura que Pedir cotización.
- **FR-004**: Continuar por WhatsApp y Modificar MUST tener la misma altura entre sí y seguir siendo accionables en 375px.
- **FR-005**: MUST NOT achicar el buscador cuando está visible (componer / Modificar). MUST NOT cambiar copy, WhatsApp, 007 ni el layout de Ida y vuelta 006.

### Key Entities

- **Card cotizado**: `#hero-search` mostrando solo el resumen; talla reducida vs. modo buscador.
- **Hero**: Marca, foto y primer pantallazo que MUST seguir dominando.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Un revisor, en 1280 y 375, confirma que el card cotizado **no** parte el Hero (marca/foto siguen siendo el foco; el resumen es un pie compacto).
- **SC-002**: La altura percibida del card cotizado es **menor** que la del buscador de Transporte en el mismo ancho; los CTAs del resumen se perciben más bajos que Pedir cotización, sin caer a “letra admin”.
- **SC-003**: 100% de las acciones Continuar por WhatsApp y Modificar siguen siendo usables; 0 overflow-x por el resumen.
- **SC-004**: 007 se cumple (solo resumen; Modificar restaura el buscador a su tamaño normal).

## Assumptions

- El problema es **volumen del card cotizado**, no el flujo ni el copy.
- Compactar = **moderado**: menos padding, tipo y botones un paso más bajos que 008, **una sola escala**, sin caja gris anidada. MUST NOT opción C (solo padding) ni B (mínimo agresivo).
- El buscador “grande” al componer es intencional (006/005); solo se reduce el estado resumen.

## Out of Scope

- Rediseñar marca, foto, catálogo o FAQ.
- Quitar Modificar o el resumen.
- Precios o campos nuevos.
