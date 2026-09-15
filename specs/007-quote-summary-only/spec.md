# Feature Specification: Solo el resumen tras cotizar

**Feature Branch**: `007-quote-summary-only`

**Created**: 2026-09-15

**Status**: Draft

**Input**: User description: "cuando se le da pedir cotizacion, debe salir solamente el resumen de cotizacion, no deberia salir el buscador"

## Relación con las features 005 y 006

`specs/005-hero-booking-bar` y `specs/006-round-trip-single-row` siguen vigentes para layout, copy de CTAs, FAB, validaciones y WhatsApp. **Esta feature 007 es la fuente vigente para qué se ve en el card del Hero tras un envío válido.**

| Tema 005 | Estado en 007 |
|----------|----------------|
| Tras Pedir cotización: resumen **inline** y el **formulario permanece visible** debajo (como 001) | **Reemplazado**: MUST mostrarse **solo** el resumen de cotización. MUST NOT seguir mostrando el buscador (tabs, campos, Pedir cotización) a la vez que el resumen. |
| Un solo feedback (no “TU SOLICITUD” en el header) | **Se conserva**. |
| Naranja no abre WhatsApp; verde **Continuar por WhatsApp** sí | **Se conserva**. |
| Layout de Ida y vuelta en una fila (006) | **Se conserva** para cuando el buscador está visible. |

## Clarifications

### Session 2026-09-15

- Q: ¿Cómo vuelve el visitante al buscador si el resumen es lo único visible? → A: **Modificar** en el resumen (no en el header): muestra de nuevo el buscador con los valores previos; el resumen se oculta hasta un nuevo Pedir cotización válido. MUST NOT exigir recargar la página como única salida.

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Ver solo la confirmación después de cotizar (Priority: P1)

Un visitante completa Transporte o Por horas y pulsa **Pedir cotización**. Si los datos son válidos, el card del Hero deja de parecer un buscador: desaparecen pestañas, tipo de viaje y campos. Queda el resumen (datos + **Continuar por WhatsApp** y, si aplica, sugerencias relacionadas). Así no compite visualmente el formulario con la confirmación.

**Why this priority**: El usuario pidió explícitamente que el buscador no conviva con el resumen; hoy ambos se apilan y recargan el primer pantallazo.

**Independent Test**: Envío válido de Transporte y de Por horas; el buscador no está a la vista; el resumen y el CTA verde sí.

**Acceptance Scenarios**:

1. **Given** un traslado o un servicio por horas válido, **When** pulsa **Pedir cotización**, **Then** el card muestra el resumen de cotización (datos + Continuar por WhatsApp) y NEVER muestra a la vez tabs Transporte/Por horas, campos ni el botón naranja Pedir cotización.
2. **Given** esa confirmación, **When** mira el header, **Then** no reaparece un estado “TU SOLICITUD” que sustituya el resumen. El naranja MUST NOT haber abierto WhatsApp.
3. **Given** el resumen visible, **When** pulsa Continuar por WhatsApp, **Then** se abre el chat comercial con el mensaje prefijado (mismo significado que 005).

---

### User Story 2 - Corregir o volver a cotizar (Priority: P2)

Si el visitante se equivocó o quiere otro trayecto, no debe recargar la página a ciegas. Desde el resumen pulsa **Modificar**. Reaparece el buscador con los datos que ya escribió, para editar y pedir de nuevo. MUST NOT recargar la página como única forma de volver.

**Why this priority**: Ocultar el formulario sin salida dejaría al visitante atrapado; 005 quitó “Modificar” del header porque el form seguía abajo.

**Independent Test**: Tras un resumen, pulsar **Modificar**; reaparecen tabs y campos con los valores previos; un nuevo envío válido vuelve a dejar solo el resumen.

**Acceptance Scenarios**:

1. **Given** el resumen a la vista, **When** pulsa **Modificar**, **Then** el buscador reaparece (tabs y campos) y el resumen se oculta hasta un nuevo envío válido. Los valores previos MUST seguir en los campos. **Modificar** está en el resumen, NEVER en el header como “TU SOLICITUD”.
2. **Given** un envío inválido (faltan datos, origen = destino, fechas incoherentes), **When** intenta Pedir cotización, **Then** el buscador permanece visible con el aviso en español; MUST NOT mostrar el resumen como si hubiera cotizado.

---

### Edge Cases

- Transporte y Por horas: el mismo patrón (solo resumen tras éxito).
- Origen = destino: se conserva el aviso y el paso a Por horas; el buscador sigue visible.
- FAB: MUST NOT tapar el CTA verde del resumen; la regla de ocultar el flotante mientras el card del Hero está en vista se conserva.
- Recargar la página: vuelve el buscador vacío/inicial (no hay persistencia).
- MUST NOT reactivar confirmación en el navbar.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: Tras un envío **válido** de Pedir cotización, el card del Hero MUST mostrar **únicamente** el resumen de cotización (datos, Continuar por WhatsApp, sugerencias relacionadas si aplican). MUST NOT mostrar el buscador (pestañas, tipo de viaje, campos, CTA naranja) al mismo tiempo.
- **FR-002**: Esta regla MUST sustituir la de 005 que dejaba el formulario visible bajo el resumen. MUST NOT volver el patrón dual header + form.
- **FR-003**: El resumen MUST conservar el significado de 005: datos del viaje o del servicio por horas, CTA verde **Continuar por WhatsApp** hacia el número comercial con mensaje prefijado. El naranja MUST NOT abrir WhatsApp.
- **FR-004**: El resumen MUST incluir un control con el texto **Modificar** (en el card, no en el navbar). Al activarlo MUST mostrar de nuevo el buscador, ocultar el resumen y conservar los valores ya introducidos. MUST NOT exigir recargar la página para editar.
- **FR-005**: Si la validación falla, MUST permanecer el buscador y los mensajes actuales; MUST NOT mostrar el resumen.
- **FR-006**: MUST NOT cambiar layout de Ida y vuelta (006), catálogo, FAQ, marca del Hero, número WhatsApp ni el significado de las validaciones.

### Key Entities

- **Resumen de cotización**: Única superficie visible del card tras un envío válido.
- **Buscador**: Tabs y formularios de Transporte / Por horas; visible antes de cotizar y al modificar.
- **Control de modificar**: Botón **Modificar** en el resumen para recuperar el buscador.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Tras el 100% de los envíos válidos de prueba (Transporte y Por horas), un revisor ve el resumen y 0 controles del buscador (tabs, campos, Pedir cotización) en el card.
- **SC-002**: Tras pulsar **Modificar**, el buscador es de nuevo usable en un intento; los datos previos siguen ahí; el resumen no queda a la vista hasta un nuevo envío válido.
- **SC-003**: El 100% de los envíos inválidos de prueba dejan el buscador a la vista y 0 resumen de éxito.
- **SC-004**: Continuar por WhatsApp sigue abriendo `wa.me` al número comercial; 0 aperturas de WhatsApp al pulsar Pedir cotización.

## Assumptions

- “El buscador” = pestañas Transporte/Por horas, pills de tipo de viaje, todos los campos y el CTA naranja.
- El control de vuelta es un botón **Modificar** en el resumen, no un enlace “Volver a cotizar” ni recargar.
- El card del Hero (mismo recuadro blanco) se conserva; solo cambia su contenido visible.
- 006 (una fila en ida y vuelta) aplica cuando el buscador está mostrado.
- Número WhatsApp: `+57 304 214 3149`.

## Out of Scope

- Persistencia de la cotización al recargar o en otra pestaña.
- Volver el estado de solicitud al navbar.
- Precios, inventario, nuevos campos.
