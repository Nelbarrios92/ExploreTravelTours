# Contrato UI: buscador al pie en escritorio

**014 manda** la posición del buscador en **≥768px**. **011–013 mandan** **&lt;768px**.

## MUST

- `@media (min-width: 768px)`: `.hero-section` altura de ventana (`100vh`); `.hero-layout` columna con el buscador al **final**; `.search-accordion-toggle { display: none }`.
- Compositor visible: `height: auto` (o equivalente), `overflow` que no recorte campos 006. MUST NOT aplicar `height: 0` de 012.
- `@media (max-width: 767px)`: conservar 013 (mensaje / acciones) y 011/012 (franja, altura 0 colapsado, WAAPI). `height: auto` del Hero para el acordeón **aquí**, no en 768.

## MUST NOT

- Mostrar la franja Pedir cotización en escritorio.
- Cambiar copy, 006 grid, `script.js`, wrappers 013, o compactación 010 móvil.
- Acordeón o `display: none` del compositor en ≥768 salvo estado cotizado 007.
