# Feature Specification: Ida y vuelta en una sola fila

**Feature Branch**: `006-round-trip-single-row`

**Created**: 2026-09-15

**Status**: Draft

**Input**: User description: "El buscador cuando se selecciona ida y vuelta deberia tener todos sus inputs en una misma linea y no hacer ese salto de linea, eso hace que se rompa visualmente y genere mala experiencia del lado del usuario"

## Relación con la feature 005

`specs/005-hero-booking-bar` sigue siendo la fuente vigente para copy de CTAs, un solo feedback, FAB, densidad, pills, swap, Por horas y validaciones. **Esta feature 006 es la fuente vigente solo para el layout de Ida y vuelta en escritorio.**

| Tema 005 | Estado en 006 |
|----------|----------------|
| Ida y vuelta en ~1280px: **dos filas deliberadas** (fechas arriba; hora, pasajeros y CTA abajo) | **Reemplazado**: todos los campos de Ida y vuelta MUST permanecer en **una sola fila** en el mismo ancho de escritorio donde Solo ida ya cabe en una fila. MUST NOT saltar hora, pasajeros o el CTA a una segunda banda. |
| Orden mental de viaje (regreso después de origen, destino y fecha de ida) | **Se conserva**. |
| Resto de 005 (Pedir cotización, resumen inline, FAB, Por horas, móvil en columna) | **Se conserva**. |

005 no se reabre para rediseñar el cotizador: el trabajo de 006 es corregir el salto de línea percibido como rotura.

## Clarifications

### Session 2026-09-15

- Q: ¿Cómo cabe Ida y vuelta en una sola fila en un escritorio típico (~1280px)? → A: **Una fila en escritorio típico**: todos los controles visibles; se puede compactar un poco el aire (campos más estrechos); MUST NOT recortar textos, MUST NOT usar scroll horizontal, MUST NOT bajar a una segunda banda. MUST NOT reservar la fila única solo a pantallas muy anchas ni ocultar etiquetas ni achicar el texto hasta densidad de administración.

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Completar ida y vuelta sin ruptura visual (Priority: P1)

Un visitante en escritorio elige Transporte e **Ida y vuelta**. Espera una barra continua: origen, intercambio, destino, fecha de ida, fecha de regreso, hora, pasajeros y pedir cotización en **la misma línea**. Hoy el panel se parte en dos bandas; eso se siente roto y obliga a buscar el botón y los campos de hora más abajo. Tras el cambio, ida y vuelta se lee como la misma barra que solo ida, solo que con el campo de regreso extra, sin salto.

**Why this priority**: El salto de línea es el defecto visible que daña la primera impresión del cotizador.

**Independent Test**: En escritorio, activar Ida y vuelta y comprobar que ningún campo de traslado ni el CTA naranja cae a una segunda fila.

**Acceptance Scenarios**:

1. **Given** Transporte e Ida y vuelta en un escritorio típico (~1280px de ancho de ventana), **When** el visitante recorre el cotizador, **Then** origen, intercambio de lugares, destino, fecha de ida, fecha de regreso, hora, pasajeros y Pedir cotización aparecen en **una sola fila** horizontal, todos visibles, sin scroll horizontal del panel. NEVER hay un salto que deje hora, pasajeros o el CTA en una banda inferior. MAY estrecharse un poco los campos; MUST NOT recortar etiquetas ni valores hasta hacerlos ilegibles.
2. **Given** ese layout, **When** compara con Solo ida, **Then** la única diferencia de estructura es la presencia de fecha de regreso en esa misma fila; el panel no parece “otro formulario” ni un bloque partido.
3. **Given** Ida y vuelta, **When** recorre los campos de izquierda a derecha, **Then** el orden sigue siendo el del viaje: origen → destino (con intercambio entre ellos) → fecha de ida → fecha de regreso → hora → pasajeros → Pedir cotización. La fecha de regreso NEVER vuelve al primer puesto.

---

### User Story 2 - Seguir usando el cotizador en pantallas estrechas (Priority: P2)

En teléfono, apilar campos sigue siendo necesario: una sola fila de todos los controles no cabe y recortaría o haría scroll horizontal. El visitante en móvil no pierde la cotización; el arreglo de una fila aplica al escritorio, no fuerza siete controles ilegibles en 375px.

**Why this priority**: Corregir escritorio no debe romper el flujo que 005 ya exige en móvil.

**Independent Test**: En ~375px, Ida y vuelta apila; no hay desbordamiento horizontal del panel.

**Acceptance Scenarios**:

1. **Given** ~375px e Ida y vuelta, **When** usa el cotizador, **Then** los campos se apilan en una columna (o reflujo estrecho ya aceptado) y el CTA permanece usable a ancho completo. MUST NOT haber scroll horizontal causado por forzar una sola fila.
2. **Given** un ancho intermedio (tablet) donde ya no cabe una fila cómoda, **When** el panel reflowea, **Then** el cambio es un reflujo intencional, no el salto a mitad de controles que hoy se percibe como error en escritorio.

