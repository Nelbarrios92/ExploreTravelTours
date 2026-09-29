# Feature Specification: Buscador más compacto en móvil

**Feature Branch**: `010-mobile-search-compact`

**Created**: 2026-09-15

**Status**: Draft

**Input**: User description: "en parte mobile, el buscador se ve grande, y el swift del destino esta sobrando, necesito que mejores esa parte"

## Relación con las features 005–009

**010 es la fuente vigente solo para el buscador en vista estrecha (móvil), mientras se está componiendo.**

| Tema | Estado en 010 |
|------|----------------|
| 006: una fila Ida y vuelta en escritorio ~1280 | **Se conserva.** |
| 005: intercambiar origen y destino | **Se conserva en escritorio**, donde origen y destino van en la misma fila. En móvil ese control **sobra** y MUST no ocuparse espacio. |
| 007–009: tras cotizar, solo resumen compacto; Modificar restaura el formulario | **Se conservan.** Esta feature no cambia el card cotizado. |
| Copy, validaciones, WhatsApp, pills Transporte / Por horas | **Se conservan.** |

## Clarifications

### Session 2026-09-15

- Q: ¿Cuánto se compacta el buscador en el teléfono (además de quitar el intercambio origen/destino)? → A: **Moderada**: menos padding y campos un poco más bajos; Pedir cotización sigue claramente el CTA principal; labels legibles. MUST NOT compactación agresiva (CTA y letra al mínimo) ni limitar el cambio a solo ocultar el intercambio.
- Q: En el teléfono, ¿cómo se colocan origen y destino una vez que desaparece el intercambio? → A: **Apilados** a ancho completo, uno bajo el otro, sin el botón entre ellos. MUST NOT una fila origen \| destino en móvil.
- Q: En móvil, ¿los demás campos (fecha, hora, pasajeros, Pedir cotización) también van apilados, o algunos van en pareja? → A: **Todo apilado** a ancho completo. MUST NOT emparejar fecha \| hora ni otras parejas en el teléfono.

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Primer pantallazo usable en el teléfono (Priority: P1)

Un visitante abre la homepage en el teléfono. El Hero debe seguir viéndose (marca y foto), y el buscador al pie debe caber como una barra de reserva **más contenida**: campos apilados, tapables, sin parecer un formulario de administración inflado. Hoy el panel se siente **grande** en móvil y empuja de más el primer pantallazo.

**Why this priority**: El usuario reporta el tamaño del buscador en móvil; es el primer contacto de conversión en el canal más usado.

**Independent Test**: En ~375px, con Transporte visible (antes de cotizar), un revisor confirma que el panel es visiblemente más compacto que hoy y que marca/foto del Hero siguen percibiéndose.

**Acceptance Scenarios**:

1. **Given** el primer pantallazo en ~375px y el buscador visible, **When** el visitante mira el Hero, **Then** el panel de reserva es un pie **más bajo** por compactación **moderada** (aire y campos un paso más contenidos; Pedir cotización sigue siendo el CTA principal), no un bloque que se come casi todo el viewport ni un formulario de letra mínima.
2. **Given** Transporte o Por horas en móvil, **When** completa campos y pulsa Pedir cotización, **Then** cada campo y el CTA van **a ancho completo**, uno bajo el otro (sin parejas fecha \| hora); labels y botón siguen legibles y pulsables; el significado de las validaciones no cambia.
3. **Given** escritorio ~1280px, **When** usa el buscador, **Then** la barra **no** se achica con esta feature: densidad y una fila de 006 se mantienen.

---

### User Story 2 - Sin control de intercambio en móvil (Priority: P1)

En el teléfono origen y destino van uno debajo del otro. Entre ellos aparece el control de **intercambiar** (el “swift” / flechas de origen–destino). En esa disposición **sobra**: no ahorra un gesto claro y solo añade altura y ruido. El visitante escribe origen y destino por separado; no necesita el botón.

**Why this priority**: El usuario lo señala como elemento que sobra en móvil.

**Independent Test**: En ~375px el control de intercambio no se ve ni se puede pulsar; origen y destino siguen editables. En ~1280px el intercambio sigue visible y funciona.

**Acceptance Scenarios**:

1. **Given** Transporte en ~375px, **When** mira entre Origen y Destino, **Then** **no** hay control de intercambiar; cada campo va **a ancho completo**, uno bajo el otro (nunca una fila origen \| destino en el teléfono).
2. **Given** origen y destino rellenos en escritorio, **When** usa intercambiar, **Then** los valores se invierten como hoy.
3. **Given** Por horas en móvil, **When** mira el formulario, **Then** tampoco aparece un control de intercambio de lugares (no aplica a recogida única).

---

### User Story 3 - Cotizar y modificar sin perder el arreglo móvil (Priority: P2)

Tras Pedir cotización, el visitante ve el resumen compacto (009). Al pulsar **Modificar**, recupera el buscador **ya en la versión compacta de móvil**, sin el control de intercambio.

**Why this priority**: El flujo 007 debe seguir coherente con el nuevo layout estrecho.

