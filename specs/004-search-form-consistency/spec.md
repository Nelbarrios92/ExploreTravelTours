# Feature Specification: Consistencia UX del buscador del Hero

**Feature Branch**: `004-search-form-consistency`

**Created**: 2026-09-14

**Status**: Draft

**Input**: User description: "Rediseñar y mejorar el buscador principal de la landing (Transporte / Por horas) para consistencia visual, jerarquía, labels, CTA estable y responsive, sin cambiar la lógica de negocio ni romper validaciones, cotización o WhatsApp."

## Clarifications

### Session 2026-09-14

- Q: ¿Cómo se integra Solo ida / Ida y vuelta sin que el panel salte al cambiar a Por horas? → A: Franja de chrome de **la misma altura en ambos modos**. El control Solo ida / Ida y vuelta solo se muestra en Transporte; en Por horas esa franja queda vacía o con espacio reservado, sin un segundo control.

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Percibir un solo buscador con dos modos (Priority: P1)

Un visitante en el primer pantallazo usa el buscador al pie del Hero. Ve dos pestañas del **mismo tamaño y altura**: Transporte y Por horas. El activo usa el azul oscuro de marca; el inactivo se ve claramente neutro (no “casi tan fuerte” como el activo). Al cambiar de pestaña, el panel **no parece otro producto**: misma altura de campos, mismo ritmo de espacio, misma jerarquía y el botón **Buscar / Continuar** en la misma posición relativa. Solo cambian los campos que el modo necesita.

**Why this priority**: El problema de negocio es de percepción: hoy las dos modalidades se sienten como formularios distintos (altura, CTA que salta, tabs y campos desiguales).

**Independent Test**: Alternar Transporte y Por horas en escritorio amplio y comprobar que tabs, altura de campos y CTA no “saltan”; el usuario describe un solo componente.

**Acceptance Scenarios**:

1. **Given** el buscador en escritorio, **When** el visitante compara las dos pestañas, **Then** tienen la misma altura y el mismo ancho entre sí, y no cambian de tamaño al activarse.
2. **Given** Transporte activo, **When** pasa a Por horas y vuelve, **Then** no percibe un formulario más alto/ancho de forma inesperada; los campos de entrada tienen la misma altura entre modos; la franja bajo las pestañas (donde vive Solo ida / Ida y vuelta en Transporte) conserva la misma altura en Por horas aunque no muestre radios.
3. **Given** cualquier modo, **When** mira el CTA, **Then** lee exactamente “Buscar / Continuar” y, en escritorio cuando el ancho lo permite, permanece en la misma fila que los campos sin saltar de línea solo por cambiar de modo.
4. **Given** el tab inactivo, **When** lo compara con el activo, **Then** el activo es azul oscuro de marca y el inactivo es claramente más neutro (fondo/borde/texto grises, no azul competitivo).

---

### User Story 2 - Completar Transporte o Por horas con labels claros (Priority: P1)

El visitante entiende cada campo porque **todos** usan el mismo patrón: etiqueta pequeña arriba y control debajo (no unos con etiqueta flotante y otros solo con placeholder). En Transporte ve Origen, Destino, Fecha, Hora y Pasajeros; Solo ida / Ida y vuelta vive en una franja bajo las pestañas, limpia, sin romper la fila de campos. Esa franja **existe también en Por horas** (vacía o reservada) para no cambiar la altura del panel. Si elige Ida y vuelta, aparece Fecha de regreso de modo compacto (segunda fila de campos si hace falta), no un layout roto. En Por horas ve Lugar de recogida, Duración, Fecha, Hora y Pasajeros. **Duración** se lee como etiqueta “Duración” y valor “Selecciona” (con indicador de lista) **sin solaparse**. Las opciones de duración actuales se conservan.

**Why this priority**: Labels inconsistentes y el solape Duración/Selecciona son los fallos de uso más visibles.

**Independent Test**: Rellenar ambos modos leyendo solo las etiquetas; en Duración no hay texto superpuesto; Solo ida / Ida y vuelta sigue funcionando.

**Acceptance Scenarios**:

1. **Given** cualquier campo del buscador, **When** el visitante lo mira en vacío o con valor, **Then** hay etiqueta visible encima (o un único patrón equivalente aplicado a **todos** los campos); MUST NOT mezclar un campo solo-placeholder con otros con etiqueta.
2. **Given** Por horas y Duración vacío, **When** mira el control, **Then** ve “Duración” y “Selecciona” como textos distintos, sin solaparse.
3. **Given** Transporte, **When** usa Solo ida, **Then** no se le exige fecha de regreso y la fila principal permanece estable.
4. **Given** Transporte e Ida y vuelta, **When** elige esa opción, **Then** puede indicar fecha de regreso sin que el CTA desaparezca ni el panel se desborde en horizontal.
5. **Given** las duraciones ya ofrecidas (1 a 12 horas), **When** abre Duración, **Then** esas opciones siguen disponibles.

