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

```
#arquitectura 

```mermaid
sequenceDiagram
    participant Cliente
    participant MedioPago as Medio de pago digital
    participant Servicio as Servicio de procesamiento
    participant DB as Base de datos
    participant App as App / Panel

    Cliente->>MedioPago: Realiza un pago
    MedioPago->>Servicio: Llega mensaje o notificación
    Servicio->>Servicio: Extrae valor, fecha, pagador y referencia
    Servicio->>DB: Guarda pago normalizado
    App->>DB: Consulta coincidencias o balances
    App->>DB: Marca pago como validado
    App->>Cliente: Confirma venta registrada

```



