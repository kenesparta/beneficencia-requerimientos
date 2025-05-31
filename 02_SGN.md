# Casos de Uso - Sistema de Gestión de Servicios Funerarios

## CU-SERFUN-001: Gestionar Nichos

### Descripción
Permite registrar, modificar y consultar información de nichos en el cementerio.

### Actores
- **Principal**: Empleado de Servicios Funerarios
- **Secundario**: Usuario Público (consulta online)

### Precondiciones
- El empleado debe estar autenticado en el sistema
- Los pabellones deben estar previamente registrados

### Flujo Principal - Registrar Nicho
1. El empleado accede al módulo de gestión de nichos
2. El sistema muestra la interfaz de registro
3. El empleado selecciona el pabellón donde se ubicará el nicho
4. El empleado ingresa los datos del nicho:
   - Código/número de nicho
   - Ubicación (fila, columna)
   - Tipo de nicho (temporal, perpetuo, familiar)
   - Dimensiones
   - Estado (disponible, ocupado, en mantenimiento)
   - Precio base
5. El sistema valida que el código de nicho sea único en el pabellón
6. El sistema registra el nicho
7. El sistema confirma el registro exitoso

### Flujo Alternativo - Modificar Nicho
3a. El empleado busca un nicho existente
3b. El sistema muestra los datos actuales del nicho
3c. El empleado modifica los campos necesarios
3d. El sistema valida los cambios
3e. El sistema actualiza la información

### Flujo Alternativo - Consulta Pública Online
1. El usuario público accede al portal web
2. El sistema muestra el formulario de búsqueda
3. El usuario ingresa criterios de búsqueda (código nicho, pabellón)
4. El sistema muestra el estado del nicho (disponible/ocupado)
5. Si está ocupado, muestra información básica del difunto (si es público)

### Postcondiciones
- Nicho registrado/modificado en el sistema
- Información disponible para consulta pública

### Excepciones
- **E1**: Código de nicho duplicado
- **E2**: Pabellón no existe o inactivo

---

## CU-SERFUN-002: Gestionar Difuntos

### Descripción
Permite registrar y gestionar información de difuntos inhumados en el cementerio.

### Actores
- **Principal**: Empleado de Servicios Funerarios

### Precondiciones
- El empleado debe estar autenticado
- Debe existir un nicho disponible para la inhumación

### Flujo Principal - Registrar Difunto
1. El empleado accede al módulo de gestión de difuntos
2. El sistema muestra la interfaz de registro
3. El empleado ingresa el DNI del difunto
4. El sistema consulta automáticamente RENIEC para obtener datos
5. El sistema muestra la información obtenida de RENIEC:
   - Nombres completos
   - Fecha de nacimiento
   - Fecha de defunción (si está disponible)
   - Lugar de nacimiento
6. El empleado complementa con datos adicionales:
   - Fecha y hora de fallecimiento (si no está en RENIEC)
   - Causa de muerte
   - Lugar de fallecimiento
   - Datos del certificado de defunción
7. El empleado selecciona el nicho donde será inhumado
8. El sistema valida que el nicho esté disponible
9. El sistema registra al difunto y actualiza el estado del nicho

### Flujo Alternativo - Difunto sin DNI
3a. El empleado indica que no tiene DNI
3b. El sistema permite registro manual de todos los datos
3c. El empleado ingresa manualmente toda la información

### Flujo Alternativo - Consulta Pública por Difunto
1. El usuario público accede al portal de consultas
2. El sistema muestra opciones de búsqueda
3. El usuario puede buscar por:
   - Nombre completo
   - DNI
   - Fecha de fallecimiento
4. El sistema muestra resultados coincidentes
5. El usuario selecciona un resultado
6. El sistema muestra información del difunto y ubicación del nicho

### Postcondiciones
- Difunto registrado en el sistema
- Nicho marcado como ocupado
- Información disponible para consulta pública

---

## CU-SERFUN-003: Gestionar Pagos de Nichos

### Descripción
Permite registrar y gestionar los pagos realizados por nichos y servicios funerarios.

### Actores
- **Principal**: Empleado de Servicios Funerarios
- **Secundario**: Concesionario (familiar)

