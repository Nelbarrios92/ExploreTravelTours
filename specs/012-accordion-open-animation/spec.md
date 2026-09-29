# Feature Specification: Animación al abrir y cerrar el acordeón

**Feature Branch**: `012-accordion-open-animation`

**Created**: 2026-09-15

**Status**: Draft

**Input**: User description: "a la parte del acordeon en mobile del buscador, puedes agregarle animacion al abrir y cerrar? para que no sea tan simple para el user"

## Relación con las features 011 y anteriores

**012 es la fuente vigente solo para el movimiento percibido al abrir y cerrar el acordeón del buscador en móvil.**

| Tema | Estado en 012 |
|------|----------------|
| 011: acordeón, franja Pedir cotización, cerrado al cargar, naranja envía, Modificar abre | **Se conserva.** |
| 010: densidad y apilado con el panel abierto | **Se conserva.** |
| Escritorio / resumen 009 | **Se conservan.** MUST NOT animar el buscador de escritorio ni el card cotizado. |

## Clarifications

### Session 2026-09-15

- Q: ¿Qué se anima al abrir y cerrar? → A: **Altura**: el formulario se despliega y se pliega. MUST NOT solo opacidad ni exigir altura+opacidad juntas.
- Q: ¿Dónde corre esa animación de altura? → A: **Solo** al abrir/cerrar con la cabecera Pedir cotización. MUST NOT animar el paso al resumen ni Modificar.

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Abrir y cerrar se siente fluido (Priority: P1)

Un visitante en el teléfono toca **Pedir cotización**. Hoy el formulario aparece o desaparece de golpe. Quiere ver el panel **desplegarse y plegarse** con una animación breve y clara, para que el gesto no se sienta tosco.

**Why this priority**: El usuario pide explícitamente que deje de ser “tan simple” (abrupto).

**Independent Test**: En ~375px, abrir y cerrar una vez: un revisor percibe transición (el cuerpo no parpadea de 0 a 100 al instante).

**Acceptance Scenarios**:

1. **Given** el acordeón cerrado en ~375px, **When** pulsa la franja, **Then** el formulario **se despliega en altura** (el pie crece de forma perceptible), no un corte seco ni un fundido sin crecimiento.
2. **Given** el acordeón abierto, **When** pulsa la franja, **Then** el formulario **se pliega en altura** con la misma familia y duración percibida.
3. **Given** escritorio ~1280px, **When** usa el buscador, **Then** no hay acordeón ni esta animación.

---

### User Story 2 - La animación no estorba cotizar (Priority: P1)

La animación es corta. El visitante puede escribir y enviar en cuanto el panel está usable. Un segundo toque rápido (abrir y cerrar seguido) no deja el panel “a medias” de forma permanente: termina en abierto o cerrado coherente.

**Why this priority**: El movimiento no debe retrasar la conversión.

**Independent Test**: Abrir, completar un campo enseguida, cerrar y reabrir; valores intactos (011). Envío válido sigue yendo a 009.

**Acceptance Scenarios**:

1. **Given** una apertura, **When** el movimiento termina, **Then** todos los campos 010 son usables; Pedir cotización naranja sigue siendo el envío.
2. **Given** toques seguidos en la franja, **When** el usuario deja de pulsar, **Then** el acordeón acaba **abierto o cerrado del todo**, no un estado intermedio congelado.
3. **Given** un envío válido o Modificar, **When** cambia a resumen o vuelve al form, **Then** el cambio es **inmediato** (sin plegado/desplegado de altura); 007/009/011 se cumplen; el panel abierto muestra errores si los hay.

---

### User Story 3 - Respeto a menos movimiento (Priority: P2)

Quien tiene el sistema en “reducir movimiento” no debe verse forzado a una animación llamativa. En ese caso abrir/cerrar MAY ser inmediato (como 011).

**Why this priority**: Accesibilidad; el Hero y el FAQ ya cuidan el movimiento.

**Independent Test**: Con preferencia de menos movimiento activa, el toggle no muestra el desplegado largo; el resto de 011 sigue.

**Acceptance Scenarios**:

1. **Given** el visitante pide menos movimiento al sistema, **When** abre o cierra, **Then** el cambio es **instantáneo o casi** (sin el desplegado suave de US1).
2. **Given** el resto de visitantes, **When** abren, **Then** sí perciben la animación breve de US1.

---

### Edge Cases

- Ida y vuelta (más alto): la apertura MUST cubrir la altura real; MUST NOT recortar campos a mitad de animación al terminar.
- Estado cotizado: MUST NOT animar el resumen 009 ni el tránsito cotizar/Modificar.
- Rotación a escritorio: MUST NOT dejar el compositor a media altura; se ve completo (006).
- MUST NOT animación larga, de rebote o de “espectáculo” que retrase más de lo breve.
- La señal de la cabecera (chevron) MAY acompañar el movimiento; el texto sigue **Pedir cotización**.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: En vista estrecha, al abrir el acordeón del buscador (componer) con la franja, el cuerpo MUST **crecer en altura** de oculto a visible, no un salto instantáneo ni un cambio solo de opacidad — salvo FR-005.
- **FR-002**: Al cerrar con la franja, MUST haber un **plegado en altura** equivalente.
- **FR-003**: La animación MUST ser **breve** (el visitante percibe el gesto en menos de medio segundo en condiciones normales) y **suave** (sin rebote exagerado).
- **FR-004**: Comportamiento 011 MUST conservarse: copy, cerrado al cargar, naranja envía, Modificar abre, valores al reabrir, 010 abierto, 009 cotizado.
- **FR-005**: Si el sistema indica reducir movimiento, abrir/cerrar MUST NOT usar el desplegado suave; MAY ser instantáneo.
- **FR-006**: MUST NOT aplicar esta animación al buscador de escritorio, al card cotizado, al **paso al resumen** ni a **Modificar** (solo el gesto de la franja).

### Key Entities

- **Apertura / cierre animado**: Cambio de **altura** del cuerpo del acordeón en móvil (clarificación A).
- **Preferencia de menos movimiento**: Señal del sistema del visitante para no forzar animación.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Un revisor en ~375px confirma que abrir y cerrar **cambian la altura** del pie (desplegar/plegar), no un corte ni solo un fundido, y que el movimiento dura **menos de 0,5 s** percibidos.
- **SC-002**: 100% de los envíos válidos y Modificar siguen el flujo 011/009 **sin** animación de altura; 0 campos recortados al terminar de abrir con la franja.
- **SC-003**: En ~1280px, 0 animación de acordeón. Con “reducir movimiento”, 0 desplegado suave.
- **SC-004**: Tras toques rápidos, el panel acaba 100% abierto o 100% cerrado.

## Assumptions

- “No tan simple” = falta de **transición de altura**, no un rediseño ni un efecto largo tipo marketing. MUST NOT opción B (solo opacidad) ni C (altura+opacidad obligatorias).
- Duración objetivo: **corta** (&lt; 0,5 s), misma familia al abrir y al cerrar (ease suave, sin bounce).
- 011 sigue siendo la fuente de cuándo hay acordeón; 012 solo anima el **gesto de la franja** (clarificación A). Cotizar/Modificar instantáneos.
- Respetar reducir movimiento es el default de accesibilidad (no se pide confirmación).

## Out of Scope

- Cambiar copy, layout 010/006 o el resumen 009.
- Animar el Hero, el catálogo o el FAQ.
- Librerías de animación o vídeo.
