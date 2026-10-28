# Boc Market

Puesto de merch de una banda: catálogo, stock, venta en conciertos y cierre de caja. Los términos canónicos están en inglés (son los del código); entre paréntesis, el nombre en la interfaz en castellano.

## Tienda

**Shop** (Tienda):
El puesto de merch de una banda, con su catálogo, su stock y su historial. Un dispositivo contiene exactamente una Shop.
_Avoid_: Store, Market, Band, Account

**Backup** (Copia):
Archivo que contiene una Shop completa y permite restaurarla o trasladarla a otro dispositivo.
_Avoid_: Export, Sync, Dump

## Catálogo

**Product** (Producto):
Artículo de merch que la banda vende, con foto y precio propio. Al darlo de alta se decide si tiene Sizes: si las tiene, su Stock se lleva por Size; si no, directamente en el Product.
_Avoid_: Item, Article, Merch

**Size** (Talla):
Talla en la que se ofrece un Product con tallas.
_Avoid_: Variant, Option

**Pack** (Pack):
Conjunto de Products que se vende junto a un precio propio, sin stock propio.
_Avoid_: Bundle, Combo, Kit

**Archived Product** (Producto archivado):
Product retirado de la venta que se conserva por tener historial.
_Avoid_: Deleted product, Inactive product

## Stock

**Stock** (Stock):
Unidades disponibles de un Product, o de una Size de un Product. Siempre es el resultado de sus Stock Movements.
_Avoid_: Inventory, Quantity

**Stock Movement** (Movimiento de stock):
Cambio en el Stock con un motivo: venta, reposición, ajuste, regalo, defectuoso o devolución.
_Avoid_: Stock update, Adjustment (como término general)

**Restock** (Reposición):
Stock Movement que añade unidades nuevas recibidas.
_Avoid_: Purchase, Entry

**Defective** (Defectuoso):
Motivo de un Stock Movement que retira unidades no vendibles.
_Avoid_: Damaged, Broken, Waste

## Caja

**Cash Session** (Caja):
Periodo de venta asociado a un concierto, desde que se abre con un Float hasta que se cierra con un Cash Count. Una vez cerrada es inmutable.
_Avoid_: Register, Shift, Event, Till

**Float** (Fondo de caja):
Efectivo con el que se abre una Cash Session para dar cambio.
_Avoid_: Initial cash, Opening balance

**Cash Count** (Arqueo):
Comparación entre el efectivo esperado y el contado al cerrar una Cash Session.
_Avoid_: Reconciliation, Closing

**Cash Discrepancy** (Descuadre):
Diferencia entre el efectivo esperado y el contado en un Cash Count.
_Avoid_: Error, Mismatch

## Venta

**Cart** (Cesta):
Selección de Products y Packs en curso, antes de cobrar.
_Avoid_: Basket, Order

**Sale** (Venta):
Venta cobrada dentro de una Cash Session con un único Payment Method. Nunca se modifica ni se borra.
_Avoid_: Order, Transaction, Purchase

**Sale Line** (Línea):
Product o Pack, con su Size si aplica y su cantidad, dentro de un Cart o una Sale.
_Avoid_: Item, Row

**Payment Method** (Método de pago):
Forma en que el cliente paga: efectivo, tarjeta o Bizum. Se registra, no se procesa.
_Avoid_: Payment type, Tender

**Change** (Cambio):
Efectivo devuelto al cliente cuando entrega más del total.
_Avoid_: Vuelta (en código)

**Discount** (Descuento):
Rebaja en % o en € sobre una Sale Line o sobre el total de un Cart.
_Avoid_: Promotion, Offer, Coupon

**Preset Discount** (Descuento predefinido):
Discount con nombre configurado en la Shop, como "Socio 10 %".
_Avoid_: Discount code, Rule

**Receipt** (Ticket):
Justificante informativo de una Sale que el cliente recibe a través de un QR. No es una factura.
_Avoid_: Invoice, Factura, Bill

**Receipt Number** (Número de ticket):
Número correlativo de una Sale dentro de su Shop.
_Avoid_: Sale ID, Invoice number

## Devoluciones

**Return** (Devolución):
Operación que deshace total o parcialmente una Sale anterior, en forma de Refund o de Exchange.
_Avoid_: Cancellation, Void, Anulación

**Refund** (Reembolso):
Return en la que el dinero vuelve al cliente.
_Avoid_: Chargeback, Reversal

**Exchange** (Cambio de producto):
Return en la que el cliente se lleva otros Products a cambio, pagando o recibiendo la diferencia.
_Avoid_: Swap, Change (reservado para el efectivo devuelto)

## BOC

**Tip** (Propina):
Aportación voluntaria de un usuario de la app al grupo BOC.
_Avoid_: Donation, Contribution
