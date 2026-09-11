# Feature Specification: Identidad tipográfica del Hero

**Feature Branch**: `002-hero-brand-typography`

**Created**: 2026-09-11

**Status**: Draft

**Input**: User description: "Mejorar la identidad tipográfica y la jerarquía visual del Hero de la página de inicio: convertir 'Explore Travel Tours' en identificador de marca contemporáneo y editorial, subordinado al H1 'Tu viaje comienza con la forma de moverte.', con composición izquierda/fotografía derecha, responsive y sin rediseño del resto del sitio."

## Clarifications

### Session 2026-09-11

- Q: ¿El identificador “Explore Travel Tours” puede usar una tipografía distinta a la del resto del sitio? → A: Sí. Se permite una tipografía de display contemporánea únicamente para ese identificador en el Hero; el resto del sitio conserva el sistema tipográfico actual.
- Q: ¿Qué copy debe tener el subtítulo del Hero? → A: Apoyo alineado al H1 (transporte privado y vehículos premium), no el texto genérico de destinos del Caribe. La frase exacta se puede pulir en planificación; no se inventan ofertas nuevas.
- Q: ¿Qué texto es el titular principal de la página? → A: El mensaje “Tu viaje comienza con la forma de moverte.” es el único titular principal. “Explore Travel Tours” es identificador visual, no el heading de la página. El nombre de la agencia se conserva en el título del documento y en los datos de negocio.

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Percibir la marca como premium y contemporánea (Priority: P1)

Un visitante llega a la homepage de Explore Travel Tours (agencia de Cartagena cuyo valor se centra en transporte privado, alquiler de vehículos y experiencias). En el primer pantallazo ve el nombre **Explore Travel Tours** como identificador de marca: grande, memorable y con carácter editorial, no como un rótulo genérico o anticuado de agencia turística. Inmediatamente debajo, separado con claridad, lee el mensaje principal **Tu viaje comienza con la forma de moverte.** Ese titular es visiblemente más importante que el nombre. El subtítulo explica la propuesta de valor (transporte privado y vehículos premium) sin competir. A la derecha (en escritorio) la fotografía de Cartagena con el vehículo sigue siendo protagonista. El visitante no siente la pantalla sobrecargada ni que el nombre “grite” más que el mensaje.

**Why this priority**: El problema de negocio es de percepción de marca en el primer contacto. Si el nombre se ve antiguo o si se “arregla” solo agrandándolo, el Hero no transmite turismo premium, Cartagena, elegancia, modernidad, confianza, movilidad y experiencia.

**Independent Test**: Con el resto del sitio igual, un revisor y el cliente pueden juzgar solo el bloque marca + H1 + subtítulo sobre la fotografía: el nombre ya no se percibe antiguo; tiene presencia; el H1 sigue siendo el elemento de comunicación principal.

**Acceptance Scenarios**:

1. **Given** un visitante en escritorio en el primer pantallazo del Hero, **When** mira el bloque de contenido izquierdo, **Then** ve “Explore Travel Tours” como identificador de marca (eyebrow premium), no como el titular principal de la página, en formato de nombre propio (no forzado a mayúsculas completas).
2. **Given** el mismo Hero, **When** compara el peso visual del nombre y del H1, **Then** el H1 “Tu viaje comienza con la forma de moverte.” es el elemento tipográfico dominante; el nombre es considerable pero claramente subordinado.
3. **Given** el bloque de marca, **When** el revisor evalúa personalidad tipográfica, **Then** percibe carácter contemporáneo, sofisticado y de marca (no fuente genérica, no estética de boda/evento, no agencia turística cliché), claramente distinto del tratamiento de títulos del resto del sitio.
4. **Given** el cliente que hoy percibe el nombre como antiguo, **When** revisa el Hero actualizado, **Then** ya no describe esa presentación como tipografía antigua o poco sofisticada.

---

### User Story 2 - Leer una composición editorial clara en escritorio (Priority: P1)

En escritorio, el visitante percibe una composición deliberada, con aire y jerarquía cercana a:

Explore Travel Tours  
━━━━━━━━━━━━━━━━━━  

Tu viaje comienza  
con la forma de  
moverte.

