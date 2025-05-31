# Casos de Uso - Sistema Contable

## Preguntas para Completar el Diseño

Antes de presentar los casos de uso completos, necesito clarificar algunos aspectos:

1. **Integración con sistema actual**: El TDR menciona "evaluar la posibilidad de integrar el actual sistema contable de la SBA con el SIG SBA". ¿Existe un sistema contable previo? ¿Qué datos/funcionalidades se conservarían?

2. **Roles específicos**: ¿Cuáles son los roles contables específicos? (Contador, Auxiliar Contable, Tesorero, etc.)

3. **Centros de costo**: ¿Cómo se estructuran los centros de costo? ¿Por áreas, proyectos, servicios específicos?

4. **Monedas**: ¿Se manejan múltiples monedas o solo Soles y Dólares?

5. **Conciliación bancaria**: ¿Cuántas cuentas bancarias manejan aproximadamente?

6. **Periodicidad de reportes**: ¿Los reportes son diarios, semanales, mensuales?

7. Que procesos genera un asiento contable.

---

## CU-CONTA-001: Gestionar Configuración SUNAT

### Descripción
Permite configurar la interfaz con SUNAT para carga automática de tipos de cambio y verificación de contribuyentes.

### Actores
- **Principal**: Administrador Contable
- **Secundario**: Servicio SUNAT (API)

### Precondiciones
- El usuario debe tener permisos de administrador contable
- Conexión a internet disponible
- Credenciales de acceso a servicios SUNAT configuradas

### Flujo Principal
1. El administrador accede al módulo de configuración SUNAT
2. El sistema muestra la configuración actual de la interfaz
3. El administrador configura:
   - URL de servicios SUNAT
   - Credenciales de acceso
   - Frecuencia de actualización (diaria)
   - Horario de sincronización automática
4. El sistema valida la conectividad con SUNAT
5. El sistema programa la tarea automática de sincronización
6. El sistema confirma la configuración exitosa

### Flujo Alternativo - Sincronización Manual
3a. El administrador selecciona sincronización manual
3b. El sistema ejecuta la carga inmediata de:
   - Tipos de cambio del día
   - Actualización de estado de contribuyentes
3c. El sistema muestra el resultado de la sincronización

### Postcondiciones
- Configuración SUNAT guardada
- Sincronización automática programada
- Tipos de cambio actualizados

### Excepciones
- **E1**: Error de conectividad con SUNAT
- **E2**: Credenciales inválidas
- **E3**: Servicio SUNAT no disponible

---

## CU-CONTA-002: Generar Estados Financieros

### Descripción
Permite generar y visualizar los cuatro estados financieros obligatorios y reportes de análisis de cuentas.

### Actores
- **Principal**: Contador
- **Secundario**: Gerente General

### Precondiciones
- Asientos contables registrados para el período
- Plan de cuentas configurado
- Período contable abierto o cerrado

### Flujo Principal
1. El contador accede al módulo de estados financieros
2. El sistema muestra las opciones de generación
3. El contador selecciona:
   - Tipo de estado financiero (Balance General, Estado de Resultados, Estado de Flujo de Efectivo, Estado de Cambios en el Patrimonio) (?) son solo esos estados financieros?
   - Período (fecha desde - fecha hasta)
   - Nivel de detalle (resumido/detallado)
   - Moneda (nacional/extranjera)
4. El sistema procesa la información contable
5. El sistema genera el estado financiero solicitado
6. El sistema muestra el reporte en pantalla
7. El contador puede exportar a Excel/PDF

### Flujo Alternativo - Análisis de Cuentas
3a. El contador selecciona "Análisis de Cuentas"
3b. El sistema solicita filtros específicos:
   - Cuenta contable específica
   - Centro de costo
   - Proyecto
3c. El sistema genera el análisis detallado de movimientos

### Postcondiciones
- Estado financiero generado
- Reporte disponible para exportación
- Log de generación registrado

---

## CU-CONTA-003: Gestionar Estados de Cuenta/Historial Financiero

### Descripción
Permite generar estados de cuenta de clientes, proveedores y otros terceros con saldos a cualquier fecha.

### Actores
- **Principal**: Auxiliar Contable
- **Secundario**: Contador

### Precondiciones
- Terceros registrados en el sistema
- Movimientos contables asociados a los terceros

