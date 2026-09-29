# Contrato UI: Hero móvil (mensaje vs acciones)

**013 manda** la composición vertical del copy del Hero en **&lt;768px**. **011/012** mandan el pie de cotización.

## MUST

- Wrappers `.hero-message` (marca, regla, descripción) y `.hero-actions` (Explorar servicios, redes) dentro de `.hero-content`.
- Vista estrecha: `.hero-content` alinea el mensaje **al inicio**; `.hero-actions` usa **`margin-top: auto`** para sentarse sobre `.hero-footer`.
- Al abrir/cerrar la franja: desplazamiento de `.hero-message` **&lt; ~8 px**; el botón **no** usa `position` encima del formulario.
- Solo ida abierto: `.lets-go-btn` visible, completo, clicable, **en flujo** inmediatamente encima del buscador.
- `min-width: 768px`: misma composición percibida que antes de 013 (stack centrado).

## MUST NOT

- `justify-content: center` en `.hero-content` en &lt;768px (re-centra y mueve el título).
- Cambiar textos, Fraunces, overlay, 011/012 o `script.js`.
- Superponer el acordeón sobre Explorar servicios en solo ida.
- Fijar el título al viewport al scrollear la página.