### Precondiciones
- Debe existir un contrato de concesión de nicho
- El empleado debe estar autenticado

### Flujo Principal - Registrar Pago Presencial
1. El empleado accede al módulo de pagos
2. El sistema muestra la interfaz de registro de pagos
3. El empleado busca al concesionario o el nicho
4. El sistema muestra las deudas pendientes y próximos vencimientos
5. El empleado selecciona los conceptos a pagar:
   - Renovación de nicho
   - Servicios adicionales
   - Multas por mora
6. El sistema calcula el monto total
7. El empleado registra el método de pago (efectivo, tarjeta)
8. El sistema genera el comprobante de pago
9. El sistema actualiza los estados de pago
10. El sistema imprime el recibo

### Flujo Alternativo - Pago Online
1. El concesionario accede al portal web
2. El sistema solicita autenticación (DNI, código de nicho)
3. El sistema muestra las deudas pendientes
4. El concesionario selecciona los conceptos a pagar
5. El sistema redirige a la pasarela de pagos
6. El concesionario completa el pago con:
   - Visa/Mastercard
   - Yape
   - Otras opciones habilitadas
7. La pasarela confirma el pago exitoso
8. El sistema actualiza automáticamente los estados
9. El sistema envía comprobante por email

### Postcondiciones
- Pago registrado en el sistema
- Estados de cuentas actualizados
- Comprobante generado

---

## CU-SERFUN-004: Generar Concesión de Nichos

### Descripción
Permite crear contratos de concesión de nichos para nuevos difuntos.

### Actores
- **Principal**: Empleado de Servicios Funerarios

### Precondiciones
- Debe existir un nicho disponible
- Los datos del difunto deben estar registrados

### Flujo Principal
1. El empleado accede al módulo de concesiones
2. El sistema muestra la interfaz de nueva concesión
3. El empleado busca y selecciona al difunto registrado
4. El empleado selecciona un nicho disponible
5. El empleado ingresa datos del concesionario:
   - DNI (consulta automática a RENIEC)
   - Nombres completos
   - Dirección
   - Teléfono
   - Email
   - Relación con el difunto
6. El empleado define los términos de la concesión:
   - Tipo de concesión (temporal/perpetua)
   - Período de vigencia
   - Monto de la concesión
   - Forma de pago
7. El sistema genera el contrato de concesión
8. El sistema actualiza el estado del nicho a "concesionado"
9. El sistema programa las fechas de renovación (si aplica)

### Postcondiciones
- Contrato de concesión generado
- Nicho asignado al concesionario
- Cronograma de pagos establecido

---

## CU-SERFUN-005: Gestionar Renovaciones

### Descripción
Permite procesar renovaciones de concesiones de nichos y gestionar reintegros.

### Actores
- **Principal**: Empleado de Servicios Funerarios

### Precondiciones
- Debe existir una concesión vencida o próxima a vencer

### Flujo Principal - Procesar Renovación
1. El empleado accede al módulo de renovaciones
2. El sistema muestra las concesiones pendientes de renovación
3. El empleado selecciona una concesión específica
4. El sistema calcula el monto de renovación incluyendo:
   - Costo base de renovación
   - Recargos por mora (si aplica)
   - Servicios adicionales
5. El empleado registra el pago de renovación
6. El sistema extiende el período de vigencia
7. El sistema actualiza las fechas de próximo vencimiento
8. El sistema genera nueva documentación

### Flujo Alternativo - Procesar Reintegro
3a. El empleado selecciona opción de reintegro
3b. El sistema solicita motivo del reintegro
3c. El empleado ingresa la justificación
3d. El sistema calcula el monto a reintegrar según políticas
3e. El empleado autoriza el reintegro
3f. El sistema genera la orden de reintegro
3g. El sistema libera el nicho para nueva concesión

### Postcondiciones
- Concesión renovada o reintegro procesado
- Documentación actualizada

---

## CU-SERFUN-006: Gestionar Unión de Cuerpos

### Descripción
Permite registrar la inhumación de múltiples cuerpos en un mismo nicho (hasta 6 personas).

### Actores
- **Principal**: Empleado de Servicios Funerarios

