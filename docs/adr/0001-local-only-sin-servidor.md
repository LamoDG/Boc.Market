# La app es 100 % local, sin servidor

Cada dispositivo contiene una única Shop en SQLite y no hay backend, cuentas ni sincronización. Los conciertos suelen no tener cobertura, la app es gratuita y no queremos costes ni datos personales que custodiar. Elegido frente a un backend con sincronización.

## Consequences

- Varios dispositivos vendiendo a la vez no están soportados; cada uno sería una Shop independiente.
- La única vía para copias de seguridad y para traspasar una Shop entre móviles es el Backup en archivo compartido con la hoja Compartir del sistema.
- Si se pierde el dispositivo sin Backup, se pierde la Shop.
