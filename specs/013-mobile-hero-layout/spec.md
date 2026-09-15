# Feature Specification: Composición del Hero en móvil

**Feature Branch**: `013-mobile-hero-layout`

**Created**: 2026-09-15

**Status**: Draft

**Input**: User description: "el contenido del hero en mobile, el titulo deberia estar mas arriba, acto seguio la descripcion, y el boton no lo subas tanto. la idea con esto es que cuando se abra el solicitar cotizacion no se vea que se mueve lo demas, vale?"

## Relación con las features anteriores

**013 es la fuente vigente para la composición vertical del bloque de copy del Hero en vista estrecha (título, descripción y botón de explorar).**

| Tema | Estado en 013 |
|------|----------------|
| 011/012: acordeón Pedir cotización, animación de altura, cerrado al cargar | **Se conservan.** MUST NOT cambiar el comportamiento del buscador. |
| 002: copy, tipografía de marca y H1/subtítulo | **Se conservan.** MUST NOT reescribir textos ni cambiar fuentes. |
| Constitución: Hero a viewport completo, overlay, WhatsApp | **Se conservan.** |
| Escritorio (~768px y más) | **Sin cambio** de composición del Hero. |

## Clarifications

### Session 2026-09-15

- Q: Al abrir Pedir cotización, ¿qué debe quedarse quieto? → A: **Solo título y descripción**. Explorar servicios y redes MAY subir; MUST NOT exigir que el botón también se quede fijo.
- Q: En el caso típico (solo ida), ¿Explorar servicios sigue usable? → A: **Sí**: visible y tocable, justo encima del buscador (puede haber subido). MUST NOT taparlo ni ocultarlo en ese caso.

## User Scenarios & Testing *(mandatory)*

### User Story 1 - El mensaje queda arriba, el botón no se pega al título (Priority: P1)

Un visitante en el teléfono ve el primer pantallazo. Quiere leer el **título** cerca de la parte superior (bajo el menú), la **descripción** justo debajo, y el botón **Explorar servicios** más abajo, sin que todo el bloque quede centrado en el hueco que deja el buscador.

**Why this priority**: El usuario pide explícitamente título más arriba, descripción a continuación y el botón no tan subido.

**Independent Test**: En ~375px, con el acordeón cerrado, un revisor confirma el orden y que hay más aire entre la descripción y el botón que entre título y descripción.

**Acceptance Scenarios**:

1. **Given** la vista estrecha con el buscador plegado, **When** mira el Hero, **Then** ve el título (identificador de marca del Hero) **más arriba** que hoy, no a media altura de la foto.
2. **Given** el mismo pantallazo, **When** lee el texto, **Then** la descripción va **inmediatamente después** del título (misma familia de lectura, sin un hueco grande entre ambos).
3. **Given** el botón Explorar servicios, **When** compara con título y descripción, **Then** el botón **no** está pegado a esa pareja de textos: queda **más abajo** (más cerca del pie / buscador que del título).

---

### User Story 2 - Abrir Pedir cotización no mueve el mensaje (Priority: P1)

El visitante abre **Pedir cotización**. El formulario crece. El título y la descripción **no deben parecer que saltan**; el crecimiento se come el aire entre la descripción y el pie. El botón y las redes **no** forman parte de ese anclaje (clarificación A).

**Why this priority**: Es el “vale” del pedido: estabilidad percibida al abrir el buscador.

**Independent Test**: En ~375px, anotar dónde está el título (y la descripción) con el acordeón cerrado; abrir Pedir cotización; confirmar que ese bloque de texto sigue en el mismo sitio a simple vista.

**Acceptance Scenarios**:

1. **Given** el acordeón cerrado en ~375px, **When** abre Pedir cotización, **Then** título y descripción **no se perciben desplazados**. Si algo se acerca al pie, es el bloque de acción, no el mensaje.
2. **Given** el acordeón abierto, **When** lo cierra, **Then** título y descripción siguen anclados arriba; el botón vuelve a verse más bajo (US1).
3. **Given** escritorio ~1280px, **When** usa el Hero, **Then** no aplica esta composición móvil; el buscador no es acordeón (011).

---

### User Story 3 - El botón puede ceder; el mensaje no (Priority: P2)

Si al abrir el formulario hace falta hueco, Explorar servicios **MAY** subir, pero en **solo ida** MUST seguir **entero y tocable** encima del buscador. Las redes MAY perder protagonismo. MUST NOT sacrificarse título y descripción.

**Why this priority**: El botón cede posición, no desaparece en el flujo típico.

**Independent Test**: Abrir el acordeón en ~375px (solo ida): título y descripción fijos; Explorar servicios completo y usable sobre la franja.

