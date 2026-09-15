# Feature Specification: Buscador desplegable en móvil

**Feature Branch**: `011-mobile-search-accordion`

**Created**: 2026-09-15

**Status**: Draft

**Input**: User description: "perfecto, ahora ahi mismo en mobile me gustaria que el buscador sea desplegable, tipo acordeon"

## Relación con las features 005–010

**011 es la fuente vigente solo para mostrar u ocultar el buscador al componer en vista estrecha (móvil).**

| Tema | Estado en 011 |
|------|----------------|
| 010: compactación moderada, campos apilados, sin intercambio en móvil | **Se conserva** cuando el acordeón está **abierto**. |
| 006: una fila Ida y vuelta en escritorio | **Se conserva.** En escritorio el buscador **no** es acordeón: sigue siempre visible. |
| 007–009: tras cotizar, solo resumen compacto; Modificar restaura el formulario | **Se conservan.** El acordeón **no** aplica al card cotizado. |
| Copy, validaciones, WhatsApp | **Se conservan.** |

## Clarifications

### Session 2026-09-15

- Q: ¿Qué texto lleva la cabecera del acordeón (franja cerrada) en el teléfono? → A: **Pedir cotización**. MUST NOT “Cotizar traslado” ni “Traslado o por horas” como título de la franja.
- Q: Con el formulario desplegado, ¿la cabecera Pedir cotización sigue ahí para cerrar? → A: **Sí**: franja + formulario debajo; tocar la franja cierra. MUST NOT ocultar la cabecera al abrir ni sustituirla solo por un chevron.
- Q: Con el panel abierto hay dos “Pedir cotización” (franja + botón naranja). ¿Qué hace la cabecera? → A: Mismo texto **Pedir cotización** + señal de abierto/cerrado; el naranja sigue siendo el envío. MUST NOT cambiar la franja a “Cerrar”.

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Primer pantallazo con el Hero libre (Priority: P1)

Un visitante abre la homepage en el teléfono. El buscador compacto de 010 sigue siendo alto si está todo abierto. Quiere un **acordeón**: una franja clara al pie con el texto **Pedir cotización** y, al tocarla, se **despliega** el formulario. Al llegar, el bloque está **cerrado** para que marca y foto del Hero se vean de verdad.

**Why this priority**: El usuario pide el acordeón en el mismo sitio móvil; es el siguiente recorte del primer pantallazo.

**Independent Test**: En ~375px, al cargar (antes de cotizar), el pie es una sola franja accionable; al tocarla aparece el buscador 010; al tocarla otra vez se pliega.

**Acceptance Scenarios**:

1. **Given** el primer pantallazo en ~375px, **When** el visitante aún no ha abierto el buscador, **Then** ve una **cabecera** de acordeón con el texto **Pedir cotización** y **no** el formulario completo. El Hero (marca y foto) domina.
2. **Given** esa cabecera, **When** la pulsa, **Then** se despliega Transporte o Por horas con densidad 010 (apilado, sin intercambio) **debajo de la misma franja** Pedir cotización. Puede volver a pulsar esa cabecera para **cerrar**.
3. **Given** escritorio ~1280px, **When** mira el Hero, **Then** el buscador **no** es acordeón: barra siempre visible (006).

---

### User Story 2 - Completar la cotización con el panel abierto (Priority: P1)

Con el acordeón abierto, el visitante rellena y pide cotización igual que hoy. Los errores y el aviso origen = destino se ven **dentro** del panel abierto (no detrás de un acordeón cerrado).

**Why this priority**: El acordeón no debe impedir convertir.

**Independent Test**: Abrir → completar Transporte o Por horas → Pedir cotización válido; o fallar validación y leer el aviso sin reabrir a ciegas.

**Acceptance Scenarios**:

1. **Given** el acordeón abierto, **When** envía un traslado válido, **Then** ocurre 007: desaparece el formulario/acordeón y queda el **resumen** compacto (009).
2. **Given** el acordeón abierto y un error (campo vacío, origen = destino, fecha inválida), **When** envía, **Then** el panel **sigue abierto** y el mensaje es visible.
3. **Given** Por horas, **When** abre el acordeón, **Then** el modo Por horas se despliega con la misma lógica (abrir/cerrar cabecera).

---

### User Story 3 - Modificar vuelve a un formulario usable (Priority: P2)

Tras el resumen, **Modificar** debe devolver el buscador **ya desplegado** en móvil, listo para editar, no una cabecera cerrada que oculta los datos.

