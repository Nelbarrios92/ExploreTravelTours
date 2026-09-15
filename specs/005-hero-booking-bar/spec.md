# Feature Specification: Booking bar premium del Hero

**Feature Branch**: `005-hero-booking-bar`

**Created**: 2026-09-14

**Status**: Draft

**Input**: User description: "Rediseñar el buscador/cotizador del Hero (#hero-search) como booking bar de movilidad premium (dirección de arte + fricciones UX), sin romper cotización por WhatsApp. Supera a specs/004-search-form-consistency: no basta unificar tabs/labels."

## Clarifications

### Session 2026-09-14

- Q: ¿El CTA naranja debe decir WhatsApp si el envío no abre WhatsApp? → A: Dos pasos honestos. Naranja: **Pedir cotización** (muestra el resumen). Verde: **Continuar por WhatsApp**. El naranja MUST NOT abrir WhatsApp.
- Q: ¿Cómo se organizan los 7 controles de Ida y vuelta en ~1280px? → A: **Dos filas deliberadas**, mismo orden de lectura: (1) Origen · Destino · Fecha de ida · Fecha de regreso; (2) Hora · Pasajeros · Pedir cotización alineado al final. MUST NOT forzar una sola fila de siete ítems.

## Relación con la feature 004

`specs/004-search-form-consistency` cubría consistencia visual (tabs iguales, labels, CTA en fila). **Esta feature 005 es la fuente de producto vigente** para el cotizador del Hero. Lo que 004 sigue siendo válido se reafirma aquí (un solo componente, dos modos, vanilla, validaciones). Lo siguiente de 004 **queda reemplazado**:

| Tema 004 | Estado en 005 |
|----------|----------------|
| CTA “Buscar / Continuar” (FR-008 / SC-003 de 004) | **Reemplazado**: naranja **Pedir cotización**; verde **Continuar por WhatsApp**. MUST NOT decir “Buscar”. |
| Franja chrome vacía en Por horas para igualar altura | **Reemplazado**: altura estable **sin** spacer vacío que se sienta “roto”; p. ej. misma estructura de campos/slots. |
| Densidad compacta tipo admin (~texto pequeño, poco padding) | **Reemplazado**: densidad premium (UI ≥14px, campos ~48–52px de alto). |
| Dos feedbacks post-envío (resumen en el panel + estado `has-request` en el header) | **Reemplazado**: **un solo** patrón. Preferencia: resumen **inline** en el card + CTA WhatsApp. MUST NOT saltar la confirmación al navbar y ocultar el resumen. |
| Orden DOM de “Fecha de regreso” primero + layout que envuelve mal el CTA | **Reemplazado**: orden mental de viaje (ver FR de ida y vuelta). |

004 no se reabre: no hace falta “solo embellecer” su CSS. El trabajo de 005 incluye DOM, orden, interacción y dirección de arte.

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Cotizar un traslado con orden mental claro (Priority: P1)

Un visitante en el primer pantallazo quiere un traslado. En una **barra de reserva** al pie del Hero elige Transporte y Solo ida o Ida y vuelta (controles tipo segmento / pills, no radios nativos crudos). Completa origen, destino, fechas y hora en el **orden en que piensa el viaje**. En ida y vuelta, la fecha de regreso viene **después** de origen, destino y fecha de ida — no antes. El botón naranja del panel es usable: no lo tapa el botón flotante verde de WhatsApp. Al confirmar, entiende que pide una **cotización**, no una búsqueda de inventario.

**Why this priority**: Orden de campos, overlap del FAB y copy engañoso bloquean la conversión del primer pantallazo.

**Independent Test**: Solo ida e ida y vuelta en ~1280px y ~375px; CTA visible y clicable; orden visual de fechas correcto.

**Acceptance Scenarios**:

1. **Given** Transporte e Ida y vuelta en escritorio ~1280px, **When** el visitante recorre los campos, **Then** ve dos filas deliberadas: primero Origen → Destino → Fecha de ida → Fecha de regreso; debajo Hora → Pasajeros → Pedir cotización (CTA al final de esa fila). La fecha de regreso NEVER aparece antes de origen, destino y fecha de ida.
2. **Given** ese layout, **When** mira el CTA, **Then** el botón está en la segunda fila con hora y pasajeros (no envuelto solo ni cubierto por el FAB).
3. **Given** 375px y 1280px, **When** el buscador y el FAB coinciden en pantalla, **Then** hay **0 solape** entre el flotante de WhatsApp y el CTA del cotizador.
4. **Given** el CTA naranja del panel, **When** lo lee, **Then** dice **Pedir cotización** (no “Buscar” ni “Cotizar por WhatsApp” en ese botón).

