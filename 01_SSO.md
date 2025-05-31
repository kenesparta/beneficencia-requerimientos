# Casos de Uso - Sistema de Gestión de Accesos (SSO)

Toda la parte de gestion de usuarios sera implementada usando el API de Keycloack, no se requiere implementacion de Backend.

## CU-SSO-001: Gestionar Usuarios

### Descripción
Permite a un administrador registrar, modificar y eliminar usuarios del sistema.

### Actores
- **Principal**: Administrador del Sistema
- **Secundario**: Usuario (afectado por las operaciones)

### Precondiciones
- El administrador debe estar autenticado en el sistema
- El administrador debe tener permisos para gestionar usuarios

### Flujo Principal - Registrar Usuario
1. El administrador accede al módulo de gestión de usuarios
2. El sistema muestra la interfaz de registro de usuarios
3. El administrador ingresa los datos del nuevo usuario
4. El sistema valida que el nombre de usuario y correo sean únicos
5. El sistema genera la contraseña encriptada
6. El sistema registra el usuario y asigna un ID único
7. El sistema confirma la creación exitosa

### Flujo Alternativo - Modificar Usuario
3a. El administrador busca y selecciona un usuario existente
3b. El sistema muestra los datos actuales del usuario
3c. El administrador modifica los campos necesarios
3d. El sistema valida los cambios
3e. El sistema actualiza la información del usuario

### Flujo Alternativo - Eliminar Usuario
3a. El administrador busca y selecciona un usuario existente
3b. El sistema solicita confirmación de eliminación
3c. El administrador confirma la eliminación
3d. El sistema verifica que el usuario no tenga sesiones activas
3e. El sistema elimina lógicamente al usuario (cambio de estado)

### Postcondiciones
- Usuario creado/modificado/eliminado según la operación realizada
- Registro de auditoría generado

### Excepciones
- **E1**: Nombre de usuario ya existe
- **E2**: Correo electrónico ya registrado
- **E3**: Usuario tiene sesiones activas (no se puede eliminar)

---

## CU-SSO-002: Gestionar Sistemas/Componentes

### Descripción
Permite registrar, modificar y eliminar los sistemas o componentes que formarán parte del ecosistema SSO.

### Actores
- **Principal**: Administrador del Sistema

### Precondiciones
- El administrador debe estar autenticado
- El administrador debe tener permisos para gestionar sistemas

### Flujo Principal - Registrar Sistema
1. El administrador accede al módulo de gestión de sistemas
2. El sistema muestra la interfaz de registro
3. El administrador ingresa:
   - Nombre del sistema/componente
   - Descripción
   - URL base
   - Tipo de integración (SAML, OAuth, JWT, etc.)
   - Estado (activo/inactivo)
   - Configuraciones específicas de integración
4. El sistema valida la información
5. El sistema genera las credenciales de integración (client_id, secret, etc.)
6. El sistema registra el nuevo sistema/componente

### Postcondiciones
- Sistema/componente registrado en el directorio SSO
- Credenciales de integración generadas

---

## CU-SSO-003: Gestionar Perfiles

### Descripción
Permite crear, modificar y eliminar perfiles que agrupan conjuntos de roles y permisos.

### Actores
- **Principal**: Administrador del Sistema

### Precondiciones
- El administrador debe estar autenticado
- Los roles a asignar deben existir previamente

### Flujo Principal
1. El administrador accede al módulo de gestión de perfiles
2. El sistema muestra la lista de perfiles existentes
3. El administrador selecciona crear nuevo perfil
4. El administrador ingresa:
   - Nombre del perfil
   - Descripción
   - Lista de roles asignados
   - Sistemas aplicables
5. El sistema valida la información
6. El sistema crea el perfil con los roles asignados

---

## CU-SSO-004: Gestionar Roles

### Descripción
Permite definir, modificar y eliminar roles que determinan las funcionalidades disponibles. Utilizar RBAC (Role-Based Access Control)

### Actores
- **Principal**: Administrador del Sistema

### Flujo Principal
1. El administrador accede a la gestión de roles
2. El sistema muestra los roles existentes
3. El administrador crea un nuevo rol especificando:
   - Nombre del rol
   - Descripción
   - Sistema al que pertenece
   - Lista de permisos asociados
4. El sistema valida que el rol no exista en ese sistema
5. El sistema registra el nuevo rol

---

## CU-SSO-005: Gestionar Menús

