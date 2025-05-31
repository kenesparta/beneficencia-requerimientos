Preguntas para el diseño del Sistema de Gestión Presupuestal:

- Estructuras organizacionales: ¿Cuáles son los "órganos estructurados" específicos de la SBA? (por ejemplo: Gerencia General, Área de Servicios Funerarios, etc.)

- Certificación presupuestal: ¿Quién puede solicitar y aprobar las certificaciones presupuestales? ¿Hay límites de monto?

- Integración contable: ¿El sistema presupuestal debe integrarse automáticamente con el sistema contable para el control de ejecución?

- Plan Estratégico vs PAT: ¿El Plan Estratégico Institucional es de varios años y el PAT (Plan Anual de Trabajo) es anual? ¿Cómo se relacionan?

- Evaluaciones trimestrales: ¿Quién realiza estas evaluaciones y qué acciones se pueden tomar según los resultados?

- Control de ingresos: ¿La SBA tiene ingresos propios además del presupuesto asignado? ¿De qué tipo?


# Casos de Uso - Sistema de Gestión Presupuestal (SGP) (?)


## CU-SGP-001: Gestionar Cuadro de Necesidades
(?) Ver las bases legales para el cuadro de necesidades

### Descripción
Permite generar y mantener el cuadro de necesidades por cada órgano estructurado o meta presupuestal de la SBA.

### Actores
- **Principal**: Responsable de Área/Órgano
- **Secundario**: Coordinador Presupuestal, Gerente General

### Precondiciones
- El usuario debe estar autenticado
- Debe tener permisos para gestionar presupuesto de su área
- El período fiscal debe estar activo

### Flujo Principal - Generar Cuadro de Necesidades
1. El responsable del área accede al módulo de gestión presupuestal
2. El sistema muestra las opciones de gestión por órgano estructurado
3. El responsable selecciona "Generar Cuadro de Necesidades"
4. El sistema solicita:
   - Órgano estructurado o meta presupuestal
   - Período (año fiscal)
   - Tipo de necesidad (gastos corrientes, inversión, etc.)
5. El responsable ingresa las necesidades detallando:
   - Descripción de la necesidad
   - Justificación
   - Monto estimado
   - Período de ejecución
   - Prioridad (alta, media, baja)
   - Clasificador presupuestal
6. El sistema valida la consistencia de la información
7. El sistema registra el cuadro de necesidades
8. El sistema notifica al coordinador presupuestal

### Flujo Alternativo - Modificar Cuadro
3a. El responsable selecciona un cuadro existente
3b. El sistema verifica que esté en estado "borrador" o "en revisión"
3c. El responsable modifica los campos necesarios
3d. El sistema actualiza la información

### Flujo Alternativo - Consolidar Necesidades
1a. El coordinador presupuestal accede a consolidación
1b. El sistema muestra todos los cuadros por órgano
1c. El coordinador revisa y consolida las necesidades
1d. El sistema genera el cuadro consolidado institucional

### Postcondiciones
- Cuadro de necesidades registrado y disponible para revisión
- Notificación enviada a coordinador presupuestal

### Excepciones
- **E1**: Montos exceden techo presupuestal del área
- **E2**: Clasificador presupuestal no válido
- **E3**: Período fiscal cerrado para modificaciones

---

## CU-SGP-002: Gestionar Catálogo de Bienes y Servicios (?)

Consultar si se va usar el catadolo del SIAF o si ustedes tienen su propio catalogo. Segun el catalogo se tiene que alimentar el cuadro de necesidades.

### Descripción
Permite crear y mantener el catálogo de bienes y servicios utilizado para la planificación presupuestal.

### Actores
- **Principal**: Coordinador Presupuestal
- **Secundario**: Responsable de Logística

### Precondiciones
- Usuario autenticado con permisos de gestión de catálogo
- Clasificadores presupuestales configurados

### Flujo Principal - Crear Item del Catálogo
1. El coordinador accede al módulo de catálogo
2. El sistema muestra la interfaz de gestión del catálogo
3. El coordinador selecciona "Agregar nuevo item"
4. El coordinador ingresa:
   - Código del bien/servicio
   - Descripción detallada
   - Unidad de medida
   - Precio referencial
   - Clasificador presupuestal asociado
   - Tipo (bien o servicio)
   - Estado (activo/inactivo)
