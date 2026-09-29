# Quickstart: Solo el resumen tras cotizar

Contrato: [quote-view.md](./contracts/quote-view.md).

## Prerrequisitos

Servir la raíz. Viewports 375 y 1280.

## Recorrido

1. Completar Transporte válido → **Pedir cotización**. El card muestra el resumen y **0** tabs/campos/Pedir cotización. Header sin “TU SOLICITUD”. El naranja no abrió WhatsApp.
2. **Continuar por WhatsApp** apunta a `wa.me/573042143149` con el mensaje.
3. **Modificar**: reaparecen tabs y campos con los mismos valores; el resumen desaparece.
4. Volver a Pedir cotización válido: otra vez solo el resumen.
5. Por horas: mismo patrón (éxito = solo resumen).
6. Origen = destino (o fecha inválida): buscador visible, aviso, **sin** resumen de éxito.
7. 375px: resumen usable; FAB no tapa Continuar por WhatsApp / Modificar.

## Esperado de negocio

Sin precios; layout 006 al componer Ida y vuelta.