### Descripción
Permite configurar la estructura de menús y opciones disponibles para cada rol/perfil. El menú principal unificado que agrupe todos los sistemas.

### Actores
- **Principal**: Administrador del Sistema

### Flujo Principal
1. El administrador accede a la configuración de menús
2. El sistema muestra la estructura jerárquica actual
3. El administrador puede:
   - Crear nuevos elementos de menú
   - Modificar elementos existentes
   - Establecer jerarquías padre-hijo
   - Asignar iconos y rutas
   - Definir el orden de visualización
4. El sistema actualiza la estructura de menús

---

## CU-SSO-006: Gestionar Permisos

### Descripción
Permite definir permisos granulares que pueden ser asignados a roles.

### Actores
- **Principal**: Administrador del Sistema

### Flujo Principal
1. El administrador accede a la gestión de permisos
2. El sistema muestra los permisos existentes organizados por sistema
3. El administrador puede:
   - Crear nuevos permisos especificando:
     - Código único del permiso
     - Nombre descriptivo
     - Sistema al que pertenece
     - Recurso afectado
     - Acción permitida (crear, leer, actualizar, eliminar)
4. El sistema registra el permiso

---

## CU-SSO-007: Iniciar Sesión

### Descripción
Permite a un usuario autenticarse en el sistema SSO y acceder a los sistemas integrados.

### Actores
- **Principal**: Usuario del Sistema

### Precondiciones
- El usuario debe estar registrado y activo
- El sistema debe estar disponible

### Flujo Principal
1. El usuario accede a la página de inicio de sesión
2. El sistema muestra el formulario de autenticación
3. El usuario ingresa sus credenciales:
   - Nombre de usuario o correo electrónico
   - Contraseña
4. El sistema valida las credenciales
5. El sistema verifica que el usuario esté activo
6. El sistema genera el token de sesión (JWT)
7. El sistema registra el inicio de sesión en auditoría (?)
8. El sistema redirige al usuario al dashboard principal
9. El sistema muestra los sistemas/aplicaciones disponibles según sus permisos

### Flujos Alternativos
**3a. Autenticación con segundo factor**
1. Después de validar credenciales, el sistema solicita el segundo factor
2. El usuario ingresa el código 2FA
3. El sistema valida el código

### Excepciones
- **E1**: Credenciales incorrectas
- **E2**: Usuario inactivo o bloqueado
- **E3**: Demasiados intentos fallidos
- **E4**: Código 2FA incorrecto

---

## CU-SSO-008: Recuperar Contraseña (?)

### Descripción
Permite a un usuario restablecer su contraseña cuando la ha olvidado.

### Actores
- **Principal**: Usuario del Sistema

### Flujo Principal
1. El usuario accede a la opción "Olvidé mi contraseña"
2. El sistema muestra el formulario de recuperación
3. El usuario ingresa su correo electrónico
4. El sistema valida que el correo esté registrado
5. El sistema genera un token de recuperación temporal
6. El sistema envía un correo con el enlace de recuperación
7. El usuario hace clic en el enlace del correo
8. El sistema valida el token y su vigencia
9. El sistema muestra el formulario de nueva contraseña
10. El usuario ingresa y confirma la nueva contraseña
11. El sistema valida las políticas de contraseña
12. El sistema actualiza la contraseña
13. El sistema invalida el token de recuperación
14. El sistema confirma el cambio exitoso

### Excepciones
- **E1**: Correo no registrado
- **E2**: Token expirado o inválido
- **E3**: Nueva contraseña no cumple políticas

---

## CU-SSO-009: Configurar Servidor de Email (?)

### Descripción
Permite configurar y gestionar el servidor SMTP para el envío de correos electrónicos del sistema.

### Actores
- **Principal**: Administrador del Sistema

### Precondiciones
- El administrador debe estar autenticado
- Debe tener permisos de configuración del sistema

### Flujo Principal
1. El administrador accede al módulo de configuración de email
2. El sistema muestra la configuración actual del servidor SMTP
3. El administrador configura los parámetros:
   - Servidor SMTP (host y puerto)
   - Tipo de seguridad (TLS/SSL)
   - Credenciales de autenticación
   - Email remitente por defecto
   - Plantillas de correo (recuperación, notificaciones, etc.)
4. El sistema valida la configuración
5. El sistema realiza una prueba de conexión
6. El sistema guarda la configuración