5. El sistema valida que el código sea único
6. El sistema registra el item en el catálogo
7. El sistema confirma la creación exitosa

### Flujo Alternativo - Actualizar Precios
3a. El coordinador selecciona "Actualizar precios masivamente"
3b. El sistema permite importar archivo con nuevos precios
3c. El sistema valida el formato y consistencia
3d. El sistema actualiza los precios en el catálogo
3e. El sistema genera reporte de cambios realizados

### Postcondiciones
- Catálogo actualizado y disponible para planificación
- Historial de cambios registrado

---

## CU-SGP-003: Generar PIA (Presupuesto Institucional de Apertura)

(?) Consultar si se va usar el SIAF

### Descripción
Permite generar el Presupuesto Institucional de Apertura tanto de ingresos como egresos para el año fiscal.

### Actores
- **Principal**: Coordinador Presupuestal
- **Secundario**: Gerente General, Contador

### Precondiciones
- Cuadros de necesidades consolidados
- Catálogo de bienes y servicios actualizado
- Marco macroeconómico multianual disponible

### Flujo Principal
1. El coordinador presupuestal accede a formulación del PIA
2. El sistema muestra el dashboard de formulación presupuestal
3. El coordinador selecciona "Generar PIA" para el año fiscal
4. El sistema solicita confirmación del año y parámetros base
5. **Formulación de Ingresos**:
   5a. El sistema presenta las fuentes de financiamiento disponibles
   5b. El coordinador ingresa las estimaciones de ingresos por:
       - Recursos ordinarios
       - Recursos directamente recaudados
       - Donaciones y transferencias
       - Recursos por operaciones oficiales de crédito
   5c. El sistema valida las proyecciones contra históricos
6. **Formulación de Egresos**:
   6a. El sistema carga los cuadros de necesidades consolidados
   6b. El coordinador asigna recursos por:
       - Gastos corrientes (personal, bienes, servicios)
       - Gastos de capital (inversiones)
       - Servicio de deuda
   6c. El sistema verifica equilibrio presupuestal (ingresos = egresos)
7. El sistema genera el PIA estructurado por clasificadores
8. El coordinador revisa y valida el presupuesto generado
9. El sistema guarda el PIA para aprobación
10. El sistema notifica al Gerente General para aprobación

### Validaciones del Sistema
- Equilibrio presupuestal obligatorio
- Montos no pueden exceder techos establecidos
- Clasificadores deben ser válidos según normativa
- Consistencia con marcos normativos

### Postcondiciones
- PIA generado y listo para aprobación
- Documento disponible para revisión de gerencia

---

## CU-SGP-004: Generar PIM (Presupuesto Institucional Modificado)
(?) Consultar si se va usar el SIAF

### Descripción
Permite generar modificaciones al presupuesto durante el año fiscal, actualizando el PIA original.

### Actores
- **Principal**: Coordinador Presupuestal
- **Secundario**: Responsable de Área, Gerente General

### Precondiciones
- PIA aprobado y vigente
- Justificación documentada para la modificación
- Disponibilidad presupuestal verificada

### Flujo Principal - Modificación Presupuestal
1. El coordinador presupuestal accede a modificaciones presupuestales
2. El sistema muestra el PIA vigente y modificaciones anteriores
3. El coordinador selecciona "Nueva Modificación PIM"
4. El sistema solicita:
   - Tipo de modificación (crédito suplementario, transferencia, etc.)
   - Órgano/programa afectado
   - Justificación de la modificación
5. **Para Transferencias**:
   5a. El coordinador selecciona partidas de origen (disminución)
   5b. El coordinador selecciona partidas de destino (aumento)
   5c. El sistema verifica disponibilidad en partidas origen
   5d. El sistema valida que no se afecten compromisos existentes
6. **Para Créditos Suplementarios**:
   6a. El coordinador especifica la fuente de financiamiento adicional
   6b. El sistema verifica la disponibilidad de recursos
   6c. El coordinador asigna los recursos a partidas específicas
