# Boc Market

App móvil de merch para bandas (stock, venta, ticket QR, caja). 100 % local, sin servidor. Expo + React Native + TypeScript + SQLite.

- Qué construimos y por qué: `docs/PRD.md`. Léelo antes de diseñar o implementar una funcionalidad.
- Vocabulario del dominio: `GLOSSARY.md`. Decisiones de arquitectura: `docs/adr/`.

## Idioma

- Código, identificadores y mensajes de commit en inglés.
- Todo texto visible en la interfaz pasa por i18n con sus tres traducciones (es, ca, en).
- Documentación en castellano.

## Dominio

Nombra el código con los términos de `GLOSSARY.md` (Shop, CashSession, Sale, Return, Pack, StockMovement…). Un concepto nuevo entra primero en el glosario, vía `/domain-modeling`, y después en el código.

## Invariantes

- El stock cambia solo creando un `StockMovement` con motivo; el stock actual se deriva de los movimientos.
- `Sale`, `StockMovement` y `CashSession` cerradas son append-only: se corrigen con nuevos registros (una `Return`, un ajuste), nunca editando o borrando.
- El dinero es un entero en céntimos de principio a fin.

## Arquitectura

La lógica de negocio (cesta, descuentos, packs, arqueo, devoluciones, codificación del ticket) vive en módulos de TypeScript puro, sin imports de React, Expo ni SQLite, detrás de interfaces profundas. Las pantallas y la capa de persistencia solo la invocan.

## Definición de terminado

Una tarea está terminada cuando typecheck, lint y tests están en verde. La lógica de negocio se construye con `/tdd`.

## Flujo

- Una rama por funcionalidad, commits pequeños.
- `/code-review` antes de abrir un PR; `/pr` para la descripción.
- Pide confirmación antes de: añadir una dependencia, hacer push o abrir un PR. Ante varias opciones de librería, prefiere el módulo oficial de Expo.