**Independent Test**: En 375px: cotizar → resumen 009 → Modificar → buscador compacto sin swap.

**Acceptance Scenarios**:

1. **Given** un envío válido en móvil, **When** ve el resumen, **Then** el card cotizado sigue las reglas de 009 (no se agranda ni se rediseña aquí).
2. **Given** Modificar en móvil, **When** vuelve el formulario, **Then** aplica la compactación de 010 y el intercambio sigue oculto.

---

### Edge Cases

- Ida y vuelta en móvil: más campos (fecha de regreso) MAY alargar el panel; MUST seguir más compacto que el buscador móvil actual, **apilados** (no emparejados), sin scroll horizontal de la página.
- Errores y aviso origen = destino: el mensaje MAY sumar altura; MUST NOT reaparecer el control de intercambio en móvil.
- Rotación o ventana más ancha (tablet/escritorio): cuando origen y destino van **en la misma fila**, el intercambio MUST volver a estar disponible.
- MUST NOT compactar hasta densidad de panel de administración ni recortar labels.
- MUST NOT cambiar el FAB verde de WhatsApp ni el CTA naranja Pedir cotización en significado.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: En vista estrecha (teléfono), el buscador **mientras se compone** MUST verse **más compacto** que hoy con compactación **moderada**: menos padding y campos un poco más bajos, labels legibles, Pedir cotización **sigue siendo** el CTA principal (no se achica al mínimo). MUST NOT compactación agresiva ni dejar el panel del mismo tamaño salvo quitar el intercambio.
- **FR-002**: En esa vista, el control de **intercambiar origen y destino** MUST **no mostrarse**. Origen y destino MUST ir **apilados a ancho completo** (uno bajo el otro). MUST NOT colocarlos en una sola fila en el teléfono. El visitante MUST poder seguir escribiendo cada uno por separado.
- **FR-003**: En vista ancha (escritorio), el buscador MUST conservar densidad y layout vigentes (006 una fila; intercambio origen/destino visible y operativo).
- **FR-004**: La compactación MUST aplicar a **Transporte** (solo ida e ida y vuelta) y a **Por horas** en la misma vista estrecha. En el teléfono, fecha, hora, pasajeros y Pedir cotización MUST ir **apilados a ancho completo**, igual que origen y destino. MUST NOT emparejar campos (p. ej. fecha \| hora) en esa vista.
- **FR-005**: Validaciones, copy, WhatsApp, 007 (solo resumen tras cotizar) y 009 (tamaño del card cotizado) MUST conservarse. MUST NOT rediseñar marca, catálogo ni FAQ.

### Key Entities

- **Buscador en móvil**: Panel de reserva al pie del Hero en viewport estrecho, estado “componer”.
- **Control de intercambio**: Acción que invierte origen y destino; útil en fila horizontal, sobrante cuando los campos están apilados.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Un revisor en ~375px confirma que el buscador **antes de cotizar** es visiblemente más bajo/contenido que antes (compactación **moderada**, no solo sin intercambio), que Pedir cotización se percibe aún como el CTA principal, y que el Hero (marca y foto) se percibe mejor en el primer pantallazo.
- **SC-002**: En ~375px, **0** controles de intercambio visibles; **todos** los campos del buscador (origen, destino, fechas, hora, pasajeros, CTA) se perciben a **ancho completo** apilados; 100% de los envíos válidos siguen pudiéndose completar escribiendo origen y destino (o recogida en Por horas).
- **SC-003**: En ~1280px, intercambiar origen/destino sigue funcionando en un intento; Ida y vuelta sigue en una sola fila (006).
- **SC-004**: 0 overflow horizontal de la página por el buscador en 375 / 768 / 1280. Campos y Pedir cotización siguen usables al tacto en 375.
- **SC-005**: Tras cotizar, el resumen cumple 009; Modificar en móvil restaura el formulario compacto sin intercambio.

## Assumptions

- “Swift del destino” se interpreta como el **botón de intercambiar origen y destino** (icono de flechas), no como un destino turístico ni como un tipo de viaje.
- Compactar en móvil es **moderado** (clarificación A): menos padding y campos un paso más bajos; Pedir cotización permanece el CTA principal. MUST NOT tipografía de administración ni un rediseño de marca. MUST NOT opción B (agresiva) ni C (solo quitar intercambio).
- En móvil, **todos** los campos del buscador van **apilados a ancho completo** (clarificaciones de disposición). El intercambio se oculta en esa disposición y se muestra en escritorio cuando los lugares van en la misma fila. No se elimina la capacidad en escritorio. MUST NOT opción de emparejar fecha \| hora en el teléfono.
- 768px (tablet) sigue el mismo criterio: si los lugares van apilados, sin intercambio; si van en fila, con intercambio.
- No se piden campos nuevos, precios ni inventario.

## Out of Scope

- Cambiar el layout de escritorio de 006.
- Rediseñar el card cotizado (009).
- Quitar origen o destino como campos.
- Catálogo, FAQ, header o FAB de WhatsApp.
