# Quickstart: Booking bar del Hero

Contrato: [booking-bar.md](./contracts/booking-bar.md).

## Prerrequisitos

Servir la raíz. Viewports 375, 768, 1280×800.

## Recorrido

1. Primer pantallazo: cotizador al pie; CTA naranja **Pedir cotización**; FAB **no** tapa el CTA (oculto o fuera).
2. Tabs Transporte / Por horas: mismo sistema visual; Por horas **sin** hueco vacío raro.
3. Solo ida ~1280: una fila origen–destino–fecha–hora–pasajeros–CTA.
4. Ida y vuelta ~1280: fila 1 origen, destino, fecha ida, fecha regreso; fila 2 hora, pasajeros, Pedir cotización. Fecha de regreso **no** está primero.
5. Swap origen/destino; placeholders reales; ≥5 sugerencias del datalist.
6. Pedir cotización válido: resumen **en el card** + Continuar por WhatsApp. Header **sin** “TU SOLICITUD”. El naranja no abre WhatsApp.
7. Origen = destino: aviso + Cambiar a Por horas.
8. Por horas: duración 1–12, sin solape de label; mismo CTA.
9. 375px: columna única, CTA full width, 0 overlap FAB, sin overflow-x.
10. Scroll al catálogo: el FAB puede reaparecer. Marca del Hero / catálogo / FAQ sin rediseño.

## Esperado de negocio

Mensajes de validación en español; `wa.me/573042143149`; sin precios.
