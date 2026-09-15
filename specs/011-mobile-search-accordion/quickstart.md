# Quickstart: Acordeón del buscador

Contrato: [accordion.md](./contracts/accordion.md).

## Prerrequisitos

Servir la raíz. **375**, **768**, **1280**.

## Recorrido

1. **375** al cargar: pie = franja **Pedir cotización** + chevron; **no** se ven tabs ni campos. Hero (marca/foto) más libre que 010 abierto.
2. Pulsar la franja: se abre el buscador 010 **debajo**; la franja sigue diciendo Pedir cotización; `aria-expanded="true"`. El naranja no se ha enviado.
3. Pulsar la franja otra vez: se cierra; al reabrir, origen/destino u otros valores **siguen**.
4. Abrir, enviar vacío o origen=destino: panel **sigue abierto** y el aviso se lee.
5. Envío válido: resumen **009**; **sin** franja de acordeón. **Modificar**: formulario **abierto** (010).
6. **768 / 1280**: sin franja de acordeón; buscador siempre visible; 1280 ida-vuelta una fila; swap visible.

## Esperado de negocio

WhatsApp y validaciones sin cambio. FAB verde no sustituye la franja.
