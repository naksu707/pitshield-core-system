# Especificación de Requerimientos · PitShield Core System

> 🇪🇸 Español · [🇬🇧 English](../en/REQUIREMENTS.md)

| Campo                  | Valor                                                                 |
| ---------------------- | --------------------------------------------------------------------- |
| **Producto**           | PitShield Core System                                                 |
| **Versión**            | 1.1                                                                   |
| **Estado**             | Aprobado para diseño                                                  |
| **Mercado inicial**    | Colombia (moneda COP, facturación electrónica DIAN)                   |
| **Historias de usuario** | [`HISTORIAS-USUARIO.md`](HISTORIAS-USUARIO.md)                      |

---

## Contenido

1. [Propósito y alcance](#1-propósito-y-alcance)
2. [¿Por qué PitShield? Necesidades del mercado](#2-por-qué-pitshield-necesidades-del-mercado)
3. [Roles del sistema](#3-roles-del-sistema)
4. [Requerimientos funcionales (RF)](#4-requerimientos-funcionales-rf)
5. [Reglas de negocio (RN)](#5-reglas-de-negocio-rn)
6. [Requerimientos no funcionales (RNF)](#6-requerimientos-no-funcionales-rnf)
7. [Restricciones y supuestos](#7-restricciones-y-supuestos)
8. [Plan de entregas](#8-plan-de-entregas)
9. [Matriz de trazabilidad](#9-matriz-de-trazabilidad)
10. [Glosario](#10-glosario)

---

## 1. Propósito y alcance

Este documento define **qué debe hacer** PitShield Core System y **bajo qué condiciones**. Es la base para el diseño, el desarrollo, las pruebas automáticas y las pruebas manuales.

**Dentro del alcance:**

- Gestión de talleres mecánicos y centros de *detailing* como clientes de la plataforma (modelo SaaS multi-taller).
- Clientes, vehículos e historial digital del vehículo.
- Agenda, órdenes de trabajo, presupuestos, inventario y compras.
- Facturación, pagos presenciales y en línea, notas crédito y reembolsos.
- Garantías extendidas y microseguros: elegibilidad, emisión, coberturas, reclamos y comisiones.
- Portal web del cliente y notificaciones.
- Reportes, estadísticas y analítica para el taller, la plataforma y las aseguradoras.
- Inteligencia artificial: chatbots para clientes (portal web y WhatsApp) y para el personal del taller, y agentes de apoyo.

**Fuera del alcance (versión 1.0):**

- Aplicaciones móviles nativas (el portal del cliente es web responsive).
- Contabilidad completa (nómina, balances, declaración de impuestos). PitShield entrega los reportes que necesita el contador.
- Emisión propia de pólizas: la aseguradora aliada es quien asume el riesgo; PitShield actúa como canal de venta y gestión.

---

## 2. ¿Por qué PitShield? Necesidades del mercado

Los talleres mecánicos y centros de *detailing* tradicionales enfrentan tres grandes problemas operativos y financieros. **PitShield** los resuelve integrando soluciones Fintech en su plataforma.

### 2.1 La falta de confianza del cliente

* **El problema:** el sector sufre de una desconfianza generalizada. Los propietarios dudan de si los repuestos facturados realmente se instalaron, si los precios son justos o si los diagnósticos son legítimos.
* **La solución:** un **Historial Digital del Vehículo** inmutable y transparente, con kilometraje, repuestos instalados y evidencia en fotos o video de cada servicio.

### 2.2 Desorden administrativo y pérdida de margen

* **El problema:** muchos talleres dependen del papel, hojas de cálculo o puntos de venta genéricos, sin facturación electrónica, pagos digitales ni seguimiento financiero.
* **La solución:** un **módulo de facturación y cobros** integrado, con facturación electrónica, costeo automático por orden de trabajo, pasarelas de pago y métricas en tiempo real.

### 2.3 Riesgo en garantías y ventas perdidas

* **El problema:** cuando un repuesto o trabajo falla después del servicio, el taller asume el costo o pierde al cliente. Además, no tiene productos recurrentes para aumentar el valor promedio de venta.
* **La solución:** **garantías extendidas y microseguros embebidos**, emitidos en el momento del cobro y respaldados por una aseguradora. Los reclamos se gestionan de forma digital y el taller gana una comisión por cada producto vendido.

---

## 3. Roles del sistema

| Rol                              | Descripción                                                                                |
| -------------------------------- | ------------------------------------------------------------------------------------------ |
| **Administrador de Plataforma**  | Equipo de PitShield. Da de alta talleres y aseguradoras, configura productos y comisiones. |
| **Administrador del Taller**     | Dueño o gerente. Configura el taller, gestiona usuarios y consulta reportes.               |
| **Asesor de Servicio**           | Recibe vehículos, crea órdenes de trabajo y presupuestos, y atiende al cliente.            |
| **Técnico**                      | Diagnostica, registra evidencias, consume repuestos y ejecuta el trabajo.                  |
| **Cajero**                       | Genera facturas, registra pagos, notas crédito y reembolsos.                               |
| **Encargado de Inventario**      | Administra repuestos, proveedores y compras.                                               |
| **Cliente**                      | Propietario del vehículo. Usa el portal para consultar, aprobar y pagar.                   |
| **Auditor de Aseguradora**       | Revisa y decide los reclamos de garantías y microseguros.                                  |
| **Sistema**                      | Procesos automáticos: tareas programadas, *webhooks* y notificaciones.                     |

Un usuario puede tener más de un rol dentro de un taller (por ejemplo, Administrador y Cajero en un taller pequeño).

---

## 4. Requerimientos funcionales (RF)

> Los requerimientos se agrupan por módulo. Los que se agregaron después tomaron el siguiente número disponible, por eso algunos módulos no van en orden numérico.

### Módulo 1 · Autenticación, usuarios y seguridad

| ID        | Requerimiento                                                                                                                                       |
| --------- | --------------------------------------------------------------------------------------------------------------------------------------------------- |
| **RF-01** | El sistema debe permitir iniciar y cerrar sesión con correo y contraseña, y cerrar la sesión automáticamente cuando expire.                          |
| **RF-02** | El sistema debe permitir recuperar la contraseña por correo y cambiarla estando autenticado.                                                       |
| **RF-03** | El sistema debe permitir crear, editar, activar y desactivar usuarios, y asignarles uno o varios roles.                                            |
| **RF-04** | El sistema debe registrar en auditoría las acciones relevantes (quién, qué, cuándo y sobre qué registro) y permitir consultarlas con filtros.       |
| **RF-05** | El sistema debe registrar la autorización de tratamiento de datos personales y atender solicitudes de consulta, actualización o supresión.        |

### Módulo 2 · Talleres y configuración

| ID        | Requerimiento                                                                                                     |
| --------- | ----------------------------------------------------------------------------------------------------------------- |
| **RF-06** | El sistema debe permitir registrar y actualizar los datos comerciales y fiscales del taller (NIT, razón social, logo). |
| **RF-07** | El sistema debe permitir configurar impuestos, numeración de facturas y resolución de facturación del taller.     |
| **RF-08** | El sistema debe permitir gestionar sucursales con sus horarios de atención.                                       |

### Módulo 3 · Clientes, vehículos e historial digital

| ID        | Requerimiento                                                                                                                      |
| --------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| **RF-09** | El sistema debe permitir registrar, buscar y actualizar clientes, y vincularlos a uno o varios vehículos.                         |
| **RF-10** | El sistema debe registrar vehículos por placa y VIN, con marca, modelo, año, motor, tipo de uso y kilometraje.                    |
| **RF-11** | El sistema debe mostrar el historial digital del vehículo en orden cronológico: servicios, repuestos, evidencias y coberturas.    |
| **RF-12** | El sistema debe permitir transferir la propiedad de un vehículo conservando su historial.                                         |
| **RF-13** | El sistema debe impedir la eliminación del historial y guardar el valor anterior de cada corrección.                              |

### Módulo 4 · Servicios, agenda y técnicos

| ID        | Requerimiento                                                                                                   |
| --------- | --------------------------------------------------------------------------------------------------------------- |
| **RF-14** | El sistema debe permitir gestionar el catálogo de servicios con precio, duración estimada y estado.             |
| **RF-15** | El sistema debe permitir crear, confirmar, reprogramar y cancelar citas según la disponibilidad de la sucursal. |
| **RF-16** | El sistema debe permitir asignar técnicos a una orden de trabajo y registrar el tiempo de mano de obra.         |

### Módulo 5 · Órdenes de trabajo

| ID        | Requerimiento                                                                                                                                  |
| --------- | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| **RF-17** | El sistema debe registrar la recepción del vehículo: kilometraje, nivel de combustible, daños visibles, objetos dejados y fotos de ingreso.    |
| **RF-18** | El sistema debe crear órdenes de trabajo con código único y controlar su ciclo de vida según el flujo de estados definido (RN-10).            |
| **RF-19** | El sistema debe permitir registrar síntomas, diagnóstico, observaciones y evidencias multimedia.                                              |
| **RF-20** | El sistema debe generar presupuestos versionados con servicios, repuestos, mano de obra, impuestos y descuentos.                              |
| **RF-21** | El sistema debe permitir que el cliente apruebe o rechace el presupuesto de forma remota.                                                     |
| **RF-22** | El sistema debe registrar la entrega del vehículo con el kilometraje de salida y la conformidad del cliente.                                  |

### Módulo 6 · Inventario, proveedores y compras

| ID        | Requerimiento                                                                                                                       |
| --------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| **RF-23** | El sistema debe gestionar repuestos con código, costo, precio de venta, stock disponible, reservado y mínimo.                       |
| **RF-24** | El sistema debe reservar, consumir y devolver repuestos según el avance de la OT, y registrar ajustes con motivo.                   |
| **RF-25** | El sistema debe gestionar proveedores y órdenes de compra, e incrementar el stock al registrar la recepción.                        |

### Módulo 7 · Facturación y pagos

| ID        | Requerimiento                                                                                                                       |
| --------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| **RF-26** | El sistema debe convertir una OT finalizada en factura con el detalle de mano de obra, repuestos, impuestos y descuentos.           |
| **RF-27** | El sistema debe enviar la factura electrónica a la DIAN mediante un proveedor tecnológico autorizado y guardar su CUFE.             |
| **RF-28** | El sistema debe registrar pagos presenciales (efectivo, tarjeta, transferencia) y pagos parciales.                                  |
| **RF-29** | El sistema debe generar enlaces de pago en línea y actualizar la factura al recibir la confirmación de la pasarela (*webhook*).    |
| **RF-30** | El sistema debe emitir notas crédito y gestionar reembolsos sin eliminar la factura original.                                       |

### Módulo 8 · Garantías, microseguros y reclamos

| ID        | Requerimiento                                                                                                                            |
| --------- | ---------------------------------------------------------------------------------------------------------------------------------------- |
| **RF-31** | El sistema debe permitir configurar productos de protección: tipo, aseguradora, cobertura, vigencia, precio, comisión y condiciones.     |
| **RF-32** | El sistema debe evaluar la elegibilidad del vehículo y emitir la garantía o microseguro durante el cobro, con certificado digital.       |
| **RF-33** | El sistema debe mostrar las coberturas con su estado y vigencia, y gestionar su vencimiento y cancelación.                              |
| **RF-34** | El sistema debe permitir radicar reclamos con evidencias, hacer su seguimiento y registrar el dictamen del auditor.                     |
| **RF-35** | El sistema debe calcular y liquidar las comisiones de la plataforma y del taller por cada producto vendido y transacción procesada.     |

### Módulo 9 · Portal del cliente

| ID        | Requerimiento                                                                                                                           |
| --------- | --------------------------------------------------------------------------------------------------------------------------------------- |
| **RF-36** | El sistema debe invitar al cliente al portal y permitirle activar su cuenta.                                                            |
| **RF-37** | El portal debe permitir al cliente consultar sus vehículos, historial, OT, presupuestos, facturas, pagos, coberturas y reclamos.        |

### Módulo 10 · Notificaciones

| ID        | Requerimiento                                                                                                         |
| --------- | --------------------------------------------------------------------------------------------------------------------- |
| **RF-38** | El sistema debe enviar notificaciones automáticas por correo y WhatsApp ante eventos del servicio.                    |
| **RF-39** | El sistema debe generar recordatorios de mantenimiento preventivo por tiempo o kilometraje estimado.                  |
| **RF-40** | El sistema debe permitir al cliente elegir sus canales de notificación y retirar su autorización para mensajes.       |

### Módulo 11 · Reportes, estadísticas y analítica

| ID        | Requerimiento                                                                                                          |
| --------- | ---------------------------------------------------------------------------------------------------------------------- |
| **RF-41** | El sistema debe mostrar un tablero financiero: ingresos, cartera pendiente, reembolsos y comisiones por periodo.       |
| **RF-42** | El sistema debe generar reportes operativos (OT, tiempos, servicios) y de inventario (movimientos, stock crítico).     |
| **RF-43** | El sistema debe permitir exportar los reportes a CSV y PDF.                                                            |
| **RF-48** | El sistema debe mostrar un tablero de indicadores clave (KPI) del taller con su tendencia y estadísticas de servicios, técnicos y demanda. |
| **RF-49** | El sistema debe ofrecer al Administrador de Plataforma estadísticas de uso y de negocio de toda la plataforma, con comparaciones anónimas entre talleres. |
| **RF-50** | El sistema debe ofrecer a cada aseguradora estadísticas de sus coberturas, reclamos y siniestralidad.                  |

### Módulo 12 · Inteligencia artificial y chatbots

| ID        | Requerimiento                                                                                                                                  |
| --------- | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| **RF-44** | El sistema debe ofrecer agentes de IA de apoyo para diagnóstico, mantenimiento preventivo, inventario y preanálisis de reclamos. |
| **RF-45** | El sistema debe registrar cada interacción relevante con los agentes de IA y si su recomendación fue aceptada o descartada.                   |
| **RF-51** | El sistema debe ofrecer un chatbot para clientes, en el portal web y por WhatsApp, que responda sobre sus vehículos, citas, órdenes, facturas y coberturas, y que permita agendar, reprogramar y cancelar citas. |
| **RF-52** | El sistema debe ofrecer un asistente conversacional para el personal del taller que responda preguntas en lenguaje natural sobre los datos e indicadores del taller, según los permisos de cada rol. |
| **RF-53** | El sistema debe permitir configurar la base de conocimiento del chatbot, transferir la conversación a un asesor y medir la calidad de las conversaciones. |

### Módulo 13 · Administración de la plataforma

| ID        | Requerimiento                                                                                                         |
| --------- | --------------------------------------------------------------------------------------------------------------------- |
| **RF-46** | El sistema debe permitir dar de alta, activar y suspender talleres, y crear su primer Administrador del Taller.       |
| **RF-47** | El sistema debe permitir registrar aseguradoras aliadas y sus usuarios auditores.                                    |

---

## 5. Reglas de negocio (RN)

| ID        | Regla                              | Descripción y restricciones                                                                                                                                                   |
| --------- | ---------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **RN-01** | Elegibilidad de cobertura          | Por defecto, un producto de protección solo aplica a vehículos con menos de 120 000 km, menos de 10 años y uso particular (no servicio público ni flotas). Cada producto puede definir sus propios límites. |
| **RN-02** | Inmutabilidad de documentos        | Una factura emitida o una OT facturada no puede editarse ni eliminarse. Los cambios se hacen con notas crédito auditables.                                                     |
| **RN-03** | Comisión de plataforma             | PitShield retiene un porcentaje configurable por cada producto de protección emitido y por cada pago en línea procesado, antes de liquidar al taller.                       |
| **RN-04** | Inspección obligatoria             | Para activar una cobertura, el técnico debe adjuntar al menos 2 fotos del repuesto nuevo instalado y registrar el kilometraje exacto.                                         |
| **RN-05** | Validación de inventario           | Una OT no puede pasar a "En Proceso" si los repuestos requeridos no tienen stock disponible suficiente.                                                                     |
| **RN-06** | Aislamiento por taller             | Todo registro operativo pertenece a un taller. Un usuario solo ve datos de su taller, salvo el Administrador de Plataforma y el Auditor en los reclamos asignados.           |
| **RN-07** | Bloqueo por intentos fallidos      | Tras 5 intentos fallidos de inicio de sesión en 15 minutos, la cuenta se bloquea 15 minutos. El enlace de recuperación de contraseña vence en 30 minutos y es de un solo uso. |
| **RN-08** | Identidad del vehículo             | La placa y el VIN son únicos dentro de un taller. El historial registrado por otro taller solo es visible si el propietario lo autoriza desde el portal.                     |
| **RN-09** | Vigencia del presupuesto           | Un presupuesto vence a los 15 días (configurable). Cualquier trabajo adicional requiere una nueva versión aprobada por el cliente.                                           |
| **RN-10** | Flujo de estados de la OT          | Borrador → Pendiente de Aprobación → Aprobada → En Proceso ⇄ En Espera → Finalizada → Lista para Entrega → Entregada. "Cancelada" solo es posible antes de "Finalizada".    |
| **RN-11** | Origen de la factura               | Solo se factura una OT en estado "Finalizada" o posterior. Una OT genera una sola factura.                                                                                   |
| **RN-12** | Pagos idempotentes                 | El identificador de transacción de la pasarela es único. Un mismo evento recibido dos veces no registra dos pagos.                                                           |
| **RN-13** | Pagos parciales                    | Una factura queda "Pagada" cuando la suma de sus pagos iguala el total. El saldo nunca puede ser negativo ni superar el total.                                               |
| **RN-14** | Condiciones del reclamo            | Solo se radica un reclamo con cobertura vigente, dentro de los 30 días siguientes a la falla y con al menos una evidencia de la falla.                                       |
| **RN-15** | Decisión humana                    | Los agentes de IA solo recomiendan. Ningún estado final (diagnóstico, cobertura, reclamo, pago) cambia sin la acción de un usuario autorizado.                              |
| **RN-16** | Límite de recordatorios            | Se envía como máximo un recordatorio por vehículo y condición cada 30 días, y nunca a un cliente que retiró su autorización.                                                |
| **RN-17** | Stock no negativo                  | Ningún movimiento puede dejar el stock disponible de un repuesto por debajo de cero.                                                                                         |
| **RN-18** | Moneda e impuestos                 | Los valores se manejan en pesos colombianos (COP). El IVA por defecto es 19 % y cada servicio o repuesto puede tener su propia tarifa (incluida exenta).                     |
| **RN-19** | Datos personales                   | Los datos del cliente solo se tratan con su autorización expresa, según la Ley 1581 de 2012. Las solicitudes del titular se responden en máximo 15 días hábiles.          |
| **RN-20** | Cancelación con consumo            | Si una OT tiene repuestos ya consumidos, su cancelación requiere facturar lo consumido o registrar una justificación aprobada por el Administrador del Taller.              |
| **RN-21** | Alcance de los chatbots            | Los chatbots solo usan la información del usuario autenticado y la base de conocimiento del taller, y nunca inventan precios, estados ni coberturas. Solo ejecutan acciones de bajo riesgo (agendar, reprogramar o cancelar citas) y siempre con la confirmación del usuario. No aprueban presupuestos, no registran pagos ni radican reclamos. |
| **RN-22** | Traspaso a un asesor               | El chatbot transfiere la conversación a un asesor cuando el cliente lo pide, cuando no entiende la consulta dos veces seguidas o cuando detecta una queja. Fuera del horario de atención registra la solicitud e informa cuándo será atendida. |
| **RN-23** | Datos agregados                    | La analítica de la plataforma y de las aseguradoras muestra datos agregados. Las comparaciones entre talleres son anónimas y solo se muestran si el grupo tiene al menos 5 talleres. |

---

## 6. Requerimientos no funcionales (RNF)

| ID         | Categoría              | Criterio de aceptación / métrica                                                                                                                                         |
| ---------- | ---------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **RNF-01** | Seguridad              | Control de acceso por roles (RBAC) con JWT de corta duración y *refresh token*, contraseñas con BCrypt, HTTPS (TLS 1.2 o superior) y mitigación del OWASP Top 10.      |
| **RNF-02** | Disponibilidad         | En producción, disponibilidad mínima del 99.5 % mensual.                                                                                                                 |
| **RNF-03** | Multi-taller (SaaS)    | Aislamiento lógico estricto: el Taller A nunca puede ver ni consultar datos del Taller B. Se verifica con pruebas automáticas en cada *endpoint*.                         |
| **RNF-04** | Rendimiento            | Con 50 usuarios concurrentes por taller, el percentil 95 de las consultas (historial, inventario, facturas) es menor a 1.5 s y la generación de una factura menor a 3 s. |
| **RNF-05** | Cumplimiento fiscal    | Facturación electrónica según la normativa DIAN vigente, a través de un proveedor tecnológico autorizado.                                                               |
| **RNF-06** | Privacidad             | Cumplimiento de la Ley 1581 de 2012 (habeas data). Datos sensibles cifrados en reposo y nunca escritos en los *logs*.                                                    |
| **RNF-07** | Usabilidad             | Interfaz responsive (el portal del cliente se usa desde el celular) y accesible según WCAG 2.1 nivel AA.                                                                 |
| **RNF-08** | Localización           | Interfaz en español (es-CO), moneda COP, zona horaria America/Bogota y fechas en formato dd/mm/aaaa.                                                                     |
| **RNF-09** | Mantenibilidad         | Monolito modular con un módulo por dominio. Código en español, revisión de *pull request* obligatoria y análisis estático en CI.                                         |
| **RNF-10** | Calidad y pruebas      | Cobertura mínima del 80 % en servicios y dominio. La integración continua bloquea el *merge* si falla una prueba. Los flujos críticos tienen pruebas E2E.                |
| **RNF-11** | Observabilidad         | *Logs* estructurados con identificador de correlación, *health checks* y métricas expuestas.                                                                             |
| **RNF-12** | Respaldo               | Copias de seguridad diarias de la base de datos con retención mínima de 7 días (pérdida máxima de datos: 24 horas).                                                      |
| **RNF-13** | Archivos multimedia    | Fotos JPG/PNG de hasta 10 MB y videos MP4 de hasta 100 MB, guardados en almacenamiento de objetos y servidos con enlaces temporales.                                     |
| **RNF-14** | API                    | API REST versionada (`/api/v1`) y documentada con OpenAPI.                                                                                                                |
| **RNF-15** | Portabilidad           | Backend, frontend y base de datos se ejecutan en contenedores Docker. El entorno local se levanta con un solo comando.                                                    |
| **RNF-16** | Rendimiento de la IA   | El chatbot da su primera respuesta en menos de 5 s (percentil 95). Si el proveedor de IA no responde, el chatbot lo indica y ofrece hablar con un asesor.               |
| **RNF-17** | Privacidad y costo de la IA | Antes de enviar datos al proveedor de IA se enmascaran documentos, teléfonos y correos. El proveedor no puede usar los datos para entrenar modelos. Cada taller tiene un límite mensual de uso configurable. |
| **RNF-18** | Analítica              | Los tableros cargan en menos de 3 s con 12 meses de datos y se actualizan al menos cada 15 minutos.                                                                      |

---

## 7. Restricciones y supuestos

**Restricciones**

- Backend en Java con Spring Boot, frontend en React con TypeScript y base de datos PostgreSQL.
- El desarrollo (código, base de datos, *commits* e *issues*) se hace en español. La documentación se publica en español e inglés.
- Equipo de 3 desarrolladores, con gestión en GitHub Projects.
- La IA se integra con Spring AI, para poder cambiar de proveedor de modelo de lenguaje (LLM) sin reescribir el módulo. El proveedor se elige al iniciar la Entrega 3.

**Supuestos**

- Las integraciones externas (pasarela de pago, facturación electrónica, aseguradora y WhatsApp) se desarrollan primero contra sus entornos de prueba (*sandbox*) o simuladores.
- La aseguradora aliada define las coberturas reales. Los valores de este documento son configurables y de referencia.
- El portal del cliente y el sistema del taller comparten el mismo frontend, con vistas según el rol.

---

## 8. Plan de entregas

| Entrega        | Contenido                                                                                                               | Módulos         |
| -------------- | ----------------------------------------------------------------------------------------------------------------------- | --------------- |
| **MVP**        | Acceso y roles, talleres, clientes, vehículos e historial, agenda, órdenes de trabajo, inventario, facturación y pagos presenciales | 1 – 7, 13 (alta de talleres) |
| **Entrega 2**  | Pagos en línea, factura electrónica, garantías y microseguros, reclamos, portal del cliente y notificaciones          | 7 – 10, 13      |
| **Entrega 3**  | Estadísticas y analítica, exportaciones, chatbots (portal, WhatsApp y personal) y agentes de inteligencia artificial    | 11, 12          |

La prioridad y la entrega de cada historia de usuario aparecen en [`HISTORIAS-USUARIO.md`](HISTORIAS-USUARIO.md).

---

## 9. Matriz de trazabilidad

| Requerimiento | Historias de usuario      | Requerimiento | Historias de usuario      |
| ------------- | ------------------------- | ------------- | ------------------------- |
| RF-01         | HU-001, HU-049            | RF-25         | HU-024                    |
| RF-02         | HU-002                    | RF-26         | HU-025                    |
| RF-03         | HU-003                    | RF-27         | HU-057                    |
| RF-04         | HU-004                    | RF-28         | HU-056                    |
| RF-05         | HU-050                    | RF-29         | HU-026, HU-027            |
| RF-06         | HU-005                    | RF-30         | HU-028                    |
| RF-07         | HU-051                    | RF-31         | HU-065                    |
| RF-08         | HU-006                    | RF-32         | HU-029, HU-030            |
| RF-09         | HU-007, HU-052            | RF-33         | HU-031, HU-058            |
| RF-10         | HU-008                    | RF-34         | HU-032, HU-033            |
| RF-11         | HU-009                    | RF-35         | HU-059                    |
| RF-12         | HU-010                    | RF-36         | HU-060                    |
| RF-13         | HU-011                    | RF-37         | HU-034 – HU-037           |
| RF-14         | HU-012                    | RF-38         | HU-038                    |
| RF-15         | HU-013                    | RF-39         | HU-039                    |
| RF-16         | HU-014, HU-053            | RF-40         | HU-061                    |
| RF-17         | HU-054                    | RF-41         | HU-040                    |
| RF-18         | HU-015, HU-019, HU-020    | RF-42         | HU-041, HU-042            |
| RF-19         | HU-016                    | RF-43         | HU-062                    |
| RF-20         | HU-017                    | RF-44         | HU-043, HU-044, HU-046, HU-047 |
| RF-21         | HU-018                    | RF-45         | HU-048, HU-075            |
| RF-22         | HU-055                    | RF-46         | HU-063                    |
| RF-23         | HU-021                    | RF-47         | HU-064                    |
| RF-24         | HU-022, HU-023            | RF-48         | HU-066, HU-067            |
|               |                           | RF-49         | HU-068                    |
|               |                           | RF-50         | HU-069                    |
|               |                           | RF-51         | HU-045, HU-070, HU-071    |
|               |                           | RF-52         | HU-073                    |
|               |                           | RF-53         | HU-072, HU-074, HU-075    |

---

## 10. Glosario

| Término                  | Significado                                                                                                       |
| ------------------------ | ----------------------------------------------------------------------------------------------------------------- |
| **OT**                   | Orden de trabajo: el registro de todo lo que se le hace a un vehículo en una visita al taller.                    |
| **VIN**                  | Número de identificación del vehículo, único en el mundo (17 caracteres).                                         |
| **Taller (*tenant*)**    | Cada empresa cliente de PitShield. Sus datos están aislados de los demás talleres.                               |
| **Garantía extendida**   | Compromiso de reparar una pieza o trabajo si falla dentro de un plazo, más allá de la garantía legal.            |
| **Microseguro**          | Póliza de bajo costo respaldada por una aseguradora, que cubre fallas mecánicas definidas.                       |
| **Cobertura**            | Una garantía o microseguro emitido para un vehículo, con su vigencia y condiciones.                              |
| **Reclamo**              | Solicitud para que la cobertura pague una falla.                                                                  |
| **Nota crédito**         | Documento que anula o reduce una factura sin borrarla.                                                            |
| **CUFE**                 | Código único que la DIAN asigna a cada factura electrónica.                                                       |
| ***Webhook***            | Aviso automático que un servicio externo (por ejemplo, la pasarela de pago) envía a PitShield cuando algo ocurre. |
| **Idempotencia**         | Propiedad de una operación que, repetida, produce el mismo resultado (evita pagos duplicados).                   |
| **RBAC**                 | Control de acceso basado en roles.                                                                                |
| **Chatbot**              | Asistente que conversa en lenguaje natural con el cliente o con el personal.                                     |
| **LLM**                  | Modelo de lenguaje: la IA que entiende y redacta las respuestas del chatbot.                                      |
| **KPI**                  | Indicador clave de desempeño, por ejemplo el ticket promedio o la tasa de aprobación de presupuestos.            |
| **Ticket promedio**      | Valor promedio facturado por orden de trabajo.                                                                    |
| **Siniestralidad**       | Lo que la aseguradora paga en reclamos dividido entre lo que recibe en primas. Mide el riesgo de un producto.    |
