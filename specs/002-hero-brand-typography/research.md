# Research: Identidad tipográfica del Hero

## 1. Cara de display para el identificador

**Decision**: Fraunces (Google Fonts), pesos 400–600, `display=swap`, token CSS `--font-display: 'Fraunces', serif`. Uso exclusivo de `.hero-brand`.

**Rationale**: Serif óptica contemporánea (no caligráfica ni “wedding”). Contrasta con Montserrat (H1/UI) y evita Playfair en el nombre (riesgo ornamental citado en la spec). Encaja con turismo premium / Cartagena sin cliché de agencia. Se carga igual que las fuentes actuales: un `<link>` de Google Fonts, sin npm.

**Alternatives considered**:

- Playfair Display en el identificador — rechazada (clarificación A vs B; estética clásica/bodas).
- Instrument Serif — válida y más “tech”; menos calor caribeño.
- Syne / sans display — más movilidad, menos editorial.
- Self-host WOFF — más control, añade archivos y no está en el modelo actual.

## 2. Jerarquía H1 vs marca (tamaño y rol)

**Decision**: El H1 usa Montserrat (`--font-sans`) con `clamp` **mayor** que `.hero-brand`. El identificador es considerable (`clamp` intermedio, ~45–70% del cuerpo óptico del H1 en desktop) pero peso/contraste/leading dejan al H1 como dominante. El nombre deja de ser el `h1`; pasa a `<p class="hero-brand">` (o equivalente no-heading).

**Rationale**: Hoy `.hero-title` es el nombre a `clamp(2.5rem, 8vw, 6.5rem)`. Mover ese máximo al mensaje y bajar el nombre evita “arreglarlo agrandándolo”. Semántica alineada a clarificación A y SEO (título de pestaña + JSON-LD siguen con la agencia).

**Alternatives considered**:

- Nombre como `h1` visualmente pequeño — contradice a11y y SC-004.
- Dos headings — dos titulares principales, prohibido en spec.

## 3. Composición de tres líneas del H1

**Decision**: Tres fragmentos en markup (`<span class="hero-title-line">` o `<br class="hero-title-break">`). En `min-width: 1024px` cada fragmento es línea; bajo 1024px los saltos forzados se anulan y el H1 refluye al ancho.

**Rationale**: FR-004 pide ~tres líneas en desktop; FR-014 prohíbe forzarlas en móvil. `clamp` + breaks condicionales evitan magia de una sola resolución.

**Alternatives considered**:

- `max-width` solo — el wrap no garantiza las tres frases.
- Saltos `<br>` fijos — dañan móvil.

## 4. Separación marca–H1

**Decision**: Espacio vertical rítmico (`margin` en `rem`/`clamp`) más una regla de 1px, ancho acotado al identificador o ligeramente menor, blanco a ~0.55–0.75 de opacidad, sin degradado.

**Rationale**: El brief muestra una línea editorial; FR-005 permite divisor sobrio si no es protagonista.

**Alternatives considered**: Solo aire (más débil vs mock). Ornamento o doble línea (sobrecarga).

## 5. Copy del subtítulo y CTA

**Decision**: Subtítulo: *“Transporte privado y vehículos premium para moverte por Cartagena con confianza.”* CTA visible: *“Explorar servicios”* (`href="#experiences"` se conserva).

**Rationale**: Línea de movilidad (clarificación B); no destinos/precios/flota nuevos; tono constitucional (cercano, sin anglicismos). El CTA publicado “Ver Servicios” se alinea a FR-016.

**Alternatives considered**: Conservar el párrafo de “maravillas del Caribe” — rechazado. Quitar subtítulo — rechazado (opción C).

## 6. Contraste sobre la fotografía

**Decision**: Conservar `.hero-overlay` y `text-shadow` del bloque izquierdo. Ajustar overlay **solo** si el texto nuevo pierde contraste; no rediseñar la foto ni los swoosh.

**Rationale**: Constitución (calidad) y FR-013. Los adornos quedan fuera de alcance.

**Alternatives considered**: Quitar overlay (rompe legibilidad). Overlay más pesado global (apaga el vehículo).

## 7. Carga de fuentes

**Decision**: Ampliar el `href` de Google Fonts existente; `display=swap`. Fallback `serif` en `.hero-brand`. Sin JS de font-loading.

**Rationale**: Principio V; el Hero sigue legible si Fraunces tarda.

**Alternatives considered**: `@font-face` local — archivos extra. Librería de webfonts — dependencia innecesaria.