### Postcondiciones
- Servidor de email configurado y funcional
- Plantillas de correo disponibles para uso

---

## CU-SSO-010: Gestionar Integración con Keycloak

### Descripción
Permite configurar y gestionar la integración con el servidor Keycloak para federación de identidades.

### Actores
- **Principal**: Administrador del Sistema

### Precondiciones
- Servidor Keycloak desplegado y accesible
- El administrador debe tener credenciales de administración de Keycloak

### Flujo Principal - Configurar Integración
1. El administrador accede al módulo de integración Keycloak
2. El sistema muestra la interfaz de configuración
3. El administrador configura:
   - URL del servidor Keycloak
   - Realm a utilizar
   - Client ID y Client Secret
   - Mapeo de atributos de usuario
   - Configuración de roles y grupos
4. El sistema valida la conectividad con Keycloak
5. El sistema sincroniza la configuración inicial
6. El sistema confirma la integración exitosa

### Flujo Alternativo - Sincronizar Usuarios
3a. El administrador selecciona sincronización de usuarios
3b. El sistema obtiene usuarios desde Keycloak
3c. El sistema mapea los usuarios según configuración
3d. El sistema actualiza la base local con usuarios sincronizados

### Postcondiciones
- Integración con Keycloak activa
- Usuarios sincronizados (si aplica)

---

## CU-SSO-011: Configurar Autenticación de Dos Factores (2FA)

### Descripción
Permite configurar y gestionar la autenticación de dos factores para usuarios.

### Actores
- **Principal**: Administrador del Sistema
- **Secundario**: Usuario Final

### Precondiciones
- Sistema de email configurado
- Usuario debe estar autenticado para configurar su 2FA

### Flujo Principal - Configurar 2FA por Usuario
1. El usuario accede a su perfil de seguridad
2. El sistema muestra las opciones de 2FA disponibles:
   - Autenticador por aplicación (TOTP)
   - Código por email
   - Código por SMS (si está disponible)
3. El usuario selecciona el método preferido
4. **Si es TOTP**:
   4a. El sistema genera un código QR con la clave secreta
   4b. El usuario escanea el QR con su aplicación autenticadora
   4c. El usuario ingresa el código generado para verificación
5. **Si es Email**:
   5a. El sistema envía un código de verificación al email
   5b. El usuario ingresa el código recibido
6. El sistema valida la configuración
7. El sistema activa 2FA para el usuario
8. El sistema genera códigos de respaldo de emergencia

### Flujo Principal - Administrar 2FA Global
1. El administrador accede a configuración de seguridad
2. El sistema muestra opciones globales de 2FA:
   - Habilitar/deshabilitar 2FA obligatorio
   - Métodos permitidos
   - Configuración de proveedores (SMTP, SMS gateway)
   - Políticas de códigos de respaldo
3. El administrador configura las políticas deseadas
4. El sistema aplica la configuración global

### Postcondiciones
- 2FA configurado para el usuario/sistema
- Códigos de respaldo generados

---

## CU-SSO-012: Autenticación con 2FA

### Descripción
Proceso de autenticación que incluye el segundo factor de autenticación.

### Actores
- **Principal**: Usuario del Sistema

### Precondiciones
- Usuario debe tener 2FA activado
- Usuario debe haber iniciado sesión con credenciales válidas

### Flujo Principal
1. El usuario completa el login inicial (usuario/contraseña)
2. El sistema valida las credenciales primarias
3. El sistema identifica que el usuario tiene 2FA activo
4. El sistema determina el método 2FA configurado
5. **Si es TOTP**:
   5a. El sistema solicita el código de la aplicación autenticadora
   5b. El usuario ingresa el código TOTP
   5c. El sistema valida el código contra la clave secreta
6. **Si es Email**:
   6a. El sistema genera y envía código temporal por email
   6b. El usuario ingresa el código recibido
   6c. El sistema valida el código y su vigencia
7. El sistema completa la autenticación
8. El sistema genera el token de sesión completo

### Flujo Alternativo - Usar Código de Respaldo
5a. El usuario selecciona "usar código de respaldo"
5b. El sistema solicita un código de respaldo
5c. El usuario ingresa uno de sus códigos de emergencia
5d. El sistema valida y marca el código como usado
5e. Continúa con el paso 7

### Excepciones
- **E1**: Código 2FA incorrecto o expirado
- **E2**: Demasiados intentos fallidos
- **E3**: Todos los códigos de respaldo agotados