### Precondiciones
- Debe existir un nicho con capacidad disponible
- Los difuntos deben estar registrados

### Flujo Principal
1. El empleado accede al módulo de unión de cuerpos
2. El sistema muestra la interfaz de gestión
3. El empleado selecciona el nicho base
4. El sistema muestra la ocupación actual del nicho
5. El empleado agrega nuevos difuntos:
   - Busca y selecciona al difunto registrado
   - Verifica relación familiar o autorización
   - Confirma la adición
6. El sistema valida que no se exceda la capacidad máxima (6 personas)
7. El sistema actualiza el registro del nicho
8. El sistema genera documentación de la unión

### Postcondiciones
- Múltiples difuntos registrados en el mismo nicho
- Capacidad del nicho actualizada

---

## CU-SERFUN-007: Gestionar Mausoleos

### Descripción
Permite gestionar la venta de lotes en mausoleos y el registro de traslados.

### Actores
- **Principal**: Empleado de Servicios Funerarios

### Precondiciones
- Deben existir mausoleos registrados en el sistema

### Flujo Principal - Venta de Lote en Mausoleo
1. El empleado accede al módulo de mausoleos
2. El sistema muestra los mausoleos disponibles
3. El empleado selecciona un mausoleo específico
4. El sistema muestra los lotes disponibles indicando:
   - Tipo (capilla/subterráneo)
   - Capacidad (número de cadáveres)
   - Precio
   - Estado
5. El empleado registra la venta especificando:
   - Datos del comprador
   - Tipo de lote seleccionado
   - Capacidad contratada
   - Forma de pago
6. El sistema genera el contrato de venta
7. El sistema actualiza la disponibilidad del mausoleo

### Flujo Alternativo - Registrar Traslado a Mausoleo
3a. El empleado selecciona opción de traslado
3b. El sistema solicita datos del nicho origen
3c. El empleado selecciona el lote de mausoleo destino
3d. El empleado especifica el tipo de traslado:
   - Interno (dentro del mismo cementerio)
   - Unión (con otros restos familiares)
3e. El sistema registra el traslado
3f. El sistema libera el nicho original
3g. El sistema actualiza la ocupación del mausoleo

### Postcondiciones
- Lote de mausoleo vendido o traslado registrado
- Inventario actualizado

---

## CU-SERFUN-008: Gestionar Servicios de Incineración

### Descripción
Permite registrar y gestionar servicios de incineración de restos.

### Actores
- **Principal**: Empleado de Servicios Funerarios

### Precondiciones
- Debe existir autorización legal para la incineración
- El empleado debe estar autenticado

### Flujo Principal
1. El empleado accede al módulo de incineración
2. El sistema muestra la interfaz de registro
3. El empleado ingresa los datos del servicio:
   - Datos del difunto
   - Cementerio de procedencia
   - Fecha programada de incineración
   - Datos del concesionario/familiar autorizado
   - Documentos legales requeridos
4. El sistema valida la documentación requerida
5. El empleado programa la fecha de incineración
6. El sistema registra el servicio
7. El sistema genera la orden de servicio
8. Al completar la incineración:
   8a. El empleado registra la finalización
   8b. El sistema actualiza el estado
   8c. El sistema genera certificado de incineración

### Postcondiciones
- Servicio de incineración registrado
- Documentación generada

---

## CU-SERFUN-009: Gestionar Pabellones

### Descripción
Permite registrar y gestionar pabellones del cementerio, incluyendo ampliaciones.

### Actores
- **Principal**: Administrador de Servicios Funerarios

### Precondiciones
- El administrador debe estar autenticado

### Flujo Principal - Registrar Pabellón
1. El administrador accede al módulo de pabellones
2. El sistema muestra la interfaz de registro
3. El administrador ingresa los datos del pabellón:
   - Nombre/código del pabellón
   - Ubicación en el cementerio
   - Número de filas
   - Número de columnas
   - Tipo de nichos que contendrá
   - Fecha de construcción
4. El sistema calcula automáticamente la capacidad total
5. El sistema registra el pabellón
6. El sistema permite generar automáticamente los nichos base

