/># SQL-Normalizacion-Ecomercce
Normalizacion y Estructura Relacional SQL
# Proyecto: Normalización de Base de Datos E-commerce 🛒
**Institución:** Cesde - Nivel 1
**Herramientas:** Excel, SQL Server Management Studio (SSMS)

## 📋 Descripción
Este proyecto demuestra la transformación de una estructura de datos plana (Excel) hacia un modelo relacional normalizado en SQL Server. Se aplicaron las primeras tres formas normales (1FN, 2FN, 3FN) para garantizar la integridad de la información y eliminar la redundancia.

## 📉 El Problema Inicial (Excel)
Originalmente, la información se encontraba en una tabla plana con los siguientes problemas:
<img width="715" height="86" alt="image" src="https://github.com/user-attachments/assets/52834a7a-7822-48ee-8145-c6fd21d7d121" />
* **Grupos repetitivos:** Columnas como `Producto1`, `Producto2`, `Precio1`, `Precio2` que limitaban la cantidad de artículos por pedido.
* **Redundancia:** Repetición innecesaria de nombres de ciudades y clientes en cada fila.
* **Riesgo de inconsistencia:** Si un cliente cambiaba de ciudad, había que actualizarlo en múltiples filas.

## 🏗️ Solución y Normalización
Se crearon 5 tablas relacionadas para separar las entidades del negocio:

1. **Ciudades:** Catálogo de ubicaciones.
2. **Clientes:** Información de usuarios vinculada a una ciudad.
3. **Productos:** Catálogo de artículos y precios base.
4. **Pedidos:** Registro de la transacción (quién compró y cuándo).
5. **DetallePedidos:** Relación de muchos a muchos que permite múltiples productos en un mismo pedido.

### 📐 Diagrama Entidad-Relación (DER)
![Diagrama de Base de Datos]
<img width="674" height="421" alt="image" src="https://github.com/user-attachments/assets/86f9af05-3f44-43fc-89b6-9c50ff6fdc07" />
) 

## 🚀 Consultas Principales
Se implementaron consultas con **JOINs** para reconstruir la información y generar reportes de ventas:

```sql
SELECT 
    P.PedidoID,
    C.Nombre AS Cliente,
    Ci.Nombre AS Ciudad,
    Pr.Nombre AS Producto,
    DP.Precio AS PrecioVenta,
    P.Fecha
FROM Pedidos P
JOIN Clientes C ON P.ClienteID = C.ClienteID
JOIN Ciudades Ci ON C.CiudadID = Ci.CiudadID
JOIN DetallePedidos DP ON P.PedidoID = DP.PedidoID
JOIN Productos Pr ON DP.ProductoID = Pr.ProductoID;
