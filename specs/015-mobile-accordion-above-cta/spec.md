# Feature Specification: Acordeón móvil encima de Explorar servicios

**Feature Branch**: `015-mobile-accordion-above-cta`

**Created**: 2026-09-15

**Status**: Draft

**Input**: User description: "en mobile quiero cambiar de posicion el buscador, que el acordeon salga encima del boton explorar servicios"

## Relación con las features anteriores

**015 es la fuente vigente solo para el orden vertical del buscador respecto a Explorar servicios en vista estrecha.**

| Tema | Estado en 015 |
|------|----------------|
| 011/012: franja Pedir cotización, cerrado al cargar, animación de altura | **Se conservan.** Solo cambia **dónde** está el bloque. |
| 013: título arriba, descripción junta, mensaje que no salta al abrir | **Se conservan.** Explorar ya no va “pegado al pie del buscador”: el buscador queda **encima** de Explorar. |
| 014: barra de escritorio al pie del Hero, sin acordeón | **Se conserva.** MUST NOT mover el buscador de escritorio. |
| 006–009, WhatsApp, copy | **Se conservan.** |

## Clarifications

### Session 2026-09-15

- Q: ¿El acordeón sube junto al título o solo se intercambia con Explorar? → A: **Par abajo**: título/descripción arriba; aire; **franja Pedir cotización y, debajo, Explorar**. MUST NOT pegar el buscador a la descripción ni quitar el aire de 013.

## User Scenarios & Testing *(mandatory)*

### User Story 1 - En el teléfono, Pedir cotización está sobre Explorar (Priority: P1)

Un visitante en el móvil ve el Hero. Quiere cotizar **antes** de bajar a Explorar servicios: la franja **Pedir cotización** (y el formulario al abrir) MUST aparecer **encima** del botón Explorar servicios, no debajo.

**Why this priority**: Es el único cambio pedido: posición del acordeón respecto a ese botón.

**Independent Test**: En ~375px, cerrado: marca/descripción arriba; **aire**; franja Pedir cotización; **debajo** Explorar servicios.

**Acceptance Scenarios**:

1. **Given** ~375px con el acordeón cerrado, **When** mira el Hero, **Then** la franja Pedir cotización está **justo encima** de Explorar servicios, **abajo** del pantallazo (no pegada al título).
2. **Given** el mismo pantallazo, **When** abre el acordeón, **Then** el formulario crece **hacia el aire** (arriba del par) o empuja Explorar un poco; Explorar sigue **debajo** del buscador.
3. **Given** ~1280px, **When** mira el Hero, **Then** el buscador sigue en el **pie** (014), sin acordeón, y Explorar no cambia de rol.

---

### User Story 2 - Abrir el acordeón no desordena el mensaje (Priority: P1)

Al abrir Pedir cotización, título y descripción siguen anclados arriba (013). El par franja+Explorar está abajo; el crecimiento se come el **aire** entre descripción y ese par. Explorar permanece **bajo** el formulario.

**Why this priority**: 013 no debe romperse al reordenar el pie.

**Independent Test**: En ~375px, anotar título; abrir; el título casi no se mueve; Explorar baja o se mantiene bajo el form.

**Acceptance Scenarios**:

1. **Given** acordeón cerrado en ~375px, **When** abre, **Then** título y descripción se desplazan **menos de ~8 px**.
2. **Given** el panel abierto (solo ida), **When** busca Explorar servicios, **Then** el botón está **completo y tocable debajo** del formulario.
3. **Given** cierre de la franja, **When** el panel se pliega, **Then** Explorar vuelve a verse bajo la franja, sin intercalarse en el mensaje.

---

### User Story 3 - Cotizar y Modificar respetan el nuevo orden (Priority: P2)

Resumen 009 y Modificar en móvil: el card o el formulario abierto siguen **encima** de Explorar servicios (no reaparecen bajo el botón).

**Why this priority**: El flujo 007 no debe recolocar el buscador al pie.

**Independent Test**: Cotizar en 375 → resumen encima de Explorar; Modificar → form encima de Explorar.

**Acceptance Scenarios**:

1. **Given** envío válido en móvil, **When** aparece el resumen, **Then** está **encima** de Explorar servicios.
2. **Given** Modificar, **When** vuelve el formulario, **Then** el acordeón abierto sigue **encima** de Explorar.

---

### Edge Cases

- Redes sociales del Hero: van **con** Explorar (debajo del acordeón); MUST NOT intercalarse entre franja y formulario.
- Ida y vuelta / teclado: MAY hacer scroll; MUST NOT tapar Explorar **encima** del form.
- Escritorio ≥768: 014; 0 reorden respecto a Explorar.
- MUST NOT cambiar textos de la franja, 012, ni compactación 010 del panel abierto.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: En vista estrecha, el bloque de cotización (franja y, si está abierto, el formulario; o el resumen 009) MUST mostrarse **encima** de Explorar servicios.
- **FR-002**: El orden de lectura móvil MUST ser: mensaje 013 → **aire** → buscador/acordeón → Explorar servicios (y redes con Explorar). MUST NOT pegar el acordeón a la descripción (clarificación A).
- **FR-003**: 011/012 MUST conservarse (cerrado al cargar, franja Pedir cotización, altura al toggle).
- **FR-004**: Al abrir, título y descripción MUST mantener posición percibida (013 / Δ &lt; ~8 px); Explorar MAY bajar.
- **FR-005**: Vista ancha MUST conservar 014 (buscador al pie, sin acordeón).
- **FR-006**: MUST NOT alterar copy, WhatsApp, 006 ni validaciones.

### Key Entities

- **Bloque de cotización móvil**: Franja + compositor o resumen; encima de Explorar.
- **Bloque Explorar**: Botón Explorar servicios y redes; debajo del cotizador en móvil.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: En ~375px, cerrado: franja **encima** de Explorar y **en el tercio inferior** (no junto al título). Abierto y cotizado: cotizador sigue encima de Explorar.
- **SC-002**: Al abrir la franja, título/descripción se mueven **&lt; ~8 px**; Explorar sigue tocable bajo el form.
- **SC-003**: En ~1280px, 0 cambio de posición del buscador respecto a 014.

## Assumptions

- Vista estrecha = &lt;768px (011). “Encima” = más arriba en la pantalla, no una capa superpuesta que tape Explorar.
- Las redes viajan con Explorar, debajo del acordeón.
- 013 sigue mandando el mensaje arriba y el aire; 015 solo pone el cotizador **inmediatamente encima** de Explorar, ambos abajo.

## Out of Scope

- Rediseñar el acordeón, 012, 010 o el pie de escritorio 014.
- Catálogo, FAQ, tipografía 002, WhatsApp.
