# Historias de Usuario - PitShield Core System

> 🇪🇸 Español · [🇬🇧 English](../en/USER-STORY.md)

> **Documento de Backlog para Producción:** Especificación de Historias de Usuario (HU) con Criterios de Aceptación en formato BDD (Behavior-Driven Development / Gherkin) para el desarrollo de la plataforma PitShield Core System.

| Campo                 | Valor                                                                                  |
| --------------------- | -------------------------------------------------------------------------------------- |
| **Total de HU**       | 75 historias en 13 módulos                                                             |
| **Requerimientos**    | [`REQUERIMIENTOS.md`](REQUERIMIENTOS.md) (RF, RN y RNF citados en cada historia)       |
| **Prioridad**         | Alta (imprescindible para su entrega) · Media (importante) · Baja (deseable)           |
| **Entregas**          | MVP · Entrega 2 · Entrega 3 (ver el plan de entregas en los requerimientos)            |

> Los roles (Administrador de Plataforma, Administrador del Taller, Asesor de Servicio, Técnico, Cajero, Encargado de Inventario, Cliente, Auditor de Aseguradora y Sistema) se describen en la sección 3 de los requerimientos. Las historias de cada módulo no siempre van en orden numérico: las nuevas se agregaron con el siguiente número disponible para no cambiar los identificadores existentes.

---

## Módulos