### Flujo Principal
1. El auxiliar accede al módulo de estados de cuenta
2. El sistema muestra las opciones de generación
3. El auxiliar selecciona:
   - Tipo de tercero (cliente/proveedor/otros)
   - Tercero específico o todos
   - Fecha de corte
   - Moneda
4. El sistema calcula los saldos hasta la fecha especificada
5. El sistema genera el estado de cuenta
6. El sistema muestra el detalle de movimientos y saldo final
7. El auxiliar puede enviar por email o exportar

### Flujo Alternativo - Estado Consolidado
3a. El auxiliar selecciona "Estado consolidado por tipo"
3b. El sistema genera un resumen de saldos por todos los terceros del tipo seleccionado

### Postcondiciones
- Estado de cuenta generado
- Saldos calculados correctamente
- Disponible para envío/exportación

---

## CU-CONTA-004: Gestionar Reportes por Centros de Costo

### Descripción
Permite generar reportes financieros segmentados por centros de costo, actividades, servicios o proyectos.

### Actores
- **Principal**: Contador
- **Secundario**: Jefe de Área

### Precondiciones
- Centros de costo configurados
- Asientos contables con centros de costo asignados

### Flujo Principal
1. El contador accede al módulo de reportes por centros de costo
2. El sistema muestra la estructura de centros de costo
3. El contador selecciona:
   - Centro de costo específico o grupo
   - Período de análisis
   - Tipo de reporte (ingresos/egresos/ambos)
   - Nivel de detalle
4. El sistema procesa los movimientos del período
5. El sistema genera el reporte segmentado
6. El sistema muestra comparativos con períodos anteriores
7. El contador puede pedir el detalle en cualquier cuenta (?)

### Flujo Alternativo - Comparativo Multi-Centro
3a. El contador selecciona múltiples centros de costo
3b. El sistema genera un reporte comparativo
3c. El sistema incluye gráficos de participación porcentual

### Postcondiciones
- Reporte generado por centro de costo
- Análisis comparativo disponible

---

## CU-CONTA-005: Gestionar Comprobantes de Pago (?)

### Descripción
Permite registrar y gestionar comprobantes de pago para gastos y recibos de ingreso.

### Actores
- **Principal**: Auxiliar Contable
- **Secundario**: Tesorero

### Precondiciones
- Plan de cuentas configurado
- Terceros registrados
- Numeración de comprobantes configurada

### Flujo Principal - Registrar Comprobante de Gasto
1. El auxiliar accede al registro de comprobantes
2. El sistema muestra el formulario de comprobante de pago
3. El auxiliar ingresa:
   - Tipo de comprobante
   - Número de comprobante
   - Fecha
   - Proveedor/tercero
   - Detalle de cuentas contables
   - Importes por cuenta
   - Centro de costo (si aplica)
   - Documento sustentatorio
4. El sistema valida que el comprobante cuadre (debe = haber)
5. El sistema genera el asiento contable automáticamente
6. El sistema asigna número correlativo interno
7. El sistema confirma el registro

### Flujo Alternativo - Recibo de Ingreso
3a. El auxiliar selecciona "Recibo de Ingreso"
3b. El sistema ajusta el formulario para ingresos
3c. El auxiliar registra los datos del ingreso
3d. El sistema genera asiento automático de ingreso

### Postcondiciones
- Comprobante registrado
- Asiento contable generado
- Movimiento reflejado en cuentas

---

## CU-CONTA-006: Gestionar Emisión de Cheques (?) preguntar si aplica.

### Descripción
Permite emitir cheques y vouchers con reportes de seguimiento por bancos y proveedores.

### Actores
- **Principal**: Tesorero
- **Secundario**: Contador

### Precondiciones
- Cuentas bancarias configuradas
- Chequeras registradas en el sistema
- Comprobantes de pago aprobados

### Flujo Principal
1. El tesorero accede al módulo de emisión de cheques
2. El sistema muestra las cuentas bancarias disponibles
3. El tesorero selecciona:
   - Cuenta bancaria
   - Comprobante de pago a cancelar
   - Número de cheque
4. El sistema valida que el cheque esté disponible
5. El sistema genera el cheque con los datos del beneficiario
6. El tesorero confirma los datos del cheque
7. El sistema marca el cheque como emitido
8. El sistema genera el voucher correspondiente
9. El sistema actualiza el estado del comprobante de pago