---

## CU-SSO-013: Gestionar Códigos de Respaldo

### Descripción
Permite generar y gestionar códigos de respaldo para acceso de emergencia.

### Actores
- **Principal**: Usuario del Sistema
- **Secundario**: Administrador del Sistema

### Flujo Principal - Regenerar Códigos
1. El usuario accede a configuración de seguridad
2. El sistema muestra el estado actual de códigos de respaldo
3. El usuario solicita regenerar códigos
4. El sistema invalida códigos anteriores
5. El sistema genera 10 nuevos códigos únicos
6. El sistema muestra los códigos para que el usuario los guarde
7. El usuario confirma que ha guardado los códigos
8. El sistema confirma la regeneración

### Flujo Alternativo - Admin Reset
1. El administrador accede a gestión de usuarios
2. El administrador selecciona un usuario específico
3. El administrador solicita reset de 2FA
4. El sistema desactiva 2FA del usuario
5. El sistema notifica al usuario por email
6. El usuario debe reconfigurar 2FA en próximo login

---

## CU-SSO-014: Envío de Notificaciones por Email

### Descripción
Gestiona el envío automatizado de correos electrónicos para diversos eventos del sistema.

### Actores
- **Principal**: Sistema (automático)
- **Secundario**: Usuario destinatario

### Flujo Principal
1. El sistema detecta un evento que requiere notificación:
   - Recuperación de contraseña
   - Nuevo usuario creado
   - Código 2FA
   - Alertas de seguridad
   - Cambios en permisos
2. El sistema selecciona la plantilla de email apropiada
3. El sistema personaliza la plantilla con datos específicos
4. El sistema envía el email via servidor SMTP configurado
5. El sistema registra el envío en logs de auditoría

### Tipos de Notificaciones
- **Recuperación de contraseña**: Enlace temporal para reset
- **Bienvenida**: Credenciales iniciales para nuevos usuarios
- **Códigos 2FA**: Códigos temporales de autenticación
- **Alertas de seguridad**: Login desde nueva ubicación/dispositivo
- **Cambios de permisos**: Notificación de modificaciones en accesos

---

## CU-SSO-015: Federación de Identidades

### Descripción
Permite la autenticación federada usando Keycloak como proveedor de identidad.

### Actores
- **Principal**: Usuario del Sistema
- **Secundario**: Servidor Keycloak

### Flujo Principal
1. El usuario accede al sistema SIG SBA
2. El sistema detecta configuración de federación activa
3. El usuario selecciona "Iniciar sesión con Keycloak"
4. El sistema redirige al usuario a Keycloak
5. El usuario se autentica en Keycloak
6. Keycloak valida credenciales y permisos
7. Keycloak retorna token de autenticación al SIG SBA
8. El sistema valida el token con Keycloak
9. El sistema mapea usuario y permisos desde Keycloak
10. El sistema crea sesión local para el usuario
11. El usuario accede al dashboard del SIG SBA

### Postcondiciones
- Usuario autenticado vía federación
- Sesión sincronizada entre sistemas

---

## Configuraciones Técnicas Requeridas

### Integración con Servidor de Email
- **Protocolo**: SMTP con TLS/SSL
- **Plantillas**: HTML responsivas para diferentes tipos de notificación
- **Configuración**: Host, puerto, credenciales, email remitente
- **Logs**: Registro de envíos exitosos y fallos

### Integración con Keycloak
- **Protocolo**: OpenID Connect / OAuth 2.0
- **Configuración**: Realm, Client ID/Secret, endpoints
- **Mapeo**: Atributos de usuario, roles, grupos
- **Sincronización**: Manual o automática de usuarios

### Sistema 2FA
- **TOTP**: Compatible con Google Authenticator, Authy
- **Email**: Códigos temporales de 6 dígitos
- **Respaldo**: 10 códigos de emergencia de uso único
- **Políticas**: Tiempo de expiración, intentos máximos

## Preguntas Adicionales para Completar el Diseño

1. Mencionar las y áreas/departamentos.

2. ¿Cuáles son los requisitos específicos de complejidad y vigencia de las contraseñas?

3. ¿Se permite sesiones concurrentes (al mismo tiempo)?

4. Audtoria ¿Qué nivel de detalle se requiere en los logs de auditoría?

5. ¿Se requiere también 2FA por SMS o solo email y TOTP?
