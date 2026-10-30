# Indicadores de control y estándares de desempeño

Los estándares son **propuestos** para la etapa piloto y deben calibrarse con datos reales de los primeros meses de uso.

## Indicadores de gestión

| Indicador | Fórmula | Estándar propuesto | Frecuencia | Fuente |
|---|---|---|---|---|
| Exactitud de inventario | (ítems con stock físico = stock del sistema ÷ ítems contados) × 100 | ≥ 98 % | Mensual | AJUSTE en MOVIMIENTO_STOCK |
| Tasa de quiebres | productos con stock 0 y demanda ÷ productos activos × 100 | ≤ 2 % | Semanal | PRODUCTO, MOVIMIENTO_STOCK |
| Índice de rotación | costo de los egresos del período ÷ stock promedio valorizado | ≥ 6 por año (referencia a calibrar) | Mensual | PRODUCTO, MOVIMIENTO_STOCK |
| Cumplimiento de reposición | órdenes recibidas dentro de `tiempo_entrega_dias` ÷ órdenes emitidas × 100 | ≥ 90 % | Mensual | PROVEEDOR, MOVIMIENTO_STOCK |
| Atención de alertas | alertas con orden aprobada en 24 h hábiles ÷ alertas generadas × 100 | ≥ 95 % | Semanal | Panel de alertas |
| Rechazo por validación | movimientos rechazados ÷ movimientos intentados × 100 | ≤ 5 % (si sube, revisar capacitación o datos) | Mensual | Registro de validaciones |

## Estándares técnicos de desempeño

| Característica | Estándar |
|---|---|
| Tiempo de respuesta al registrar un movimiento | ≤ 2 s en el percentil 95 |
| Disponibilidad mensual del módulo | ≥ 99,5 % |
| Movimientos sin usuario (`id_usuario` nulo) | 0 |
| Movimientos con `id_usuario` inexistente en USUARIO | 0 |
| Stock negativo sin configuración explícita | 0 casos |
| Proveedores inactivos con órdenes automáticas | 0 casos |

## Consultas de auditoría técnica

```sql
-- Movimientos sin usuario responsable (debe devolver 0 filas)
SELECT id_movimiento
FROM movimiento_stock
WHERE id_usuario IS NULL;

-- Productos con stock negativo (debe devolver 0 filas salvo configuración explícita)
SELECT id_producto, id_deposito, stock_resultante
FROM movimiento_stock m
WHERE stock_resultante < 0;

-- Movimientos con usuario inexistente (integridad referencial)
SELECT m.id_movimiento FROM movimiento_stock m
LEFT JOIN usuario u ON u.id_usuario = m.id_usuario WHERE u.id_usuario IS NULL;
```