---

### User Story 3 - Usar el buscador en tablet y móvil sin overflow (Priority: P2)

En tablet el visitante ve una adaptación progresiva (no una fila forzada que recorta). En móvil: pestañas en una fila, campos apilados, botón a ancho completo después de los campos, área táctil cómoda, sin recortes ni scroll horizontal de la página por el buscador. El submit y las validaciones (campos vacíos, fechas, origen = destino → aviso y pasar a Por horas) siguen igual.

**Why this priority**: La consistencia desktop no sirve si el panel se rompe en el teléfono, donde llega buena parte del tráfico.

**Independent Test**: 375px y ~768px: tabs, pila de campos, CTA full width, sin overflow-x; una búsqueda válida y una inválida como hoy.

**Acceptance Scenarios**:

1. **Given** un viewport móvil, **When** usa el buscador, **Then** los tabs caben en una fila, los campos se apilan y el CTA va al final a ancho completo, con tamaño cómodo para el dedo.
2. **Given** tablet, **When** el ancho no alcanza para una sola fila, **Then** los campos se reorganizan sin overflow horizontal ni textos cortados.
3. **Given** errores o el aviso origen = destino, **When** aparecen, **Then** no desplazan el CTA fuera de un patrón predecible de forma permanente (el mensaje puede añadir altura; al ocultarse, el layout vuelve).

---

### Edge Cases

- Ida y vuelta: la fecha de regreso extra MUST NOT forzar todos los controles en una sola fila ni tapar el CTA de forma permanente.
- Resumen de cotización (franja encima del formulario, CTA WhatsApp): MUST seguir apareciendo tras una búsqueda válida; esta feature MUST NOT cambiar su significado ni mover el buscador al centro del Hero.
- Aviso origen = destino y botón “Cambiar a Por horas”: MUST conservarse; al aceptar, el modo Por horas MUST verse con el mismo sistema visual nuevo.
- Campos fecha/hora nativos del dispositivo: MUST seguir el mismo ritmo de etiqueta + control; MUST NOT volver al solape de textos.
- Zoom de texto del sistema: campos MUST seguir usables; el Hero MAY crecer.
- Mensajes de error en español: MUST permanecer accionables; MUST NOT desaparecer por el rediseño visual.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: El buscador del Hero MUST seguir ofreciendo exactamente dos modos: Transporte y Por horas, con la misma lógica de negocio actual (validaciones, resumen de cotización, WhatsApp, origen = destino).
- **FR-002**: Transporte MUST pedir Origen, Destino, Fecha (de ida), Hora y Pasajeros, y MUST conservar Solo ida / Ida y vuelta en una franja bajo las pestañas. Por horas MUST reservar **la misma altura de franja** sin mostrar radios equivalentes. Ida y vuelta MUST pedir fecha de regreso; MUST NOT pedir hora de regreso.
- **FR-003**: Por horas MUST pedir Lugar de recogida, Duración (opciones actuales 1–12 horas), Fecha, Hora y Pasajeros.
- **FR-004**: Visualmente, ambos modos MUST sentirse como un único componente: misma altura de campos, misma franja bajo tabs, mismo espaciado interno de referencia, misma jerarquía y posición estable del CTA al cambiar de tab (salvo el crecimiento puntual de mensajes de error, fecha de regreso o resumen).
- **FR-005**: Las dos pestañas MUST tener la misma altura y el mismo tamaño entre sí y MUST NOT redimensionarse al cambiar de modo. El activo MUST usar el azul oscuro de marca; el inactivo MUST ser netamente más neutro.
- **FR-006**: Todos los campos MUST usar un único sistema de etiqueta: **etiqueta pequeña arriba y control debajo**. MUST NOT mezclar ese patrón con campos que solo muestren placeholder como única etiqueta.
- **FR-007**: Duración MUST mostrar la etiqueta “Duración” y el estado vacío “Selecciona” (con indicación de lista) **sin superposición** de textos.
- **FR-008**: El CTA MUST conservar el texto “Buscar / Continuar” y la acción actual (validar y mostrar resumen / no abrir WhatsApp solo). En escritorio, cuando el ancho lo permita, MUST vivir en la **misma fila** que los campos y MUST NOT saltar de línea solo por cambiar de modalidad. En móvil MUST ir después de los campos a ancho completo.
- **FR-009**: En escritorio amplio, Transporte (solo ida) MUST aproximarse a una fila: Origen | Destino | Fecha | Hora | Pasajeros | Buscar. Por horas MUST alinear Lugar de recogida | Duración | Fecha | Hora | Pasajeros | Buscar en el mismo esqueleto.
- **FR-010**: Tablet MUST adaptar el número de columnas de forma progresiva. Móvil MUST apilar. MUST NOT haber overflow horizontal causado por el buscador.
- **FR-011**: Paleta MUST reutilizar la identidad existente: azul oscuro (tab activo / énfasis), naranja (CTA Buscar), grises claros (bordes/secundario), blanco (superficie), verde solo para WhatsApp (resumen/contacto). MUST NOT introducir una paleta nueva ni sombras exageradas.
- **FR-012**: El buscador MUST permanecer compacto, al pie del Hero, sin tapar el mensaje de marca ni rediseñar Hero, catálogo, navbar u otras secciones.
- **FR-013**: MUST NOT cambiar reglas de validación, textos de error de negocio, número WhatsApp, ni el flujo de cotización salvo lo imprescindible para no romper el layout (p. ej. orden visual de un aviso).
- **FR-014**: MUST NOT añadir un framework, librería de date-picker o dependencia nueva para conseguir la consistencia visual.

