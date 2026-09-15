# Feature Specification: Buscador de escritorio otra vez en el pie del Hero

**Feature Branch**: `014-desktop-search-footer`

**Created**: 2026-09-15

**Status**: Draft

**Input**: User description: "mira, quiero que no me toques nada en como esta en mobile, el boton de permitir cotizar debe quedar como esta ahora mismo en mobile pero ese buscador en desktop deberia quedar como estaba antes, en el pie del hero"

## Relación con las features anteriores

**014 es la fuente vigente solo para la posición del buscador en escritorio (siempre visible, pie del Hero).**

| Tema | Estado en 014 |
|------|----------------|
| Móvil: acordeón Pedir cotización (011/012), composición 013 | **Se congela.** MUST NOT cambiar franja, animación, ni título/descripción/botón Explorar. |
| 006: una fila Ida y vuelta en escritorio | **Se conserva** una vez el buscador vuelve al pie. |
| 007–009: resumen / Modificar | **Se conservan** en ambos anchos. |
| Copy, validaciones, WhatsApp | **Se conservan.** |

## User Scenarios & Testing *(mandatory)*

### User Story 1 - En el ordenador el cotizador vuelve al pie (Priority: P1)

Un visitante en escritorio ve el primer pantallazo. Quiere la **barra de cotización abajo del Hero**, como antes del recorte móvil: marca y texto arriba/centro, buscador **siempre visible** pegado al pie de esa foto a pantalla completa — no un acordeón ni el formulario “flotando” a media altura.

**Why this priority**: El usuario pide explícitamente restaurar el pie en desktop y no tocar el móvil.

**Independent Test**: En ~1280px, el buscador (tabs + campos 006) está al borde inferior del Hero; no hay franja Pedir cotización.

**Acceptance Scenarios**:

1. **Given** ~1280px al cargar (sin cotizar), **When** mira el Hero, **Then** el buscador está **en el pie** del primer pantallazo, a todo el ancho útil de la barra, **siempre desplegado**.
2. **Given** ese pantallazo, **When** busca la franja móvil Pedir cotización, **Then** **no** la ve: no hay acordeón en escritorio.
3. **Given** Ida y vuelta en ese pie, **When** elige ese modo, **Then** sigue 006 (una fila en ~1280).

---

### User Story 2 - El teléfono no se mueve (Priority: P1)

En el teléfono, **Pedir cotización** (franja), el plegado/desplegado y el Hero 013 (título arriba, descripción junta, Explorar más abajo, mensaje que no salta al abrir) MUST verse **igual que ahora**.

**Why this priority**: “No me toques nada en cómo está en mobile” y “el botón de Pedir cotización debe quedar como está”.

**Independent Test**: En ~375px, mismo recorrido 013+011: cerrado = franja; abrir = formulario; título no salta.

**Acceptance Scenarios**:

1. **Given** ~375px, **When** carga, **Then** solo la franja **Pedir cotización** (cerrada); copy y Explorar servicios como 013.
2. **Given** esa franja, **When** la abre y la cierra, **Then** 011/012 se cumplen; el mensaje del Hero no se recentra.
3. **Given** escritorio y móvil, **When** compara, **Then** el cambio 014 **solo** se percibe en escritorio.

---

### User Story 3 - Cotizar y Modificar en el pie de escritorio (Priority: P2)

En escritorio, enviar y Modificar siguen 007/009 **dentro de esa barra del pie**, no un layout distinto a “como antes”.

**Why this priority**: Restaurar posición no debe romper el flujo de cotización.

**Independent Test**: En ~1280px, Pedir cotización válido → resumen en el pie; Modificar → formulario otra vez en el pie.

**Acceptance Scenarios**:

1. **Given** escritorio, **When** envía válido, **Then** el resumen 009 sustituye el formulario **en el pie del Hero**.
2. **Given** ese resumen, **When** pulsa Modificar, **Then** el formulario vuelve **en el mismo pie**, abierto (sin acordeón).

---

### Edge Cases

- Tablet ~768px: mismo criterio que 011 (sin acordeón a partir de 768); el buscador MUST estar al pie del Hero, no a media foto.
- Rotar de móvil a escritorio: desaparece la franja; aparece la barra completa al pie; datos del formulario se conservan.
- MUST NOT reintroducir acordeón en desktop ni compactación 010 en desktop.
- MUST NOT cambiar textos, WhatsApp ni catálogo.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: En vista ancha, el buscador MUST anclarse al **pie del Hero** (primer pantallazo), como la barra 005/006 anterior al recorte móvil.
- **FR-002**: En vista ancha, el buscador MUST estar **siempre visible** al componer. MUST NOT mostrar la franja Pedir cotización ni plegar el formulario.
- **FR-003**: En vista estrecha, MUST NOT alterar 011, 012 ni 013 (franja, animación, composición del copy, Explorar servicios).
- **FR-004**: 006 (ida y vuelta una fila en ~1280), 007–009 y validaciones MUST conservarse.
- **FR-005**: Tras cotizar o Modificar en escritorio, el card / formulario MUST seguir en ese **pie**, no en otra zona del Hero.

### Key Entities

- **Pie de escritorio**: Barra de cotización anclada abajo del Hero en ≥768px.
- **Franja móvil**: Pedir cotización 011; fuera de alcance de cambio.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: En ~1280px, un revisor confirma que el buscador está en el **borde inferior del Hero** (no a media altura) y ocupa el rol de barra de pie.
- **SC-002**: En ~1280px, 0 franja de acordeón. En ~375px, 100% del comportamiento móvil actual (franja + 013).
- **SC-003**: 100% de envíos válidos y Modificar en escritorio ocurren en ese pie; WhatsApp y copy iguales.

## Assumptions

- “Botón de permitir cotizar” = franja **Pedir cotización** del acordeón móvil.
- “Como estaba antes” = barra de cotización **siempre abierta al pie del Hero** (005/006), no el estado intermedio si el buscador quedó subido o metido en la columna de copy.
- Vista estrecha = &lt;768px (igual que 011). Vista ancha = ≥768px.
- No se pide rediseñar campos de escritorio ni densidades 010.

## Out of Scope

- Cambiar el acordeón, la animación 012 o el layout 013 en móvil.
- Cambiar catálogo, FAQ, tipografía 002 o CTAs de WhatsApp.
- Inventar un tercer layout para tablet distinto de “pie sin acordeón”.
