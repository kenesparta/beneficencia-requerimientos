# Estimación de Horas - Sistema Integral de Gestión (SIG SBA)

## Resumen Ejecutivo

Basado en el análisis de los documentos proporcionados, se han identificado 5 sistemas principales que componen el SIG SBA. A continuación se presenta la estimación detallada de horas de desarrollo para cada módulo.

## 1. Sistema de Gestión de Accesos (SSO)

### Backend Development
| Componente | Descripción | Horas |
|------------|-------------|-------|
| Integración Keycloak | Configuración y conexión con API Keycloak | 48 |
| Gestión de Usuarios | CRUD usuarios (delegado a Keycloak) | 20 |
| Gestión de Roles y Permisos | Sistema RBAC completo | 40 |
| Gestión de Perfiles | Agrupación de roles | 32 |
| Autenticación 2FA | TOTP y Email 2FA | 56 |
| Recuperación de contraseña | Flujo completo con email | 32 |
| Gestión de menús dinámicos | Menús según permisos de usuario | 40 |
| APIs de integración | Endpoints para otros sistemas | 48 |
| Configuración de email | SMTP y plantillas | 20 |
| Federación de identidades | OpenID Connect/OAuth2 | 40 |
| Auditoría y logs de seguridad | Sistema completo de trazabilidad | 32 |
| **Subtotal Backend** | | **408** |

### Frontend Development
| Componente | Descripción | Horas |
|------------|-------------|-------|
| Dashboard principal | Interfaz unificada de sistemas | 40 |
| Gestión de usuarios (admin) | Formularios CRUD | 32 |
| Configuración de perfiles | Interface de asignación de roles | 32 |
| Login y autenticación | Pantallas de login, 2FA, recuperación | 48 |
| Gestión de menús | Editor visual de menús | 40 |
| Configuración de sistema | Pantallas de administración | 32 |
| Portal de autoservicio | Interface para usuarios finales | 24 |
| **Subtotal Frontend** | | **248** |

### Testing y QA
| Componente | Descripción | Horas |
|------------|-------------|-------|
| Unit Testing | Pruebas unitarias | 56 |
| Integration Testing | Pruebas de integración | 40 |
| Security Testing | Pruebas de seguridad y vulnerabilidades | 32 |
| Performance Testing | Pruebas de carga y rendimiento | 24 |
| **Subtotal Testing** | | **152** |

**Total Sistema SSO: 808 horas**

---

## 2. Sistema Contable

### Backend Development
| Componente | Descripción | Horas |
|------------|-------------|-------|
| Plan de cuentas | CRUD y configuración contable | 50 |
| Asientos contables | Generación automática y manual | 56 |
| Estados financieros | 4 estados principales | 64 |
| Integración SUNAT | Tipos de cambio, validaciones RUC | 48 |
| Conciliación bancaria | Automatización y manual | 56 |
| Conversión de moneda | Multi-moneda automática | 50 |
| Comprobantes de pago | CRUD completo | 50 |
| Centros de costo | Gestión y reportes | 50 |
| Presupuesto por centro | Control presupuestario | 48 |
| Reportes SUNAT | PDTs y libros electrónicos | 64 |
| Carga de asientos automáticos | Integración con otros sistemas | 60 |
| Estados de cuenta | Terceros y saldos | 50 |
| Regularización diferencias | Automática de tipo de cambio | 40 |
| Análisis financiero | KPIs y ratios financieros | 32 |
| Gestión de impuestos | Cálculos automáticos IGV, Renta | 50 |
| **Subtotal Backend** | | **768** |

### Frontend Development
| Componente | Descripción | Horas |
|------------|-------------|-------|
| Dashboard contable | KPIs y métricas principales | 50 |
| Registro de asientos | Formularios de captura | 48 |
| Consulta de estados financieros | Reportes interactivos | 56 |
| Gestión de terceros | CRUD proveedores/clientes | 32 |
| Conciliación bancaria | Interface de matching | 50 |
| Configuración SUNAT | Pantallas de configuración | 32 |
| Reportes y exportación | Excel, PDF, formatos SUNAT | 48 |
| Análisis financiero visual | Gráficos y dashboards avanzados | 40 |
| **Subtotal Frontend** | | **356** |

