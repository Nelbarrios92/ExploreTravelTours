# Quickstart: Buscador compacto en móvil

Contrato: [mobile-search.md](./contracts/mobile-search.md).

## Prerrequisitos

Servir la raíz. Viewports **375**, **768**, **1280**. Estado **componer** (no cotizado).

## Recorrido

1. **375** Transporte solo ida: anotar altura del card vs. antes. Panel **más bajo**; marca/foto del Hero más visibles. Origen, destino, fecha, hora, pasajeros y Pedir cotización **apilados** a ancho completo. **0** botón de intercambio entre origen y destino. Inputs ~44px; Pedir cotización ~50px.
2. Ida y vuelta 375: aparece fecha de regreso **en su propia fila**; sigue sin swap; 0 overflow-x.
3. Por horas 375: recogida y resto apilados; sin intercambio.
4. Pedir cotización válido: resumen **009**. **Modificar**: formulario compacto 010 otra vez, sin swap.
5. **768**: origen | intercambio | destino en fila; el botón **sí** se ve y al pulsarlo invierte valores.
6. **1280**: una fila ida-vuelta (006); intercambio funciona; campos ~50px.

## Esperado de negocio

Validaciones, WhatsApp y copy sin cambio.
