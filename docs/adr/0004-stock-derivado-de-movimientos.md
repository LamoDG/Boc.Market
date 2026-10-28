# El Stock se deriva de Stock Movements append-only

El Stock no se guarda como un número editable: es la suma de Stock Movements, cada uno con su motivo. Sales, Stock Movements y Cash Sessions cerradas nunca se modifican ni se borran; los errores se corrigen con registros nuevos (un Return, un ajuste). Así cualquier cifra de stock o de caja es explicable y el Cash Count de una Cash Session cerrada no puede cambiar a posteriori. Elegido frente a un campo de cantidad editable, más simple pero sin historial.