### Flujo Alternativo - Reporte de Cheques
1a. El tesorero solicita reporte de cheques girados
1b. El sistema solicita filtros (banco, fechas, proveedor)
1c. El sistema genera reporte con estado de cheques

### Postcondiciones
- Cheque emitido y registrado
- Voucher generado
- Estado de chequera actualizado

---

## CU-CONTA-007: Gestionar Carga de Asientos Automáticos

### Descripción
Permite recibir e integrar asientos contables desde otros sistemas del SIG SBA para evitar doble digitación. (?) preguntar sobre el sistema actual de contabilidad, entender como funciona el sistema SIG SBA.
### Actores
- **Principal**: Sistema (automático)
- **Secundario**: Contador

### Precondiciones
- Sistemas origen configurados e integrados
- Mapeo de cuentas contables definido
- Interfaz de integración activa

### Flujo Principal
1. El sistema origen envía información contable al sistema contable
2. El sistema contable recibe los datos en formato estándar
3. El sistema valida la estructura de los datos
4. El sistema aplica el mapeo de cuentas configurado
5. El sistema valida que los asientos cuadren
6. El sistema genera los asientos contables automáticamente
7. El sistema marca los asientos como "automáticos"
8. El sistema notifica al contador sobre nuevos asientos

### Flujo Alternativo - Validación Manual
6a. Si existen inconsistencias, el sistema marca para revisión manual
6b. El contador recibe notificación de asientos pendientes
6c. El contador revisa y aprueba/corrige los asientos

### Postcondiciones
- Asientos integrados automáticamente
- Eliminación de doble digitación
- Trazabilidad del origen de asientos

---

## CU-CONTA-007.5: Entender el sistema SIG SBA
entender como funciona el sistema SIG SBA.

---

## CU-CONTA-008: Gestionar Conversión de Moneda (?)

### Descripción
Permite convertir operaciones en moneda extranjera a moneda nacional usando tipos de cambio actualizados. Serequiere conexion a una API de conversion, BN/SUNAT.

### Actores
- **Principal**: Auxiliar Contable
- **Secundario**: Sistema (automático)

### Precondiciones
- Tipos de cambio actualizados diariamente
- Operaciones registradas en moneda extranjera

### Flujo Principal
1. El auxiliar registra una operación en moneda extranjera
2. El sistema identifica que requiere conversión
3. El sistema obtiene el tipo de cambio del día
4. El sistema calcula el equivalente en moneda nacional
5. El sistema registra ambos importes (original y convertido)
6. El sistema genera asientos en moneda nacional (?)
7. El sistema mantiene la trazabilidad de la conversión

### Flujo Alternativo - Conversión Masiva
1a. El auxiliar solicita conversión masiva de un período
1b. El sistema procesa todas las operaciones pendientes
1c. El sistema aplica tipos de cambio correspondientes a cada fecha

### Postcondiciones
- Operaciones convertidas a moneda nacional
- Registros de conversión mantenidos
- Estados financieros en moneda nacional

---

## CU-CONTA-009: Gestionar Regularización de Diferencias de Cambio (?) Cual es la logica de la regularizacion

### Descripción
Permite el ajuste automático de diferencias de cambio que se generen por fluctuaciones en el tipo de cambio.

### Actores
- **Principal**: Contador
- **Secundario**: Sistema (automático)

### Precondiciones
- Saldos en moneda extranjera existentes
- Tipos de cambio históricos y actuales disponibles

### Flujo Principal
1. El contador ejecuta el proceso de regularización
2. El sistema identifica cuentas con saldos en moneda extranjera
3. El sistema calcula las diferencias de cambio por cuenta
4. El sistema determina si son ganancias o pérdidas cambiarias
5. El sistema genera asientos automáticos de regularización
6. El sistema actualiza los saldos a tipo de cambio actual
7. El sistema genera reporte de diferencias procesadas

### Flujo Alternativo - Regularización Automática
1a. El sistema ejecuta regularización automática al cierre del mes
1b. El sistema notifica al contador sobre ajustes realizados

### Postcondiciones
- Diferencias de cambio regularizadas
- Saldos actualizados a TC vigente
- Asientos de ajuste generados

---


