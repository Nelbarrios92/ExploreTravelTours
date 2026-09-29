# Quickstart: Ida y vuelta en una sola fila

Contrato: [round-trip-row.md](./contracts/round-trip-row.md).

## Prerrequisitos

Servir la raíz. Viewports 375, 768, **1280×800**.

## Recorrido

1. Transporte, Solo ida, ~1280: una fila (origen … CTA). Anotar que el CTA no baja.
2. Activar **Ida y vuelta**: aparece fecha de regreso **en esa misma fila**, a la derecha de fecha de ida; hora, pasajeros y Pedir cotización **no** bajan a una segunda banda.
3. Recorrer izquierda→derecha: origen, swap, destino, ida, regreso, hora, pasajeros, Pedir cotización. Labels legibles; sin scroll horizontal del panel.
4. Volver a Solo ida: desaparece regreso; sigue una fila (sin hueco de segunda banda).
5. ~375px e Ida y vuelta: campos apilados, CTA usable, **sin** overflow-x.
6. ~768px: reflujo en varias filas **aceptable**; no es el criterio de fallo de 1280.
7. Pedir cotización válido: resumen inline + WhatsApp igual que 005 (regresión).

## Esperado de negocio

Sin precios; `wa.me/573042143149` sin cambio.
