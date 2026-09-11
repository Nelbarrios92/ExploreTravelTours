# Quickstart: Identidad tipográfica del Hero

Validación manual. No hay suite automatizada.

## Prerrequisitos

- Servir la raíz del repo (p. ej. Live Preview, `npx serve`, o abrir `index.html` con las rutas de `assets/` resolubles).
- Contratos: [hero-typography.md](./contracts/hero-typography.md), [hero-copy.md](./contracts/hero-copy.md).

## Recorrido

1. Cargar la homepage. Sin scroll en desktop ~1280×800.
2. Comprobar copy: identificador, H1 (tres líneas), subtítulo de movilidad, CTA “Explorar servicios”.
3. Comprobar que el nombre **no** es el único título enorme; el H1 de viaje es dominante.
4. Inspeccionar (lector de pantalla o inspector): un solo `h1` con el mensaje de viaje; `.hero-brand` no es `h1`.
5. Confirmar foto/vehículo visibles a la derecha y buscador flush al pie (sin desplazarlo).
6. Navbar, WhatsApp, Instagram, menú móvil: igual que antes.
7. Redimensionar a 768 y 375: marca más pequeña; H1 no forzado a tres líneas; texto legible sobre overlay.
8. Scroll: header sólido; ancla del CTA llega a experiencias.
9. Otras secciones: títulos Playfair/Montserrat sin Fraunces.

## Esperado

- Cliente/revisor ya no describe el nombre como tipografía antigua.
- Fraunces solo en el identificador; swap no deja el bloque vacío (fallback serif).
- Sin overflow-x; sin nuevas secciones ni iconos.

## Fuera de esta prueba

- Cambiar el buscador, catálogo, FAQ o adornos del Hero.
