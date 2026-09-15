# Quickstart: Consistencia del buscador

Validación manual. Contrato: [search-layout.md](./contracts/search-layout.md). Lógica: spec 001 (cotización / WhatsApp).

## Prerrequisitos

Servir la raíz del repo. Escritorio ~1280×800 y móvil ~375px.

## Recorrido UX

1. Primer pantallazo: buscador al pie, foto y marca visibles.
2. Tabs: mismo tamaño; activo azul oscuro; inactivo gris neutro. Alternar 5 veces: la franja bajo tabs **no salta**; campos misma altura; CTA no pasa a barra full-width solo por el tab.
3. Transporte Solo ida: fila Origen–Destino–Fecha–Hora–Pasajeros–Buscar (1280). Labels arriba, no flotantes.
4. Ida y vuelta: aparece Fecha de regreso (segunda fila); CTA sigue en la primera fila a la derecha.
5. Por horas: Lugar de recogida, Duración (etiqueta + “Selecciona” sin solape), Fecha, Hora, Pasajeros, Buscar. Opciones 1–12 h.
6. Submit válido en ambos modos: `#quote-summary` + Continuar por WhatsApp (verde). Buscar sigue naranja.
7. Origen = destino: no cotiza; “Cambiar a Por horas” funciona; Por horas usa el mismo look.
8. 768 y 375: sin overflow-x; tabs en una fila; campos apilados en 375; CTA full width al final; touch cómodo.
9. Navbar, Hero marca, catálogo: sin rediseño.

## Esperado (negocio)

Validaciones y mensajes en español iguales en significado. Sin pago en el sitio.

## Fuera

Cambiar catálogo, FAQ, o el copy del H1.
