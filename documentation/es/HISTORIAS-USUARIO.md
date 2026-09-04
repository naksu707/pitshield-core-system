# Historias de Usuario - PitShield Core System

> **Documento de Backlog para Producción:** Especificación de Historias de Usuario (HU) con Criterios de Aceptación en formato BDD (Behavior-Driven Development / Gherkin) para el desarrollo de la plataforma PitShield Core System.

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
11. [Módulo 11: Reportes y Analítica](#11-módulo-11-reportes-y-analítica)
12. [Módulo 12: Agentes de Inteligencia Artificial](#12-módulo-12-agentes-de-inteligencia-artificial)

---

# 1. Módulo 1: Autenticación, Usuarios y Seguridad

### HU-001: Inicio de Sesión y Control de Acceso por Roles (RBAC)
* **Como:** Usuario del Sistema
* **Quiero:** Iniciar sesión con mis credenciales
* **Para:** Acceder únicamente a las funciones permitidas según mi rol.

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

---

# 2. Módulo 2: Talleres y Configuración

### HU-005: Configuración de Datos del Taller
* **Como:** Administrador del Taller
* **Quiero:** Registrar y actualizar los datos comerciales y fiscales del taller
* **Para:** Utilizarlos en facturas, comprobantes y comunicaciones.

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

---

# 3. Módulo 3: Clientes, Vehículos e Historial Digital

### HU-007: Registro y Vinculación de Cliente
* **Como:** Asesor de Servicio
* **Quiero:** Registrar un cliente y vincularlo a uno o varios vehículos
* **Para:** Mantener la información del propietario y facilitar las comunicaciones.

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

---

# 4. Módulo 4: Servicios, Agenda y Técnicos

### HU-012: Gestión del Catálogo de Servicios
* **Como:** Administrador del Taller
* **Quiero:** Crear, editar, activar o desactivar servicios
* **Para:** Mantener actualizado el catálogo que puede ofrecer el taller.

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

---

# 5. Módulo 5: Órdenes de Trabajo

### HU-015: Creación de Orden de Trabajo
* **Como:** Asesor de Servicio
* **Quiero:** Crear una Orden de Trabajo asociada a un cliente, vehículo y servicios solicitados
* **Para:** Iniciar formalmente la atención del vehículo.

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

> **Estados recomendados:** Borrador → Pendiente de Aprobación → Aprobada → En Proceso → En Espera → Finalizada → Lista para Entrega → Completada / Cancelada.

### HU-020: Cancelación y Modificación Controlada de OT
* **Como:** Asesor de Servicio / Administrador
* **Quiero:** Cancelar o modificar una OT según su estado
* **Para:** Reflejar cambios solicitados por el cliente o imprevistos operativos.

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

---

# 6. Módulo 6: Inventario, Proveedores y Compras

### HU-021: Gestión de Repuestos y Stock
* **Como:** Encargado de Inventario
* **Quiero:** Consultar y administrar existencias de repuestos
* **Para:** Mantener control del inventario disponible.

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

---

# 8. Módulo 8: Garantías, Microseguros y Reclamos

> **Nota funcional:** El producto debe definir claramente si PitShield comercializa garantías extendidas, microseguros o ambos. Las HU siguientes contemplan ambos conceptos sin asumir que jurídicamente sean equivalentes.

### HU-029: Evaluación de Elegibilidad
* **Como:** Asesor de Servicio
* **Quiero:** Consultar si un vehículo y servicio cumplen las condiciones de cobertura
* **Para:** Ofrecer únicamente productos para los que el cliente sea elegible.

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

---

# 9. Módulo 9: Portal del Cliente

### HU-034: Consulta de Vehículos e Historial
* **Como:** Cliente
* **Quiero:** Consultar mis vehículos y su historial autorizado
* **Para:** Conocer los servicios realizados y el estado de mis vehículos.

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

---

# 10. Módulo 10: Notificaciones Automáticas

### HU-038: Notificaciones de Eventos del Servicio
* **Como:** Sistema
* **Quiero:** Enviar notificaciones automáticas sobre eventos importantes
* **Para:** Mantener informados al cliente y al personal.

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

---

# 11. Módulo 11: Reportes y Analítica

### HU-040: Dashboard Financiero
* **Como:** Dueño / Gerente del Taller
* **Quiero:** Consultar indicadores financieros
* **Para:** Evaluar ingresos, cobros, pagos pendientes y rentabilidad.

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

```gherkin
Escenario: Reporte de inventario
  DADO QUE existen movimientos registrados
  CUANDO el usuario consulte un periodo
  ENTONCES el sistema muestra entradas, consumos, devoluciones, ajustes y productos con stock crítico.
```

---

# 12. Módulo 12: Agentes de Inteligencia Artificial

> Los agentes de IA deben funcionar como **asistentes de apoyo**. Las decisiones técnicas, financieras, de cobertura y aprobación de reclamos que tengan impacto real deben permanecer bajo control de usuarios autorizados.

### HU-043: Agente IA de Diagnóstico Asistido
* **Como:** Técnico del Taller
* **Quiero:** Consultar un agente IA utilizando síntomas, historial y datos del vehículo
* **Para:** Obtener recomendaciones que apoyen el diagnóstico técnico.

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

```gherkin
Escenario: Recomendación preventiva
  DADO QUE existe historial suficiente del vehículo
  CUANDO el agente analice sus datos
  ENTONCES genera recomendaciones de mantenimiento
  Y las relaciona con kilometraje, tiempo o historial disponible.
```

### HU-045: Agente IA de Atención al Cliente
* **Como:** Cliente
* **Quiero:** Consultar información del servicio mediante un asistente IA
* **Para:** Obtener respuestas rápidas sobre mis vehículos, OT, citas y garantías.

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

```gherkin
Escenario: Registro de interacción
  DADO QUE un usuario utiliza un agente IA en un proceso crítico
  CUANDO el agente genere una recomendación
  ENTONCES el sistema registra usuario, fecha, agente, contexto permitido y resultado de la interacción
  Y permite identificar si la recomendación fue aceptada o descartada.
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
- Los agentes IA deben presentar sus resultados como asistencia y no como sustitución de decisiones humanas cuando exista impacto técnico, financiero, contractual o de cobertura.
- Los errores de integraciones externas deben registrarse y permitir seguimiento.
- Las notificaciones deben evitar envíos duplicados.
- Las funcionalidades de facturación, pagos, seguros y comunicaciones deben implementarse conforme a las reglas regulatorias y proveedores que se definan para el mercado objetivo.