**Why this priority**: 007 pide recuperar el formulario; un acordeón cerrado rompería esa promesa.

**Independent Test**: Cotizar en 375 → Modificar → formulario 010 visible (acordeón abierto).

**Acceptance Scenarios**:

1. **Given** el resumen en móvil, **When** pulsa Modificar, **Then** el acordeón está **abierto** y muestra el formulario compacto 010.
2. **Given** ese estado, **When** cierra el acordeón, **Then** vuelve a la franja; los datos que había escrito **no se pierden** al reabrir.

---

### Edge Cases

- Al rotar o pasar a vista ancha: el acordeón MUST dejar de aplicarse; el buscador se ve completo (006/005).
- Un solo acordeón: Transporte y Por horas son pestañas **dentro** del panel abierto, no dos acordeones apilados.
- Estado cotizado: MUST NOT mostrar cabecera de acordeón encima del resumen; 009 manda.
- MUST NOT exigir que el visitante “adivine” que puede cotizar: la cabecera cerrada MUST mostrar **Pedir cotización**.
- Accesible al tacto: la zona de abrir/cerrar MUST ser la **misma franja** en abierto y cerrado; MUST haber señal de estado además del texto fijo **Pedir cotización** (no solo un icono mudo; el naranja no se usa para plegar).

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: En vista estrecha (teléfono), el buscador **al componer** MUST comportarse como **acordeón**: cabecera **siempre visible** (abierto o cerrado) con el texto **Pedir cotización** y una **señal de estado** (abierto vs cerrado); el cuerpo (formulario) se muestra u oculta al activar esa cabecera. MUST NOT ocultar la cabecera al desplegar ni cambiar su texto a “Cerrar”. El botón naranja del formulario MUST seguir siendo el único envío.
- **FR-002**: En la primera carga en esa vista, el acordeón MUST estar **cerrado**.
- **FR-003**: Con el panel abierto, layout y densidad MUST seguir **010**. Validaciones y WhatsApp MUST conservar su significado.
- **FR-004**: En vista ancha (escritorio), MUST NOT haber acordeón; el buscador permanece siempre desplegado (006).
- **FR-005**: Tras Pedir cotización válido, MUST aplicarse 007/009 (solo resumen). Tras **Modificar**, el acordeón MUST abrirse con el formulario. Errores de envío MUST dejar el panel abierto.
- **FR-006**: Al cerrar y reabrir (sin cotizar), los valores ya escritos MUST conservarse.

### Key Entities

- **Acordeón del buscador**: Cabecera + cuerpo del panel de reserva en móvil, solo estado “componer”.
- **Cabecera**: Control que abre y cierra; etiqueta **Pedir cotización**.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Un revisor en ~375px confirma que, al cargar, el pie es **una franja** con **Pedir cotización** (no el formulario 010 completo) y que el Hero se percibe más libre que con 010 siempre abierto.
- **SC-002**: En un intento, abrir → ver campos (franja sigue diciendo Pedir cotización) → cerrar → reabrir funciona; 100% de los envíos válidos se hacen con el **botón naranja**, no con la franja.
- **SC-003**: En ~1280px, 0 comportamiento de acordeón; Ida y vuelta sigue en una fila (006).
- **SC-004**: Tras cotizar, el resumen cumple 009; Modificar en 375 deja el formulario **visible** (acordeón abierto). 0 overflow horizontal por el acordeón.

## Assumptions

- “Ahí mismo en mobile” = el mismo pie del Hero, viewport estrecho como 010 (~375; criterio de pila vs fila de 010).
- Acordeón **clásico** (clarificación A): cabecera siempre visible; el formulario va debajo al abrir. Cerrado al llegar: el usuario acaba de compactar porque el panel tapaba el Hero.
- Un acordeón, dos modos (pestañas dentro). Copy de cabecera: **Pedir cotización** siempre (clarificaciones B y A del texto). MUST NOT “Cerrar”, “Cotizar traslado” ni “Traslado o por horas” como título de la franja. El envío es el CTA naranja.
- No se pide recordar abierto/cerrado entre visitas (sin persistencia de visitante; constitución).
- Escritorio y tablet en fila (cuando 010 muestra intercambio) no usan acordeón.

## Out of Scope

- Cambiar 006, catálogo, FAQ, FAB de WhatsApp.
- Rediseñar el card cotizado (009).
- Precios, inventario o campos nuevos.