7. El sistema calcula el nuevo PIM resultante
8. El sistema genera la resolución de modificación presupuestal
9. El coordinador envía para aprobación según monto y tipo

### Flujo Alternativo - Modificación de Emergencia
4a. Para modificaciones de emergencia
4b. El sistema aplica procedimiento simplificado
4c. Se requiere ratificación posterior

### Postcondiciones
- PIM actualizado con las modificaciones aprobadas
- Resolución de modificación generada
- Notificación a áreas afectadas

---

## CU-SGP-005: Controlar Ejecución Presupuestal
(?) Consultar si se va usar el SIAF

### Descripción
Permite realizar el control y seguimiento de la ejecución presupuestal de ingresos y gastos en tiempo real.

### Actores
- **Principal**: Coordinador Presupuestal, Contador
- **Secundario**: Responsables de Área, Gerente General

### Precondiciones
- PIA/PIM aprobado y vigente
- Integración con sistema contable activa
- Registros de compromisos y devengados actualizados

### Flujo Principal - Control de Ejecución
1. El usuario accede al módulo de control presupuestal
2. El sistema muestra el dashboard de ejecución con:
   - Resumen por tipo de gasto
   - Avance por órganos estructurados
   - Alertas de sobre-ejecución o sub-ejecución
3. El usuario selecciona el período y nivel de análisis
4. El sistema presenta:
   - **Ejecución de Ingresos**:
     - Ingresos programados vs recaudados
     - Proyección de ingresos para el resto del año
     - Análisis de estacionalidad
   - **Ejecución de Gastos**:
     - Presupuesto inicial (PIA)
     - Modificaciones (PIM)
     - Compromisos asumidos
     - Devengados ejecutados
     - Pagos realizados
     - Saldo disponible
5. El sistema calcula automáticamente:
   - Porcentaje de ejecución por partida
   - Velocidad de ejecución (tendencia)
   - Proyección de cierre de año
6. El usuario puede generar reportes específicos por:
   - Clasificador funcional
   - Clasificador económico
   - Fuente de financiamiento
   - Centro de costo

### Flujo Alternativo - Alertas Automáticas
4a. El sistema detecta desviaciones significativas
4b. Genera alertas automáticas para:
    - Partidas con ejecución menor al 25% al segundo trimestre
    - Partidas en riesgo de sobre-ejecución
    - Compromisos que exceden saldos disponibles
4c. Envía notificaciones a responsables

### Postcondiciones
- Control de ejecución actualizado
- Reportes de seguimiento disponibles
- Alertas generadas según configuración

---

## CU-SGP-006: Gestionar Plan Estratégico Institucional

(?) Detallar sobre que deberia contener el plan. Identificar si es objetivo, presupuestal o economico.

### Descripción
Permite elaborar, actualizar y hacer seguimiento al Plan Estratégico Institucional de la SBA.

### Actores
- **Principal**: Coordinador de Planificación
- **Secundario**: Gerente General, Responsables de Área

### Precondiciones
- Usuario autenticado con permisos de planificación
- Diagnóstico institucional disponible
- Lineamientos estratégicos definidos

### Flujo Principal - Elaborar Plan Estratégico
1. El coordinador accede al módulo de planificación estratégica
2. El sistema muestra la plantilla del plan estratégico
3. El coordinador desarrolla:
   - **Análisis situacional**:
     - Diagnóstico interno (fortalezas, debilidades)
     - Análisis externo (oportunidades, amenazas)
     - Análisis de stakeholders
   - **Direccionamiento estratégico**:
     - Misión y visión institucional
     - Valores organizacionales
     - Objetivos estratégicos
   - **Estrategias y acciones**:
     - Estrategias por objetivo
     - Acciones estratégicas específicas
     - Indicadores de resultado
     - Metas cuantificadas
   - **Recursos requeridos**:
     - Estimación presupuestal por estrategia
     - Recursos humanos necesarios
     - Recursos técnicos y logísticos
4. El sistema valida la consistencia entre objetivos y recursos
5. El coordinador vincula objetivos estratégicos con el presupuesto
6. El sistema genera el documento del Plan Estratégico
7. Se envía para revisión y aprobación

