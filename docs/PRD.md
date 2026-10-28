# Boc Market — PRD

## Problema

Las bandas venden merch en sus conciertos con libretas, notas del móvil o de memoria. Al acabar el bolo no saben con certeza qué se ha vendido, cuánto stock queda por talla, con qué método se ha cobrado ni si el efectivo cuadra. En las salas a menudo no hay cobertura.

## Solución

App móvil gratuita (Android e iOS) para que una banda gestione su puesto de merch: catálogo con stock, venta rápida con cesta, ticket por QR, devoluciones y cierre de caja. Funciona 100 % en local, sin servidor ni conexión.

Creada por el grupo BOC. Cada banda instala la app y crea su propia tienda.

## Usuarios

- **Admin de la tienda**: miembro de la banda o persona que lleva la mesa de merch. Único rol; tiene acceso a todo.
- **Cliente del concierto**: no usa la app. Solo escanea el QR del ticket con su móvil.

## Decisiones de plataforma

- React Native + Expo + TypeScript, SQLite local.
- Un móvil = una tienda = una caja. Sin cuentas, sin login, sin servidor.
- Acceso protegido con PIN o biometría opcional.
- Idiomas: castellano, catalán e inglés (imprescindibles). Sigue el idioma del dispositivo, con selector en Ajustes.
- Modo oscuro por defecto (salas a oscuras), botones grandes; modo claro opcional.

## Requisitos funcionales

### Tienda

- Primer arranque: "Crear tu tienda" con nombre, logo y moneda (solo euro en la v1).
- Ajustes: mensaje opcional del ticket, descuentos predefinidos, PIN/biometría, idioma, tema.
- "Borrar tienda" con doble confirmación y sugerencia de hacer copia antes.

### Productos

- Alta con foto (cámara o galería), comprimida y guardada en el dispositivo. Una foto por producto.
- Precio final en euros, impuestos incluidos, sin desglose de IVA.
- Tallas opcionales elegidas de una lista estándar (XS–XXL) ampliable. Stock por talla, precio único por producto.
- Variantes solo por talla. Cada color es un producto distinto.
- Sin categorías. El catálogo se ordena a mano.
- Un producto con ventas no se borra, se archiva (desaparece de la venta, se mantiene en el historial).
- Aviso de stock bajo con umbral opcional por producto.

### Packs

- Producto especial compuesto por otros productos, con precio propio.
- No tiene stock propio: está disponible si lo están todos sus componentes.
- Al venderse descuenta stock de cada componente. Si un componente tiene tallas, se elige al añadir el pack a la cesta.

### Stock

- El stock nunca se edita directamente: todo cambio es un movimiento con motivo (venta, reposición, ajuste, regalo, defectuoso, devolución).
- Historial de movimientos por producto y talla.
- No se puede vender un producto o talla con stock 0.

### Caja

- Para vender hace falta una caja abierta, con nombre del evento, fecha y fondo inicial en efectivo.
- Solo una caja abierta a la vez.
- **Hacer caja**: arqueo del efectivo. Esperado = fondo + ventas en efectivo − reembolsos en efectivo, comparado con lo contado. Tarjeta y Bizum se muestran como totales informativos.
- Se puede cerrar con diferencia añadiendo una nota.
- Una caja cerrada es inmutable.
- Al cerrar se genera un resumen compartible (imagen o PDF): totales por método, unidades por producto y talla, descuentos, devoluciones y diferencia de arqueo.

### Venta

- Pantalla en cuadrícula de fotos. Tocar un producto lo añade a la cesta; si tiene tallas, aparece un selector con solo las tallas con stock.
- Cesta siempre visible con total y botón Cobrar.
- Descuentos predefinidos (p. ej. "Socio 10 %") y manuales, en % o €, por línea o sobre el total. Quedan registrados y desglosados en la caja.
- Un único método de pago por venta: efectivo, tarjeta o Bizum. Solo se registra; el cobro se hace por fuera.
- En efectivo, la app pide lo entregado y calcula el cambio.

### Ticket

- Al cobrar se muestra un QR que contiene el ticket codificado en la URL (tras el `#`) de una página estática pública (GitHub Pages). Funciona sin conexión del vendedor; no pasa por ningún servidor.
- La página muestra el ticket en el idioma del navegador del cliente.
- Contenido: nombre de la tienda, número de ticket correlativo (se conserva al migrar), fecha y hora, líneas (producto, talla, cantidad, precio), descuentos, total, método de pago, mensaje opcional y pie "Hecho con Boc Market · una app de BOC" con enlace a BOC.
- Sin logo (no cabe en el QR).
- Ticket informativo, no factura legal.

### Devoluciones

- Parten de una venta existente: desde el historial o escaneando el QR del ticket. Se eligen las líneas devueltas.
- **Reembolso**: el dinero sale por un método de pago y cuenta en la caja abierta en ese momento.
- **Cambio**: entra lo devuelto, sale lo nuevo y se cobra o devuelve la diferencia.
- Lo devuelto vuelve al stock vendible o se marca como defectuoso.
- Las ventas nunca se borran. Los errores de cobro se corrigen con una devolución.

### Copias y traspaso entre móviles

- Exportar la tienda completa (productos, fotos, stock, ventas, devoluciones, cajas) a un archivo, compartido con la hoja Compartir del sistema (AirDrop, Quick Share, WhatsApp, Drive, email…).
- Importar ese archivo sustituye la tienda del dispositivo, previa confirmación.
- Mismo mecanismo para copia de seguridad, cambio de móvil y migración.
- Aviso si hace más de X días que no se hace copia.
- Exportación de ventas a CSV.

### Sobre BOC

- Pantalla con foto del grupo, bio en los tres idiomas y enlaces a Spotify, Instagram y web. Contenido fijo dentro de la app.
- Bote de propinas con compra integrada (Apple/Google), solo cuando se publique en las tiendas.

## Requisitos no funcionales

- Funciona completamente offline.
- Venta rápida: pocos toques de producto a QR, con cola delante de la mesa.
- Todos los textos de interfaz traducibles desde el inicio.
- Integridad de datos: ventas, movimientos y cajas cerradas no se modifican ni se borran.

## Fuera de alcance (v1)

- Sincronización entre varios móviles (modelo principal + satélites queda como evolución).
- Pago mixto.
- Variantes talla × color.
- Categorías.
- Factura legal / Veri\*factu (consultar con la contabilidad de la banda).
- Integración con datáfono o pasarela de pago.
- Publicación en App Store y Play Store, y bote de propinas.

## Lanzamiento

1. **v1 interna**: BOC la usa en conciertos reales (APK / TestFlight).
2. **Publicación gratuita** en App Store y Play Store con bote de propinas. Antes, `/research` sobre las normas de aportaciones de Apple y Google.

## Criterios de éxito

- BOC usa la app en sus conciertos sin volver a la libreta.
- Al hacer caja, el efectivo cuadra o la diferencia queda explicada.
- El stock por talla de la app coincide con el recuento físico.
- Se puede pasar la tienda a otro móvil sin perder datos.