---

### Edge Cases

- Activar Ida y vuelta MUST añadir fecha de regreso **en la misma fila** en escritorio, no empujar el resto abajo.
- Volver a Solo ida MUST quitar fecha de regreso y seguir en una fila, sin dejar un hueco de segunda banda.
- El botón de intercambio de origen y destino forma parte de la misma fila en escritorio; MUST NOT ser la causa de un wrap del resto de campos.
- Labels y valores MUST seguir legibles (no texto recortado ilegible) al caber en una fila; MAY compactarse el aire (anchos). MUST NOT ocultar etiquetas, MUST NOT bajar el texto a densidad de administración, MUST NOT introducir scroll horizontal en el panel.
- Validaciones, copy de CTAs, resumen inline, FAB y Por horas: sin cambio de significado respecto a 005.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: En un escritorio típico (~1280px), con Transporte e Ida y vuelta, el cotizador MUST mostrar **todos** los controles de traslado (origen, intercambio, destino, fecha de ida, fecha de regreso, hora, pasajeros y Pedir cotización) en **una sola fila**, visibles a la vez. MUST NOT partir el conjunto en dos bandas. MUST NOT exigir un monitor extra-ancho para esa fila. MUST NOT recortar textos, MUST NOT usar scroll horizontal interno, MUST NOT ocultar etiquetas para ganar espacio. MAY reducir un poco el ancho de cada campo.
- **FR-002**: Esta regla MUST sustituir la de 005 que exigía dos filas deliberadas para Ida y vuelta. MUST NOT conservarse el salto “fechas arriba / hora-pasajeros-CTA abajo” como diseño deseado.
- **FR-003**: El orden de lectura MUST seguir el viaje: origen, destino (intercambio entre ambos), fecha de ida, fecha de regreso, hora, pasajeros, Pedir cotización.
- **FR-004**: En pantallas estrechas (móvil) el cotizador MUST seguir apilando o refluyendo para evitar recortes y scroll horizontal. MUST NOT imponer la fila única de escritorio en ~375px.
- **FR-005**: Solo ida MUST seguir cabiendo en una fila a ~1280px; el cambio a Ida y vuelta MUST insertar fecha de regreso en esa misma fila, no crear una segunda.
- **FR-006**: MUST NOT cambiar el significado de validaciones, WhatsApp, copy de Pedir cotización / Continuar por WhatsApp, modos Transporte | Por horas, catálogo, FAQ ni marca del Hero.

### Key Entities

- **Fila de Ida y vuelta**: Banda única de controles de traslado en escritorio, incluida la fecha de regreso y el CTA naranja.
- **Tipo de viaje**: Solo ida | Ida y vuelta; solo cambia si aparece fecha de regreso, no el número de filas en escritorio.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: En Ida y vuelta a ~1280px de ancho de ventana, 100% de los controles de traslado listados en FR-001 comparten una sola fila; 0 controles de ese conjunto aparecen en una segunda banda; 0 scroll horizontal del panel; etiquetas y valores siguen leyéndose.
- **SC-002**: Un revisor, al pasar de Solo ida a Ida y vuelta en ese ancho, confirma que el panel no “se rompe” (no aparece un escalón de campos abajo); el único control nuevo es la fecha de regreso en la misma línea.
- **SC-003**: En ~375px, 0 scroll horizontal del panel al usar Ida y vuelta; el CTA sigue siendo accionable.
- **SC-004**: El 100% de las reglas de cotización de 005 que no son layout de Ida y vuelta (un feedback, CTAs, validaciones, FAB) siguen cumpliéndose en una pasada de revisión.

## Assumptions

- El problema reportado ocurre en **escritorio típico (~1280px)**, no solo en pantallas ultraanchas: ahí Solo ida ya cabe en una fila y Ida y vuelta no MUST bajar a una segunda banda.
- Compactar “un poco el aire” significa anchos de campo, no esconder labels ni tipografía minúscula.
- “Todos sus inputs” incluye el control de intercambio de lugares y el botón Pedir cotización, no solo los campos de texto/fecha.
- En tablet y móvil, si una fila única deja de caber, se permite reflujo; lo prohibido es el salto a dos filas **en ~1280px**.
- Densidad y paleta de 005 se mantienen; no se pide un rediseño de marca.
- El número WhatsApp y el flujo de cotización no cambian.

## Out of Scope

- Nuevos campos (hora de regreso, precios, inventario).
- Cambiar Por horas, catálogo, FAQ o tipografía de marca.
- Forzar una sola fila de todos los controles en móvil.