El nombre ocupa su propio registro. Hay una separación clara (espacio y/o un divisor sobrio) antes del H1. El H1 se lee en aproximadamente tres líneas: “Tu viaje comienza / con la forma de / moverte.” El subtítulo queda debajo, más pequeño, como explicación. El CTA “Explorar servicios” y el enlace de Instagram siguen disponibles sin convertirse en protagonistas. El contenido permanece a la izquierda; la fotografía y el vehículo conservan protagonismo a la derecha. El nombre se integra con la foto (legible, con contraste) y no pelea innecesariamente con ella.

**Why this priority**: La jerarquía y la composición son el medio para que la marca gane presencia sin usurpar el H1 ni tapar la fotografía.

**Independent Test**: En un viewport de escritorio amplio se puede capturar el Hero y verificar líneas, separación marca–H1, alineación izquierda y visibilidad del sujeto de la foto, sin usar otras secciones.

**Acceptance Scenarios**:

1. **Given** un viewport de escritorio, **When** el visitante mira el H1, **Then** el copy exacto es “Tu viaje comienza con la forma de moverte.” y la composición permite una lectura visual de aproximadamente tres líneas (“Tu viaje comienza”, “con la forma de”, “moverte.”).
2. **Given** el nombre y el H1, **When** el visitante recorre el bloque de arriba abajo, **Then** existe una separación clara entre ambos (no se leen como un solo bloque tipográfico continuo).
3. **Given** el Hero en escritorio, **When** observa la distribución, **Then** el bloque de contenido (marca, H1, subtítulo, CTA, Instagram) está en la zona izquierda y la fotografía de Cartagena con el vehículo conserva protagonismo en la zona derecha.
4. **Given** el Hero, **When** evalúa densidad visual, **Then** la composición se siente editorial y no sobrecargada: sin exceso de efectos, sombras innecesarias, degradados decorativos sin función ni elementos turísticos cliché añadidos.
5. **Given** el subtítulo, **When** el visitante lo lee, **Then** explica transporte privado y/o vehículos premium como apoyo del H1, permanece subordinado, y MUST NOT ser el copy genérico de “maravillas del Caribe / aventuras inolvidables”.

---

### User Story 3 - Conservar jerarquía y legibilidad en tablet y móvil (Priority: P2)

En tablet y móvil el visitante sigue identificando la marca y leyendo el mensaje principal con excelente contraste sobre la fotografía. El nombre se reduce de forma proporcional; el H1 se adapta al ancho disponible. No se fuerza la misma partición de tres líneas del escritorio si eso perjudica la legibilidad o provoca cortes extraños. El orden de lectura (marca → separación → H1 → subtítulo → acciones) se conserva. El Hero no depende de valores pensados para una sola resolución: la jerarquía se mantiene al cambiar el ancho.

**Why this priority**: Una identidad premium que se rompe en el teléfono deja de ser creíble para el viajero que descubre la agencia en móvil.

**Independent Test**: Recorrer el Hero en anchos de móvil, tablet y escritorio y confirmar orden, contraste y que el H1 sigue dominando al nombre.

**Acceptance Scenarios**:

1. **Given** un viewport móvil, **When** el visitante ve el Hero, **Then** “Explore Travel Tours” es visible y proporcionado (más pequeño que en escritorio) y el H1 se adapta al ancho sin perderse ni quedar ilegible.
2. **Given** un viewport móvil, **When** la partición de tres líneas del escritorio no cabe con naturalidad, **Then** el H1 puede refluir a un número de líneas distinto; MUST NOT forzar la misma composición si daña la lectura.
3. **Given** tablet, **When** el visitante compara con escritorio y móvil, **Then** la jerarquía (H1 > marca > subtítulo) se mantiene y el texto sigue contrastado sobre la fotografía.
4. **Given** un cambio de ancho entre los breakpoints habituales del sitio, **When** el revisor redimensiona, **Then** el resultado no se percibe como un arreglo solo para una resolución concreta.

---

### Edge Cases

