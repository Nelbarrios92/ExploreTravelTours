# Research: Composición del Hero en móvil

## Causa del salto

**Decision**: Tratar el salto como **re-centrado flex**, no como un bug del acordeón.

**Rationale**: `.hero-content` tiene `flex: 1` y `justify-content: center`. `.hero-layout` es columna `space-between` con el buscador en `.hero-footer`. Al crecer el pie (012), el hueco de `.hero-content` se achica y **todo** el stack (título, texto, botón) se vuelve a centrar → el mensaje “sube”.

**Alternatives considered**: Culpar a `setAccordionOpen` (el pie debe crecer; 012 se conserva). `position: sticky` en el título (fuera de alcance: no fijar al scroll de página).

## Anclar mensaje, empujar acciones

**Decision**: En `index.html`, agrupar marca + regla + descripción en `.hero-message` y botón + `.hero-social` en `.hero-actions`. En `@media (max-width: 767px)`: `.hero-content { justify-content: flex-start; }`, `.hero-actions { margin-top: auto; }`. Escritorio (`min-width: 768px`): sin `margin-top: auto`; `.hero-content` sigue centrando el stack.

**Rationale**: El aire vive en el margen automático entre mensaje y acciones. Al encogerse `.hero-content`, ese margen baja a 0 y las acciones suben; `.hero-message` permanece al inicio (FR-001–005, clarificación A). Explorar servicios queda justo encima del pie (FR-007). Mismo corte **767px** que 011/012.

**Alternatives considered**: `justify-content: space-between` sin wrappers (repartiría huecos entre marca, regla y subtítulo). Grid de 3 filas (más CSS). Medir y fijar `top` en JS (viola “sin JS” y G5). Overlay del formulario sobre el botón (rechazado en clarificar).

## Ida y vuelta / teclado

**Decision**: No forzar `overflow: hidden` extra en el Hero. Si mensaje + botón + formulario no caben, el documento MAY hacer scroll (spec). MUST NOT recortar el título. En solo ida, el botón MUST quedar por encima del buscador en el flujo (no `position: absolute` sobre el form).

**Rationale**: Edge case del spec; el caso de aceptación es solo ida a ~375px.

**Alternatives considered**: Encoger tipografía al abrir (cambia 002). Ocultar redes al abrir (MAY compactar, no obligatorio en típico).

## Desktop

**Decision**: Cero reglas nuevas de composición para `min-width: 768px` salvo que los wrappers no alteren el centrado actual.

**Rationale**: SC-003 / FR-006.

**Alternatives considered**: Aplicar el ancla también en tablet (el usuario no lo pidió; 011 no usa acordeón ≥768).