---

### User Story 2 - Cotizar por horas con la misma calidad (Priority: P1)

El mismo visitante cambia a Por horas. Ve Lugar de recogida, Duración (1–12 h, “Selecciona” sin solaparse con la etiqueta), Fecha, Hora y Pasajeros, con la **misma** jerarquía, tamaño de texto, altura de campo y posición del CTA que en Transporte. El cambio de modo no parece otro producto ni deja un hueco vacío raro.

**Why this priority**: Si Por horas se siente de segunda, se rompe la booking bar única.

**Independent Test**: Completar Por horas y comparar con Transporte: misma densidad y CTA; sin spacer vacío evidente.

**Acceptance Scenarios**:

1. **Given** Por horas, **When** compara con Transporte (solo ida), **Then** labels, altura de campos y CTA siguen el mismo sistema visual.
2. **Given** el cambio de tab, **When** alterna modos, **Then** la altura del panel es estable de forma **intencional** (misma estructura), MUST NOT depender de una franja vacía que se perciba como error de layout.
3. **Given** Duración vacío, **When** mira el campo, **Then** etiqueta y “Selecciona” no se superponen.

---

### User Story 3 - Entender el outcome (WhatsApp) y ver una sola confirmación (Priority: P1)

Tras un envío válido, el visitante ve **un** resumen en el propio card del buscador, con los datos y un CTA verde a WhatsApp. El header **no** se convierte en la confirmación principal ni oculta ese resumen. El copy del botón naranja ya alineó expectativas: no hay “búsqueda” de cupos.

**Why this priority**: Hoy hay dos feedbacks a medias; eso genera desconfianza.

**Independent Test**: Enviar Transporte y Por horas válidos; un solo bloque de confirmación observable; WhatsApp con el mensaje prefijado.

**Acceptance Scenarios**:

1. **Given** un formulario válido, **When** pulsa **Pedir cotización**, **Then** ve el resumen **inline** en el panel (datos + **Continuar por WhatsApp**) y MUST NOT perderlo porque el foco pasó a un estado de navbar.
2. **Given** esa confirmación, **When** recorre la cabecera, **Then** no hay un segundo “tu solicitud” que sustituya o contradiga el resumen del card (el header MAY conservar Contactar Ya genérico). El naranja MUST NOT haber abierto WhatsApp.
3. **Given** origen = destino en Transporte, **When** envía, **Then** no se genera cotización; ve el aviso actual y puede pasar a Por horas (mismo significado que hoy).

---

### User Story 4 - Usar el cotizador en tablet y móvil (Priority: P2)

En móvil: una columna, CTA a ancho completo, tabs/pills usables, sin overflow horizontal, FAB sin tapar el CTA. En tablet: adaptación progresiva.

**Why this priority**: Gran parte del tráfico es móvil; el overlap FAB es peor ahí.

**Independent Test**: 375 / 768 / 1280 según quickstart futuro; sin overflow-x.

**Acceptance Scenarios**:

1. **Given** 375px, **When** usa el cotizador, **Then** campos apilados, CTA full width, tabs en una fila, 0 overlap FAB↔CTA.
2. **Given** 768px, **When** no cabe una sola fila, **Then** reflujo sin recortes ni scroll horizontal por el panel.

---

### User Story 5 - Intercambiar ruta y elegir lugares (Priority: P2)

En Transporte, un control permite **intercambiar** origen y destino. Los campos de lugar ofrecen sugerencias reales del negocio (Cartagena, aeropuerto, destinos ya publicados, etc.), con placeholders comprensibles — no un espacio en blanco.

**Why this priority**: Reduce error y esfuerzo; no bloquea cotizar a mano.

**Independent Test**: Swap copia valores; datalist o equivalente muestra destinos del catálogo/negocio; se puede seguir escribiendo texto libre.

**Acceptance Scenarios**:

1. **Given** origen y destino rellenos, **When** usa intercambiar, **Then** los valores se invierten y los campos siguen válidos para enviar.
2. **Given** un campo de lugar, **When** lo enfoca, **Then** ve sugerencias de sitios reales de Explore y un placeholder de ejemplo (p. ej. Cartagena, Aeropuerto).

---

### Edge Cases

