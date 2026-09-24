# RetailOps — Requerimientos del Proyecto

## 1. Contexto

RetailOps simula el backend de una cadena ficticia de minimarkets con múltiples sucursales.

El sistema debe mantener consistencia entre ventas, inventario y movimientos de stock.

## 2. Problema principal

Actualmente existen riesgos de inconsistencias entre las ventas registradas y el inventario disponible en cada sucursal.

El sistema debe evitar que:

- se vendan productos sin stock suficiente;
- una venta quede registrada sin descontar inventario;
- el inventario cambie sin dejar trazabilidad;
- usuarios sin permisos modifiquen información sensible;
- existan registros duplicados de inventario para un mismo producto y sucursal.

## 3. Actores del sistema

### ADMIN

Puede administrar:

- productos;
- categorías;
- sucursales;
- usuarios;
- inventario;
- reportes.

### MANAGER

Puede:

- consultar inventario;
- registrar ajustes;
- consultar ventas;
- consultar reportes.

### CASHIER

Puede:

- consultar productos disponibles;
- registrar ventas;
- consultar sus operaciones permitidas.

## 4. Reglas de negocio iniciales

- Cada sucursal mantiene su propio inventario.
- Un producto puede existir en múltiples sucursales.
- No debe existir más de un inventario para la misma combinación producto-sucursal.
- No se puede vender una cantidad superior al stock disponible.
- Todo cambio de inventario debe generar un movimiento.
- Toda venta debe completarse completamente o revertirse.
- El precio utilizado en una venta debe conservarse históricamente.
- Los productos y sucursales podrán desactivarse sin eliminar su historial.
- Las operaciones sensibles deberán identificar al usuario responsable.

## 5. Entidades iniciales

- Product
- Category
- Branch
- Inventory
- InventoryMovement
- Sale
- SaleDetail
- User

## 6. Objetivo técnico

Construir una API REST con Java y Spring Boot que garantice:

- consistencia de datos;
- seguridad;
- trazabilidad;
- manejo adecuado de errores;
- pruebas automatizadas;
- documentación;
- despliegue reproducible.