- Nombre largo en móvil: “Explore Travel Tours” MUST permanecer en una o dos líneas naturales; MUST NOT recortarse, superponerse al H1 ni invadir de forma permanente el sujeto principal de la fotografía.
- Zoom de texto o tamaño de letra aumentado del sistema: marca, H1 y subtítulo MUST seguir leyéndose; MUST NOT solaparse de forma ilegible.
- Contraste sobre zonas claras u oscuras de la fotografía: el texto del bloque izquierdo MUST permanecer excelente de leer; el recurso de legibilidad (p. ej. overlay existente) MUST conservarse o ajustarse solo en lo necesario para este bloque, sin rediseñar la foto.
- Elementos decorativos existentes sobre la fotografía: MUST NOT ser el foco de esta feature; si interfieren con la nueva jerarquía, MAY revisarse después; MUST NOT añadirse nuevos adornos para “compensar” la tipografía.
- Navbar, logo, WhatsApp e Instagram: MUST seguir usables; la nueva presencia del nombre en el Hero MUST NOT duplicar de forma confusa el logo del header ni tapar la navegación.
- Lectores de pantalla y esquema de títulos: el titular principal anunciado MUST ser el mensaje de viaje; MUST NOT haber dos titulares principales (nombre + mensaje). El nombre de la agencia MUST seguir reconocible en el título de la pestaña/página y en los datos de negocio ya publicados.
- Buscador en el pie del Hero (si está presente): MUST permanecer en su zona; esta feature MUST NOT desplazarlo al centro ni taparlo con el bloque de marca.
- Escritorio estrecho / tablet ancha: la zona izquierda MUST ceder espacio a la foto de forma gradual; MUST NOT aplastar el H1 contra el borde ni cubrir el vehículo de forma total.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: El Hero MUST presentar el identificador de marca con el texto exacto “Explore Travel Tours” (formato de nombre propio; MUST NOT exigirse versales completas).
- **FR-002**: El identificador de marca MUST funcionar como eyebrow / firma de identidad: presencia considerable, memorable y con personalidad propia, y MUST permanecer visualmente subordinado al H1.
- **FR-003**: El H1 MUST conservar el copy exacto “Tu viaje comienza con la forma de moverte.” y MUST ser el único titular principal de la página (máximo peso visual y de comunicación). “Explore Travel Tours” MUST NOT ser el heading principal del documento.
- **FR-004**: En escritorio, el H1 MUST poder leerse con una división visual clara de aproximadamente tres líneas: “Tu viaje comienza” / “con la forma de” / “moverte.”
- **FR-005**: MUST existir una separación clara entre el identificador de marca y el H1 (espaciado y, si aporta claridad editorial, un divisor sobrio). El divisor MUST NOT convertirse en adorno protagonista.
- **FR-006**: El subtítulo MUST apoyar el H1 con la propuesta de valor de movilidad: transporte privado y vehículos premium. MUST permanecer subordinado al H1. MUST NOT usar el copy genérico publicado de destinos del Caribe (“maravillas… aventuras inolvidables…”). MUST NOT convertirse en protagonista ni inventar ofertas, precios, flota o destinos nuevos. La redacción exacta MAY afinarse en planificación dentro de esa línea.
- **FR-007**: El bloque de contenido del Hero (marca, H1, subtítulo, CTA de exploración de servicios, Instagram) MUST permanecer en la zona izquierda en escritorio; la fotografía de Cartagena y el vehículo MUST conservar protagonismo en la zona derecha.
- **FR-008**: La presentación del nombre MUST resolverse con jerarquía, carácter tipográfico, espaciado, contraste y composición. MUST NOT resolverse únicamente aumentando el tamaño de letra.
- **FR-009**: La tipografía del identificador de marca MUST transmitir turismo premium, Cartagena, elegancia, modernidad, confianza, movilidad y experiencia. MUST NOT evocar agencia turística genérica o anticuada, ni una estética excesivamente ornamental, clásica o de bodas/eventos. El identificador MUST poder usar una tipografía de display contemporánea **exclusiva del Hero**; MUST NOT sustituir el sistema tipográfico de las demás secciones. La familia concreta se elige en planificación; esta spec fija el alcance (solo el identificador) y el carácter (contemporáneo, no ornamental).
- **FR-010**: El identificador MUST sentirse como marca contemporánea (identidad), no como texto decorativo suelto.
- **FR-011**: La composición MUST sentirse editorial, premium y deliberada, comparable en principio (no en copia) a la claridad de marcas digitales contemporáneas de referencia (p. ej. Airbnb, Stripe, Vercel, Apple y estudios editoriales premium): jerarquía, simplicidad, espacio y percepción de calidad.
- **FR-012**: El Hero MUST evitar sobrecarga: MUST NOT añadir iconos nuevos, beneficios extra, efectos excesivos, sombras innecesarias, degradados decorativos sin función ni clichés turísticos.
- **FR-013**: El texto del bloque izquierdo MUST tener excelente legibilidad sobre la fotografía en escritorio, tablet y móvil (contraste y lectura sostenida, no solo en una captura).
- **FR-014**: La solución MUST contemplar escritorio, tablet y móvil. En móvil, el nombre MUST reducirse de forma proporcional y el H1 MUST adaptarse al ancho; MUST NOT forzar la composición de tres líneas del escritorio si perjudica la legibilidad.
- **FR-015**: La solución MUST comportarse de forma coherente al cambiar el ancho (sistema de tamaños y ritmo), no como valores arbitrarios válidos solo para una resolución.
- **FR-016**: CTA “Explorar servicios”, enlace de Instagram, navbar (Inicio, Servicios, Testimonios), logo del header, CTA de WhatsApp y fotografía de fondo MUST conservarse en su rol actual. El título de página y los datos estructurados de agencia MUST seguir identificando Explore Travel Tours. Esta feature MUST NOT rediseñarlos salvo el mínimo necesario para no romper jerarquía o contraste del bloque de marca.
- **FR-017**: Esta feature MUST limitarse al Hero de la homepage y a la relación visual entre “Explore Travel Tours” y el H1 (más el subtítulo en tanto que apoyo de jerarquía).
- **FR-018**: El resultado MUST poder entregarse dentro del modelo actual del sitio (página de marketing estática, sin nueva plataforma de producto ni dependencias innecesarias). MUST NOT exigir un framework o herramienta extra solo para conseguir la jerarquía tipográfica.
- **FR-019**: El copy del H1 MUST NOT cambiar en esta especificación. MUST NOT incluirse rediseño completo del sitio, nuevos iconos, nuevos beneficios bajo el Hero, nuevos servicios, cambios de contenido comercial, cambios de arquitectura de navegación, rediseño de otras secciones ni nuevas funcionalidades.