### Key Entities

- **Modo Transporte**: Búsqueda de traslado; campos de ruta; tipo de viaje Solo ida / Ida y vuelta.
- **Modo Por horas**: Búsqueda por tiempo; recogida + duración 1–12 h.
- **Pestaña de modo**: Control Transporte | Por horas; dimensiones fijas entre estados.
- **Franja de tipo de viaje**: Zona de altura fija bajo las pestañas; contiene Solo ida / Ida y vuelta solo en Transporte.
- **Campo de búsqueda**: Par etiqueta + control (texto, fecha, hora, número o lista).
- **CTA Buscar / Continuar**: Dispara la validación y el resumen; no es el botón verde de WhatsApp.
- **Resumen de cotización**: Franja existente encima del formulario (fuera del rediseño de negocio).

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Al menos 8 de 10 revisores, al cambiar de tab, describen “el mismo buscador con otros campos”, no “otro formulario”.
- **SC-002**: En escritorio ~1280px, las dos pestañas miden lo mismo (ancho y alto) en ambos modos; la franja bajo tabs tiene la misma altura en Transporte y Por horas; un recorte superpuesto no muestra salto de tamaño de tabs ni de esa franja.
- **SC-003**: En escritorio ~1280px, modo Solo ida y modo Por horas, el CTA permanece en la fila de campos (no pasa a una barra de ancho completo solo por cambiar de tab).
- **SC-004**: El 100% de los campos del buscador muestran etiqueta visible además del valor; 0 casos de texto de etiqueta solapado con “Selecciona” u otro placeholder en Duración.
- **SC-005**: Una búsqueda válida de Transporte y una de Por horas siguen mostrando el resumen de cotización con CTA a WhatsApp, sin pago en el sitio, igual que antes en significado.
- **SC-006**: Origen = destino sigue sin cotizar y ofrece pasar a Por horas; tras aceptar, Por horas usa el mismo sistema visual.
- **SC-007**: En 375px y 768px no hay overflow horizontal atribuible al buscador; en 375px el CTA es de ancho completo al final de los campos.
- **SC-008**: Un revisor confirma que Hero (marca), catálogo y navbar no fueron rediseñados en esta feature.

## Assumptions

- El buscador actual vive al pie del Hero, con dos formularios de modo, pestañas Transporte / Por horas, radios Solo ida / Ida y vuelta, campos con etiqueta flotante y un CTA a menudo fuera de la fila de campos (de ahí el salto visual). Duración es una lista 1–12 horas con “Selecciona”, lo que choca con la etiqueta flotante.
- Se adopta **etiqueta arriba + campo debajo** en todos los controles porque el patrón flotante no es fiable en listas y fechas nativas y el brief lo prefiere. No se mezclan los dos sistemas.
- Solo ida / Ida y vuelta no añade una fila extra exclusiva de Transporte: hay una franja de altura compartida; en Por horas no hay control simulado ni desactivado.
- “Misma altura al cambiar de tab” se refiere al **bloque de campos + CTA**, no a prohibir altura extra cuando hay errores, ida-vuelta o resumen.
- Compacto y profesional en desktop; en móvil, formulario vertical táctil. Breakpoints de referencia: ~375, ~768, ~1024/1280.
- La lógica de `Buscar / Continuar`, validaciones y WhatsApp del resumen se reutilizan; el trabajo es de presentación y estructura visual.
- Verde solo en acciones WhatsApp ya existentes (resumen, header, flotante), no en Buscar / Continuar.

## Out of Scope

- Cambiar copy comercial del Hero, catálogo, FAQ o navbar.
- Nuevos modos (p. ej. eSIM) o nuevos campos de negocio (hora de vuelta, precios).
- Motor de disponibilidad o mapas.
- Reemplazar fecha/hora nativas por un calendario de terceros.
- Rediseño del resumen de cotización más allá de no romperlo y alinearlo al mismo panel.
- Control de viaje desactivado o “falso” en Por horas para simetría (la franja se reserva vacía).
