# Feature Specification: Escala unificada del resumen de cotización

**Feature Branch**: `008-quote-summary-scale`

**Created**: 2026-09-15

**Status**: Draft

**Input**: User description: "arregla ahora el resumen de cotizacion, entiende que esa parte toda debe manejar el mismo tamaño para que no se rompa visualmente ni le de una mala experiencia al usuario"

## Relación con las features 005–007

`specs/007-quote-summary-only` sigue vigente: tras Pedir cotización válido solo se ve el resumen; **Modificar** recupera el buscador. `006` rige el layout del buscador. **008 es la fuente vigente para la escala visual del resumen** (título, filas de datos, Continuar por WhatsApp, Modificar, sugerencias).

| Tema previo | Estado en 008 |
|-------------|----------------|
| Resumen “compacto/admin” (texto claramente más pequeño que el buscador, CTAs de distinta altura) | **Reemplazado**: todo el bloque del resumen MUST compartir **una misma escala** (cuerpo, etiquetas y botones alineados al sistema del card del Hero). |
| Copy, WhatsApp, Modificar, ocultar buscador | **Se conservan**. |

## Clarifications

### Session 2026-09-15

- Q: ¿El resumen va en una caja interior compacta o llena el card como el buscador? → A: **Mismo padding que el buscador**: el resumen llena el card blanco. MUST NOT una cajita interior más apretada; el arreglo no es solo agrandar letra dentro del recuadro gris actual.

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Leer el resumen como un solo bloque (Priority: P1)

Tras cotizar, el visitante ve título, pares etiqueta/valor, el botón verde y Modificar (y a veces enlaces relacionados). Hoy esos trozos se sienten de tamaños distintos: el listado se ve menudo frente a los botones, o al revés, y el card “se rompe”. Quiere una sola familia de tamaño: se lee de arriba abajo sin saltos de escala ni recortes.

**Why this priority**: El resumen es ahora la única superficie del card; si la escala es inconsistente, la confirmación se percibe barata o rota.

**Independent Test**: En 375px y ~1280px, comparar título, datos y ambos CTAs: una sola escala; nada ilegible ni desbordado.

**Acceptance Scenarios**:

1. **Given** un resumen visible (Traslado o Por horas), **When** el visitante recorre título, datos, Continuar por WhatsApp y Modificar, **Then** percibe **el mismo sistema de tamaño** (cuerpo ≥ el del buscador; botones de altura comparable entre sí). NEVER un bloque “minúsculo” junto a otro “de otro producto”.
2. **Given** ~1280px y ~375px, **When** mira el card, **Then** el resumen ocupa el mismo aire interior que el buscador (no un recuadro anidado más chico). MUST NOT haber recorte de texto, solape entre filas ni scroll horizontal causado por el resumen.
3. **Given** sugerencias relacionadas visibles, **When** las lee, **Then** usan la misma escala de cuerpo que las etiquetas/valores, no un tercer tamaño ajeno.

---

### User Story 2 - Mismo card en móvil y escritorio (Priority: P2)

En teléfono el resumen no debe volverse un bloque denso ilegible ni inflarse de forma distinta al escritorio. La escala es la misma familia; solo puede refluir el ancho.

**Why this priority**: 007 deja el resumen a pantalla completa del card en todos los anchos.

**Independent Test**: 375 vs 1280: misma jerarquía; CTA verde y Modificar usables (altura táctil suficiente).

**Acceptance Scenarios**:

1. **Given** 375px, **When** usa Continuar por WhatsApp y Modificar, **Then** ambos son accionables a ancho del card, misma altura percibida, sin taparse entre sí.
2. **Given** 1280px, **When** compara con 375, **Then** no aparece un “modo admin compacto” solo en escritorio: la escala de cuerpo y botones es la del mismo sistema.

---

### Edge Cases

- Listas largas (ida y vuelta con más filas): MUST NOT comprimir el texto por debajo de la escala acordada para “hacer caber”.
- Relacionados ausentes: el bloque de CTAs MUST mantener la misma escala (no se encoge el resto).
- Contraste AA sobre el fondo del resumen.
- MUST NOT reintroducir una caja gris interior más pequeña que el padding del card.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: Todo el contenido del resumen (título, etiquetas, valores, Continuar por WhatsApp, Modificar, texto de relacionados) MUST pertenecer a **una sola escala tipográfica y de controles**, alineada a la del buscador del mismo card (cuerpo de UI ≥14px percibidos; botones de altura equivalente entre sí, ~la de Pedir cotización). El resumen MUST usar el **mismo padding** del card que el buscador. MUST NOT presentarse como una caja interior compacta anidada.
- **FR-002**: MUST NOT dejar el listado de datos en una densidad claramente menor (tipo “letra pequeña de admin”) respecto a título o botones.
- **FR-003**: En 375px y ~1280px el resumen MUST caber en el card sin overflow horizontal ni solapes.
- **FR-004**: Continuar por WhatsApp y Modificar MUST compartir la misma altura de control y el mismo ancho de card; MUST NOT uno alto y otro bajo.
- **FR-005**: MUST NOT cambiar copy, número WhatsApp, flujo 007 ni el grid de Ida y vuelta 006.

### Key Entities

- **Resumen de cotización**: Superficie única post-éxito (007).
- **Escala del card**: Sistema de tamaño compartido entre buscador (cuando está visible) y resumen.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Un revisor confirma 0 saltos de escala obvios entre título, datos y los dos CTAs, y que el resumen **no** vive en una cajita interior más apretada que el buscador.
- **SC-002**: Etiquetas y valores del resumen se leen al menos tan grandes como las etiquetas del buscador (mismo umbral de cuerpo de UI).
- **SC-003**: Ambos CTAs del resumen tienen la misma altura percibida; en 375px son accionables sin solape.
- **SC-004**: 0 overflow horizontal del card atribuible al resumen en 375 y 1280.
- **SC-005**: 007 sigue cumpliéndose: tras éxito no reaparece el buscador; Modificar lo restaura.

## Assumptions

- “Mismo tamaño” = **misma escala de sistema** (cuerpo + altura de botón), no que el título tenga exactamente los mismos píxeles que una etiqueta.
- El resumen **no** se diferencia del buscador con un recuadro interior más denso; puede no tener fondo extra o usar el mismo fondo que el card.
- Fraunces sigue solo en la marca del Hero; el título del resumen MAY usar la serif de sección ya usada, a tamaño coherente con el cuerpo, no un display enorme.

## Out of Scope

- Rediseñar catálogo, FAQ o marca.
- Nuevos campos en el resumen.
- Cambiar el flujo de cotización o WhatsApp.