### Flujo Alternativo - Actualizar Plan
3a. El coordinador selecciona un plan existente
3b. El sistema permite modificar componentes específicos
3c. Se registra la versión y motivos del cambio

### Postcondiciones
- Plan Estratégico Institucional elaborado
- Vinculación con presupuesto establecida
- Base para formulación del PAT creada

---

## CU-SGP-007: Formular Plan Anual de Trabajo (PAT) modificado

### Descripción
Permite elaborar y modificar el Plan Anual de Trabajo alineado con el Plan Estratégico Institucional, esto es trimestral.

### Actores
- **Principal**: Coordinador de Planificación
- **Secundario**: Responsables de Área, Coordinador Presupuestal

### Precondiciones
- Plan Estratégico Institucional aprobado
- PIA formulado para el año fiscal
- Estructura organizacional definida

### Flujo Principal - Formular PAT
1. El coordinador accede a formulación del PAT
2. El sistema carga los objetivos del Plan Estratégico
3. El coordinador desarrolla para cada objetivo:
   - **Actividades específicas del año**:
     - Descripción detallada de actividades
     - Cronograma de ejecución
     - Responsable de ejecución
     - Recursos necesarios
   - **Metas anuales**:
     - Indicadores cuantificables
     - Valores meta para el año
     - Medio de verificación
   - **Presupuesto asignado**:
     - Vinculación con partidas del PIA
     - Distribución temporal del gasto
4. El sistema valida:
   - Coherencia con objetivos estratégicos
   - Disponibilidad presupuestal
   - Factibilidad de cronogramas
5. El coordinador genera el PAT consolidado
6. El sistema calcula automáticamente:
   - Distribución presupuestal por trimestre
   - Cronograma maestro de actividades
   - Indicadores de seguimiento
7. Se envía para aprobación de gerencia

### Flujo Alternativo - PAT Modificado
1a. Durante el año se requieren ajustes al PAT
1b. El coordinador accede a "Modificar PAT"
1c. Se justifican los cambios propuestos
1d. Se actualiza el PAT y se genera nueva versión

### Postcondiciones
- PAT formulado y aprobado
- Base para seguimiento trimestral establecida
- Cronograma de actividades generado

---

## CU-SGP-008: Evaluar Plan Anual de Trabajo

### Descripción
Permite realizar la evaluación trimestral del avance del Plan Anual de Trabajo. Esta evgaluacion es despues de la ejecucion

### Actores
- **Principal**: Coordinador de Planificación
- **Secundario**: Responsables de Área, Gerente General

### Precondiciones
- PAT aprobado y en ejecución
- Información de avance registrada por las áreas
- Trimestre fiscal cerrado

### Flujo Principal - Evaluación Trimestral
1. El coordinador accede al módulo de evaluación del PAT
2. El sistema muestra el PAT vigente por trimestre
3. El coordinador solicita información de avance a las áreas
4. Los responsables de área registran:
   - Porcentaje de avance por actividad
   - Logros obtenidos
   - Dificultades encontradas
   - Medidas correctivas propuestas
5. El sistema calcula automáticamente:
   - Porcentaje de avance por objetivo estratégico
   - Cumplimiento de metas trimestrales
   - Ejecución presupuestal asociada
6. El coordinador analiza:
   - Desviaciones significativas
   - Causas de incumplimiento
   - Impacto en objetivos anuales
7. El sistema genera el informe de evaluación trimestral
8. Se proponen ajustes al PAT si es necesario
9. El informe se presenta a gerencia para decisiones

### Indicadores de Evaluación
- Porcentaje de actividades ejecutadas según cronograma
- Cumplimiento de metas por indicador
- Eficiencia en uso de recursos (presupuestal)
- Nivel de impacto en objetivos estratégicos

### Postcondiciones
- Evaluación trimestral completada
- Informe de seguimiento generado
- Recomendaciones para ajustes identificadas

---

## CU-SGP-009: Evaluar Ejecución PIA/PIM

### Descripción
Permite realizar la evaluación trimestral de la ejecución del Presupuesto Institucional.

### Actores
- **Principal**: Coordinador Presupuestal
- **Secundario**: Contador, Gerente General