### Testing y QA
| Componente | Descripción | Horas |
|------------|-------------|-------|
| Unit Testing | Pruebas unitarias | 56 |
| Integration Testing | Integración SUNAT y otros sistemas | 40 |
| Accuracy Testing | Validación de cálculos contables | 32 |
| Compliance Testing | Validación normativas SUNAT | 24 |
| **Subtotal Testing** | | **152** |

**Total Sistema Contable: 1,294 horas**

---

## 3. Sistema de Gestión Presupuestal (SGP)

### Backend Development
| Componente | Descripción | Horas |
|------------|-------------|-------|
| Cuadro de necesidades | CRUD por órgano estructurado | 40 |
| Catálogo bienes y servicios | Gestión de catálogo | 32 |
| Generación PIA | Presupuesto inicial de apertura | 56 |
| Generación PIM | Modificaciones presupuestales | 48 |
| Control de ejecución | Seguimiento en tiempo real | 56 |
| Plan estratégico institucional | CRUD y seguimiento | 48 |
| Plan anual de trabajo (PAT) | Formulación y modificación | 48 |
| Evaluación trimestral PAT | Seguimiento y reportes | 40 |
| Evaluación PIA/PIM | Análisis de ejecución | 40 |
| Certificación presupuestal | Generación automática | 40 |
| Integración contable | Sincronización automática | 40 |
| Alertas presupuestales | Sistema de notificaciones | 24 |
| **Subtotal Backend** | | **512** |

### Frontend Development
| Componente | Descripción | Horas |
|------------|-------------|-------|
| Dashboard presupuestal | KPIs y alertas | 40 |
| Formulación presupuestal | Interfaces PIA/PIM | 56 |
| Control de ejecución | Reportes interactivos | 48 |
| Gestión de certificaciones | CRUD certificaciones | 32 |
| Planificación estratégica | Formularios de planes | 40 |
| Evaluaciones trimestrales | Reportes de seguimiento | 40 |
| Análisis comparativo | Gráficos evolutivos | 24 |
| **Subtotal Frontend** | | **280** |

### Testing y QA
| Componente | Descripción | Horas |
|------------|-------------|-------|
| Unit Testing | Pruebas unitarias | 40 |
| Integration Testing | Integración con contabilidad | 32 |
| Business Logic Testing | Validación de reglas presupuestales | 32 |
| Workflow Testing | Pruebas de flujos de aprobación | 16 |
| **Subtotal Testing** | | **120** |

**Total Sistema SGP: 912 horas**

---

## 4. Sistema de Servicios Funerarios

### Backend Development
| Componente | Descripción | Horas |
|------------|-------------|-------|
| Gestión de nichos | CRUD completo | 40 |
| Gestión de difuntos | Registro con integración RENIEC | 48 |
| Gestión de pagos | Presencial y online | 56 |
| Concesión de nichos | Contratos y documentación | 40 |
| Gestión de renovaciones | Proceso automático y manual | 40 |
| Unión de cuerpos | Lógica de múltiples difuntos | 32 |
| Gestión de mausoleos | Venta de lotes y traslados | 40 |
| Servicios de incineración | CRUD completo | 32 |
| Gestión de pabellones | Administración de infraestructura | 32 |
| Modificaciones de nichos | Lápidas, rejas, etc. | 24 |
| Re-inhumaciones | Proceso especializado | 24 |
| Alertas de vencimiento | Sistema automático | 32 |
| Pagos en línea | Integración con pasarelas | 48 |
| Integración RENIEC | API para consulta de datos | 40 |
| Reportes estadísticos | Análisis de ocupación y servicios | 24 |
| **Subtotal Backend** | | **552** |

### Frontend Development
| Componente | Descripción | Horas |
|------------|-------------|-------|
| Portal público | Consultas online para ciudadanos | 56 |
| Dashboard operativo | Vista general del cementerio | 40 |
| Gestión de nichos | Interface administrativa | 40 |
| Registro de difuntos | Formularios con RENIEC | 40 |
| Gestión de pagos | Interface de cobranza | 40 |
| Portal de pagos online | Interface para concesionarios | 40 |
| Reportes cementerio | Dashboards específicos | 40 |
| Gestión de concesiones | Formularios de contratos | 32 |
| Mapa interactivo | Visualización del cementerio | 32 |
| **Subtotal Frontend** | | **360** |

