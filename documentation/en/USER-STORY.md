# User Stories - PitShield Core System

> **Production Backlog Document:** Specification of User Stories (US) with Acceptance Criteria in BDD (Behavior-Driven Development / Gherkin) format for the development of the PitShield Core System platform.

---

## Modules

1. [Module 1: Authentication, Users and Security](#1-module-1-autenticación-users-y-seguridad)
2. [Module 2: Workshops and Configuration](#2-module-2-workshopes-y-withfiguration)
3. [Module 3: Customers, Vehicles and Digital History](#3-module-3-customers-vehicles-e-history-digital)
4. [Module 4: Services, Scheduling and Technicians](#4-module-4-services-agenda-y-technicians)
5. [Module 5: Work ORrders](#5-module-5-órdenes-de-trabajo)
6. [Module 6: Inventory, Suppliers and Purchawithoutg](#6-module-6-inventory-supplieres-y-compras)
7. [Module 7: Invoicing and Payments](#7-module-7-invoiceción-y-payments)
8. [Module 8: Warranties, Microinsurance and Claims](#8-module-8-warrantys-microinsurances-y-claims)
9. [Module 9: Customer Portal](#9-module-9-portal-del-customer)
10. [Module 10: Automated Notifications](#10-module-10-notifications-automáticas)
11. [Module 11: Reports and Analytics](#11-module-11-reports-y-analítica)
12. [Module 12: Artificial Intelligence Agents](#12-module-12-agentes-de-inteligencia-artificial)

---

# 1. Module 1: Authentication, Users and Security

### HU-001: Login and Role-Based Access Control (RBAC)
* **As a:** System User
* **I want to:** Iniciar sesión with mis credenciales
* **So that:** Acceder only a las funciones permitidas according to mi rol.

```gherkin
Scenario: Inicio de sesión exitoso
  GIVEN the user existe y se encuentra activo
  WHEN enter sus credenciales válidas
  THEN the system withcede el acceso
  AND shows only los modules permitidos for su rol.

Scenario: Credenciales inválidas
  GIVEN the user existe
  WHEN enter una withtraseña incorrecta
  THEN the system deniega el acceso
  AND shows un mensaje de credenciales inválidas.

Scenario: Usuario inactivo
  GIVEN the user se encuentra desactivado
  WHEN intente iniciar sesión with credenciales válidas
  THEN the system deniega el acceso
  AND shows un mensaje indicando que la cuenta no está activa.
```

### HU-002: Password Recovery and Change
* **As a:** System User
* **I want to:** Recuperar o cambiar mi withtraseña
* **So that:** Mantener el acceso a mi cuenta de forma segura.

```gherkin
Scenario: Recuperación de withtraseña
  GIVEN the user tiene un correo recordsdo
  WHEN solicite recuperar su withtraseña
  THEN the system sends un enlace temporal al correo recordsdo
  AND allows establecer una nueva withtraseña.

Scenario: Cambio de withtraseña autenticado
  GIVEN the user inició sesión
  WHEN enter su withtraseña current y una nueva withtraseña válida
  THEN the system updates la withtraseña
  AND withfirma la operación.
```

### HU-003: Management of Usuarios y Roles
* **As a:** Workshop Administrator
* **I want to:** Crear, editar, activar, desactivar users y asignar roles
* **So that:** Controlar who puede utilizar las funciones dthe system.

```gherkin
Scenario: User creation
  GIVEN the administrator se encuentra en Management of Usuarios
  WHEN registre un user with valid data y assign un rol
  THEN the system crea la cuenta
  AND la deja available according to el status withfigurado.

Scenario: User deactivation
  GIVEN existe un user activo
  WHEN the administrator lo desactive
  THEN the system impide new accesos
  AND preserves su history de actions.
```

### HU-004: Action and Access Auditing
* **As a:** Workshop Administrator
* **I want to:** Consultar las actions relevantes realizadas en the system
* **So that:** Mantener trazabilidad y detectar cambios no autorizados.

```gherkin
Scenario: Registro de una acción auditable
  GIVEN un user modifica un registro crítico
  WHEN la operación sea completada
  THEN the system records user, date, time, acción y registro afectado
  AND preserves la information de audit.

Scenario: Audit withsultstion
  GIVEN existen eventos recordsdos
  WHEN the administrator withsulte la audit
  THEN the system allows filtrar por user, date, module y type de acción.
```

---

# 2. Module 2: Workshops and Configuration

### HU-005: Workshop Data Configuration
* **As a:** Workshop Administrator
* **I want to:** Registrar y updatesr los data comerciales y fiscales del workshop
* **So that:** Utilizarlos en invoices, comprobantes y comunicaciones.

```gherkin
Scenario: Successful update
  GIVEN the administrator se encuentra en Configuración
  WHEN modifique los data permitidos y save los cambios
  THEN the system updates el perfil del workshop
  AND utiliza los new data en future emisiones.
```

### HU-006: Management of Sucursales y Horarios
* **As a:** Workshop Administrator
* **I want to:** Configurar branches, timerios y availability
* **So that:** ORrganizar la operación y agenda del workshop.

```gherkin
Scenario: Branch creation
  GIVEN the administrator tiene permissions de withfiguration
  WHEN registre una branch with valid data
  THEN the system crea la branch
  AND allows withfigurar su timerio de atención.

Scenario: Schedule update
  GIVEN existe una branch
  WHEN the administrator modifique su timerio
  THEN the system updates la availability for future appointments.
```

---

# 3. Module 3: Customers, Vehicles and Digital History

### HU-007: Customer Registration and Vehicle Linking
* **As a:** Service Advisor
* **I want to:** Registrar un customer y vincularlo a uno o varios vehicles
* **So that:** Mantener la information del propietario y facilitar las comunicaciones.

```gherkin
Scenario: Registro y vinculación exitosa
  GIVEN the customer no existe
  WHEN the advisor complete los required data y lo vincule a un vehicle
  THEN the system crea el perfil
  AND establece la relación entre customer y vehicle.

Scenario: Customer existente
  GIVEN the customer ya existe
  WHEN the advisor enter un identificador recordsdo
  THEN the system shows the customer existente
  AND allows vincular un new vehicle without duplicar el perfil.
```

### HU-008: Vehicle Registration and Initial History
* **As a:** Service Advisor
* **I want to:** Registrar un vehicle ingresando placa, VIN, marca, modelo, año y kilometraje
* **So that:** Crear su hoja de vida digital.

```gherkin
Scenario: Successful recordstion
  GIVEN la placa y el VIN no están recordsdos
  WHEN the advisor complete los campos obligatorios
  AND press "Guardar Vehículo"
  THEN the system crea el perfil
  AND generates la línea de tiempo inicial.

Scenario: Duplicate plate or VIN
  GIVEN la placa o VIN ya existe
  WHEN the user intente recordsr the vehicle
  THEN the system blocks el duplicado
  AND shows el registro existente.
```

### HU-009: Digital History Consultation
* **As a:** Workshop Technician
* **I want to:** Buscar un vehicle por placa o VIN
* **So that:** Consultar intervenciones, parts, evidences y warrantys associateds.

```gherkin
Scenario: Successful withsultstion
  GIVEN the vehicle tiene history recordsdo
  WHEN the technician lo busque por placa o VIN
  THEN the system shows el history ordenado cronológicamente
  AND allows withsultsr las evidences autorizadas.

Scenario: Vehicle not found
  GIVEN the vehicle no existe
  WHEN the technician realice la búsqueda
  THEN the system informa que no fue enwithtrado
  AND ofrece iniciar su registro si tiene permissions.
```

### HU-010: Vehicle ORwnership Transfer
* **As a:** Administrator / Service Advisor
* **I want to:** Cambiar el propietario associated a un vehicle
* **So that:** Mantener la withtinuidad del history without eliminar information anterior.

```gherkin
Scenario: Successful transfer
  GIVEN the vehicle tiene un propietario current
  WHEN the user autorizado registre al new propietario y withfirm la transferencia
  THEN the system updates el propietario vigente
  AND preserves el history previo dthe vehicle.

Scenario: Transfer traceability
  GIVEN se realizó una transferencia
  WHEN se withsulte la audit
  THEN the system shows who realizó el cambio, when y what propietarios estuvieron associateds.
```

### HU-011: History Immutability and Auditing
* **As a:** Workshop Administrator
* **I want to:** Garantizar la trazabilidad de los eventos críticos del history vehicular
* **So that:** Evitar la eliminación o modificación no withtrolada de information histórica.

```gherkin
Scenario: Attempt to delete historical record
  GIVEN existe un registro histórico associated a una ORT finalizada
  WHEN un user intente eliminarlo
  THEN the system blocks la eliminación
  AND records el intento en audit.

Scenario: Information correction
  GIVEN existe information que requires corrección
  WHEN un user autorizado realice un cambio permitido
  THEN the system preserves el valor anterior
  AND records el new valor, user, date y reason.
```

---

# 4. Module 4: Services, Scheduling and Technicians

### HU-012: Management ofl Catálogo de Servicios
* **As a:** Workshop Administrator
* **I want to:** Crear, editar, activar o desactivar services
* **So that:** Mantener updatesdo el catálogo que puede ofrecer el workshop.

```gherkin
Scenario: Create service
  GIVEN the administrator tiene permissions
  WHEN registre nombre, descripción, price y duración estimada válidos
  THEN the system crea el service
  AND lo deja available for quotes y appointments.

Scenario: Deactivate service
  GIVEN existe un service activo
  WHEN the administrator lo desactive
  THEN no estará available for nuevas appointments
  AND preservesrá su uso en registros históricos.
```

### HU-013: Management of Citas y Agenda
* **As a:** Customer / Service Advisor
* **I want to:** Crear, withsultsr, withfirm, reprogramar y cancelar appointments
* **So that:** ORrganizar la atención del workshop.

```gherkin
Scenario: Appointment creation
  GIVEN existe availability for el service soliappointmentdo
  WHEN the user select vehicle, service, date y time
  THEN the system crea la appointment
  AND records su status como "Pending" o "Confirmed" according to el flujo withfigurado.

Scenario: Unavailable time slot
  GIVEN el timerio ya está ocupado
  WHEN the user intente reservarlo
  THEN the system blocks la reserva
  AND shows timerios availables.

Scenario: Rescheduling
  GIVEN existe una appointment activa
  WHEN un user autorizado select un new timerio available
  THEN the system updates la appointment
  AND preserves el history de la modificación.
```

### HU-014: Technician Assignment to Work ORrder
* **As a:** Service Advisor / Administrator
* **I want to:** Asignar uno o varios technicians a una ORT
* **So that:** Definir responsables de la ejecución del service.

```gherkin
Scenario: Successful assignment
  GIVEN existe una ORT pendiente de ejecución
  WHEN the advisor select un technician available
  THEN the system lo asigna a la ORT
  AND records la date y user que realizó la asignación.

Scenario: Technician unavailable
  GIVEN the technician no tiene availability for el period requerido
  WHEN the advisor intente asignarlo
  THEN the system advierte la inavailability
  AND soliappointment select otro technician o period.
```

---

# 5. Module 5: Work ORrders

### HU-015: Work ORrder Creation
* **As a:** Service Advisor
* **I want to:** Crear una ORrden de Trabajo associated a un customer, vehicle y services soliappointmentdos
* **So that:** Iniciar formalmente la atención dthe vehicle.

```gherkin
Scenario: Creación de ORT
  GIVEN the customer y vehicle están recordsdos
  WHEN the advisor select los services soliappointmentdos
  AND save la orden
  THEN the system generates un código unique de ORT
  AND la crea en status "Draft".
```

### HU-016: Vehicle Diagnosis and Evidence
* **As a:** Workshop Technician
* **I want to:** Registrar síntomas, diagnóstico, observaciones y evidences
* **So that:** Documentar técnicamente el status dthe vehicle.

```gherkin
Scenario: Diagnosis recordstion
  GIVEN existe una ORT en status editable
  WHEN the technician registre el diagnóstico y upload las evidences requeridas
  THEN the system guarda la information
  AND la asocia a la ORT y al history dthe vehicle.

Scenario: Required evidence
  GIVEN un service requires evidence de ingreso
  WHEN the technician intente avanzar without uploadla
  THEN the system blocks el avance
  AND soliappointment la evidence faltante.
```

### HU-017: Quote Generation
* **As a:** Service Advisor
* **I want to:** Generar un quote with services, parts, mano de obra, impuestos y descuentos
* **So that:** Presentar al customer el cost estimado antes de ejecutar trabajos adicionales.

```gherkin
Scenario: Quote generatested
  GIVEN la ORT withtiene services y costs válidos
  WHEN the advisor genere el quote
  THEN the system calcula subtotales, impuestos, descuentos y total
  AND records la versión del quote.

Scenario: Quote modification
  GIVEN el quote aún no ha sido aprobado
  WHEN the advisor modifique sus withceptos
  THEN the system recalcula el total
  AND preserves la trazabilidad de la versión anterior.
```

### HU-018: Remote Quote Approval
* **As a:** Vehicle ORwner
* **I want to:** Revisar y aprobar o rechazar el quote from mi teléfono
* **So that:** Autorizar los trabajos without desplazarme al workshop.

```gherkin
Scenario: Approval
  GIVEN the customer recibió un quote vigente
  WHEN revise el detalle y press "Aprobar Trabajo"
  THEN the system records la aprobación
  AND cambia la ORT al status correspondiente.

Scenario: Rejection
  GIVEN the customer recibió un quote vigente
  WHEN press "Rechazar Trabajo" e indicate el reason
  THEN the system records el rechazo
  AND notifica al workshop.
```

### HU-019: Management ofl Ciclo de Vida de la ORT
* **As a:** Administrator / Service Advisor
* **I want to:** Controlar los statuss de una ORT
* **So that:** Garantizar que las operaciones ocurran en el orden correcto.

```gherkin
Scenario: Valid state transition
  GIVEN la ORT cumple las withditions del status current
  WHEN un user autorizado solicite avanzar
  THEN the system cambia al siguiente status permitido
  AND records la transición en audit.

Scenario: Invalid state transition
  GIVEN la ORT no cumple las withditions requeridas
  WHEN the user intente avanzar
  THEN the system blocks la transición
  AND shows las withditions pendientes.
```

> ****Recommended states:**** Draft → Pending de Approval → Approved → In Progress → On Hold → Finished → Ready for Delivery → Completed / Cancelled.

### HU-020: Controlled Work ORrder Cancellation and Modification
* **As a:** Service Advisor / Administrator
* **I want to:** Cancelar o modificar una ORT according to su status
* **So that:** Reflejar cambios soliappointmentdos por the customer o imprevistos operativos.

```gherkin
Scenario: Cancelación de ORT
  GIVEN la ORT se encuentra en un status que allows cancelación
  WHEN the user autorizado indicate un reason y withfirm
  THEN the system cambia la ORT a "Cancelled"
  AND ejecuta las operaciones de inventory y invoiceción correspondientes.

Scenario: Modification not allowed
  GIVEN la ORT se encuentra en un status cerrado
  WHEN the user intente modificarla
  THEN the system blocks la edición
  AND records el intento si corresponde.
```

---

# 6. Module 6: Inventory, Suppliers and Purchawithoutg

### HU-021: Management of Repuestos y Stock
* **As a:** Inventory Manager
* **I want to:** Consultar y administrar existencias de parts
* **So that:** Mantener withtrol del inventory available.

```gherkin
Scenario: Stock withsultstion
  GIVEN existen parts recordsdos
  WHEN the manager withsulte inventory
  THEN the system shows existencias availables, reservadas y utilizadas.

Scenario: Minimum stock
  GIVEN un repuesto alcanza o baja del stock mínimo withfigurado
  WHEN the system currentice el inventory
  THEN generates una alerta de reposición.
```

### HU-022: Parts Reservation and Consumption
* **As a:** System / Inventory Manager
* **I want to:** Reservar y deswithtar parts according to el avance de una ORT
* **So that:** Evitar descuadres entre stock available y piezas realmente utilizadas.

```gherkin
Scenario: Stock reservation
  GIVEN una ORT aprobada requires 2 unidades de un repuesto
  WHEN the system withfirm la ejecución
  THEN reserva las 2 unidades
  AND reduce el stock available without marcarlas todavía como withsumidas.

Scenario: Consumption
  GIVEN las piezas fueron utilizadas
  WHEN the technician registre el withsumo
  THEN the system las marca como withsumidas
  AND updates el inventory.
```

### HU-023: Inventory Returns and Adjustments
* **As a:** Inventory Manager
* **I want to:** Registrar devoluciones y ajustes por avería, merma o corrección
* **So that:** Mantener el inventory físico y digital withoutcronizado.

```gherkin
Scenario: Return of unused part
  GIVEN una pieza está reservada pero no fue utilizada
  WHEN the manager registre su devolución
  THEN the system libera la reserva
  AND devuelve la cantidad al stock available.

Scenario: Shrinkage adjustment
  GIVEN existe una diferencia física justificada
  WHEN the manager registre el ajuste with reason
  THEN the system updates el stock
  AND records el movimiento en audit.
```

### HU-024: Management of Proveedores y Órdenes de Compra
* **As a:** Inventory Manager
* **I want to:** Registrar supplieres y órdenes de compra
* **So that:** Controlar el abastecimiento de parts.

```gherkin
Scenario: Supplier recordstion
  GIVEN el supplier no existe
  WHEN the manager registre sus data
  THEN the system crea el supplier.

Scenario: Purchase receipt
  GIVEN existe una orden de compra pendiente
  WHEN the manager registre la recepción de 10 unidades
  THEN the system incrementa el stock
  AND records el cost unitario de la compra.
```

---

# 7. Module 7: Invoicing and Payments

### HU-025: Work ORrder to Invoice Conversion
* **As a:** Administrator / Cashier
* **I want to:** Generar una invoice a partir de una ORT finalizada
* **So that:** Formalizar el collection del service.

```gherkin
Scenario: Invoice generatestion
  GIVEN la ORT está finalizada y withtiene un total válido
  WHEN el cajero genere the invoice
  THEN the system crea un documento unique
  AND preserves la relación with la ORT.
```

### HU-026: Remote Payment and Payment Link
* **As a:** Administrator / Cashier
* **I want to:** Enviar un enlace de payment al customer
* **So that:** Facilitar el payment remoto.

```gherkin
Scenario: Payment link sending
  GIVEN existe una invoice pendiente
  WHEN el cajero solicite el link de payment
  THEN the system generates un enlace associated a the invoice
  AND lo sends via el withfigured channel.

Scenario: Payment rejected
  GIVEN the customer intenta pagar una invoice
  WHEN la pasarela rechace la transacción
  THEN the invoice permanece pendiente
  AND the system records el result del intento.
```

### HU-027: Payment Confirmation via Webhook
* **As a:** System
* **I want to:** Actualizar el status de una invoice al recibir la withfirmación de la pasarela
* **So that:** Mantener withoutcronizados payments y invoiceción.

```gherkin
Scenario: Successful payment
  GIVEN existe una invoice pendiente
  WHEN el webhook válido withfirm el payment
  THEN the system records la transacción
  AND marca the invoice como "Paid".

Scenario: Duplicate webhook
  GIVEN un payment ya fue recordsdo
  WHEN la pasarela envíe nuevamente el mismo evento
  THEN the system no duplica el payment
  AND mantiene un unique registro de la transacción.
```

### HU-028: Credit Notes and Refunds
* **As a:** Administrator / Cashier
* **I want to:** Anular o ajustar invoices y gestionar reembolsos
* **So that:** Mantener la trazabilidad withtable without eliminar documentos.

```gherkin
Scenario: Credit note
  GIVEN existe una invoice emitida que requires ajuste
  WHEN the administrator registre el reason
  THEN the system generates la nota crédito correspondiente
  AND preserves the invoice original.

Scenario: Refund
  GIVEN existe un payment susceptible de devolución
  WHEN the user autorizado solicite un reembolso
  THEN the system records la solicitud
  AND updates el status according to la respuesta de la pasarela.
```

---

# 8. Module 8: Warranties, Microinsurance and Claims

> **Functional note:** > **Functional note:** The product must clearly define whether PitShield offers extended warranties, microinsurance, or both. The following User Stories withsider both withcepts without assuming that they are legally equivalent.

### HU-029: Eligibility Assessment
* **As a:** Service Advisor
* **I want to:** Consultar si un vehicle y service cumplen las withditions de cobertura
* **So that:** ORfrecer only productos for los que the customer sea elegible.

```gherkin
Scenario: Eligible vehicle
  GIVEN the vehicle cumple las withditions withfiguradas
  WHEN the advisor withsulte la elegibilidad
  THEN the system shows el producto available
  AND presenta price, cobertura y validity.

Scenario: Ineligible vehicle
  GIVEN the vehicle no cumple una withdición
  WHEN the advisor withsulte la elegibilidad
  THEN the system indica que no es elegible
  AND shows el reason.
```

### HU-030: Warranty or Microinsurance Issuance
* **As a:** Service Advisor
* **I want to:** Emitir el producto de protección seleccionado por the customer
* **So that:** Activar su cobertura y generatesr el certificado correspondiente.

```gherkin
Scenario: Successful issuance
  GIVEN the customer acepta el producto y cumple la elegibilidad
  WHEN finalice la compra
  THEN the system records the coverage
  AND generates un certificado o póliza digital with su status y validity.

Scenario: Failed issuance
  GIVEN la entidad emisora no withfirma la emisión
  WHEN the system procese la solicitud
  THEN no activa the coverage
  AND records el result for seguimiento.
```

### HU-031: Coverage Consultation and Tracking
* **As a:** Customer / Asesor
* **I want to:** Consultar las coberturas activas y su validity
* **So that:** Conocer what services o componentes están protegidos.

```gherkin
Scenario: Coverage withsultstion
  GIVEN existe una cobertura activa
  WHEN the user withsulte the vehicle
  THEN the system shows validity, cobertura, status y withditions principales.
```

### HU-032: Claim Submission and Tracking
* **As a:** Workshop Administrator
* **I want to:** Radicar un claim with evidences y withsultsr su status
* **So that:** Gestionar la solicitud de cobertura hasta su resolución.

```gherkin
Scenario: Claim submission
  GIVEN the coverage está activa
  WHEN the administrator upload las evidences requeridas y describa la falla
  THEN the system crea the claim
  AND lo records como "Under Review".

Scenario: Information request
  GIVEN el auditor requires evidence adicional
  WHEN solicite information
  THEN the claim pasa a "Information Required"
  AND el workshop recibe la solicitud.

Scenario: Tracking
  GIVEN existe un claim activo
  WHEN the user withsulte su status
  THEN the system shows el status current y las actuaciones recordsdas.
```

### HU-033: Claim Audit and Decision
* **As a:** Insurance Auditor
* **I want to:** Revisar evidences y aprobar, rechazar o soliappointmentr information
* **So that:** Determinar si the claim cumple las withditions de cobertura.

```gherkin
Scenario: Approval
  GIVEN the claim tiene evidence sufficient
  WHEN el auditor lo apruebe
  THEN the system cambia el status a "Aprobado"
  AND records el dictamen y auditor.

Scenario: Rejection
  GIVEN the claim no cumple las withditions
  WHEN el auditor lo rechace e indicate un reason
  THEN the system cambia el status a "Rejected"
  AND notifica al workshop.

Scenario: Information request
  GIVEN falta evidence
  WHEN el auditor solicite information adicional
  THEN the system cambia el status a "Information Required"
  AND records exactamente what information falta.
```

---

# 9. Module 9: Customer Portal

### HU-034: Vehicle and History Consultation
* **As a:** Customer
* **I want to:** Consultar mis vehicles y su history autorizado
* **So that:** Conocer los services realizados y el status de mis vehicles.

```gherkin
Scenario: Consulta del history
  GIVEN the customer tiene un vehicle associated
  WHEN acceda al portal
  THEN puede withsultsr los registros que tiene permiso for visualizar
  AND puede revisar las evidences availables.
```

### HU-035: Work ORrder Tracking
* **As a:** Customer
* **I want to:** Consultar el status de mi ORT
* **So that:** Conocer el avance del service.

```gherkin
Scenario: Consulta de status
  GIVEN existe una ORT associated al customer
  WHEN acceda al portal
  THEN the system shows su status current
  AND la information relevante autorizada por el workshop.
```

### HU-036: Invoice and Payment Consultation
* **As a:** Customer
* **I want to:** Consultar mis invoices y statuss de payment
* **So that:** Mantener withtrol de mis obligaciones y transactions.

```gherkin
Scenario: Consulta de invoice
  GIVEN existe una invoice associated al customer
  WHEN acceda al portal
  THEN puede withsultsr el documento y su status de payment.

Scenario: Factura pendiente
  GIVEN the invoice está pendiente
  WHEN the customer la withsulte
  THEN the system shows una opción de payment si está available.
```

### HU-037: Warranty and Claim Consultation
* **As a:** Customer
* **I want to:** Consultar mis warrantys y claims
* **So that:** Conocer las coberturas y el avance de solicitudes.

```gherkin
Scenario: Warranty withsultstion
  GIVEN existe una cobertura associated al vehicle
  WHEN the customer la withsulte
  THEN the system shows validity, status y cobertura.

Scenario: Claim withsultstion
  GIVEN existe un claim associated
  WHEN the customer acceda al portal
  THEN puede withsultsr su status y las updatesciones permitidas.
```

---

# 10. Module 10: Automated Notifications

### HU-038: Service Event Notifications
* **As a:** System
* **I want to:** Enviar notifications automáticas about eventos importantes
* **So that:** Mantener informados al customer y al personal.

```gherkin
Scenario: Notificación de aprobación
  GIVEN the customer aprueba un quote
  WHEN the system registre la aprobación
  THEN notifica al personal correspondiente.

Scenario: Vehículo listo for entrega
  GIVEN la ORT cambia a "Ready for Delivery"
  WHEN se registre el cambio
  THEN the system notifica al customer via el withfigured channel.
```

### HU-039: Automated Maintenance Reminders
* **As a:** System (Job Programado)
* **I want to:** Detectar vehicles próximos a maintenance por tiempo o kilometraje
* **So that:** Incentivar el maintenance preventivo.

```gherkin
Scenario: Mantenimiento próximo
  GIVEN un vehicle cumple la withdición withfigurada de tiempo o kilometraje estimado
  WHEN se ejecute la rutina programada
  THEN the system generates un recordatorio
  AND proporciona una opción for agendar una appointment.

Scenario: Evitar notifications duplicadas
  GIVEN ya se envió un recordatorio for la misma withdición
  WHEN vuelva a ejecutarse la rutina
  THEN the system evita enviar notifications duplicadas within del period withfigurado.
```

---

# 11. Module 11: Reports and Analytics

### HU-040: Financial Dashboard
* **As a:** Workshop ORwner / Manager
* **I want to:** Consultar indicadores financieros
* **So that:** Evaluar ingresos, collections, payments pendientes y rentabilidad.

```gherkin
Scenario: Consulta mensual
  GIVEN existen transactions recordsdas
  WHEN el gerente select un period
  THEN the system shows ingresos, invoiceción, payments pendientes, reembolsos y comisiones aplicables.
```

### HU-041: ORperational Reports
* **As a:** Workshop ORwner / Manager
* **I want to:** Consultar indicadores de operación
* **So that:** Evaluar el desempeño del workshop.

```gherkin
Scenario: Consulta operativa
  GIVEN existen ORT y services recordsdos
  WHEN el gerente withsulte un period
  THEN the system shows ORT abiertas, finalizadas, canceladas, tiempos de atención y services realizados.
```

### HU-042: Inventory Reports
* **As a:** Inventory Manager / Gerente
* **I want to:** Consultar movimientos y niveles de inventory
* **So that:** Tomar decisiones de abastecimiento.

```gherkin
Scenario: Reporte de inventory
  GIVEN existen movimientos recordsdos
  WHEN the user withsulte un period
  THEN the system shows entradas, withsumos, devoluciones, ajustes y productos with stock crítico.
```

---

# 12. Module 12: Artificial Intelligence Agents

> Los agentes de IA deben funcionar como **asistentes de apoyo**. Las decisiones técnicas, financieras, de cobertura y aprobación de claims que tengan impacto real deben permanecer bajo withtrol de users autorizados.

### HU-043: AI-Assisted Diagnostic Agent
* **As a:** Workshop Technician
* **I want to:** Consultar un agente IA utilizando síntomas, history y data dthe vehicle
* **So that:** ORbtener recomendaciones que apoyen el diagnóstico technician.

```gherkin
Scenario: Recomendación de diagnóstico
  GIVEN existe una ORT with information sufficient
  WHEN the technician solicite asistencia al agente IA
  THEN el agente analiza la information available
  AND presenta posibles causas, verificaciones sugeridas y nivel de withfianza.

Scenario: Información insufficient
  GIVEN la information available no es sufficient
  WHEN the technician withsulte al agente
  THEN el agente indica what data adicionales serían necesarios
  AND no presenta una withclusión como diagnóstico definitivo.
```

### HU-044: AI Preventive Maintenance Agent
* **As a:** System / Gerente del Taller
* **I want to:** Analizar el history y comportamiento dthe vehicle
* **So that:** Generar recomendaciones de maintenance preventivo.

```gherkin
Scenario: Recomendación preventiva
  GIVEN existe history sufficient dthe vehicle
  WHEN el agente analice sus data
  THEN generates recomendaciones de maintenance
  AND las relaciona with kilometraje, tiempo o history available.
```

### HU-045: AI Customer Service Agent
* **As a:** Customer
* **I want to:** Consultar information del service via un asistente IA
* **So that:** ORbtener respuestas rápidas about mis vehicles, ORT, appointments y warrantys.

```gherkin
Scenario: Consulta autorizada
  GIVEN the customer está autenticado
  WHEN withsulte al agente about su vehicle o service
  THEN el agente responde only with information a la que the customer tenga acceso.

Scenario: Información no available
  GIVEN la pregunta requires information que el agente no puede verificar
  WHEN the customer realice la withsults
  THEN el agente indica que no puede withfirmla
  AND evita inventar information.
```

### HU-046: AI Inventory Agent
* **As a:** Inventory Manager
* **I want to:** ORbtener recomendaciones basadas en withsumo y existencias
* **So that:** Anticipar necesidades de abastecimiento.

```gherkin
Scenario: Recomendación de reposición
  GIVEN existen movimientos históricos de inventory
  WHEN the manager solicite un análisis
  THEN el agente identifica productos with riesgo de agotamiento
  AND presenta una recomendación explicable basada en los data availables.
```

### HU-047: AI Claim Pre-Analysis Agent
* **As a:** Insurance Auditor
* **I want to:** Recibir un preanálisis automático de las evidences de un claim
* **So that:** Priorizar y agilizar la revisión humana.

```gherkin
Scenario: Successful pre-analysis
  GIVEN existe un claim with information y evidences sufficients
  WHEN el agente procese el caso
  THEN generates un resumen de evidences, posibles inwithsistencias y criterios relevantes
  AND presenta el result como recomendación for revisión humana.

Scenario: Mandatory human decision
  GIVEN el agente generates una recomendación
  WHEN el auditor withsulte el result
  THEN the system no cambia automáticamente el status final dthe claim
  AND requires que el auditor emita el dictamen.
```

### HU-048: AI Interaction Traceability
* **As a:** Administrator
* **I want to:** Registrar las interactions y recomendaciones relevantes de los agentes IA
* **So that:** Mantener trazabilidad y supervisión about su uso.

```gherkin
Scenario: Interaction logging
  GIVEN un user utiliza un agente IA en un proceso crítico
  WHEN el agente genere una recomendación
  THEN the system records user, date, agente, withtexto permitido y result de la interacción
  AND allows identificar si la recomendación fue aceptada o descartada.
```

---

## Cross-Cutting Acceptance Rules

These rules apply to all User Stories where applicable:

- El sistema debe validar permissions antes de ejecutar operaciones.
- Critical records must not be physically deleted; traceability must be preserved.
- Financial operations must be idempotent to prevent duplicate payments or transactions.
- State transitions must follow the defined workflow.
- Relevant operations must generateste audit records.
- Customer and vehicle information must only be visible to authorized users.
- Las evidences multimedia deben preservesr su relación with the vehicle, ORT o claim correspondiente.
- AI agents must present their results as assistance and not as a replacement for human decisions when there is technical, financial, withtrcurrent, or coverage-related impact.
- Errors from external integrations must be logged and traceable.
- Notifications must prevent duplicate deliveries.
- Invoicing, payment, insurance, and communication features must be implemented according to the regulatory requirements and providers defined for the target market.
