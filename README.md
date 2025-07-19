# bd_e_commerce: caso BD transaccional

📦 Caso  Base de Datos Transaccional
Proyecto: Sistema de Gestión de Pedidos para E-commerce – ComercioFácil S.A.

🧭 Contexto del Negocio
ComercioFácil S.A. es una empresa de e-commerce con sede en Argentina, especializada en la venta de productos tecnológicos, electrodomésticos y artículos para el hogar. Sus operaciones se realizan tanto en canales propios (sitio web institucional y WhatsApp Business) como en plataformas externas como Mercado Libre, Facebook Marketplace y otras.

En los últimos años, el negocio ha experimentado un crecimiento sostenido en volumen de ventas, diversidad de productos y alcance geográfico. Esta expansión trajo consigo una complejidad operativa creciente: mayor necesidad de trazabilidad de pedidos, control de stock en tiempo real, análisis de canales de venta, y automatización del seguimiento logístico.

Frente a este escenario, la empresa identificó como necesidad crítica el diseño e implementación de una base de datos transaccional robusta y escalable, que permita registrar y gestionar las operaciones comerciales de punta a punta de forma estructurada.

🎯 Objetivo del Sistema
El objetivo principal es diseñar una base de datos relacional transaccional que cumpla los siguientes propósitos:

Registrar las órdenes de compra realizadas por clientes.

Asociar múltiples productos a cada orden (modelo relacional N:N).

Gestionar información de productos, incluyendo precio actual y stock disponible.

Registrar los métodos de pago utilizados por los clientes.

Identificar el canal de venta en el que se concretó cada transacción.

Controlar y actualizar el estado de los envíos asociados a cada pedido.

Mantener coherencia entre stock y ventas confirmadas.

Servir como base estructural para el desarrollo futuro de soluciones de inteligencia de negocios (BI).

📦 Procesos Cubiertos por el Modelo
Registro y gestión de clientes: alta de nuevos usuarios con datos personales, zona y canal de contacto.

Gestión del catálogo de productos: carga de productos, precios, stock actual y atributos básicos.

Operación de órdenes de compra: creación de pedidos con múltiples productos, método de pago y canal de origen.

Gestión logística básica: seguimiento del estado de envío por pedido (pendiente, en camino, entregado, cancelado).

Control transaccional de stock: ajuste automático de unidades disponibles al confirmar una orden.

🧱 Entidades del Modelo
Entidad	Descripción
Cliente	Información básica de clientes: nombre, zona, contacto y fecha de alta.
Producto	Catálogo activo: nombre, descripción, categoría, precio unitario y stock.
Orden	Encabezado de cada compra: fecha, cliente, método de pago, canal de venta.
DetalleOrden	Asociación producto–orden: cantidad, precio aplicado, total línea.
MetodoPago	Tipos de pago: tarjeta, efectivo, transferencia, etc.
CanalVenta	Canales de origen del pedido: Web, WhatsApp, Mercado Libre, etc.
Envio	Estado del pedido: transportista, estado actual, fecha estimada entrega.

🔁 Relaciones del Modelo
Un cliente puede realizar múltiples órdenes.

Una orden puede tener múltiples productos (N:N resuelto con DetalleOrden).

Cada producto puede aparecer en muchas órdenes.

Cada orden se paga con un solo método de pago y se origina en un canal de venta.

Cada orden tiene un único envío asociado.

📌 Reglas de Negocio
El stock de un producto se actualiza solo al confirmar una orden.

El precio aplicado a cada producto en una orden se congela en el momento de la compra.

El estado del envío sigue un flujo lógico: Pendiente → En preparación → En camino → Entregado / Cancelado.

Cada orden debe tener al menos un producto.

🔍 Consultas Representativas
¿Cuáles fueron los productos más vendidos en el último trimestre?

¿Qué canal de venta generó mayor facturación el mes pasado?

¿Qué clientes realizaron más de 3 compras en el año?

¿Qué órdenes están aún pendientes de envío?

¿Qué productos tienen stock menor a 10 unidades disponibles?

¿Cuál es el ticket promedio por canal?



# 📊 Caso de Inteligencia de Negocios – ComercioFácil S.A.
🧭 Contexto del Negocio
ComercioFácil S.A. es una empresa de e-commerce en expansión que gestiona ventas de productos tecnológicos, hogar y electrónica a través de múltiples canales: su sitio web propio, WhatsApp Business y marketplaces como Mercado Libre.

Con el crecimiento del negocio, la dirección general y el área comercial han identificado la necesidad de ir más allá de los reportes operativos básicos que brinda su sistema transaccional. Buscan implementar una solución de Inteligencia de Negocios (BI) que les permita transformar sus datos en decisiones estratégicas y accionables, enfocadas en:

Rentabilidad de productos y canales.

Comportamiento de clientes.

Eficiencia logística y de atención.

Planeamiento de compras y stock.

🎯 Objetivo General de la Solución BI
Diseñar e implementar una solución de Business Intelligence que permita a los equipos comerciales, logísticos y ejecutivos:

Monitorear en tiempo real los indicadores clave del negocio.

