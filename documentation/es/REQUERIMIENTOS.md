## ¿Por qué PitShield? Necesidades del Mercado y Propuesta de Valor

Los talleres mecánicos y centros de *detailing* tradicionales enfrentan tres grandes problemas operativos y financieros. **PitShield** resuelve directamente estos desafíos integrando soluciones Fintech en su plataforma.

---

### 1. La Falta de Confianza del Cliente
* **El Problema:** El sector de servicios automotrices sufre de una desconfianza generalizada. Los propietarios de vehículos suelen dudar sobre si los repuestos facturados realmente fueron instalados, si los precios son justos o si los diagnósticos son legítimos.
* **La Solución PitShield:** Un **Historial Digital del Vehículo** inmutable y transparente. PitShield genera una hoja de vida digital verificable que incluye seguimiento del kilometraje, registro de repuestos instalados y evidencia en fotos o video de cada servicio.

---

### 2. Desorden Administrativo y Pérdida de Margen
* **El Problema:** Muchos administradores de talleres todavía dependen del papel, hojas de cálculo de Excel o sistemas de punto de venta genéricos. Estas herramientas carecen de integración con normativas fiscales, flujos de pago digitales y seguimiento financiero automático, lo que genera fuga de dinero y fatiga administrativa.
* **La Solución PitShield:** Un **Módulo Fintech de Facturación y Cobros** integrado. PitShield agiliza la facturación electrónica, automatiza los costos por orden de trabajo, se conecta sin problemas con pasarelas de pago digitales y ofrece métricas financieras en tiempo real.

---

### 3. Riesgo Operativo en Garantías y Oportunidades de Venta Perdidas
* **El Problema:** Cuando un repuesto o trabajo falla después del servicio, el taller debe asumir el costo de la reparación por su cuenta o arriesgarse a perder al cliente. Además, los talleres tradicionales carecen de productos financieros recurrentes para aumentar el valor promedio de venta (*upselling*).
* **La Solución PitShield:** **Microseguros y Garantías Extendidas Embebidas (*Embedded Insurance*)**. PitShield permite a los talleres emitir planes de protección extendida respaldados por aseguradoras directamente en el momento del cobro. Si una pieza cubierta falla dentro del periodo de garantía, el reclamo se gestiona de forma digital: protegiendo el margen del taller y generando una nueva fuente de ingresos por comisión.

---

##  Requerimientos y Reglas de Negocio Completos

### A. Requerimientos Funcionales (RF)

| ID | Módulo | Descripción |
| :--- | :--- | :--- |
| **RF-01** | **Gestión de Vehículos** | El sistema debe registrar y consultar el historial por Placa o VIN, incluyendo marca, modelo, año y especificaciones técnicas. |
| **RF-02** | **Órdenes de Trabajo** | El sistema debe gestionar el ciclo de vida del servicio (Borrador, Pendiente de Aprobación, En Proceso, Listo para Entrega, Facturado). |
| **RF-03** | **Facturación Fintech** | El sistema debe convertir órdenes de trabajo en facturas digitales con desglose de mano de obra, repuestos, impuestos y descuentos. |
| **RF-04** | **Pagos Integrados** | El sistema debe integrar pasarelas de pago para cobrar vía tarjeta, transferencia y links de pago automáticos por SMS/WhatsApp. |
| **RF-05** | **Emisión de Garantías** | El sistema debe evaluar elegibilidad y emitir microseguros/garantías extendidas con un solo clic durante el cobro. |
| **RF-06** | **Gestión de Reclamos** | El sistema debe proveer un flujo para radicar, revisar y liquidar reclamos por fallas en piezas o servicio con evidencia fotográfica. |
| **RF-07** | **Inventario de Repuestos** | El sistema debe controlar existencias de repuestos, costos, precios de venta y descontar stock automáticamente al cerrar la orden. |
| **RF-08** | **Portal del Cliente** | El sistema debe permitir a los propietarios consultar su historial digital, ver fotos del avance y aprobar cotizaciones de forma remota. |
| **RF-09** | **Reportes Financieros** | El sistema debe calcular ingresos del taller, comisiones ganadas por venta de microseguros y resúmenes de impuestos. |

---

### B. Reglas de Negocio (RN)

| ID | Regla | Descripción y Restricciones |
| :--- | :--- | :--- |
| **RN-01** | **Elegibilidad de Garantía** | El microseguro solo aplica para vehículos con menos de 120,000 km, menos de 10 años de antigüedad y uso particular (no servicio público/flotas). |
| **RN-02** | **Inmutabilidad** | Una vez que una orden o factura pase a estado "Pagada", sus datos no podrán editarse ni borrarse. Cambios requieren notas crédito auditables. |
| **RN-03** | **Comisión de Plataforma** | PitShield retendrá automáticamente un % de comisión por cada garantía emitida y transacción procesada antes de liquidar al taller. |
| **RN-04** | **Inspección Obligatoria** | Para activar la garantía extendida, el técnico debe adjuntar al menos 2 fotos del repuesto nuevo instalado y registrar el kilometraje exacto. |
| **RN-05** | **Validación de Inventario** | Una orden de trabajo no puede pasar a "En Proceso" si los repuestos requeridos no cuentan con stock suficiente en el módulo de inventario. |

---

### C. Requerimientos No Funcionales (RNF)

| ID | Categoría | Criterio de Aceptación / Métrica |
| :--- | :--- | :--- |
| **RNF-01** | **Seguridad** | Control de acceso por roles (RBAC) con JWT, cifrado TLS 1.3 y cumplimiento de estándares OWASP Top 10. |
| **RNF-02** | **Disponibilidad** | Despliegue en la nube que garantice una disponibilidad mínima del 99.5% mensual. |
| **RNF-03** | **Multi-Tenancy (SaaS)** | Aislamiento lógico estricto de datos: el Taller A jamás podrá ver o consultar datos del Taller B. |
| **RNF-04** | **Rendimiento** | Las respuestas de la API para consulta de historial e inventario no deben superar los 1.5 segundos. |
| **RNF-05** | **Cumplimiento Fiscal** | El sistema debe soportar estándares de facturación electrónica local para la firma y envío de documentos fiscales. |