### Testing y QA
| Componente | Descripción | Horas |
|------------|-------------|-------|
| Unit Testing | Pruebas unitarias | 48 |
| Integration Testing | RENIEC, pasarelas de pago | 40 |
| Payment Testing | Pruebas de transacciones | 24 |
| User Acceptance Testing | Pruebas con usuarios finales | 16 |
| **Subtotal Testing** | | **128** |

**Total Sistema Servicios Funerarios: 1,040 horas**

---

## 5. Componentes Transversales

### Infraestructura y DevOps
| Componente | Descripción | Horas |
|------------|-------------|-------|
| Configuración de servidores | Setup inicial de infraestructura | 48 |
| CI/CD Pipeline | Automatización de despliegue | 40 |
| Docker containers | Containerización de servicios | 32 |
| Base de datos | Diseño e implementación | 56 |
| Monitoreo y logs | Sistema de observabilidad | 40 |
| Backup y recuperación | Estrategias de respaldo | 32 |
| Seguridad infraestructura | Hardening y certificados SSL | 32 |
| Load balancing | Balanceadores de carga | 24 |
| **Subtotal DevOps** | | **304** |

### Integraciones Generales
| Componente | Descripción | Horas |
|------------|-------------|-------|
| API Gateway | Punto único de entrada | 40 |
| Service mesh | Comunicación entre microservicios | 32 |
| Event Bus | Sistema de eventos entre módulos | 40 |
| Shared libraries | Librerías comunes | 32 |
| Message queues | Sistema de colas | 24 |
| **Subtotal Integraciones** | | **168** |

### Documentación y Capacitación
| Componente | Descripción | Horas |
|------------|-------------|-------|
| Documentación técnica | APIs, arquitectura, deployment | 56 |
| Manual de usuario | Guías por cada sistema | 80 |
| Capacitación técnica | Para equipo de TI | 32 |
| Capacitación usuarios finales | Para personal operativo | 56 |
| Videos tutoriales | Material audiovisual | 32 |
| **Subtotal Documentación** | | **256** |

**Total Componentes Transversales: 728 horas**

---

## Resumen de Estimación por Sistema

| Sistema | Backend | Frontend | Testing | Total |
|---------|---------|----------|---------|-------|
| SSO | 368h | 248h | 152h | **808h** |
| Contable | 696h | 328h | 152h | **1,294h** |
| SGP | 512h | 280h | 120h | **912h** |
| Servicios Funerarios | 552h | 360h | 128h | **1,040h** |
| Componentes Transversales | - | - | - | **728h** |
| **TOTAL PROYECTO (horas)** | | | | **4,782h** |

El costo promedio por hora es de **30.00 soles**, el cosot del proyecto es: **143,460.00 soles**

---

## Cronograma Estimado por Fases

### Fase 1: Infraestructura y SSO
- **Duración**: 24 semanas (1 persona por 8h/dia de lun-vie)
- **Horas**: 920h
- **Componentes**: DevOps, SSO completo

### Fase 2: Servicios Funerarios
- **Duración**: 26 semanas (1 persona por 8h/dia de lun-vie)
- **Horas**: 1,040h
- **Componentes**: Sistemas restantes e integraciones finales

### Fase 3: Sistema Contable y SGP
- **Duración**: 52 semanas (1 persona por 8h/dia de lun-vie)
- **Horas**: 2,088h
- **Componentes**: Desarrollo paralelo de ambos sistemas

### Fase 4: Testing, Integracion e Implementación
- **Duración**: 19 semanas (1 persona por 8h/dia de lun-vie)
- **Horas**: 734h
- **Actividades**: Pruebas integrales, capacitación, go-live

**Duración Total Estimada: 121 semanas (30 meses)**

---

## Consideraciones Adicionales

### Factores que pueden afectar la estimación:
- Complejidad de integraciones con servicios externos (RENIEC, SUNAT)
- Volumen de documentos y performance requerida en SGD
- Cambios en requerimientos durante el desarrollo
- Disponibilidad del equipo cliente para validaciones
- Complejidad de migración de datos existentes

### Recomendaciones:
- Implementación por fases para validación temprana
- Prototipado de integraciones críticas antes del desarrollo
- Buffer de contingencia del 15-20% adicional
- Plan de capacitación estructurado desde las primeras fases
- Establecimiento de un entorno de testing dedicado
