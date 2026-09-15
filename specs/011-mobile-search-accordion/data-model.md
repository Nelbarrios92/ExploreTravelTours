# Data Model: Acordeón del buscador

Sin entidades de negocio nuevas. Estado **presentacional** en `#hero-search`:

| Clase / flag | Significado |
|--------------|-------------|
| *(ninguna extra)* | Componer, acordeón **abierto** (o escritorio: cuerpo siempre visto) |
| `is-collapsed` | Componer, acordeón **cerrado** (solo &lt;768px tiene efecto visual) |
| `is-quoted` | Cotizado 007/009; cabecera y compositor ocultos |

Transiciones:

- Carga móvil → `is-collapsed`
- Toggle cabecera → entra/sale `is-collapsed` (form intacto)
- Pedir cotización OK → `is-quoted`, se quita el compositor de vista
- Modificar → sin `is-quoted`, **sin** `is-collapsed`

Campos y validación = 010/005. Sin storage.