### Precondiciones
- PIA/PIM aprobado
- Registros contables actualizados
- Trimestre fiscal cerrado

### Flujo Principal - Evaluación Trimestral PIA/PIM
1. El coordinador presupuestal accede a evaluación presupuestal
2. El sistema obtiene datos de ejecución del período
3. El sistema calcula:
   - **Análisis de Ingresos**:
     - Ingresos programados vs ejecutados
     - Variación porcentual por fuente
     - Proyección para el resto del año
   - **Análisis de Gastos**:
     - Ejecución por clasificador funcional
     - Ejecución por clasificador económico
     - Velocidad de gasto por trimestre
     - Saldos disponibles por partida
4. El sistema identifica:
   - Partidas con sub-ejecución crítica (<50% esperado)
   - Partidas en riesgo de sobre-ejecución
   - Fuentes de financiamiento con problemas de recaudación
5. El coordinador elabora análisis de:
   - Factores que afectaron la ejecución
   - Medidas correctivas implementadas
   - Proyecciones para trimestres restantes
   - Necesidades de modificación presupuestal
6. El sistema genera el informe de evaluación con:
   - Cuadros estadísticos comparativos
   - Gráficos de tendencias
   - Análisis de eficiencia presupuestal
7. Se presenta el informe a gerencia para toma de decisiones

### Postcondiciones
- Evaluación trimestral del presupuesto completada
- Recomendaciones para optimización identificadas
- Base para modificaciones presupuestales futuras

---

## CU-SGP-010: Generar Certificación Presupuestal

### Descripción
Permite generar certificaciones presupuestales que garantizan la disponibilidad de recursos para compromisos específicos.

### Actores
- **Principal**: Coordinador Presupuestal
- **Secundario**: Responsable de Área solicitante

### Precondiciones
- PIA/PIM aprobado y vigente
- Solicitud de certificación debidamente justificada
- Saldo disponible en la partida correspondiente

### Flujo Principal - Generar Certificación
1. El responsable de área solicita certificación presupuestal
2. El sistema muestra el formulario de solicitud
3. El solicitante ingresa:
   - Concepto del gasto
   - Monto requerido
   - Partida presupuestal específica
   - Período de ejecución
   - Justificación del gasto
4. El sistema valida automáticamente:
   - Disponibilidad de saldo en la partida
   - Correcta clasificación presupuestal
   - Límites de autorización del solicitante
5. Si hay disponibilidad, el coordinador presupuestal:
   - Revisa la solicitud
   - Verifica la documentación de respaldo
   - Aprueba o rechaza la certificación
6. El sistema genera la certificación presupuestal con:
   - Número único de certificación
   - Monto certificado
   - Partida específica afectada
   - Vigencia de la certificación
   - Firma digital del responsable
7. El sistema compromete el monto certificado
8. Se notifica al solicitante de la certificación aprobada

### Flujo Alternativo - Saldo Insuficiente
4a. Si no hay saldo suficiente:
4b. El sistema informa la disponibilidad actual
4c. Sugiere partidas alternativas con saldo
4d. Permite solicitar modificación presupuestal

### Postcondiciones
- Certificación presupuestal emitida
- Monto comprometido en el presupuesto
- Documento disponible para procesos de contratación

---

## Configuraciones Técnicas Requeridas

### Integración con Sistema Contable
- **Sincronización**: Automática de ejecución presupuestal
- **Frecuencia**: Diaria para compromisos y devengados
- **Datos compartidos**: Clasificadores, centros de costo, movimientos

### Reportería Automática
- **Reportes estándar**: Ejecución presupuestal, certificaciones vigentes
- **Formatos**: PDF, Excel, XML para intercambio con entidades
- **Distribución**: Automática a responsables según configuración

### Control de Versiones
- **Documentos**: PAT, Plan Estratégico, modificaciones PIM
- **Auditoría**: Registro de cambios con usuario y fecha
- **Aprobaciones**: Workflow configurable según montos y tipos

### Notificaciones Automáticas
- **Alertas**: Vencimiento de certificaciones, sub-ejecución
- **Reportes**: Envío automático de evaluaciones trimestrales
- **Escalamiento**: A niveles superiores según configuración