**Acceptance Scenarios**:

1. **Given** apertura típica (solo ida), **When** el panel está abierto, **Then** título y descripción siguen **completos y legibles**, y Explorar servicios está **visible y se puede pulsar**.
2. **Given** la misma apertura, **When** el formulario creció, **Then** el botón está **justo encima** del buscador (más arriba que en US1 si hizo falta); MUST NOT quedar debajo ni recortado por el formulario.

---

### Edge Cases

- Ida y vuelta (panel más alto) o teclado: MUST NOT hacer que el título desaparezca por el borde superior; MAY hacer scroll del Hero si ya no caben mensaje + botón + formulario. MUST NOT tapar Explorar servicios en **solo ida**.
- Estado cotizado (resumen 009): el mensaje del Hero MUST permanecer tan estable como al abrir el acordeón (el card es más bajo que el formulario abierto).
- Rotación a escritorio: composición de escritorio, sin “título pegado arriba” de 013.
- Redes sociales del Hero: van con el bloque de acción (zona que cede); MUST NOT intercalarse entre título y descripción.
- MUST NOT cambiar copy, paleta, overlay, ni el flujo WhatsApp.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: En vista estrecha, el título del Hero MUST mostrarse **arriba**, bajo la barra de navegación, no centrado en el espacio que deja el buscador.
- **FR-002**: La descripción MUST aparecer **acto seguido** del título (hueco pequeño de lectura, no un vacío de “centrado”).
- **FR-003**: El botón Explorar servicios MUST quedar **más abajo** que título+descripción; MUST NOT subirse al mismo bloque compacto superior.
- **FR-004**: Al abrir o cerrar Pedir cotización, **solo** título y descripción MUST **mantener su posición percibida**. MUST NOT re-centrar el mensaje. MUST NOT exigir el mismo anclaje para Explorar servicios ni redes (clarificación A).
- **FR-005**: El crecimiento del buscador MUST absorberse con el **aire** entre la descripción y el pie; el bloque de acción MAY subir.
- **FR-006**: MUST NOT alterar 011/012, 002 (textos y tipografía de marca), catálogo, FAQ ni el Hero de escritorio.
- **FR-007**: Con el acordeón abierto en **solo ida**, Explorar servicios MUST permanecer **completo, visible y tocable** inmediatamente encima del buscador. MUST NOT superponer el formulario sobre ese botón ni ocultarlo. Las redes MAY compactarse.

### Key Entities

- **Bloque de mensaje**: Título de marca del Hero + descripción; anclado arriba en móvil.
- **Bloque de acción**: Botón Explorar servicios (y, si aplica, redes); más bajo al cargar; al abrir en solo ida el botón sigue usable encima del pie.
- **Pie de cotización**: Franja Pedir cotización / formulario / resumen; crece y se pliega como 011/012.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: En ~375px, acordeón cerrado, un revisor confirma: título en el tercio superior del Hero (bajo el menú); descripción pegada a ese título; botón visiblemente más bajo.
- **SC-002**: Al abrir Pedir cotización en ~375px, título y descripción se desplazan **menos de ~8 px**. El botón MAY desplazarse más; el movimiento que se nota es el del formulario (y, si acaso, del bloque de acción).
- **SC-003**: En ~1280px, 0 cambio de composición del Hero respecto a la feature anterior.
- **SC-004**: 100% del copy, destinos y WhatsApp iguales; 0 recorte del título al terminar de abrir el caso típico (solo ida).
- **SC-005**: En ~375px, 100% de las aperturas **solo ida**: Explorar servicios sigue entero y se puede pulsar encima del buscador.

## Assumptions

- “Título” = identificador de marca del Hero; “descripción” = párrafo que lo sigue; “botón” = Explorar servicios. “Lo demás” que no debe saltar = **solo** el bloque de mensaje (clarificación A).
- Vista estrecha = la misma que el acordeón 011 (~menos de 768 px de ancho).
- El Hero sigue ocupando el alto de la pantalla; no se pide un Hero más bajo ni quitar el buscador del pie.
- Un desplazamiento mínimo residual (sombra, redondeo de un dígito de píxel) no cuenta como “se mueve lo demás”.
- Compactar o restar protagonismo aplica a **redes** o a paneles más altos (ida y vuelta), no a Explorar servicios en solo ida.
- No se pide rediseño de marca, ni mover el buscador a otra sección.

## Out of Scope

- Cambiar textos, fuentes, foto, overlay o CTAs de WhatsApp.
- Rediseñar 010–012 (campos, acordeón, animación, resumen).
- Hero de escritorio, catálogo, testimonios, FAQ.
- Fijar el título a la pantalla al hacer scroll de toda la página.