### Flujo Alternativo - Registrar Ampliación
3a. El administrador selecciona un pabellón existente
3b. El sistema muestra la configuración actual
3c. El administrador especifica la ampliación:
   - Nuevas filas/columnas
   - Tipo de ampliación
   - Fecha de la ampliación
3d. El sistema recalcula la capacidad
3e. El sistema registra la ampliación
3f. El sistema genera los nuevos nichos disponibles

### Postcondiciones
- Pabellón registrado o ampliado
- Capacidad del cementerio actualizada

---

## CU-SERFUN-010: Gestionar Modificaciones de Nichos

### Descripción
Permite registrar modificaciones físicas en nichos como lápidas y rejas.

### Actores
- **Principal**: Empleado de Servicios Funerarios

### Precondiciones
- El nicho debe estar concesionado
- Debe existir autorización del concesionario

### Flujo Principal
1. El empleado accede al módulo de modificaciones
2. El sistema muestra la interfaz de registro
3. El empleado busca y selecciona el nicho
4. El sistema muestra el estado actual del nicho
5. El empleado registra las modificaciones:
   - Tipo de modificación (lápida, reja, adornos)
   - Descripción detallada
   - Fecha de instalación
   - Proveedor/instalador
   - Costo (si aplica)
   - Fotos (opcional)
6. El sistema valida que la modificación esté autorizada
7. El sistema registra la modificación
8. El sistema actualiza la descripción del nicho

### Postcondiciones
- Modificación registrada en el historial del nicho
- Descripción del nicho actualizada

---

## CU-SERFUN-011: Procesar Re-inhumaciones

### Descripción
Permite registrar cuando un difunto exhumado vuelve a ser inhumado en su nicho original.

### Actores
- **Principal**: Empleado de Servicios Funerarios

### Precondiciones
- Debe existir un registro previo de exhumación
- El nicho debe estar disponible o reservado

### Flujo Principal
1. El empleado accede al módulo de re-inhumaciones
2. El sistema muestra los casos de exhumación pendientes de retorno
3. El empleado selecciona el caso específico
4. El sistema muestra el historial del difunto y nicho
5. El empleado confirma el retorno al nicho original
6. El sistema registra la re-inhumación
7. El sistema actualiza el estado del nicho
8. El sistema envía notificación automática: "Re-inhumación"
9. El sistema actualiza todos los registros relacionados

### Postcondiciones
- Re-inhumación registrada
- Notificación enviada
- Estado del nicho actualizado

---

## CU-SERFUN-012: Generar Alertas de Vencimiento (?)

### Descripción
Sistema automático que genera alertas cuando se aproxima el vencimiento de concesiones.

### Actores
- **Principal**: Sistema (automático)
- **Secundario**: Concesionarios

### Precondiciones
- Deben existir concesiones con fechas de vencimiento
- Medios de contacto configurados

### Flujo Principal
1. El sistema ejecuta proceso diario de verificación
2. El sistema identifica concesiones próximas a vencer
3. Para cada concesión, el sistema:
   - Calcula días restantes hasta vencimiento
   - Verifica si corresponde enviar alerta (30, 15, 7 días antes)
   - Obtiene datos de contacto del concesionario
4. El sistema genera la alerta personalizada
5. El sistema envía notificación por:
   - Email (si está disponible)
   - SMS (si está configurado)
   - WhatsApp (si está integrado)
6. El sistema registra el envío de la alerta
7. El sistema programa próxima alerta si es necesario

### Postcondiciones
- Alertas enviadas a concesionarios
- Registro de notificaciones actualizado

---

## CU-SERFUN-013: Procesar Pagos en Línea

### Descripción
Permite a los concesionarios realizar pagos a través del portal web usando diferentes métodos.

### Actores
- **Principal**: Concesionario
- **Secundario**: Pasarela de Pagos

### Precondiciones
- Concesionario debe estar registrado en el sistema
- Pasarelas de pago configuradas

### Flujo Principal
1. El concesionario accede al portal web
2. El sistema solicita identificación:
   - DNI del concesionario
   - Código de nicho
   - Datos adicionales de verificación
3. El sistema valida la identidad
4. El sistema muestra las deudas pendientes
5. El concesionario selecciona los conceptos a pagar
6. El sistema calcula el total incluyendo recargos
7. El concesionario selecciona método de pago:
   - Tarjeta Visa/Mastercard
   - Yape
   - Otros métodos habilitados
