# Research: Pie del buscador en escritorio

## Por qué el pie se “perdió” en ≥768px

**Decision**: El Hero a `height: auto` vive hoy en `@media (max-width: 768px)`, pensado para que el acordeón **móvil** crezca. Ese media **incluye 768px** (tablet / borde de 011) y deja de fijar el primer pantallazo a la ventana. En escritorio ancho el base ya es `100vh`, pero `is-collapsed` en el HTML más cualquier height de compositor filtrada mal puede dejar el form a media columna. 014 **separa** los cortes: crecimiento del acordeón **solo** en `max-width: 767px`; ≥768 vuelve a Hero **viewport** + barra al borde inferior.

**Rationale**: 011 no usa acordeón desde 768. Constitución IV: Hero a viewport completo. El usuario quiere “como antes, en el pie”.

**Alternatives considered**: Duplicar el buscador en el DOM (rechazado). JS que quite `is-collapsed` en resize (rechazado: G5 / “sin JS”). `position: sticky` en el footer (innecesario si el flex `space-between` + 100vh vuelve).

## `is-collapsed` en escritorio

**Decision**: En `min-width: 768px`, `.search-composer` MUST verse con altura automática **aunque** `#hero-search` lleve `is-collapsed`. Toggle sigue `display: none`. MUST NOT interpolar altura 012.

**Rationale**: El HTML carga con `is-collapsed` para 011. `setAccordionOpen` no corre al cargar en desktop de forma que quite la clase. El CSS de `height: 0` debe permanecer **dentro** de 767.

**Alternatives considered**: Quitar `is-collapsed` del HTML (rompería el cerrado inicial móvil).

## Congelar móvil

**Decision**: No reordenar `.hero-message` / `.hero-actions`. No tocar `flex-start` ni `margin-top: auto` de 013. Solo **mover** `height: auto` / `min-height: 100vh` del Hero desde el bloque 768 al bloque 767 (el resto de 768 — menú, tipografía — puede quedarse).

**Rationale**: FR-003. 375 ya entra en 767; el acordeón sigue pudiendo alargar el Hero.

**Alternatives considered**: Revertir 013 en desktop copy (el usuario no lo pidió; 013 ya dejaba escritorio en `justify-content: center`).
