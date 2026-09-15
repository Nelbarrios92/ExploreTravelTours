# Contrato UI: acordeón del buscador

**011 manda** visibilidad del compositor en **&lt;768px** al componer. **010** densidad abierto. **007/009** `.is-quoted`. **006** ≥768.

## Cabecera (MUST)

- `button type="button"` (no submit). Texto **Pedir cotización** en abierto y cerrado.
- `aria-expanded` refleja el estado. Señal visual (chevron) además del texto.
- Visible solo si **no** `.is-quoted` y viewport **&lt;768px**.
- MUST NOT parecer el CTA naranja; MUST NOT enviar el formulario.

## Cuerpo (MUST)

- Wrapper con tabs, paneles, errores y aviso origen=destino.
- &lt;768px + `is-collapsed` + no cotizado: cuerpo **no visible**.
- ≥768px: cuerpo **siempre visible** (cabecera oculta).
- Abierto: reglas 010.

## JS (MUST)

- Carga: `is-collapsed`, `aria-expanded="false"`.
- Click cabecera: toggle `is-collapsed` / `aria-expanded`.
- `hideQuote`: quitar `is-collapsed`.
- MUST NOT `localStorage` / `sessionStorage`.

## MUST NOT

- Cabecera sobre el resumen 009.
- Dos acordeones (Transporte / Por horas).
- Cambiar copy a “Cerrar”.
