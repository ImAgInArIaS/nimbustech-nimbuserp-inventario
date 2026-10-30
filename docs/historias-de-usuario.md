# Historias de Usuario — Módulo de Gestión de Inventario y Stock

Las historias se derivan de los usuarios, pantallas e indicadores del módulo (Entrega N.º 2) y de las reglas de integridad del Diccionario de Datos (Entrega N.º 3).

## HU-01 — Registrar movimientos de stock

**Como** encargado de depósito, **quiero** registrar ingresos, egresos, ajustes y devoluciones de mercadería con validación automática, **para** mantener el stock de cada depósito exacto y con trazabilidad de quién hizo cada movimiento.

Criterios de aceptación:

- La cantidad debe ser mayor que cero en INGRESO y EGRESO.
- Un EGRESO no puede superar el stock disponible, salvo configuración explícita.
- `stock_resultante` se calcula automáticamente y no puede editarse.
- Todo movimiento queda asociado a un usuario (`id_usuario` no nulo) y a un depósito activo.
- Si el movimiento no es válido, el sistema lo rechaza y muestra el motivo.

## HU-02 — Recibir alertas de reposición con orden de compra sugerida

**Como** responsable de compras, **quiero** recibir una alerta cuando un producto llega a su stock mínimo, junto con una orden de compra sugerida al proveedor, **para** reponer a tiempo y evitar quiebres de stock.

Criterios de aceptación:

- La alerta se genera cuando `stock_resultante` es menor o igual a `stock_minimo`.
- La orden sugerida usa `punto_reposicion` como cantidad y el proveedor asociado al producto.
- Si el proveedor está inactivo, no se genera orden automática y se avisa para asignar otro.
- La alerta muestra el `tiempo_entrega_dias` del proveedor para estimar la reposición.

## HU-03 — Consultar indicadores de inventario

**Como** gerente de la PyME, **quiero** ver el stock valorizado y el índice de rotación por categoría, **para** decidir qué comprar y detectar inmovilizado.

Criterios de aceptación:

- El stock valorizado se calcula con `precio_costo` y el stock actual de cada producto.
- El índice de rotación se calcula por categoría y por período seleccionable.
- Los valores pueden filtrarse por depósito.
- Los indicadores se actualizan con cada movimiento registrado.