- Ida y vuelta: fecha de regreso MUST NOT volver al primer puesto visual. En ~1280px MUST ocupar la primera fila junto a origen, destino y fecha de ida — no una sola fila de siete ítems.
- Fecha de regreso &lt; ida, fecha pasada, pasajeros &lt; 1: mismas reglas de negocio que hoy (no avanzar; mensaje en español).
- FAB: MUST NOT cubrir CTA ni el resumen inline; si se oculta el FAB mientras el cotizador está en vista, MUST reaparecer al salir de esa zona (p. ej. al bajar al catálogo).
- Locale: el visitante MUST NOT depender de interpretar mm/dd/yyyy como formato único; presentación y ayudas en sentido **es-CO** (día/mes/año).
- Contraste: texto de UI del panel MUST cumplir AA sobre el fondo blanco del card.
- Competencia de CTAs en el Hero: el cotizador es la acción **primaria** de conversión; otros CTAs del pantallazo MUST NOT rivalizar al mismo peso visual (ajuste mínimo, no rediseño total del Hero).

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: El Hero MUST conservar un cotizador al pie con exactamente dos modos: Transporte y Por horas. MUST NOT inventar precios, inventario, mapas ni modos nuevos (tours, eSIM).
- **FR-002**: Transporte MUST incluir Origen, Destino, Fecha de ida, Hora, Pasajeros y Solo ida | Ida y vuelta. Ida y vuelta MUST añadir Fecha de regreso **después** de Origen, Destino y Fecha de ida. MUST NOT pedir hora de regreso.
- **FR-003**: En escritorio ~1280px, Ida y vuelta MUST usar **dos filas deliberadas**: fila 1 Origen | Destino | Fecha de ida | Fecha de regreso; fila 2 Hora | Pasajeros | Pedir cotización (CTA al final). MUST NOT forzar siete controles en una sola fila. Solo ida MAY usar una fila (Origen | Destino | Fecha de ida | Hora | Pasajeros | CTA).
- **FR-004**: Por horas MUST incluir Lugar de recogida, Duración (1–12 horas, opciones actuales), Fecha, Hora y Pasajeros.
- **FR-005**: Validaciones MUST conservar su significado: requeridos, pasajeros ≥ 1, fechas no pasadas, regreso no anterior a la ida, origen ≠ destino (aviso y paso opcional a Por horas).
- **FR-006**: El CTA naranja del panel MUST decir exactamente **Pedir cotización**. MUST NOT contener la palabra “Buscar” ni abrir WhatsApp. MUST mostrar el resumen inline. El CTA verde del resumen MUST decir **Continuar por WhatsApp** y abrir `wa.me` al número comercial con el mensaje prefijado.
- **FR-007**: Tras un envío válido MUST existir **un solo** feedback: resumen en el card + CTA WhatsApp (`wa.me` al número comercial, mensaje prefijado). MUST NOT activar un estado de solicitud en el navbar que oculte o sustituya ese resumen.
- **FR-008**: MUST haber 0 solape entre el botón flotante de WhatsApp y el CTA (y el resumen) del cotizador en 375px y 1280px.
- **FR-009**: Tipografía de UI del panel MUST ser ≥14px en labels y controles; altura de campo percibida ~48–52px; padding generoso. MUST NOT parecer un formulario de administración denso.
- **FR-010**: Contraste del texto del panel MUST alcanzar AA sobre la superficie del card.
- **FR-011**: Transporte | Por horas MUST presentarse como segmented control fino. Solo ida | Ida y vuelta MUST ser pills (no radios nativos sin estilo).
- **FR-012**: Fechas y placeholders MUST ser comprensibles en es-CO. Campos de lugar MUST tener placeholders reales (p. ej. “Cartagena”, “Aeropuerto…”) MUST NOT usar un placeholder vacío solo para truco visual.
- **FR-013**: Transporte MUST ofrecer intercambiar Origen y Destino. Las sugerencias de lugar MUST incluir destinos/sitios reales ya ofrecidos por Explore (vanilla; texto libre permitido).
- **FR-014**: La altura al cambiar de modo MUST ser estable mediante una **misma estructura de slots**, no una franja vacía que se perciba como fallo.
- **FR-015**: El cotizador MUST ser la acción primaria de conversión del primer pantallazo; CTAs secundarios del Hero MUST ceder peso visual donde sea razonable sin rediseñar marca, foto ni catálogo.
- **FR-016**: Paleta MUST usar `--brand-blue`, `--brand-orange` (CTA de cotizar del panel) y `--whatsapp-green` solo para WhatsApp. Dirección de arte: claridad y aire tipo barra de movilidad premium; MUST NOT copiar Uber/Airbnb ni añadir marcas ajenas.
- **FR-017**: MUST NOT introducir framework, npm, datepicker de terceros, backend ni nuevos campos de negocio innecesarios.
- **FR-018**: MUST NOT rediseñar tipografía de marca del Hero, catálogo ni FAQ. Navbar solo el mínimo para **quitar o no usar** el estado de solicitud que duplica el resumen.

