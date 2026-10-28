# El Receipt va codificado dentro del QR

El QR del Receipt es la URL de una página estática pública con los datos del ticket codificados tras el `#`. Así el Receipt existe sin conexión ni servidor (ADR-0001), y el fragmento nunca llega a quien aloja la página. La página traduce los textos al idioma del navegador del cliente, por eso el QR lleva datos y no textos.

## Considered Options

- QR con un ID y Receipt publicado al sincronizar: el cliente vería "pendiente" en salas sin cobertura, y exige servidor.
- QR con texto plano: sin dependencias, pero ilegible para el cliente.

## Consequences

- El tamaño del Receipt está limitado por la capacidad del QR; el formato codificado debe ser compacto y versionado.
- Un Receipt no puede revocarse ni editarse una vez emitido. Es aceptable porque es informativo, no una factura.
