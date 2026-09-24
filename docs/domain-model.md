# RetailOps — Modelo de Dominio

## 1. Objetivo

Definir el modelo de dominio inicial de RetailOps antes de comenzar la implementación con Spring Boot, JPA y PostgreSQL.

El modelo representa productos, categorías, sucursales, inventario, movimientos de inventario, ventas, detalles de venta y usuarios.

---

## 2. Entidades

### Producto

Representa un producto comercializado por la empresa.

**Atributos:**

- `id`: Long
- `sku`: String
- `nombre`: String
- `descripcion`: String
- `precio`: BigDecimal
- `activo`: Boolean
- `fechaCreacion`: LocalDateTime
- `fechaActualizacion`: LocalDateTime

**Reglas de negocio:**

- El SKU debe ser obligatorio y único.
- El nombre es obligatorio.
- El precio debe ser mayor que cero.
- El producto no almacena directamente el stock.
- Un producto puede desactivarse sin eliminar su historial.

**Relaciones:**

- Muchos productos pertenecen a una categoría.
- Un producto puede existir en varios inventarios.
- Un producto puede aparecer en muchos detalles de venta.

---

### Categoría

Representa la clasificación de un producto.

**Atributos:**

- `id`: Long
- `nombre`: String
- `descripcion`: String
- `activo`: Boolean
- `fechaCreacion`: LocalDateTime

**Reglas de negocio:**

- El nombre es obligatorio.
- El nombre debe ser único.
- Una categoría puede desactivarse sin eliminar los productos históricos.

**Relaciones:**

- Una categoría puede tener muchos productos.
- Cada producto pertenece a una categoría.

---

### Sucursal

Representa una sede física de la cadena de minimarkets.

**Atributos:**

- `id`: Long
- `codigo`: String
- `nombre`: String
- `direccion`: String
- `activo`: Boolean
- `fechaCreacion`: LocalDateTime
- `fechaActualizacion`: LocalDateTime

**Reglas de negocio:**

- El código debe ser obligatorio y único.
- La sucursal puede desactivarse.
- No debe eliminarse físicamente si posee información histórica.

**Relaciones:**

- Una sucursal puede tener muchos registros de inventario.
- Una sucursal puede registrar muchas ventas.
- Una sucursal puede tener varios usuarios asignados.

---

### Inventario

Representa el stock disponible de un producto dentro de una sucursal específica.

**Atributos:**

- `id`: Long
- `producto`: Product
- `sucursal`: Branch
- `cantidad`: Integer
- `fechaActualizacion`: LocalDateTime

**Reglas de negocio:**

- La cantidad no puede ser negativa.
- No puede existir más de un registro de inventario para el mismo producto y sucursal.
- El stock pertenece a la combinación producto-sucursal.

**Restricción importante:**

```text
UNIQUE(producto_id, sucursal_id)