### Key Entities

- **Booking bar**: Panel de cotización al pie del Hero (sucesor del buscador denso).
- **Modo Transporte / Por horas**: Igual significado de negocio que hoy.
- **Tipo de viaje**: Solo ida | Ida y vuelta (pills).
- **Resumen de cotización inline**: Única confirmación post-envío en el card.
- **FAB WhatsApp**: Acceso global que MUST NOT tapar la barra.
- **Sugerencia de lugar**: Valor de ayuda alineado a la oferta real (ciudad, aeropuerto, destinos publicados).

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: En ida y vuelta ~1280px, un revisor confirma dos filas (fechas en la primera; hora, pasajeros y Pedir cotización en la segunda) y que el CTA no queda envuelto de forma accidental.
- **SC-002**: En 375px y 1280px, 0 píxeles de solape entre FAB y CTA/resumen del cotizador (inspección visual o recortes superpuestos).
- **SC-003**: Labels del panel ≥14px; contraste AA en texto de UI del card.
- **SC-004**: El 100% de las vistas del CTA naranja del cotizador muestran **Pedir cotización** y 0 veces la palabra “Buscar”. Tras un envío válido, el CTA verde del resumen es **Continuar por WhatsApp**.
- **SC-005**: Tras submit válido, un revisor observa **exactamente un** patrón de confirmación (resumen en el card); 0 saltos a un “estado de solicitud” en el header como feedback principal.
- **SC-006**: Origen=destino, fechas inválidas y pasajeros &lt;1 se comportan como hoy en significado (no cotizan; mensaje en español; switch a Por horas cuando aplique).
- **SC-007**: Intercambiar origen/destino funciona en un intento; al menos 5 lugares reales del negocio aparecen como sugerencia.
- **SC-008**: 8 de 10 revisores describen el panel como barra de cotización de movilidad, no como buscador genérico ni como dos formularios distintos.
- **SC-009**: Catálogo, FAQ y bloque de marca del Hero no se perciben rediseñados.

## Assumptions

- El número WhatsApp autoritativo sigue siendo `+57 304 214 3149` (`wa.me/573042143149`).
- Copy de CTAs: naranja **Pedir cotización**; verde del resumen **Continuar por WhatsApp**. El naranja no promete abrir WhatsApp.
- Solape FAB: se resuelve **ocultando el FAB mientras el cotizador está en el viewport** (o desplazándolo con safe-area); reaparece al hacer scroll hacia abajo. No se elimina el flotante del resto de la página.
- En ~1280px, Solo ida cabe en una fila de campos + CTA. Ida y vuelta usa dos filas deliberadas (fechas arriba; hora/pasajeros/CTA abajo), no un wrap accidental.
- “Estructura de slots” = ambos modos ocupan un esqueleto de campos + CTA comparable; Por horas no deja una franja hueca bajo los tabs.
- Sugerencias de lugar: reutilizar y enriquecer el `datalist` (o equivalente) con sitios ya en la oferta (Cartagena, Barranquilla, Santa Marta, aeropuerto, Barú, etc.).
- El estado `has-request` del header, si existe, se deja de usar como confirmación; el visitante modifica la cotización editando el formulario bajo el resumen (el formulario permanece visible, como en 001).
- Referencias Uber Airport / Airbnb: principios de claridad, no copia de UI ni de copy.
- 004 queda históricamente como consistencia; **005 manda** si hay conflicto.

## Out of Scope

- Precios, cupos, mapas, cuentas, pasarela, datepicker de librería, npm/framework.
- Nuevos modos (tours en el cotizador, eSIM).
- Hora de regreso en el formulario.
- Rediseño de marca del Hero, catálogo, FAQ.
- Reabrir 004 como alcance (“solo consistencia”) sin las fricciones de esta spec.
- Copiar lettering o layout de Uber/Airbnb.