## CU-CONTA-010: Gestionar Conciliación Bancaria (?) Como se realiza la conciliacion bancaria?

### Descripción
Permite realizar la conciliación automática de cuentas bancarias comparando movimientos del sistema con extractos bancarios.

### Actores
- **Principal**: Auxiliar Contable
- **Secundario**: Tesorero

### Precondiciones
- Extractos bancarios disponibles
- Movimientos bancarios registrados en el sistema
- Cuenta bancaria configurada

### Flujo Principal
1. El auxiliar accede al módulo de conciliación bancaria
2. El sistema muestra las cuentas bancarias disponibles
3. El auxiliar selecciona la cuenta y período a conciliar
4. El auxiliar carga el extracto bancario (Excel/CSV/manual)
5. El sistema compara movimientos automáticamente
6. El sistema identifica:
   - Movimientos conciliados
   - Movimientos solo en extracto
   - Movimientos solo en sistema
7. El auxiliar revisa y ajusta las diferencias
8. El sistema genera el reporte de conciliación
9. El auxiliar confirma la conciliación

### Flujo Alternativo - Conciliación Automática
4a. Si el banco tiene API, el sistema obtiene movimientos automáticamente
4b. El sistema ejecuta la conciliación sin intervención manual

### Postcondiciones
- Conciliación bancaria completada
- Diferencias identificadas y resueltas
- Reporte de conciliación generado

---

## CU-CONTA-011: Gestionar Presupuesto por Centro de Costo

### Descripción
Permite crear y controlar presupuestos por centros de costo, proyectos, servicios o actividades.

### Actores
- **Principal**: Contador
- **Secundario**: Jefe de Área

### Precondiciones
- Centros de costo configurados
- Plan de cuentas definido
- Período presupuestario establecido

### Flujo Principal
1. El contador accede al módulo de presupuestos
2. El sistema muestra los centros de costo disponibles
3. El contador selecciona el centro de costo a presupuestar
4. El contador define:
   - Período presupuestario
   - Cuentas contables incluidas
   - Importes presupuestados por cuenta
   - Distribución mensual
5. El sistema valida la consistencia del presupuesto
6. El sistema guarda el presupuesto aprobado
7. El sistema activa el control automático de ejecución

### Flujo Alternativo - Seguimiento de Ejecución
1a. El contador consulta la ejecución presupuestaria
1b. El sistema muestra comparativo presupuesto vs. ejecutado
1c. El sistema calcula porcentajes de ejecución y variaciones

### Postcondiciones
- Presupuesto creado y aprobado
- Control automático activado
- Base para seguimiento establecida

---

## CU-CONTA-012: Generar Reportes SUNAT

### Descripción
Permite generar archivos requeridos por SUNAT incluyendo PDTs y Libros Electrónicos (PLE).

### Actores
- **Principal**: Contador
- **Secundario**: Administrador Tributario

### Precondiciones
- Movimientos contables del período registrados
- Configuración SUNAT actualizada
- Plan de cuentas SUNAT configurado

### Flujo Principal
1. El contador accede al módulo de reportes SUNAT
2. El sistema muestra los tipos de reportes disponibles:
   - PDT Honorarios y personal
   - PDT 621 Retenciones/Percepciones
   - PDT DAOT Compras-Ventas
   - PLE Libros Electrónicos
   - PDT Renta Anual
3. El contador selecciona el tipo de reporte y período
4. El sistema procesa la información contable
5. El sistema aplica las reglas tributarias correspondientes
6. El sistema genera el archivo en formato SUNAT
7. El sistema permite descargar el archivo generado
8. El contador valida el contenido antes de envío

### Flujo Alternativo - Validación Previa
4a. El sistema ejecuta validaciones tributarias
4b. Si hay inconsistencias, el sistema genera reporte de errores
4c. El contador corrige los errores antes de generar archivo final

### Postcondiciones
- Archivo SUNAT generado correctamente
- Validaciones tributarias aprobadas
- Archivo listo para presentación

---

## CU-CONTA-013: Exportar Reportes a Excel

### Descripción
Permite exportar cualquier reporte del sistema contable a formato Excel para análisis adicional.

### Actores
- **Principal**: Usuario Contable (cualquier rol)

### Precondiciones
- Reporte generado en el sistema
- Permisos de exportación