### Key Entities

- **Identificador de marca (eyebrow)**: El nombre “Explore Travel Tours” dentro del Hero. Atributos: texto fijo, rol secundario frente al H1, presencia alta, carácter contemporáneo y editorial, formato de nombre propio, tipografía de display propia del Hero (no aplicada al resto del sitio).
- **Titular principal (H1)**: Mensaje “Tu viaje comienza con la forma de moverte.” Atributos: copy inmutable en esta feature, único heading principal de la página, máximo peso visual, composición ~3 líneas en escritorio, adaptable en móvil.
- **Subtítulo de valor**: Texto de apoyo alineado al H1 (transporte privado y vehículos premium). Atributos: no genérico de destinos Caribe, peso visual menor que el H1, sin ofertas nuevas.
- **Bloque de contenido izquierdo**: Agrupa identificador, separación, H1, subtítulo y acciones existentes (explorar servicios, Instagram).
- **Fotografía de Hero**: Imagen realista de Cartagena con vehículo; protagonista en la zona derecha; el texto debe integrarse, no competir.
- **Separación marca–H1**: Recurso de jerarquía (aire y/o divisor sobrio) entre identificador y titular.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: En revisión con el cliente, la presentación de “Explore Travel Tours” en el Hero ya no se describe como antigua o poco sofisticada (criterio cualitativo de aceptación del negocio).
- **SC-002**: Un revisor independiente, sin ver el brief, identifica el H1 como el mensaje principal y el nombre como marca/eyebrow en menos de 5 segundos de mirada al Hero de escritorio.
- **SC-003**: En escritorio, al menos 8 de 10 revisores coinciden en que el nombre tiene más presencia que en la versión previa y, a la vez, menor peso que el H1 (ninguno describe al nombre como el titular).
- **SC-004**: El 100% de las revisiones confirman que el H1 visible es exactamente “Tu viaje comienza con la forma de moverte.”, que es el único titular principal de la página, y que en escritorio se lee con una partición visual de aproximadamente tres líneas.
- **SC-005**: En escritorio (~1280×800), un revisor confirma que el bloque de contenido está a la izquierda, que hay separación clara marca–H1, y que el sujeto principal de la fotografía (calle/vehículo) sigue visible y protagonista a la derecha.
- **SC-006**: En 375px, 768px y 1280px, un revisor lee de corrido marca, H1 y subtítulo sobre la foto sin entrecerrar los ojos ni perder contraste; en móvil el H1 no se fuerza a tres líneas si eso empeora la lectura.
- **SC-007**: Un revisor confirma que la composición no se siente sobrecargada (sin nuevos bloques de beneficios, iconos extra ni efectos decorativos añadidos para “llenar”).
- **SC-008**: La solución se valida en al menos tres anchos (móvil, tablet, escritorio) y se percibe como el mismo sistema de jerarquía, no como un ajuste hecho solo para una captura.
- **SC-009**: Un revisor de marca confirma que el identificador transmite carácter propio (premium, contemporáneo) y no una fuente genérica ni una estética de boda/evento o de agencia turística cliché; confirma además que títulos y textos de otras secciones no cambiaron de sistema tipográfico.
- **SC-010**: Tras el cambio, un visitante que ya usaba el sitio sigue encontrando navbar, WhatsApp, CTA de servicios e Instagram; no aparecen secciones, servicios ni funcionalidades nuevas.
- **SC-011**: Un revisor confirma que el subtítulo habla de transporte privado y/o vehículos premium y que no reaparece el copy genérico de destinos del Caribe como mensaje de apoyo del Hero.

