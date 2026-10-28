# Boc Market

App móvil gratuita (Android e iOS) para que una banda gestione su puesto de merch en los conciertos: catálogo con stock por talla, venta rápida, ticket por QR, devoluciones y cierre de caja.

Funciona 100 % en el móvil: sin servidor, sin cuentas y sin necesidad de cobertura. La ha creado el grupo **BOC**.

> **Estado:** en desarrollo. Ya están definidos el producto y el dominio y montada la base técnica. La lógica de negocio y las pantallas están en construcción.

## Qué hace

- **Tienda**: cada móvil contiene una tienda, con nombre, logo, PIN o biometría opcional e idioma (castellano, catalán, inglés).
- **Productos y packs**: con foto, precio final y stock por talla o directo. Los packs agrupan productos con un precio propio.
- **Stock**: nunca se edita a mano. Cada cambio es un movimiento con motivo (venta, reposición, ajuste, regalo, defectuoso, devolución).
- **Caja**: se abre con el evento y el fondo inicial. El arqueo del efectivo compara lo esperado con lo contado y se genera un resumen al cerrar.
- **Venta**: cuadrícula de fotos, cesta y descuentos. Se registra el método de pago (efectivo, tarjeta o Bizum) y la app calcula el cambio.
- **Ticket QR**: el ticket va codificado en la URL de una página estática y el cliente lo ve en su móvil sin que pase por ningún servidor.
- **Devoluciones y cambios**: parten de una venta existente, desde el historial o escaneando el QR del ticket.
- **Copias**: se exporta e importa la tienda completa en un archivo para hacer backups o cambiar de móvil. Las ventas se pueden exportar a CSV.

## Stack

- [Expo](https://expo.dev) SDK 58 + React Native + TypeScript
- Expo Router para la navegación (`src/app/`)
- SQLite local para la persistencia
- Jest (`jest-expo`) y ESLint

## Requisitos

- Node.js 24 o superior y npm
- [Expo Go](https://expo.dev/go) en el móvil, o un emulador de Android o un simulador de iOS

## Puesta en marcha

```bash
npm install
npm start          # arranca el servidor de desarrollo de Expo
```

Escanea el QR de la terminal con Expo Go, o pulsa `a` (Android), `i` (iOS) o `w` (web).

Si se añade un módulo con código nativo que no incluye Expo Go, hace falta una development build:

```bash
npx expo run:android   # o run:ios
```

Las carpetas `android/` e `ios/` se generan automáticamente y no se editan a mano.

## Scripts

| Comando             | Qué hace                                 |
| ------------------- | ---------------------------------------- |
| `npm start`         | Servidor de desarrollo de Expo           |
| `npm run android`   | Abre la app en Android                   |
| `npm run ios`       | Abre la app en iOS                       |
| `npm run web`       | Abre la app en el navegador              |
| `npm run typecheck` | Comprobación de tipos con TypeScript     |
| `npm run lint`      | Lint con ESLint                          |
| `npm test`          | Tests con Jest                           |
| `npm run check`     | Typecheck, lint y tests (debe pasar en verde) |

Para añadir dependencias usa siempre `npx expo install <paquete>`, que elige versiones compatibles con el SDK.

## Estructura

```
src/app/        Pantallas y navegación (Expo Router)
docs/PRD.md     Qué construimos y por qué
docs/adr/       Decisiones de arquitectura
GLOSSARY.md     Vocabulario del dominio
assets/         Iconos e imágenes
```

## Principios de diseño

- **La lógica de negocio va en TypeScript puro.** La cesta, los descuentos, los packs, el arqueo, las devoluciones y la codificación del ticket no importan React, Expo ni SQLite. Las pantallas y la persistencia solo la invocan.
- **El stock se deriva de los movimientos.** Ventas, movimientos de stock y cajas cerradas son append-only y se corrigen con registros nuevos, nunca editando ni borrando.
- **El dinero es siempre un entero en céntimos.**
- **Todo texto visible pasa por i18n**, en castellano, catalán e inglés.

## Contribuir

- Una rama por funcionalidad, con commits pequeños en inglés.
- El código usa los términos de [`GLOSSARY.md`](GLOSSARY.md).
- La lógica de negocio se desarrolla con TDD.
- Una tarea está terminada cuando `npm run check` pasa en verde.
