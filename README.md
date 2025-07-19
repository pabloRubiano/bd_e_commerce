# bd_e_commerce: caso BD transaccional

🛒 Caso Propuesto – Sistema de Gestión de Pedidos para E-commerce
🧭 Contexto del Negocio
ComercioFácil S.A. es una empresa argentina de e-commerce especializada en la venta de productos de tecnología, hogar y electrónica de consumo. Opera a través de canales propios (sitio web, WhatsApp) y plataformas externas como Mercado Libre.

Actualmente, sus operaciones comerciales están en crecimiento y requieren una base de datos relacional transaccional para registrar y gestionar la información crítica de su negocio: ventas, clientes, productos, pagos y envíos.

La empresa busca mayor control sobre su operación diaria, trazabilidad de pedidos, seguimiento de entregas y organización del inventario. Esta base también servirá como base futura para la generación de reportes comerciales, métricas de rendimiento y análisis de clientes.

🎯 Objetivo del Sistema
Diseñar un modelo de base de datos relacional transaccional que permita:

Registrar órdenes de compra realizadas por los clientes.

Asociar múltiples productos a cada orden (modelo N:N).

Controlar la información de productos, stock y precios actualizados.

Registrar la forma de pago y canal de venta para cada operación.

Gestionar la información básica del envío asociado a cada orden.

Brindar la posibilidad de generar métricas clave a partir de los datos.

🧩 Alcance del Modelo
La base de datos debe cubrir los siguientes procesos:

Registro de nuevos clientes.

Carga del catálogo de productos con precio y stock.

Registro de una orden de compra con uno o varios productos.

Registro del pago y canal de venta asociado a la orden.

Registro de los datos básicos del envío (estado, fecha estimada).

Control básico de stock por producto (disminuye al confirmar venta).

🧱 Entidades Principales
Entidad	Descripción
Cliente	Información de cada cliente (nombre, contacto, dirección).
Producto	Catálogo activo de productos (nombre, precio actual, stock).
Orden	Encabezado de cada compra realizada por un cliente.
DetalleOrden	Detalle por producto de cada orden (cantidad, precio aplicado).
MetodoPago	Medios de pago disponibles (tarjeta, efectivo, transferencia).
CanalVenta	Canal por el que se concretó la compra (web, WhatsApp, marketplace).
Envio	Información del envío (estado, fecha estimada, transportista).

🔄 Relaciones
Un cliente puede generar muchas órdenes.

Una orden contiene uno o más productos (relación N:N).

Cada producto puede aparecer en muchas órdenes.

Cada orden se paga con un solo método de pago.

Cada orden se canaliza por un canal de venta.

Cada orden tiene un solo registro de envío.

📌 Reglas del Negocio
El stock del producto debe disminuir al momento de confirmar una orden.

Cada orden debe tener al menos un producto asociado.

Los precios aplicados en una orden se congelan al momento de compra.

Los estados del envío pueden ser: Pendiente, En preparación, En camino, Entregado, Cancelado.

Los canales de venta deben poder analizarse por separado para medir rentabilidad.

🔍 Consultas Representativas
¿Cuáles fueron los productos más vendidos en el último trimestre?

¿Cuál fue el canal con mayor facturación el mes pasado?

¿Cuántas órdenes fueron entregadas en los últimos 7 días?

¿Qué clientes realizaron más de 3 compras?

¿Qué productos tienen stock menor a 10 unidades?

¿Cuál es el ticket promedio por canal de venta?




📊 Caso Propuesto – Solución de Inteligencia de Negocios para ComercioFácil S.A.
🧭 Contexto del Negocio
ComercioFácil S.A. ha implementado un sistema transaccional que registra todas las operaciones de compra de sus clientes, incluyendo productos, pagos, envíos y stock. Sin embargo, la dirección comercial necesita ahora una solución de inteligencia de negocios que transforme esos datos operativos en decisiones estratégicas.

Los objetivos del área de BI serán:

Monitorear la performance del negocio en tiempo real.

Detectar oportunidades de crecimiento y mejora en canales, productos y clientes.

Medir indicadores de eficiencia operativa y rentabilidad.

Automatizar reportes ejecutivos y facilitar el análisis multidimensional.

🎯 Objetivo de la Solución BI
Diseñar una solución de Business Intelligence que:

Consuma los datos transaccionales del sistema de ventas.

Modele un esquema de datos analítico (estrella o copo de nieve).

Permita explorar las métricas clave del negocio.

Implemente dashboards con filtros por canal, tiempo, categoría y cliente.

Automatice la generación de reportes operativos y comerciales.

📐 Modelo BI (Diseño Semántico)
🔷 Hecho principal: FactVentas
Contendrá una fila por producto vendido por orden. Campos:

IdOrden

IdProducto

FechaVenta

CanalVenta

MetodoPago

Cantidad

PrecioUnitario

Descuento

TotalVenta

CostoUnitario

MargenBruto

🔶 Dimensiones
Dimensión	Contenido
DimFecha	Año, mes, día, trimestre, día de semana.
DimProducto	Categoría, nombre, proveedor.
DimCliente	Zona, tipo de cliente, antigüedad.
DimCanalVenta	Web, WhatsApp, Marketplace, etc.
DimMetodoPago	Tarjeta, transferencia, efectivo.
DimEstadoEnvio	Pendiente, En camino, Entregado, etc.

📌 Indicadores Clave a Implementar
Comerciales
Ventas totales

Ventas por canal y categoría

Ticket promedio

Clientes recurrentes vs nuevos

Logísticos
Tiempos promedio de entrega

Órdenes sin entregar

Porcentaje de entregas en tiempo

Rentabilidad
Margen bruto por producto y canal

Ranking de productos más y menos rentables

Análisis ABC (productos clave en facturación)

Clientes
Top 10 clientes por volumen

Tasa de recompra

Segmentación por comportamiento de compra

🧠 Justificación de la Solución BI
Aspecto	Valor Agregado
Orientación Estratégica	Permite decisiones basadas en datos reales, no intuición.
Escalabilidad	Se puede ampliar a campañas, marketing, devoluciones.
Visualización Ejecutiva	Presenta indicadores de forma clara, accesible y dinámica.
Automatización	Ahorra tiempo en reportes mensuales o semanales.
Proyección	Permite escenarios tipo “¿Qué pasaría si...?” sobre ventas y precios.