Analizar patrones y comportamientos de compra por cliente, canal y categoría.

Medir la rentabilidad por producto, familia y canal de venta.

Detectar cuellos de botella logísticos y optimizar tiempos de entrega.

Predecir demanda futura mediante tendencias históricas.

Automatizar reportes periódicos para cada unidad de negocio.

Tomar decisiones basadas en datos, no en intuición.

📐 Diseño de Modelo de Datos BI (Esquema Estrella)
El modelo de BI se construirá a partir del sistema transaccional ya modelado, mediante un proceso de ETL (extracción, transformación y carga) hacia un modelo dimensional optimizado para análisis.

🔷 Tabla de Hechos: FactVentas
Cada fila representa un producto vendido en una orden de compra.

Campo	Tipo	Descripción
IdVenta	Clave	ID único por fila de venta.
IdOrden	FK	Identificador de la orden de compra.
IdProducto	FK	Producto vendido.
IdCliente	FK	Cliente que realizó la compra.
IdCanalVenta	FK	Canal a través del cual se originó la orden.
IdMetodoPago	FK	Medio de pago utilizado.
IdFechaVenta	FK	Fecha de la transacción.
IdEstadoEnvio	FK	Estado del envío asociado.
Cantidad	Numérico	Unidades vendidas.
PrecioUnitario	Monetario	Precio aplicado por unidad en esa orden.
TotalVenta	Monetario	PrecioUnitario * Cantidad.
CostoUnitario	Monetario	Costo estimado del producto.
MargenBruto	Monetario	TotalVenta - (CostoUnitario * Cantidad).
DescuentoAplicado	Monetario	Monto total de descuento aplicado.

🔶 Dimensiones
DimFecha
Campo	Ejemplo
IdFechaVenta	20230715
Año	2023
Trimestre	Q3
Mes	Julio
Día	15
DíaSemana	Sábado

DimProducto
Campo	Ejemplo
IdProducto	P1023
Nombre	Auriculares Bluetooth
Categoría	Audio
Subcategoría	Accesorios
Proveedor	Logitech
Estado	Activo / Discontinuado

DimCliente
Campo	Ejemplo
IdCliente	C001122
Nombre	Juan Pérez
Zona	Córdoba
TipoCliente	Particular / Empresa
Antigüedad	3 años

DimCanalVenta
Campo	Ejemplo
IdCanalVenta	CV01
Canal	WhatsApp
Origen	Directo / Tercero

DimMetodoPago
Campo	Ejemplo
IdMetodoPago	MP03
MedioPago	Transferencia

DimEstadoEnvio
Campo	Ejemplo
IdEstadoEnvio	EE01
Estado	En camino

📊 Métricas Clave por Área
1. Área Comercial
Ventas totales por canal, período y producto.

Ranking de productos más vendidos y menos vendidos.

Ticket promedio por canal y por cliente.

Comparación de rendimiento entre canales.

Análisis de evolución mensual de ventas.

2. Área Logística
Porcentaje de órdenes entregadas en tiempo.

Tiempos promedio de entrega por zona.

Órdenes con estado pendiente o en tránsito.

Distribución de órdenes por transportista.

3. Rentabilidad
Margen bruto por producto, categoría y canal.

Costo promedio ponderado por categoría.

Análisis ABC de productos (facturación acumulada).

Rentabilidad por cliente (Customer Lifetime Value).

4. Clientes
Clientes más fieles (cantidad y frecuencia de compras).

Clientes nuevos vs recurrentes por mes.

Segmentación por comportamiento de compra.

Tasa de recompra (retención mensual).

📊 Dashboards Recomendados
Dashboard Ejecutivo General

Ventas totales, margen total, comparativo con mes anterior.

Mapa de calor por zona geográfica.

Alertas de productos con stock crítico.

Dashboard Comercial

Ranking productos/canales.

Evolución mensual de ventas.

Comparativa entre marketplaces.

Dashboard de Logística

Tiempos de entrega promedio.

Órdenes pendientes por zona.

Análisis de performance de operadores logísticos.

Dashboard de Clientes

Funnel de conversión.

Segmentación por valor.

Retención y tasa de recompra.

🔁 Automatización de Reportes
Reportes semanales automáticos de ventas y rentabilidad.

Alertas por mail para:

productos sin stock,

caída de ventas,

baja conversión por canal.

Exportación mensual a Excel/SharePoint de métricas clave.

🧠 Justificación Estratégica
Elemento	Beneficio Real
Análisis Multidimensional	Permite cortar los datos por canal, fecha, zona, cliente.
Visualización Ejecutiva	Facilita la toma de decisiones por parte de gerencias no técnicas.
Automatización	Ahorra tiempo de generación manual de reportes.
Escalabilidad	Modelo preparado para incorporar campañas, devoluciones, etc.
Toma de Decisiones	Se basa en datos reales, no en percepción o intuición.
Potencial Predictivo	Base para construir modelos de forecasting o machine learning.


<img width="710" height="467" alt="image" src="https://github.com/user-attachments/assets/c6f888e5-f2db-4437-a9bf-c273a2148c6c" />