### Flujo Principal
1. El usuario genera cualquier reporte en el sistema
2. El sistema muestra el reporte en pantalla
3. El usuario selecciona la opción "Exportar a Excel"
4. El sistema convierte el reporte a formato Excel
5. El sistema mantiene el formato y estructura original
6. El sistema genera el archivo Excel
7. El usuario descarga el archivo

### Flujo Alternativo - Exportación Programada
1a. El usuario configura exportación automática
1b. El sistema programa la generación periódica
1c. El sistema envía por email los reportes generados

### Postcondiciones
- Reporte exportado a Excel
- Formato preservado
- Archivo disponible para análisis

---

## CU-CONTA-014: Integrar Sistema Contable Actual

### Descripción
Permite evaluar e integrar el sistema contable existente de la SBA con el nuevo SIG SBA.

### Actores
- **Principal**: Administrador del Sistema
- **Secundario**: Contador Principal

### Precondiciones
- Sistema contable actual operativo
- Datos históricos identificados
- Plan de migración definido

### Flujo Principal - Evaluación
1. El administrador accede al módulo de integración
2. El sistema analiza la estructura del sistema actual
3. El administrador evalúa:
   - Datos a migrar (histórico contable)
   - Funcionalidades a preservar
   - Configuraciones actuales
   - Usuarios y permisos existentes
4. El sistema genera reporte de evaluación
5. El administrador define estrategia de integración

### Flujo Principal - Migración
1. El administrador ejecuta el proceso de migración
2. El sistema extrae datos del sistema actual
3. El sistema mapea información al nuevo esquema
4. El sistema valida la integridad de datos migrados
5. El sistema importa configuraciones aplicables
6. El sistema genera reporte de migración
7. El contador valida la información migrada

### Postcondiciones
- Datos históricos migrados
- Configuraciones preservadas
- Sistema integrado operativo

---

## CU-CONTA-015: Generar Cuentas Automáticas (?)

### Descripción
Permite la generación automática de asientos contables basados en reglas y plantillas predefinidas.

### Actores
- **Principal**: Sistema (automático)
- **Secundario**: Contador

### Precondiciones
- Plantillas de asientos configuradas
- Reglas de negocio definidas
- Eventos disparadores identificados

### Flujo Principal
1. El sistema detecta un evento que requiere asiento automático
2. El sistema identifica la plantilla aplicable
3. El sistema obtiene los datos necesarios del evento
4. El sistema aplica las reglas de cálculo configuradas
5. El sistema genera el asiento contable
6. El sistema valida que el asiento cuadre
7. El sistema registra el asiento como "automático"
8. El sistema notifica al contador (si está configurado)

### Flujo Alternativo - Configurar Plantillas
1a. El contador accede al configurador de plantillas
1b. El contador define:
   - Evento disparador
   - Cuentas contables a afectar
   - Reglas de cálculo
   - Centros de costo aplicables
1c. El sistema valida la plantilla
1d. El sistema activa la plantilla para uso automático

### Postcondiciones
- Asientos generados automáticamente
- Procesamiento sin intervención manual
- Trazabilidad del origen automático

---

## Configuraciones Técnicas Requeridas

### Integración SUNAT
- **Servicios**: API tipos de cambio, validación RUC
- **Formatos**: Archivos TXT según especificaciones SUNAT
- **Seguridad**: Certificados digitales, encriptación
- **Programación**: Tareas automáticas diarias

### Manejo de Monedas
- **Monedas**: Soles (PEN), Dólares (USD), otras según necesidad
- **Precisión**: 2 decimales para importes, 3 para tipos de cambio
- **Conversión**: Automática con TC del día

### Estructura de Datos
- **Plan de Cuentas**: Hasta 6 niveles, compatible SUNAT
- **Centros de Costo**: Estructura jerárquica flexible
- **Períodos**: Mensuales con posibilidad de reapertura

### Reportes y Exportación
- **Formatos**: Excel, PDF, TXT (SUNAT)
- **Plantillas**: Personalizables por tipo de reporte
- **Automatización**: Generación programada y envío por email

### Seguridad y Auditoría
- **Logs**: Registro completo de operaciones
- **Respaldos**: Automáticos diarios
- **Control de acceso**: Por roles y funciones específicas
- **Trazabilidad**: Seguimiento completo de modificaciones