## Assumptions

- El visitante típico es un viajero que evalúa transporte privado y experiencias en Cartagena; el primer pantallazo debe transmitir confianza premium, no un catálogo recargado.
- El copy de H1 indicado en esta spec es el autoritativo para el Hero y el titular principal de la página, aunque una versión publicada anterior usara el nombre de la empresa como único titular grande. El nombre de la agencia permanece en el título de la pestaña y en los datos de negocio.
- El subtítulo autoritativo es de apoyo a movilidad (transporte privado / vehículos premium), no el párrafo publicado de maravillas del Caribe. No implica cambio de oferta comercial ni destinos nuevos.
- El CTA de exploración de servicios e Instagram ya existen y se mantienen; no se rediseña su comportamiento.
- El buscador del pie del Hero, si está en producción, queda fuera del rediseño tipográfico salvo no romper su posición.
- Los elementos decorativos sobre la fotografía pueden revisarse en un trabajo posterior; no son el objetivo de esta spec.
- “Presencia considerable” significa que el nombre es claramente visible y memorable a distancia de un primer pantallazo de escritorio, no que iguale o supere al H1.
- La referencia a Airbnb, Stripe, Vercel y Apple es de principios (jerarquía, simplicidad, espacio, calidad), no de copia de lettering, paleta ni layout.
- Paleta, logo del header y fotografía de fondo se reutilizan; el cambio de carácter se concentra en el tratamiento del nombre y su relación con el H1.
- El identificador del Hero MAY usar una tipografía de display distinta a la de UI y títulos de sección; esa excepción no implica rediseñar la tipografía global. La familia concreta se decide en `/speckit-plan` (y, si aplica, con enmienda de constitución).
- La entrega sigue el sitio estático de marketing existente, sin nueva plataforma ni dependencias innecesarias (alineado a la constitución del proyecto).
- Accesibilidad: contraste y lectura son requisitos de éxito; no se sacrifica legibilidad por estilo.
- Breakpoints de referencia para aceptación: alrededor de 375px (móvil), 768px (tablet) y 1024px/1280px (escritorio), coherentes con el sitio actual.

## Out of Scope

- Rediseño completo del sitio o de la identidad global (nuevo logo, nueva paleta, nueva voz de marca, o cambiar la tipografía de todas las secciones).
- Aplicar la tipografía de display del identificador a títulos de servicios, testimonios u otras secciones.
- Nuevos iconos, ilustraciones o beneficios debajo del Hero.
- Nuevos servicios, destinos o cambios de contenido comercial.
- Cambios en la arquitectura de navegación.
- Rediseño de servicios, testimonios, FAQ, pie u otras secciones.
- Creación de nuevas funcionalidades (buscador, formularios, cuentas, pagos).
- Cambio del copy del H1.
- Restaurar o conservar el subtítulo genérico de destinos del Caribe como apoyo del Hero.
- Convertir el nombre en el titular principal de la página o resolver el problema solo agrandando la letra.
- Forzar la composición de tres líneas del H1 en móvil si daña la lectura.
- Copiar lettering o layouts de las marcas de referencia.
- Incorporar un framework o dependencia solo para tipografía o composición.
- Rediseño de los adornos sobre la fotografía (revisión posterior permitida, no objetivo).
