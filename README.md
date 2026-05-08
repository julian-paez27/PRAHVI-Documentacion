# Sistema de Validación y Gestión de Pagos para Comercios

Aplicación full stack orientada a comercios que necesitan registrar, validar y consultar pagos digitales en tiempo real. El sistema combina una interfaz administrativa web, una experiencia móvil, servicios backend y una base de datos relacional para centralizar ventas, empleados, reportes y configuración de códigos QR.

## Objetivo

Automatizar el control de pagos recibidos por medios digitales, reduciendo validaciones manuales y permitiendo que cada comercio pueda:

- Registrar su negocio.
- Administrar empleados o sedes.
- Capturar pagos desde mensajes/notificaciones.
- Validar ventas contra referencias de pago.
- Consultar balances diarios, semanales y mensuales.
- Generar reportes descargables.
- Actualizar datos del negocio y QR de cobro.

## Arquitectura General

```mermaid
flowchart TD
    A[Comercio / Administrador] --> B[Panel Web]
    A --> C[App Móvil / Web App]

    B --> D[API Backend PHP]
    C --> D

    C --> E[Servicio Backend Go]
    D --> F[(Base de Datos MySQL)]
    E --> F

    G[Mensajes o Notificaciones de Pago] --> E
    E --> H[Normalización del Pago]
    H --> F

    F --> I[Balances y Reportes]
    I --> B
    I --> C

    F --> J[Generación de QR Dinámico]
    J --> C


Componentes Principales
1. Panel Administrativo Web
Interfaz para que el comercio gestione su operación diaria. Incluye inicio de sesión, administración de empleados/sedes, consulta de ventas por fecha, carga de QR de cobro y acceso a reportes generales.

2. App Móvil / Web App
Experiencia enfocada en el uso desde celular. Permite registro, inicio de sesión, actualización de perfil, consulta de balance, gestión de empleados, historial de ventas y generación o actualización del QR asociado al comercio.

3. Backend PHP
Conjunto de servicios encargados de la autenticación, registro de empresas, gestión de empleados, actualización de datos, carga de QR, generación de reportes y consultas analíticas.

4. Servicio Go
Microservicio especializado en procesamiento de pagos. Recibe datos de mensajes o notificaciones, interpreta el contenido, extrae valor, referencia, fecha y pagador, y registra la información normalizada en la base de datos.

También implementa generación de QR dinámico, reconstruyendo el contenido de pago, insertando el monto solicitado y recalculando el CRC correspondiente al estándar EMV.

5. Base de Datos MySQL
La información se organiza alrededor de entidades como comercios, empleados, pagos recibidos, registros de ventas, mensajes originales y configuración del negocio.