1. [Módulo 1: Autenticación, Usuarios y Seguridad](#1-módulo-1-autenticación-usuarios-y-seguridad)
2. [Módulo 2: Talleres y Configuración](#2-módulo-2-talleres-y-configuración)
3. [Módulo 3: Clientes, Vehículos e Historial Digital](#3-módulo-3-clientes-vehículos-e-historial-digital)
4. [Módulo 4: Servicios, Agenda y Técnicos](#4-módulo-4-servicios-agenda-y-técnicos)
5. [Módulo 5: Órdenes de Trabajo](#5-módulo-5-órdenes-de-trabajo)
6. [Módulo 6: Inventario, Proveedores y Compras](#6-módulo-6-inventario-proveedores-y-compras)
7. [Módulo 7: Facturación y Pagos](#7-módulo-7-facturación-y-pagos)
8. [Módulo 8: Garantías, Microseguros y Reclamos](#8-módulo-8-garantías-microseguros-y-reclamos)
9. [Módulo 9: Portal del Cliente](#9-módulo-9-portal-del-cliente)
10. [Módulo 10: Notificaciones Automáticas](#10-módulo-10-notificaciones-automáticas)
11. [Módulo 11: Reportes, Estadísticas y Analítica](#11-módulo-11-reportes-estadísticas-y-analítica)
12. [Módulo 12: Inteligencia Artificial y Chatbots](#12-módulo-12-inteligencia-artificial-y-chatbots)
13. [Módulo 13: Administración de la Plataforma](#13-módulo-13-administración-de-la-plataforma)
14. [Reglas transversales de aceptación](#reglas-transversales-de-aceptación)
15. [Definición de terminado](#definición-de-terminado)

---

# 1. Módulo 1: Autenticación, Usuarios y Seguridad

### HU-001: Inicio de Sesión y Control de Acceso por Roles (RBAC)
* **Como:** Usuario del Sistema
* **Quiero:** Iniciar sesión con mis credenciales
* **Para:** Acceder únicamente a las funciones permitidas según mi rol.
* **Prioridad:** Alta · **Entrega:** MVP · **Requerimientos:** RF-01, RN-06, RN-07

```gherkin
Escenario: Inicio de sesión exitoso
  DADO QUE el usuario existe y se encuentra activo
  CUANDO ingrese sus credenciales válidas
  ENTONCES el sistema concede el acceso
  Y muestra únicamente los módulos permitidos para su rol.

Escenario: Credenciales inválidas
  DADO QUE el usuario existe
  CUANDO ingrese una contraseña incorrecta
  ENTONCES el sistema deniega el acceso
  Y muestra un mensaje de credenciales inválidas.

Escenario: Usuario inactivo
  DADO QUE el usuario se encuentra desactivado
  CUANDO intente iniciar sesión con credenciales válidas
  ENTONCES el sistema deniega el acceso
  Y muestra un mensaje indicando que la cuenta no está activa.
```

### HU-002: Recuperación y Cambio de Contraseña
* **Como:** Usuario del Sistema
* **Quiero:** Recuperar o cambiar mi contraseña
* **Para:** Mantener el acceso a mi cuenta de forma segura.
* **Prioridad:** Alta · **Entrega:** MVP · **Requerimientos:** RF-02, RN-07

```gherkin
Escenario: Recuperación de contraseña
  DADO QUE el usuario tiene un correo registrado
  CUANDO solicite recuperar su contraseña
  ENTONCES el sistema envía un enlace temporal al correo registrado
  Y permite establecer una nueva contraseña.

Escenario: Cambio de contraseña autenticado
  DADO QUE el usuario inició sesión
  CUANDO ingrese su contraseña actual y una nueva contraseña válida
  ENTONCES el sistema actualiza la contraseña
  Y confirma la operación.
```

### HU-003: Gestión de Usuarios y Roles
* **Como:** Administrador del Taller
* **Quiero:** Crear, editar, activar, desactivar usuarios y asignar roles
* **Para:** Controlar quién puede utilizar las funciones del sistema.
* **Prioridad:** Alta · **Entrega:** MVP · **Requerimientos:** RF-03

```gherkin
Escenario: Creación de usuario
  DADO QUE el administrador se encuentra en Gestión de Usuarios
  CUANDO registre un usuario con datos válidos y asigne un rol
  ENTONCES el sistema crea la cuenta
  Y la deja disponible según el estado configurado.

Escenario: Desactivación de usuario
  DADO QUE existe un usuario activo
  CUANDO el administrador lo desactive
  ENTONCES el sistema impide nuevos accesos
  Y conserva su historial de acciones.
```

### HU-004: Auditoría de Acciones y Accesos
* **Como:** Administrador del Taller
* **Quiero:** Consultar las acciones relevantes realizadas en el sistema
* **Para:** Mantener trazabilidad y detectar cambios no autorizados.
* **Prioridad:** Media · **Entrega:** MVP · **Requerimientos:** RF-04

```gherkin
Escenario: Registro de una acción auditable
  DADO QUE un usuario modifica un registro crítico
  CUANDO la operación sea completada
  ENTONCES el sistema registra usuario, fecha, hora, acción y registro afectado
  Y conserva la información de auditoría.

Escenario: Consulta de auditoría
  DADO QUE existen eventos registrados
  CUANDO el administrador consulte la auditoría
  ENTONCES el sistema permite filtrar por usuario, fecha, módulo y tipo de acción.
```

### HU-049: Cierre de Sesión y Expiración de la Sesión
* **Como:** Usuario del Sistema
* **Quiero:** Cerrar mi sesión y que se cierre sola cuando quede inactiva
* **Para:** Evitar que otra persona use mi cuenta en un equipo compartido.
* **Prioridad:** Alta · **Entrega:** MVP · **Requerimientos:** RF-01

```gherkin
Escenario: Cierre de sesión
  DADO QUE el usuario tiene una sesión activa
  CUANDO presione "Cerrar Sesión"
  ENTONCES el sistema invalida su sesión
  Y lo redirige a la pantalla de inicio de sesión.

Escenario: Sesión expirada
  DADO QUE la sesión del usuario expiró por inactividad
  CUANDO intente realizar una operación
  ENTONCES el sistema rechaza la operación
  Y solicita iniciar sesión nuevamente sin perder la pantalla en la que estaba.

Escenario: Bloqueo por intentos fallidos
  DADO QUE el usuario ingresó una contraseña incorrecta 5 veces en 15 minutos
  CUANDO intente iniciar sesión de nuevo
  ENTONCES el sistema bloquea la cuenta durante 15 minutos
  Y registra el bloqueo en auditoría.
```

### HU-050: Autorización y Derechos sobre Datos Personales
* **Como:** Cliente
* **Quiero:** Autorizar el tratamiento de mis datos y poder consultarlos, actualizarlos o pedir su eliminación
* **Para:** Mantener el control de mi información personal (Ley 1581 de 2012).
* **Prioridad:** Alta · **Entrega:** MVP · **Requerimientos:** RF-05, RN-19

```gherkin
Escenario: Registro de la autorización
  DADO QUE el asesor registra un cliente nuevo
  CUANDO el cliente acepte la política de tratamiento de datos
  ENTONCES el sistema guarda la fecha, el canal y la versión de la política aceptada.

Escenario: Cliente sin autorización
  DADO QUE el cliente no ha aceptado la política de tratamiento de datos
  CUANDO el asesor intente enviarle comunicaciones
  ENTONCES el sistema bloquea el envío
  Y muestra que falta la autorización.

Escenario: Solicitud de eliminación
  DADO QUE el cliente solicita eliminar sus datos personales
  CUANDO el administrador apruebe la solicitud
  ENTONCES el sistema anonimiza los datos personales del cliente
  Y conserva los documentos fiscales que la ley obliga a guardar.
```

---

# 2. Módulo 2: Talleres y Configuración

### HU-005: Configuración de Datos del Taller
* **Como:** Administrador del Taller
* **Quiero:** Registrar y actualizar los datos comerciales y fiscales del taller
* **Para:** Utilizarlos en facturas, comprobantes y comunicaciones.
* **Prioridad:** Alta · **Entrega:** MVP · **Requerimientos:** RF-06

```gherkin
Escenario: Actualización exitosa
  DADO QUE el administrador se encuentra en Configuración
  CUANDO modifique los datos permitidos y guarde los cambios
  ENTONCES el sistema actualiza el perfil del taller
  Y utiliza los nuevos datos en futuras emisiones.
```

### HU-006: Gestión de Sucursales y Horarios
* **Como:** Administrador del Taller
* **Quiero:** Configurar sucursales, horarios y disponibilidad
* **Para:** Organizar la operación y agenda del taller.
* **Prioridad:** Media · **Entrega:** MVP · **Requerimientos:** RF-08

```gherkin
Escenario: Creación de sucursal
  DADO QUE el administrador tiene permisos de configuración
  CUANDO registre una sucursal con datos válidos
  ENTONCES el sistema crea la sucursal
  Y permite configurar su horario de atención.

Escenario: Actualización de horario
  DADO QUE existe una sucursal
  CUANDO el administrador modifique su horario
  ENTONCES el sistema actualiza la disponibilidad para futuras citas.
```

### HU-051: Configuración de Impuestos y Numeración de Facturas
* **Como:** Administrador del Taller
* **Quiero:** Configurar las tarifas de impuestos, la resolución de facturación y su numeración
* **Para:** Emitir facturas válidas con los consecutivos autorizados.
* **Prioridad:** Alta · **Entrega:** MVP · **Requerimientos:** RF-07, RN-18

```gherkin
Escenario: Registro de la resolución de facturación
  DADO QUE el administrador se encuentra en Configuración
  CUANDO registre el número de resolución, el prefijo, el rango autorizado y la vigencia
  ENTONCES el sistema guarda la resolución
  Y la usa para numerar las siguientes facturas.

Escenario: Rango de numeración agotado
  DADO QUE se emitió la última factura del rango autorizado
  CUANDO el cajero intente emitir otra factura
  ENTONCES el sistema bloquea la emisión
  Y avisa al administrador que debe registrar una nueva resolución.

Escenario: Tarifa de impuesto por concepto
  DADO QUE un servicio o repuesto tiene una tarifa de IVA configurada
  CUANDO se incluya en un presupuesto o factura
  ENTONCES el sistema calcula el impuesto con esa tarifa.
```

---

# 3. Módulo 3: Clientes, Vehículos e Historial Digital

### HU-007: Registro y Vinculación de Cliente
* **Como:** Asesor de Servicio
* **Quiero:** Registrar un cliente y vincularlo a uno o varios vehículos
* **Para:** Mantener la información del propietario y facilitar las comunicaciones.
* **Prioridad:** Alta · **Entrega:** MVP · **Requerimientos:** RF-09

```gherkin
Escenario: Registro y vinculación exitosa
  DADO QUE el cliente no existe
  CUANDO el asesor complete los datos obligatorios y lo vincule a un vehículo
  ENTONCES el sistema crea el perfil
  Y establece la relación entre cliente y vehículo.

Escenario: Cliente existente
  DADO QUE el cliente ya existe
  CUANDO el asesor ingrese un identificador registrado
  ENTONCES el sistema muestra el cliente existente
  Y permite vincular un nuevo vehículo sin duplicar el perfil.
```

### HU-008: Registro de Vehículo e Historial Inicial
* **Como:** Asesor de Servicio
* **Quiero:** Registrar un vehículo ingresando placa, VIN, marca, modelo, año y kilometraje
* **Para:** Crear su hoja de vida digital.
* **Prioridad:** Alta · **Entrega:** MVP · **Requerimientos:** RF-10, RN-08

```gherkin
Escenario: Registro exitoso
  DADO QUE la placa y el VIN no están registrados
  CUANDO el asesor complete los campos obligatorios
  Y presione "Guardar Vehículo"
  ENTONCES el sistema crea el perfil
  Y genera la línea de tiempo inicial.

Escenario: Placa o VIN duplicado
  DADO QUE la placa o VIN ya existe
  CUANDO el usuario intente registrar el vehículo
  ENTONCES el sistema bloquea el duplicado
  Y muestra el registro existente.
```

### HU-009: Consulta del Historial Digital
* **Como:** Técnico del Taller
* **Quiero:** Buscar un vehículo por placa o VIN
* **Para:** Consultar intervenciones, repuestos, evidencias y garantías asociadas.
* **Prioridad:** Alta · **Entrega:** MVP · **Requerimientos:** RF-11, RN-08

```gherkin
Escenario: Consulta exitosa
  DADO QUE el vehículo tiene historial registrado
  CUANDO el técnico lo busque por placa o VIN
  ENTONCES el sistema muestra el historial ordenado cronológicamente
  Y permite consultar las evidencias autorizadas.

Escenario: Vehículo no encontrado
  DADO QUE el vehículo no existe
  CUANDO el técnico realice la búsqueda
  ENTONCES el sistema informa que no fue encontrado
  Y ofrece iniciar su registro si tiene permisos.
```

### HU-010: Transferencia de Propiedad del Vehículo
* **Como:** Administrador / Asesor de Servicio
* **Quiero:** Cambiar el propietario asociado a un vehículo
* **Para:** Mantener la continuidad del historial sin eliminar información anterior.
* **Prioridad:** Media · **Entrega:** MVP · **Requerimientos:** RF-12

```gherkin
Escenario: Transferencia exitosa
  DADO QUE el vehículo tiene un propietario actual
  CUANDO el usuario autorizado registre al nuevo propietario y confirme la transferencia
  ENTONCES el sistema actualiza el propietario vigente
  Y conserva el historial previo del vehículo.

Escenario: Trazabilidad de transferencia
  DADO QUE se realizó una transferencia
  CUANDO se consulte la auditoría
  ENTONCES el sistema muestra quién realizó el cambio, cuándo y qué propietarios estuvieron asociados.
```

### HU-011: Inmutabilidad y Auditoría del Historial
* **Como:** Administrador del Taller
* **Quiero:** Garantizar la trazabilidad de los eventos críticos del historial vehicular
* **Para:** Evitar la eliminación o modificación no controlada de información histórica.
* **Prioridad:** Alta · **Entrega:** MVP · **Requerimientos:** RF-13

```gherkin
Escenario: Intento de eliminar registro histórico
  DADO QUE existe un registro histórico asociado a una OT finalizada
  CUANDO un usuario intente eliminarlo
  ENTONCES el sistema bloquea la eliminación
  Y registra el intento en auditoría.

Escenario: Corrección de información
  DADO QUE existe información que requiere corrección
  CUANDO un usuario autorizado realice un cambio permitido
  ENTONCES el sistema conserva el valor anterior
  Y registra el nuevo valor, usuario, fecha y motivo.
```

### HU-052: Búsqueda y Actualización de Clientes
* **Como:** Asesor de Servicio
* **Quiero:** Buscar clientes por documento, nombre, teléfono o placa y actualizar sus datos
* **Para:** Atenderlos rápido y mantener su información de contacto al día.
* **Prioridad:** Alta · **Entrega:** MVP · **Requerimientos:** RF-09

```gherkin
Escenario: Búsqueda de cliente
  DADO QUE existen clientes registrados en el taller
  CUANDO el asesor escriba al menos 3 caracteres del documento, nombre, teléfono o placa
  ENTONCES el sistema muestra los clientes que coinciden
  Y sus vehículos vinculados.

Escenario: Actualización de datos de contacto
  DADO QUE el cliente cambió su teléfono o correo
  CUANDO el asesor actualice los datos y guarde
  ENTONCES el sistema guarda los nuevos datos
  Y registra el valor anterior en auditoría.

Escenario: Documento duplicado
  DADO QUE ya existe un cliente con el mismo tipo y número de documento
  CUANDO el asesor intente asignar ese documento a otro cliente
  ENTONCES el sistema bloquea el cambio
  Y muestra el cliente existente.
```

---

# 4. Módulo 4: Servicios, Agenda y Técnicos

### HU-012: Gestión del Catálogo de Servicios
* **Como:** Administrador del Taller
* **Quiero:** Crear, editar, activar o desactivar servicios
* **Para:** Mantener actualizado el catálogo que puede ofrecer el taller.
* **Prioridad:** Alta · **Entrega:** MVP · **Requerimientos:** RF-14

```gherkin
Escenario: Crear servicio
  DADO QUE el administrador tiene permisos
  CUANDO registre nombre, descripción, precio y duración estimada válidos
  ENTONCES el sistema crea el servicio
  Y lo deja disponible para presupuestos y citas.

Escenario: Desactivar servicio
  DADO QUE existe un servicio activo
  CUANDO el administrador lo desactive
  ENTONCES no estará disponible para nuevas citas
  Y conservará su uso en registros históricos.
```

### HU-013: Gestión de Citas y Agenda
* **Como:** Cliente / Asesor de Servicio
* **Quiero:** Crear, consultar, confirmar, reprogramar y cancelar citas
* **Para:** Organizar la atención del taller.
* **Prioridad:** Media · **Entrega:** MVP · **Requerimientos:** RF-15

```gherkin
Escenario: Creación de cita
  DADO QUE existe disponibilidad para el servicio solicitado
  CUANDO el usuario seleccione vehículo, servicio, fecha y hora
  ENTONCES el sistema crea la cita
  Y registra su estado como "Pendiente" o "Confirmada" según el flujo configurado.

Escenario: Horario no disponible
  DADO QUE el horario ya está ocupado
  CUANDO el usuario intente reservarlo
  ENTONCES el sistema bloquea la reserva
  Y muestra horarios disponibles.

Escenario: Reprogramación
  DADO QUE existe una cita activa
  CUANDO un usuario autorizado seleccione un nuevo horario disponible
  ENTONCES el sistema actualiza la cita
  Y conserva el historial de la modificación.
```

### HU-014: Asignación de Técnico a Orden de Trabajo
* **Como:** Asesor de Servicio / Administrador
* **Quiero:** Asignar uno o varios técnicos a una OT
* **Para:** Definir responsables de la ejecución del servicio.
* **Prioridad:** Alta · **Entrega:** MVP · **Requerimientos:** RF-16

```gherkin
Escenario: Asignación exitosa
  DADO QUE existe una OT pendiente de ejecución
  CUANDO el asesor seleccione un técnico disponible
  ENTONCES el sistema lo asigna a la OT
  Y registra la fecha y usuario que realizó la asignación.

Escenario: Técnico no disponible
  DADO QUE el técnico no tiene disponibilidad para el periodo requerido
  CUANDO el asesor intente asignarlo
  ENTONCES el sistema advierte la indisponibilidad
  Y solicita seleccionar otro técnico o periodo.
```

### HU-053: Registro de Tiempos de Mano de Obra
* **Como:** Técnico del Taller
* **Quiero:** Iniciar, pausar y terminar el registro de tiempo en las tareas de una OT
* **Para:** Que el taller conozca el tiempo real de cada trabajo y lo facture correctamente.
* **Prioridad:** Media · **Entrega:** MVP · **Requerimientos:** RF-16

```gherkin
Escenario: Registro de tiempo
  DADO QUE el técnico está asignado a una OT en estado "En Proceso"
  CUANDO inicie y luego termine una tarea
  ENTONCES el sistema registra la duración
  Y la suma a la mano de obra de la OT.

Escenario: Tarea sin asignación
  DADO QUE el técnico no está asignado a la OT
  CUANDO intente registrar tiempo en ella
  ENTONCES el sistema bloquea el registro.

Escenario: Tiempo mayor al estimado
  DADO QUE el tiempo registrado supera la duración estimada del servicio
  CUANDO el técnico termine la tarea
  ENTONCES el sistema alerta al asesor
  Y solicita una observación del técnico.
```

---

# 5. Módulo 5: Órdenes de Trabajo

### HU-015: Creación de Orden de Trabajo
* **Como:** Asesor de Servicio
* **Quiero:** Crear una Orden de Trabajo asociada a un cliente, vehículo y servicios solicitados
* **Para:** Iniciar formalmente la atención del vehículo.
* **Prioridad:** Alta · **Entrega:** MVP · **Requerimientos:** RF-18

```gherkin
Escenario: Creación de OT
  DADO QUE el cliente y vehículo están registrados
  CUANDO el asesor seleccione los servicios solicitados
  Y guarde la orden
  ENTONCES el sistema genera un código único de OT
  Y la crea en estado "Borrador".
```

### HU-016: Diagnóstico y Evidencias del Vehículo
* **Como:** Técnico del Taller
* **Quiero:** Registrar síntomas, diagnóstico, observaciones y evidencias
* **Para:** Documentar técnicamente el estado del vehículo.
* **Prioridad:** Alta · **Entrega:** MVP · **Requerimientos:** RF-19

```gherkin
Escenario: Registro de diagnóstico
  DADO QUE existe una OT en estado editable
  CUANDO el técnico registre el diagnóstico y cargue las evidencias requeridas
  ENTONCES el sistema guarda la información
  Y la asocia a la OT y al historial del vehículo.

Escenario: Evidencia obligatoria
  DADO QUE un servicio requiere evidencia de ingreso
  CUANDO el técnico intente avanzar sin cargarla
  ENTONCES el sistema bloquea el avance
  Y solicita la evidencia faltante.
```

### HU-017: Generación de Presupuesto
* **Como:** Asesor de Servicio
* **Quiero:** Generar un presupuesto con servicios, repuestos, mano de obra, impuestos y descuentos
* **Para:** Presentar al cliente el costo estimado antes de ejecutar trabajos adicionales.
* **Prioridad:** Alta · **Entrega:** MVP · **Requerimientos:** RF-20, RN-09, RN-18

```gherkin
Escenario: Presupuesto generado
  DADO QUE la OT contiene servicios y costos válidos
  CUANDO el asesor genere el presupuesto
  ENTONCES el sistema calcula subtotales, impuestos, descuentos y total
  Y registra la versión del presupuesto.

Escenario: Modificación del presupuesto
  DADO QUE el presupuesto aún no ha sido aprobado
  CUANDO el asesor modifique sus conceptos
  ENTONCES el sistema recalcula el total
  Y conserva la trazabilidad de la versión anterior.
```

### HU-018: Aprobación Remota del Presupuesto
* **Como:** Propietario del Vehículo
* **Quiero:** Revisar y aprobar o rechazar el presupuesto desde mi teléfono
* **Para:** Autorizar los trabajos sin desplazarme al taller.
* **Prioridad:** Media · **Entrega:** Entrega 2 · **Requerimientos:** RF-21, RN-09

```gherkin
Escenario: Aprobación
  DADO QUE el cliente recibió un presupuesto vigente
  CUANDO revise el detalle y presione "Aprobar Trabajo"
  ENTONCES el sistema registra la aprobación
  Y cambia la OT al estado correspondiente.

Escenario: Rechazo
  DADO QUE el cliente recibió un presupuesto vigente
  CUANDO presione "Rechazar Trabajo" e indique el motivo
  ENTONCES el sistema registra el rechazo
  Y notifica al taller.
```

### HU-019: Gestión del Ciclo de Vida de la OT
* **Como:** Administrador / Asesor de Servicio
* **Quiero:** Controlar los estados de una OT
* **Para:** Garantizar que las operaciones ocurran en el orden correcto.
* **Prioridad:** Alta · **Entrega:** MVP · **Requerimientos:** RF-18, RN-05, RN-10

```gherkin
Escenario: Avance de estado válido
  DADO QUE la OT cumple las condiciones del estado actual
  CUANDO un usuario autorizado solicite avanzar
  ENTONCES el sistema cambia al siguiente estado permitido
  Y registra la transición en auditoría.

Escenario: Cambio de estado no permitido
  DADO QUE la OT no cumple las condiciones requeridas
  CUANDO el usuario intente avanzar
  ENTONCES el sistema bloquea la transición
  Y muestra las condiciones pendientes.
```

> **Flujo de estados (RN-10):** Borrador → Pendiente de Aprobación → Aprobada → En Proceso ⇄ En Espera → Finalizada → Lista para Entrega → Entregada. "Cancelada" solo es posible antes de "Finalizada".

### HU-020: Cancelación y Modificación Controlada de OT
* **Como:** Asesor de Servicio / Administrador
* **Quiero:** Cancelar o modificar una OT según su estado
* **Para:** Reflejar cambios solicitados por el cliente o imprevistos operativos.
* **Prioridad:** Media · **Entrega:** MVP · **Requerimientos:** RF-18, RN-10, RN-20

```gherkin
Escenario: Cancelación de OT
  DADO QUE la OT se encuentra en un estado que permite cancelación
  CUANDO el usuario autorizado indique un motivo y confirme
  ENTONCES el sistema cambia la OT a "Cancelada"
  Y ejecuta las operaciones de inventario y facturación correspondientes.

Escenario: Modificación no permitida
  DADO QUE la OT se encuentra en un estado cerrado
  CUANDO el usuario intente modificarla
  ENTONCES el sistema bloquea la edición
  Y registra el intento si corresponde.
```

### HU-054: Recepción del Vehículo
* **Como:** Asesor de Servicio
* **Quiero:** Registrar el estado del vehículo al momento de recibirlo
* **Para:** Dejar constancia de cómo llegó y evitar disputas con el cliente.
* **Prioridad:** Alta · **Entrega:** MVP · **Requerimientos:** RF-17

```gherkin
Escenario: Recepción registrada
  DADO QUE el vehículo llega al taller
  CUANDO el asesor registre kilometraje, nivel de combustible, daños visibles, objetos dejados y fotos de ingreso
  ENTONCES el sistema guarda la recepción
  Y la asocia a la OT y al historial del vehículo.

Escenario: Kilometraje menor al último registrado
  DADO QUE el historial tiene un kilometraje mayor al ingresado
  CUANDO el asesor guarde la recepción
  ENTONCES el sistema muestra una alerta
  Y exige una observación que justifique la diferencia.

Escenario: Constancia para el cliente
  DADO QUE la recepción fue registrada
  CUANDO el asesor la confirme
  ENTONCES el sistema genera una constancia de recepción
  Y la envía al cliente por el canal configurado.
```

### HU-055: Entrega del Vehículo al Cliente
* **Como:** Asesor de Servicio
* **Quiero:** Registrar la entrega del vehículo con la conformidad del cliente
* **Para:** Cerrar la atención y dejar constancia del estado de salida.
* **Prioridad:** Alta · **Entrega:** MVP · **Requerimientos:** RF-22

```gherkin
Escenario: Entrega exitosa
  DADO QUE la OT está en "Lista para Entrega"
  CUANDO el asesor registre el kilometraje de salida y la conformidad del cliente
  ENTONCES el sistema cambia la OT a "Entregada"
  Y agrega la entrega al historial del vehículo.

Escenario: Entrega con saldo pendiente
  DADO QUE la factura de la OT tiene saldo pendiente
  CUANDO el asesor intente registrar la entrega
  ENTONCES el sistema advierte el saldo pendiente
  Y solo permite continuar con autorización del Administrador del Taller.

Escenario: Inconformidad del cliente
  DADO QUE el cliente no está conforme con el trabajo
  CUANDO el asesor registre la inconformidad y su motivo
  ENTONCES el sistema la guarda en la OT
  Y notifica al Administrador del Taller.
```

---

# 6. Módulo 6: Inventario, Proveedores y Compras

### HU-021: Gestión de Repuestos y Stock
* **Como:** Encargado de Inventario
* **Quiero:** Consultar y administrar existencias de repuestos
* **Para:** Mantener control del inventario disponible.
* **Prioridad:** Alta · **Entrega:** MVP · **Requerimientos:** RF-23, RN-17

```gherkin
Escenario: Consulta de stock
  DADO QUE existen repuestos registrados
  CUANDO el encargado consulte inventario
  ENTONCES el sistema muestra existencias disponibles, reservadas y utilizadas.

Escenario: Stock mínimo
  DADO QUE un repuesto alcanza o baja del stock mínimo configurado
  CUANDO el sistema actualice el inventario
  ENTONCES genera una alerta de reposición.
```

### HU-022: Reserva y Consumo de Repuestos
* **Como:** Sistema / Encargado de Inventario
* **Quiero:** Reservar y descontar repuestos según el avance de una OT
* **Para:** Evitar descuadres entre stock disponible y piezas realmente utilizadas.
* **Prioridad:** Alta · **Entrega:** MVP · **Requerimientos:** RF-24, RN-05, RN-17

```gherkin
Escenario: Reserva de stock
  DADO QUE una OT aprobada requiere 2 unidades de un repuesto
  CUANDO el sistema confirme la ejecución
  ENTONCES reserva las 2 unidades
  Y reduce el stock disponible sin marcarlas todavía como consumidas.

Escenario: Consumo
  DADO QUE las piezas fueron utilizadas
  CUANDO el técnico registre el consumo
  ENTONCES el sistema las marca como consumidas
  Y actualiza el inventario.
```

### HU-023: Devolución y Ajuste de Inventario
* **Como:** Encargado de Inventario
* **Quiero:** Registrar devoluciones y ajustes por avería, merma o corrección
* **Para:** Mantener el inventario físico y digital sincronizado.
* **Prioridad:** Media · **Entrega:** MVP · **Requerimientos:** RF-24, RN-17

```gherkin
Escenario: Devolución de repuesto no utilizado
  DADO QUE una pieza está reservada pero no fue utilizada
  CUANDO el encargado registre su devolución
  ENTONCES el sistema libera la reserva
  Y devuelve la cantidad al stock disponible.

Escenario: Ajuste por merma
  DADO QUE existe una diferencia física justificada
  CUANDO el encargado registre el ajuste con motivo
  ENTONCES el sistema actualiza el stock
  Y registra el movimiento en auditoría.
```

### HU-024: Gestión de Proveedores y Órdenes de Compra
* **Como:** Encargado de Inventario
* **Quiero:** Registrar proveedores y órdenes de compra
* **Para:** Controlar el abastecimiento de repuestos.
* **Prioridad:** Media · **Entrega:** MVP · **Requerimientos:** RF-25

```gherkin
Escenario: Registro de proveedor
  DADO QUE el proveedor no existe
  CUANDO el encargado registre sus datos
  ENTONCES el sistema crea el proveedor.

Escenario: Recepción de compra
  DADO QUE existe una orden de compra pendiente
  CUANDO el encargado registre la recepción de 10 unidades
  ENTONCES el sistema incrementa el stock
  Y registra el costo unitario de la compra.
```

---

# 7. Módulo 7: Facturación y Pagos

### HU-025: Conversión de OT a Factura
* **Como:** Administrador / Cajero
* **Quiero:** Generar una factura a partir de una OT finalizada
* **Para:** Formalizar el cobro del servicio.
* **Prioridad:** Alta · **Entrega:** MVP · **Requerimientos:** RF-26, RN-02, RN-11

```gherkin
Escenario: Generación de factura
  DADO QUE la OT está finalizada y contiene un total válido
  CUANDO el cajero genere la factura
  ENTONCES el sistema crea un documento único
  Y conserva la relación con la OT.
```

### HU-026: Cobro Remoto y Link de Pago
* **Como:** Administrador / Cajero
* **Quiero:** Enviar un enlace de pago al cliente
* **Para:** Facilitar el pago remoto.
* **Prioridad:** Media · **Entrega:** Entrega 2 · **Requerimientos:** RF-29

```gherkin
Escenario: Envío de link
  DADO QUE existe una factura pendiente
  CUANDO el cajero solicite el link de pago
  ENTONCES el sistema genera un enlace asociado a la factura
  Y lo envía mediante el canal configurado.

Escenario: Pago rechazado
  DADO QUE el cliente intenta pagar una factura
  CUANDO la pasarela rechace la transacción
  ENTONCES la factura permanece pendiente
  Y el sistema registra el resultado del intento.
```

### HU-027: Confirmación de Pago mediante Webhook
* **Como:** Sistema
* **Quiero:** Actualizar el estado de una factura al recibir la confirmación de la pasarela
* **Para:** Mantener sincronizados pagos y facturación.
* **Prioridad:** Media · **Entrega:** Entrega 2 · **Requerimientos:** RF-29, RN-12, RN-13

```gherkin
Escenario: Pago exitoso
  DADO QUE existe una factura pendiente
  CUANDO el webhook válido confirme el pago
  ENTONCES el sistema registra la transacción
  Y marca la factura como "Pagada".

Escenario: Webhook duplicado
  DADO QUE un pago ya fue registrado
  CUANDO la pasarela envíe nuevamente el mismo evento
  ENTONCES el sistema no duplica el pago
  Y mantiene un único registro de la transacción.
```

### HU-028: Notas Crédito y Reembolsos
* **Como:** Administrador / Cajero
* **Quiero:** Anular o ajustar facturas y gestionar reembolsos
* **Para:** Mantener la trazabilidad contable sin eliminar documentos.
* **Prioridad:** Media · **Entrega:** MVP · **Requerimientos:** RF-30, RN-02

```gherkin
Escenario: Nota crédito
  DADO QUE existe una factura emitida que requiere ajuste
  CUANDO el administrador registre el motivo
  ENTONCES el sistema genera la nota crédito correspondiente
  Y conserva la factura original.

Escenario: Reembolso
  DADO QUE existe un pago susceptible de devolución
  CUANDO el usuario autorizado solicite un reembolso
  ENTONCES el sistema registra la solicitud
  Y actualiza el estado según la respuesta de la pasarela.
```

### HU-056: Pago Presencial y Pagos Parciales
* **Como:** Cajero
* **Quiero:** Registrar pagos en efectivo, tarjeta o transferencia, completos o parciales
* **Para:** Llevar el control exacto de lo que paga cada cliente.
* **Prioridad:** Alta · **Entrega:** MVP · **Requerimientos:** RF-28, RN-13

```gherkin
Escenario: Pago completo
  DADO QUE existe una factura pendiente por $500.000
  CUANDO el cajero registre un pago en efectivo por $500.000
  ENTONCES el sistema marca la factura como "Pagada"
  Y genera el comprobante de pago.

Escenario: Pago parcial
  DADO QUE existe una factura pendiente por $500.000
  CUANDO el cajero registre un abono por $200.000
  ENTONCES el sistema deja la factura en "Pago Parcial"
  Y muestra un saldo pendiente de $300.000.

Escenario: Pago mayor al saldo
  DADO QUE la factura tiene un saldo de $300.000
  CUANDO el cajero intente registrar un pago por $350.000
  ENTONCES el sistema bloquea el registro
  Y muestra el saldo máximo permitido.
```

### HU-057: Emisión de Factura Electrónica
* **Como:** Sistema
* **Quiero:** Enviar cada factura al proveedor tecnológico de facturación electrónica
* **Para:** Que la factura sea válida ante la DIAN.
* **Prioridad:** Media · **Entrega:** Entrega 2 · **Requerimientos:** RF-27, RNF-05

```gherkin
Escenario: Factura validada
  DADO QUE el cajero emitió una factura
  CUANDO el proveedor tecnológico la valide ante la DIAN
  ENTONCES el sistema guarda el CUFE y el estado "Validada"
  Y envía al cliente el PDF y el XML de la factura.

Escenario: Factura rechazada
  DADO QUE el proveedor rechaza la factura por un error en los datos
  CUANDO el sistema reciba la respuesta
  ENTONCES marca la factura como "Rechazada por la DIAN"
  Y muestra al cajero el motivo para corregirlo.

Escenario: Proveedor no disponible
  DADO QUE el proveedor tecnológico no responde
  CUANDO el sistema intente enviar la factura
  ENTONCES reintenta el envío automáticamente
  Y alerta al administrador si no logra enviarla en 24 horas.
```

---

# 8. Módulo 8: Garantías, Microseguros y Reclamos

> **Nota funcional:** El producto debe definir claramente si PitShield comercializa garantías extendidas, microseguros o ambos. Las HU siguientes contemplan ambos conceptos sin asumir que jurídicamente sean equivalentes.

### HU-029: Evaluación de Elegibilidad
* **Como:** Asesor de Servicio
* **Quiero:** Consultar si un vehículo y servicio cumplen las condiciones de cobertura
* **Para:** Ofrecer únicamente productos para los que el cliente sea elegible.
* **Prioridad:** Alta · **Entrega:** Entrega 2 · **Requerimientos:** RF-32, RN-01

```gherkin
Escenario: Vehículo elegible
  DADO QUE el vehículo cumple las condiciones configuradas
  CUANDO el asesor consulte la elegibilidad
  ENTONCES el sistema muestra el producto disponible
  Y presenta precio, cobertura y vigencia.

Escenario: Vehículo no elegible
  DADO QUE el vehículo no cumple una condición
  CUANDO el asesor consulte la elegibilidad
  ENTONCES el sistema indica que no es elegible
  Y muestra el motivo.
```

### HU-030: Emisión de Garantía o Microseguro
* **Como:** Asesor de Servicio
* **Quiero:** Emitir el producto de protección seleccionado por el cliente
* **Para:** Activar su cobertura y generar el certificado correspondiente.
* **Prioridad:** Alta · **Entrega:** Entrega 2 · **Requerimientos:** RF-32, RN-03, RN-04

```gherkin
Escenario: Emisión exitosa
  DADO QUE el cliente acepta el producto y cumple la elegibilidad
  CUANDO finalice la compra
  ENTONCES el sistema registra la cobertura
  Y genera un certificado o póliza digital con su estado y vigencia.

Escenario: Emisión fallida
  DADO QUE la entidad emisora no confirma la emisión
  CUANDO el sistema procese la solicitud
  ENTONCES no activa la cobertura
  Y registra el resultado para seguimiento.
```

### HU-031: Consulta y Seguimiento de Cobertura
* **Como:** Cliente / Asesor
* **Quiero:** Consultar las coberturas activas y su vigencia
* **Para:** Conocer qué servicios o componentes están protegidos.
* **Prioridad:** Media · **Entrega:** Entrega 2 · **Requerimientos:** RF-33

```gherkin
Escenario: Consulta de cobertura
  DADO QUE existe una cobertura activa
  CUANDO el usuario consulte el vehículo
  ENTONCES el sistema muestra vigencia, cobertura, estado y condiciones principales.
```

### HU-032: Radicación y Seguimiento de Reclamos
* **Como:** Administrador del Taller
* **Quiero:** Radicar un reclamo con evidencias y consultar su estado
* **Para:** Gestionar la solicitud de cobertura hasta su resolución.
* **Prioridad:** Alta · **Entrega:** Entrega 2 · **Requerimientos:** RF-34, RN-14

```gherkin
Escenario: Radicación
  DADO QUE la cobertura está activa
  CUANDO el administrador cargue las evidencias requeridas y describa la falla
  ENTONCES el sistema crea el reclamo
  Y lo registra como "En Revisión".

Escenario: Solicitud de información
  DADO QUE el auditor requiere evidencia adicional
  CUANDO solicite información
  ENTONCES el reclamo pasa a "Información Requerida"
  Y el taller recibe la solicitud.

Escenario: Seguimiento
  DADO QUE existe un reclamo activo
  CUANDO el usuario consulte su estado
  ENTONCES el sistema muestra el estado actual y las actuaciones registradas.
```

### HU-033: Auditoría y Dictamen de Reclamos
* **Como:** Auditor de la Aseguradora
* **Quiero:** Revisar evidencias y aprobar, rechazar o solicitar información
* **Para:** Determinar si el reclamo cumple las condiciones de cobertura.
* **Prioridad:** Alta · **Entrega:** Entrega 2 · **Requerimientos:** RF-34, RN-15

```gherkin
Escenario: Aprobación
  DADO QUE el reclamo tiene evidencia suficiente
  CUANDO el auditor lo apruebe
  ENTONCES el sistema cambia el estado a "Aprobado"
  Y registra el dictamen y auditor.

Escenario: Rechazo
  DADO QUE el reclamo no cumple las condiciones
  CUANDO el auditor lo rechace e indique un motivo
  ENTONCES el sistema cambia el estado a "Rechazado"
  Y notifica al taller.

Escenario: Solicitud de información
  DADO QUE falta evidencia
  CUANDO el auditor solicite información adicional
  ENTONCES el sistema cambia el estado a "Información Requerida"
  Y registra exactamente qué información falta.
```

### HU-058: Vencimiento y Cancelación de Coberturas
* **Como:** Sistema / Administrador del Taller
* **Quiero:** Vencer las coberturas al terminar su vigencia y cancelar las que corresponda
* **Para:** Que solo las coberturas vigentes permitan radicar reclamos.
* **Prioridad:** Media · **Entrega:** Entrega 2 · **Requerimientos:** RF-33

```gherkin
Escenario: Vencimiento automático
  DADO QUE una cobertura llegó a su fecha final
  CUANDO se ejecute la rutina diaria
  ENTONCES el sistema cambia la cobertura a "Vencida"
  Y la muestra así en el historial del vehículo.

Escenario: Aviso de vencimiento próximo
  DADO QUE a una cobertura le faltan 30 días para vencer
  CUANDO se ejecute la rutina diaria
  ENTONCES el sistema notifica al cliente
  Y le ofrece renovarla si el producto lo permite.

Escenario: Cancelación
  DADO QUE el cliente solicita cancelar una cobertura vigente
  CUANDO el administrador registre la cancelación con su motivo
  ENTONCES el sistema cambia la cobertura a "Cancelada"
  Y calcula la devolución según las condiciones del producto.
```

### HU-059: Liquidación de Comisiones
* **Como:** Administrador de Plataforma / Administrador del Taller
* **Quiero:** Consultar y liquidar las comisiones por productos de protección y pagos en línea
* **Para:** Saber cuánto le corresponde a PitShield y cuánto al taller en cada periodo.
* **Prioridad:** Media · **Entrega:** Entrega 2 · **Requerimientos:** RF-35, RN-03

```gherkin
Escenario: Cálculo de comisión
  DADO QUE se emitió una cobertura por $200.000 con comisión de plataforma del 10 %
  CUANDO el sistema registre la emisión
  ENTONCES calcula $20.000 para la plataforma
  Y deja el valor restante según las condiciones del producto.

Escenario: Liquidación mensual
  DADO QUE terminó el periodo de liquidación
  CUANDO el Administrador de Plataforma genere la liquidación de un taller
  ENTONCES el sistema muestra el detalle por cobertura y transacción
  Y marca esas comisiones como liquidadas para no volver a incluirlas.
```

---

# 9. Módulo 9: Portal del Cliente

### HU-034: Consulta de Vehículos e Historial
* **Como:** Cliente
* **Quiero:** Consultar mis vehículos y su historial autorizado
* **Para:** Conocer los servicios realizados y el estado de mis vehículos.
* **Prioridad:** Media · **Entrega:** Entrega 2 · **Requerimientos:** RF-37, RN-08

```gherkin
Escenario: Consulta del historial
  DADO QUE el cliente tiene un vehículo asociado
  CUANDO acceda al portal
  ENTONCES puede consultar los registros que tiene permiso para visualizar
  Y puede revisar las evidencias disponibles.
```

### HU-035: Seguimiento de Orden de Trabajo
* **Como:** Cliente
* **Quiero:** Consultar el estado de mi OT
* **Para:** Conocer el avance del servicio.
* **Prioridad:** Media · **Entrega:** Entrega 2 · **Requerimientos:** RF-37

```gherkin
Escenario: Consulta de estado
  DADO QUE existe una OT asociada al cliente
  CUANDO acceda al portal
  ENTONCES el sistema muestra su estado actual
  Y la información relevante autorizada por el taller.
```

### HU-036: Consulta de Facturas y Pagos
* **Como:** Cliente
* **Quiero:** Consultar mis facturas y estados de pago
* **Para:** Mantener control de mis obligaciones y transacciones.
* **Prioridad:** Media · **Entrega:** Entrega 2 · **Requerimientos:** RF-37

```gherkin
Escenario: Consulta de factura
  DADO QUE existe una factura asociada al cliente
  CUANDO acceda al portal
  ENTONCES puede consultar el documento y su estado de pago.

Escenario: Factura pendiente
  DADO QUE la factura está pendiente
  CUANDO el cliente la consulte
  ENTONCES el sistema muestra una opción de pago si está disponible.
```

### HU-037: Consulta de Garantías y Reclamos
* **Como:** Cliente
* **Quiero:** Consultar mis garantías y reclamos
* **Para:** Conocer las coberturas y el avance de solicitudes.
* **Prioridad:** Media · **Entrega:** Entrega 2 · **Requerimientos:** RF-37

```gherkin
Escenario: Consulta de garantía
  DADO QUE existe una cobertura asociada al vehículo
  CUANDO el cliente la consulte
  ENTONCES el sistema muestra vigencia, estado y cobertura.

Escenario: Consulta de reclamo
  DADO QUE existe un reclamo asociado
  CUANDO el cliente acceda al portal
  ENTONCES puede consultar su estado y las actualizaciones permitidas.
```

### HU-060: Invitación y Activación del Portal del Cliente
* **Como:** Cliente
* **Quiero:** Recibir una invitación para activar mi cuenta en el portal
* **Para:** Consultar mis vehículos y servicios sin llamar al taller.
* **Prioridad:** Media · **Entrega:** Entrega 2 · **Requerimientos:** RF-36

```gherkin
Escenario: Activación exitosa
  DADO QUE el asesor registró al cliente con un correo válido
  CUANDO el cliente abra el enlace de invitación y cree su contraseña
  ENTONCES el sistema activa su cuenta
  Y le muestra únicamente sus vehículos.

Escenario: Invitación vencida
  DADO QUE el enlace de invitación tiene más de 7 días
  CUANDO el cliente intente usarlo
  ENTONCES el sistema informa que venció
  Y le permite solicitar uno nuevo.

Escenario: Cliente de varios talleres
  DADO QUE el cliente ya tiene cuenta por otro taller
  CUANDO un nuevo taller lo invite
  ENTONCES el sistema vincula el nuevo taller a su misma cuenta
  Y no crea una cuenta duplicada.
```

---

# 10. Módulo 10: Notificaciones Automáticas

### HU-038: Notificaciones de Eventos del Servicio
* **Como:** Sistema
* **Quiero:** Enviar notificaciones automáticas sobre eventos importantes
* **Para:** Mantener informados al cliente y al personal.
* **Prioridad:** Media · **Entrega:** Entrega 2 · **Requerimientos:** RF-38, RN-16

```gherkin
Escenario: Notificación de aprobación
  DADO QUE el cliente aprueba un presupuesto
  CUANDO el sistema registre la aprobación
  ENTONCES notifica al personal correspondiente.

Escenario: Vehículo listo para entrega
  DADO QUE la OT cambia a "Lista para Entrega"
  CUANDO se registre el cambio
  ENTONCES el sistema notifica al cliente mediante el canal configurado.
```

### HU-039: Recordatorios Automáticos de Mantenimiento
* **Como:** Sistema (Job Programado)
* **Quiero:** Detectar vehículos próximos a mantenimiento por tiempo o kilometraje
* **Para:** Incentivar el mantenimiento preventivo.
* **Prioridad:** Baja · **Entrega:** Entrega 2 · **Requerimientos:** RF-39, RN-16

```gherkin
Escenario: Mantenimiento próximo
  DADO QUE un vehículo cumple la condición configurada de tiempo o kilometraje estimado
  CUANDO se ejecute la rutina programada
  ENTONCES el sistema genera un recordatorio
  Y proporciona una opción para agendar una cita.

Escenario: Evitar notificaciones duplicadas
  DADO QUE ya se envió un recordatorio para la misma condición
  CUANDO vuelva a ejecutarse la rutina
  ENTONCES el sistema evita enviar notificaciones duplicadas dentro del periodo configurado.
```

### HU-061: Preferencias y Autorización de Notificaciones
* **Como:** Cliente
* **Quiero:** Elegir por qué canales recibo mensajes y dejar de recibirlos si lo deseo
* **Para:** Recibir solo la información que me interesa.
* **Prioridad:** Media · **Entrega:** Entrega 2 · **Requerimientos:** RF-40, RN-16, RN-19

```gherkin
Escenario: Cambio de canal
  DADO QUE el cliente tiene activos correo y WhatsApp
  CUANDO desactive WhatsApp en su portal
  ENTONCES el sistema deja de enviarle mensajes por WhatsApp
  Y sigue usando el correo.

Escenario: Retiro de autorización para recordatorios
  DADO QUE el cliente retiró su autorización para mensajes comerciales y recordatorios
  CUANDO se ejecute la rutina de recordatorios
  ENTONCES el sistema no le envía recordatorios
  Y solo le envía mensajes necesarios del servicio en curso.
```

---

# 11. Módulo 11: Reportes, Estadísticas y Analítica

### HU-040: Dashboard Financiero
* **Como:** Dueño / Gerente del Taller
* **Quiero:** Consultar indicadores financieros
* **Para:** Evaluar ingresos, cobros, pagos pendientes y rentabilidad.
* **Prioridad:** Media · **Entrega:** Entrega 3 · **Requerimientos:** RF-41

```gherkin
Escenario: Consulta mensual
  DADO QUE existen transacciones registradas
  CUANDO el gerente seleccione un periodo
  ENTONCES el sistema muestra ingresos, facturación, pagos pendientes, reembolsos y comisiones aplicables.
```

### HU-041: Reportes Operativos
* **Como:** Dueño / Gerente del Taller
* **Quiero:** Consultar indicadores de operación
* **Para:** Evaluar el desempeño del taller.
* **Prioridad:** Media · **Entrega:** Entrega 3 · **Requerimientos:** RF-42

```gherkin
Escenario: Consulta operativa
  DADO QUE existen OT y servicios registrados
  CUANDO el gerente consulte un periodo
  ENTONCES el sistema muestra OT abiertas, finalizadas, canceladas, tiempos de atención y servicios realizados.
```

### HU-042: Reportes de Inventario
* **Como:** Encargado de Inventario / Gerente
* **Quiero:** Consultar movimientos y niveles de inventario
* **Para:** Tomar decisiones de abastecimiento.
* **Prioridad:** Baja · **Entrega:** Entrega 3 · **Requerimientos:** RF-42

```gherkin
Escenario: Reporte de inventario
  DADO QUE existen movimientos registrados
  CUANDO el usuario consulte un periodo
  ENTONCES el sistema muestra entradas, consumos, devoluciones, ajustes y productos con stock crítico.
```

### HU-062: Exportación de Reportes
* **Como:** Dueño / Gerente del Taller
* **Quiero:** Exportar los reportes a CSV y PDF
* **Para:** Compartirlos con mi contador o analizarlos en otras herramientas.
* **Prioridad:** Baja · **Entrega:** Entrega 3 · **Requerimientos:** RF-43

```gherkin
Escenario: Exportación a CSV
  DADO QUE el gerente consulta un reporte con filtros
  CUANDO presione "Exportar CSV"
  ENTONCES el sistema descarga un archivo con los mismos datos y filtros del reporte.

Escenario: Exportación a PDF
  DADO QUE el gerente consulta un reporte
  CUANDO presione "Exportar PDF"
  ENTONCES el sistema genera un PDF con el logo del taller, el periodo y la fecha de generación.

Escenario: Reporte sin datos
  DADO QUE el periodo seleccionado no tiene registros
  CUANDO el gerente intente exportar
  ENTONCES el sistema informa que no hay datos para exportar.
```

### HU-066: Tablero de Indicadores Clave del Taller
* **Como:** Dueño / Gerente del Taller
* **Quiero:** Ver los indicadores clave del taller con su tendencia
* **Para:** Saber de un vistazo cómo va el negocio y dónde mejorar.
* **Prioridad:** Media · **Entrega:** Entrega 3 · **Requerimientos:** RF-48

```gherkin
Escenario: Consulta de indicadores
  DADO QUE existen órdenes, facturas y coberturas registradas
  CUANDO el gerente abra el tablero y seleccione un periodo
  ENTONCES el sistema muestra el ticket promedio, la tasa de aprobación de presupuestos, la tasa de clientes que regresan, el tiempo promedio de atención y el porcentaje de servicios vendidos con cobertura
  Y compara cada indicador con el periodo anterior.

Escenario: Detalle de un indicador
  DADO QUE el gerente ve un indicador en el tablero
  CUANDO haga clic en él
  ENTONCES el sistema muestra su gráfica por día, semana o mes
  Y los registros que lo componen.

Escenario: Periodo sin datos
  DADO QUE el periodo seleccionado no tiene registros
  CUANDO el gerente consulte el tablero
  ENTONCES el sistema indica que no hay datos para ese periodo
  Y no muestra valores en cero que puedan confundirse con resultados reales.
```

### HU-067: Estadísticas de Servicios y Técnicos
* **Como:** Dueño / Gerente del Taller
* **Quiero:** Ver qué servicios se venden más y cómo rinde cada técnico
* **Para:** Planear el personal, el inventario y las promociones.
* **Prioridad:** Media · **Entrega:** Entrega 3 · **Requerimientos:** RF-48

```gherkin
Escenario: Servicios más solicitados
  DADO QUE existen servicios facturados
  CUANDO el gerente consulte un periodo
  ENTONCES el sistema muestra el ranking de servicios por cantidad e ingresos
  Y su participación porcentual en el total.

Escenario: Productividad por técnico
  DADO QUE los técnicos registraron tiempos de mano de obra
  CUANDO el gerente consulte un periodo
  ENTONCES el sistema muestra por técnico las horas registradas, las OT terminadas y el tiempo real frente al estimado.

Escenario: Comportamiento por día y hora
  DADO QUE existen citas y órdenes registradas
  CUANDO el gerente consulte la demanda
  ENTONCES el sistema muestra un mapa de calor por día de la semana y franja horaria.
```

### HU-068: Analítica de la Plataforma
* **Como:** Administrador de Plataforma
* **Quiero:** Ver estadísticas de uso y de negocio de toda la plataforma
* **Para:** Tomar decisiones sobre el producto y medir su crecimiento.
* **Prioridad:** Media · **Entrega:** Entrega 3 · **Requerimientos:** RF-49, RN-23

```gherkin
Escenario: Indicadores de la plataforma
  DADO QUE existen talleres activos
  CUANDO el Administrador de Plataforma abra la analítica
  ENTONCES el sistema muestra talleres activos, órdenes por mes, ingresos por comisiones, coberturas emitidas y uso de los chatbots.

Escenario: Comparación anónima entre talleres
  DADO QUE un grupo de comparación tiene al menos 5 talleres
  CUANDO el administrador compare indicadores entre talleres
  ENTONCES el sistema muestra promedios y percentiles
  Y no revela el nombre ni los datos de ningún taller.

Escenario: Grupo demasiado pequeño
  DADO QUE un grupo de comparación tiene menos de 5 talleres
  CUANDO el administrador intente compararlo
  ENTONCES el sistema no muestra la comparación
  Y explica que el grupo es muy pequeño para proteger la confidencialidad.
```

### HU-069: Analítica de Coberturas y Siniestralidad
* **Como:** Auditor de la Aseguradora
* **Quiero:** Ver estadísticas de las coberturas y reclamos de mi aseguradora
* **Para:** Evaluar el riesgo y ajustar los productos.
* **Prioridad:** Media · **Entrega:** Entrega 3 · **Requerimientos:** RF-50, RN-23

```gherkin
Escenario: Indicadores de coberturas
  DADO QUE existen coberturas emitidas con la aseguradora
  CUANDO el auditor consulte un periodo
  ENTONCES el sistema muestra coberturas vigentes, primas emitidas, reclamos por estado, valor pagado y siniestralidad (valor pagado sobre primas).

Escenario: Fallas más frecuentes
  DADO QUE existen reclamos aprobados
  CUANDO el auditor consulte las causas
  ENTONCES el sistema muestra las fallas más frecuentes por componente, marca y modelo.

Escenario: Alcance de la información
  DADO QUE el auditor pertenece a la Aseguradora A
  CUANDO consulte la analítica
  ENTONCES el sistema solo muestra coberturas y reclamos de la Aseguradora A.
```

---

# 12. Módulo 12: Inteligencia Artificial y Chatbots

> El módulo incluye **chatbots** para clientes (portal web y WhatsApp) y para el personal del taller, y **agentes de apoyo** para diagnóstico, mantenimiento, inventario y reclamos. Los agentes de IA deben funcionar como **asistentes de apoyo**. Las decisiones técnicas, financieras, de cobertura y aprobación de reclamos que tengan impacto real deben permanecer bajo control de usuarios autorizados.

### HU-043: Agente IA de Diagnóstico Asistido
* **Como:** Técnico del Taller
* **Quiero:** Consultar un agente IA utilizando síntomas, historial y datos del vehículo
* **Para:** Obtener recomendaciones que apoyen el diagnóstico técnico.
* **Prioridad:** Baja · **Entrega:** Entrega 3 · **Requerimientos:** RF-44, RN-15

```gherkin
Escenario: Recomendación de diagnóstico
  DADO QUE existe una OT con información suficiente
  CUANDO el técnico solicite asistencia al agente IA
  ENTONCES el agente analiza la información disponible
  Y presenta posibles causas, verificaciones sugeridas y nivel de confianza.

Escenario: Información insuficiente
  DADO QUE la información disponible no es suficiente
  CUANDO el técnico consulte al agente
  ENTONCES el agente indica qué datos adicionales serían necesarios
  Y no presenta una conclusión como diagnóstico definitivo.
```

### HU-044: Agente IA de Mantenimiento Preventivo
* **Como:** Sistema / Gerente del Taller
* **Quiero:** Analizar el historial y comportamiento del vehículo
* **Para:** Generar recomendaciones de mantenimiento preventivo.
* **Prioridad:** Baja · **Entrega:** Entrega 3 · **Requerimientos:** RF-44, RN-15

```gherkin
Escenario: Recomendación preventiva
  DADO QUE existe historial suficiente del vehículo
  CUANDO el agente analice sus datos
  ENTONCES genera recomendaciones de mantenimiento
  Y las relaciona con kilometraje, tiempo o historial disponible.
```

### HU-045: Chatbot IA de Atención al Cliente
* **Como:** Cliente
* **Quiero:** Consultar información del servicio mediante un asistente IA
* **Para:** Obtener respuestas rápidas sobre mis vehículos, OT, citas y garantías.
* **Prioridad:** Media · **Entrega:** Entrega 3 · **Requerimientos:** RF-51, RN-15, RN-21

```gherkin
Escenario: Consulta autorizada
  DADO QUE el cliente está autenticado
  CUANDO consulte al agente sobre su vehículo o servicio
  ENTONCES el agente responde únicamente con información a la que el cliente tenga acceso.

Escenario: Información no disponible
  DADO QUE la pregunta requiere información que el agente no puede verificar
  CUANDO el cliente realice la consulta
  ENTONCES el agente indica que no puede confirmarla
  Y evita inventar información.
```

### HU-046: Agente IA de Inventario
* **Como:** Encargado de Inventario
* **Quiero:** Obtener recomendaciones basadas en consumo y existencias
* **Para:** Anticipar necesidades de abastecimiento.
* **Prioridad:** Baja · **Entrega:** Entrega 3 · **Requerimientos:** RF-44, RN-15

```gherkin
Escenario: Recomendación de reposición
  DADO QUE existen movimientos históricos de inventario
  CUANDO el encargado solicite un análisis
  ENTONCES el agente identifica productos con riesgo de agotamiento
  Y presenta una recomendación explicable basada en los datos disponibles.
```

### HU-047: Agente IA de Preanálisis de Reclamos
* **Como:** Auditor de la Aseguradora
* **Quiero:** Recibir un preanálisis automático de las evidencias de un reclamo
* **Para:** Priorizar y agilizar la revisión humana.
* **Prioridad:** Baja · **Entrega:** Entrega 3 · **Requerimientos:** RF-44, RN-15

```gherkin
Escenario: Preanálisis exitoso
  DADO QUE existe un reclamo con información y evidencias suficientes
  CUANDO el agente procese el caso
  ENTONCES genera un resumen de evidencias, posibles inconsistencias y criterios relevantes
  Y presenta el resultado como recomendación para revisión humana.

Escenario: Decisión humana obligatoria
  DADO QUE el agente genera una recomendación
  CUANDO el auditor consulte el resultado
  ENTONCES el sistema no cambia automáticamente el estado final del reclamo
  Y requiere que el auditor emita el dictamen.
```

### HU-048: Trazabilidad de Interacciones con IA
* **Como:** Administrador
* **Quiero:** Registrar las interacciones y recomendaciones relevantes de los agentes IA
* **Para:** Mantener trazabilidad y supervisión sobre su uso.
* **Prioridad:** Media · **Entrega:** Entrega 3 · **Requerimientos:** RF-45, RN-15

```gherkin
Escenario: Registro de interacción
  DADO QUE un usuario utiliza un agente IA en un proceso crítico
  CUANDO el agente genere una recomendación
  ENTONCES el sistema registra usuario, fecha, agente, contexto permitido y resultado de la interacción
  Y permite identificar si la recomendación fue aceptada o descartada.
```

### HU-070: Agendamiento de Citas por Chatbot
* **Como:** Cliente
* **Quiero:** Agendar, reprogramar o cancelar una cita conversando con el chatbot
* **Para:** Hacerlo a cualquier hora sin llamar al taller.
* **Prioridad:** Media · **Entrega:** Entrega 3 · **Requerimientos:** RF-51, RN-21

```gherkin
Escenario: Cita agendada
  DADO QUE el cliente está autenticado y tiene un vehículo registrado
  CUANDO le pida al chatbot una cita para un servicio
  ENTONCES el chatbot le muestra los horarios disponibles
  Y crea la cita solo después de que el cliente confirme el horario elegido.

Escenario: Sin disponibilidad
  DADO QUE no hay horarios disponibles en la fecha pedida
  CUANDO el cliente la solicite
  ENTONCES el chatbot le ofrece las fechas disponibles más cercanas.

Escenario: Reprogramación
  DADO QUE el cliente tiene una cita activa
  CUANDO le pida al chatbot cambiarla
  ENTONCES el chatbot muestra nuevos horarios
  Y actualiza la cita después de la confirmación del cliente.
```

### HU-071: Chatbot por WhatsApp
* **Como:** Cliente
* **Quiero:** Hablar con el chatbot del taller por WhatsApp
* **Para:** Consultar mi servicio desde la aplicación que ya uso.
* **Prioridad:** Media · **Entrega:** Entrega 3 · **Requerimientos:** RF-51, RN-19, RN-21

```gherkin
Escenario: Cliente identificado
  DADO QUE el número de WhatsApp coincide con el de un cliente que autorizó el canal
  CUANDO escriba al número del taller
  ENTONCES el chatbot lo saluda por su nombre
  Y responde sobre sus vehículos, citas y órdenes.

Escenario: Número no registrado
  DADO QUE el número no pertenece a ningún cliente del taller
  CUANDO la persona escriba
  ENTONCES el chatbot solo responde preguntas generales del taller
  Y no muestra información de ningún cliente.

Escenario: Verificación antes de datos sensibles
  DADO QUE el cliente pide información de una factura o cobertura
  CUANDO el chatbot vaya a responder
  ENTONCES le envía un código de verificación
  Y solo muestra la información después de validarlo.
```

### HU-072: Traspaso del Chatbot a un Asesor
* **Como:** Cliente
* **Quiero:** Que el chatbot me pase con una persona cuando lo necesite
* **Para:** Resolver lo que el chatbot no puede.
* **Prioridad:** Alta · **Entrega:** Entrega 3 · **Requerimientos:** RF-53, RN-22

```gherkin
Escenario: El cliente pide un asesor
  DADO QUE el cliente está conversando con el chatbot
  CUANDO pida hablar con una persona
  ENTONCES el chatbot transfiere la conversación a un asesor disponible
  Y el asesor ve todo el historial de la conversación.

Escenario: El chatbot no entiende
  DADO QUE el chatbot no entendió la consulta dos veces seguidas
  CUANDO el cliente escriba de nuevo sin éxito
  ENTONCES el chatbot ofrece pasarlo con un asesor.

Escenario: Fuera del horario de atención
  DADO QUE no hay asesores en horario de atención
  CUANDO el cliente pida hablar con una persona
  ENTONCES el chatbot registra la solicitud
  Y le informa cuándo será atendido.
```

### HU-073: Asistente Conversacional para el Personal
* **Como:** Personal del Taller
* **Quiero:** Hacer preguntas en lenguaje natural sobre los datos del taller
* **Para:** Obtener información sin buscar en varias pantallas.
* **Prioridad:** Baja · **Entrega:** Entrega 3 · **Requerimientos:** RF-52, RN-06, RN-21

```gherkin
Escenario: Pregunta respondida
  DADO QUE el asesor está autenticado
  CUANDO pregunte "¿Qué vehículos están listos para entrega hoy?"
  ENTONCES el asistente responde con la lista
  Y muestra enlaces a cada orden de trabajo.

Escenario: Pregunta fuera de sus permisos
  DADO QUE un técnico no tiene acceso a la información financiera
  CUANDO le pregunte al asistente por los ingresos del mes
  ENTONCES el asistente indica que no tiene permiso para esa información.

Escenario: Origen de la respuesta
  DADO QUE el asistente responde con cifras
  CUANDO el usuario vea la respuesta
  ENTONCES el asistente indica de qué reporte o consulta salen los datos.
```

### HU-074: Base de Conocimiento del Chatbot
* **Como:** Administrador del Taller
* **Quiero:** Configurar las preguntas frecuentes, horarios, políticas y precios de referencia que usa el chatbot
* **Para:** Que responda con la información correcta de mi taller.
* **Prioridad:** Media · **Entrega:** Entrega 3 · **Requerimientos:** RF-53

```gherkin
Escenario: Nueva pregunta frecuente
  DADO QUE el administrador está en la configuración del chatbot
  CUANDO agregue una pregunta y su respuesta
  ENTONCES el chatbot usa esa información en sus siguientes respuestas.

Escenario: Información desactualizada
  DADO QUE el administrador cambió el horario del taller
  CUANDO un cliente pregunte por el horario
  ENTONCES el chatbot responde con el horario nuevo.

Escenario: Pregunta sin respuesta en la base
  DADO QUE la base de conocimiento no tiene la respuesta
  CUANDO un cliente pregunte
  ENTONCES el chatbot dice que no tiene esa información y ofrece pasarlo con un asesor
  Y registra la pregunta para que el administrador la agregue.
```

### HU-075: Calificación y Analítica de Conversaciones
* **Como:** Administrador del Taller
* **Quiero:** Ver cómo le va al chatbot con los clientes
* **Para:** Mejorar sus respuestas y la atención.
* **Prioridad:** Baja · **Entrega:** Entrega 3 · **Requerimientos:** RF-45, RF-53

```gherkin
Escenario: Calificación del cliente
  DADO QUE terminó una conversación con el chatbot
  CUANDO el cliente la califique de 1 a 5
  ENTONCES el sistema guarda la calificación junto con la conversación.

Escenario: Analítica del chatbot
  DADO QUE existen conversaciones registradas
  CUANDO el administrador consulte un periodo
  ENTONCES el sistema muestra cantidad de conversaciones, temas más consultados, porcentaje resuelto sin un asesor, citas agendadas por el chatbot y calificación promedio.
```

---

# 13. Módulo 13: Administración de la Plataforma

### HU-063: Alta y Gestión de Talleres
* **Como:** Administrador de Plataforma
* **Quiero:** Registrar, activar y suspender talleres, y crear su primer administrador
* **Para:** Incorporar nuevos talleres a PitShield y controlar su acceso.
* **Prioridad:** Alta · **Entrega:** MVP · **Requerimientos:** RF-46, RN-06

```gherkin
Escenario: Alta de un taller
  DADO QUE el taller no está registrado
  CUANDO el Administrador de Plataforma registre su NIT, razón social y el correo del administrador
  ENTONCES el sistema crea el taller con sus datos aislados de los demás talleres
  Y envía una invitación al Administrador del Taller.

Escenario: NIT duplicado
  DADO QUE ya existe un taller con el mismo NIT
  CUANDO el Administrador de Plataforma intente registrarlo de nuevo
  ENTONCES el sistema bloquea el registro
  Y muestra el taller existente.

Escenario: Suspensión de un taller
  DADO QUE un taller está activo
  CUANDO el Administrador de Plataforma lo suspenda indicando el motivo
  ENTONCES los usuarios del taller no pueden operar
  Y el sistema conserva todos sus datos.
```

### HU-064: Gestión de Aseguradoras y Auditores
* **Como:** Administrador de Plataforma
* **Quiero:** Registrar las aseguradoras aliadas y sus usuarios auditores
* **Para:** Que cada reclamo llegue a la aseguradora que respalda la cobertura.
* **Prioridad:** Media · **Entrega:** Entrega 2 · **Requerimientos:** RF-47

```gherkin
Escenario: Registro de aseguradora
  DADO QUE la aseguradora no está registrada
  CUANDO el Administrador de Plataforma registre sus datos y su contacto
  ENTONCES el sistema crea la aseguradora
  Y permite asociarle productos de protección.

Escenario: Alcance del auditor
  DADO QUE un auditor pertenece a la Aseguradora A
  CUANDO consulte los reclamos
  ENTONCES el sistema muestra únicamente los reclamos de coberturas de la Aseguradora A.
```

### HU-065: Configuración de Productos de Protección
* **Como:** Administrador de Plataforma
* **Quiero:** Crear y configurar garantías extendidas y microseguros
* **Para:** Definir qué cubre cada producto, cuánto cuesta y quién puede comprarlo.
* **Prioridad:** Alta · **Entrega:** Entrega 2 · **Requerimientos:** RF-31, RN-01, RN-03

```gherkin
Escenario: Creación de producto
  DADO QUE existe una aseguradora registrada
  CUANDO el Administrador de Plataforma registre tipo, cobertura, vigencia, precio, comisión y condiciones de elegibilidad
  ENTONCES el sistema crea el producto en estado "Borrador"
  Y solo lo ofrece a los talleres cuando se publique.

Escenario: Cambio de condiciones
  DADO QUE un producto publicado tiene coberturas emitidas
  CUANDO el Administrador de Plataforma cambie su precio o condiciones
  ENTONCES el sistema crea una nueva versión del producto
  Y las coberturas ya emitidas conservan las condiciones con las que se vendieron.
```

---

## Reglas transversales de aceptación

Estas reglas aplican a todas las HU cuando correspondan:

- El sistema debe validar permisos antes de ejecutar operaciones.
- Los registros críticos no deben eliminarse físicamente; deben conservar trazabilidad.
- Las operaciones financieras deben ser idempotentes para evitar duplicidad de pagos o transacciones.
- Las transiciones de estado deben respetar el flujo definido.
- Las operaciones relevantes deben generar registros de auditoría.
- La información del cliente y del vehículo solo debe ser visible para usuarios autorizados.
- Las evidencias multimedia deben conservar su relación con el vehículo, OT o reclamo correspondiente.
- Los chatbots y agentes IA solo usan información a la que el usuario tiene acceso y nunca inventan datos que no puedan verificar (RN-21).
- Los agentes IA deben presentar sus resultados como asistencia y no como sustitución de decisiones humanas cuando exista impacto técnico, financiero, contractual o de cobertura.
- Los errores de integraciones externas deben registrarse y permitir seguimiento.
- Las notificaciones deben evitar envíos duplicados.
- Las funcionalidades de facturación, pagos, seguros y comunicaciones deben implementarse conforme a las reglas regulatorias y proveedores que se definan para el mercado objetivo.
- Toda operación debe respetar el aislamiento por taller (RN-06): ningún usuario puede ver ni modificar datos de otro taller.

---

## Definición de terminado

Una historia de usuario se considera terminada cuando:

1. Cumple todos sus escenarios de aceptación.
2. Tiene pruebas unitarias y de integración, con la cobertura mínima del 80 % en servicios y dominio (RNF-10).
3. Sus escenarios principales están automatizados (API o E2E) y los demás fueron probados manualmente con evidencia.
4. Pasó la revisión de código de al menos otro integrante del equipo.
5. La integración continua está en verde.
6. La documentación de la API (OpenAPI) está actualizada.
7. Fue demostrada y aceptada en la revisión del sprint.