8. El sistema redirige a la pasarela correspondiente
9. El concesionario completa el pago
10. La pasarela confirma la transacción
11. El sistema actualiza automáticamente los estados
12. El sistema envía comprobante por email

### Flujo Alternativo - Pago con Yape
7a. El concesionario selecciona Yape
7b. El sistema genera código QR
7c. El concesionario escanea con app Yape
7d. El concesionario confirma pago en Yape
7e. Continúa en paso 10

### Postcondiciones
- Pago procesado y confirmado
- Estados de cuenta actualizados
- Comprobante digital enviado

---

## CU-SERFUN-014: Generar Reportes

### Descripción
Permite generar diversos reportes estadísticos y de gestión del cementerio.

### Actores
- **Principal**: Administrador/Gerente de Servicios Funerarios

### Precondiciones
- El usuario debe tener permisos para generar reportes

### Flujo Principal
1. El usuario accede al módulo de reportes
2. El sistema muestra los tipos de reportes disponibles:
   - Renovaciones pendientes
   - Inhumaciones por período
   - Estado de ocupación
   - Ingresos por servicios
   - Vencimientos próximos
   - Servicios de incineración
   - Estado de mausoleos
3. El usuario selecciona el tipo de reporte
4. El sistema solicita parámetros específicos:
   - Rango de fechas
   - Pabellones específicos
   - Tipos de servicio
   - Estados de concesión
5. El usuario define los filtros deseados
6. El sistema procesa la información
7. El sistema genera el reporte en formato PDF/Excel
8. El sistema permite descarga o envío por email

### Postcondiciones
- Reporte generado según especificaciones
- Información disponible para análisis

---

## CU-SERFUN-015: Gestionar Información Pública Web

### Descripción
Permite mantener actualizada la información general disponible en la página web.

### Actores
- **Principal**: Administrador Web

### Precondiciones
- El administrador debe estar autenticado
- Portal web debe estar operativo

### Flujo Principal
1. El administrador accede al panel de gestión web
2. El sistema muestra las secciones editables:
   - Información general del cementerio
   - Horarios de atención
   - Servicios disponibles
   - Precios y tarifas
   - Requisitos y procedimientos
   - Contactos
3. El administrador selecciona la sección a editar
4. El sistema presenta editor de contenido
5. El administrador actualiza la información
6. El sistema valida el contenido
7. El administrador publica los cambios
8. El sistema actualiza automáticamente el portal web

### Postcondiciones
- Información web actualizada
- Usuarios tienen acceso a información actual

---

## Configuraciones Técnicas Requeridas

### Integración con RENIEC (?) muchas limitaciones por restriccion de datos
- **API**: Servicio web para consulta de ciudadanos
- **Datos**: Nombres, fechas, estado civil, etc.
- **Autenticación**: Certificados digitales requeridos
- **Límites**: Cuotas de consultas diarias

### Pasarelas de Pago (?)
- **Visa/Mastercard**: Integración con procesadores bancarios
- **Yape**: API oficial de BCP para comercios
- **Configuración**: Merchant ID, claves de encriptación
- **Seguridad**: Cumplimiento PCI DSS

### Sistema de Notificaciones, (?) a quien?
- **Email**: Servidor SMTP configurado
- **SMS**: Gateway SMS (Claro, Movistar, etc.) (?)
- **WhatsApp**: API Business de WhatsApp (?)
- **Plantillas**: Mensajes personalizables por tipo de alerta

## Preguntas Adicionales Específicas

1. **Políticas de vencimiento**: ¿Cuál es el período de gracia después del vencimiento antes de proceder con exhumación?

2. **Tarifas diferenciadas**: ¿Existen tarifas especiales para adultos mayores, niños, o casos sociales?

3. **Documentación legal**: ¿Qué documentos específicos se requieren para cada tipo de servicio?

4. **Integración contable**: ¿Los pagos deben integrarse automáticamente con el sistema contable?

5. **Backup de datos**: ¿Se requiere respaldo de fotos y documentos digitales? ¿En qué formato y frecuencia?