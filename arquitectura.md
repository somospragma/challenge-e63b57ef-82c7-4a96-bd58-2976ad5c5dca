# Arquitectura del Sistema de APIs

## Vista de Componentes

El sistema de APIs de Pragma está compuesto por los siguientes componentes principales, cada uno con responsabilidades bien definidas:

### 1. **API Gateway**
- **Responsabilidad**: Punto de entrada para todas las solicitudes externas. Maneja el enrutamiento, autenticación, limitación de tasa y caching.
- **Dependencias**:
  - Sistema de Autenticación (Keycloak)
  - Motor de Reglas (Drools)
  - Servicios de Negocio (APIs internas)
- **Contratos**:
  - OpenAPI 3.1 (`contratos/openapi.yaml`)
  - Límites de tasa definidos en `atributos-de-calidad.md`.

### 2. **Sistema de Autenticación (Keycloak)**
- **Responsabilidad**: Gestionar la autenticación y autorización de usuarios y servicios.
- **Dependencias**:
  - Base de Datos de Usuarios
- **Contratos**:
  - OAuth 2.0 / OpenID Connect

### 3. **Motor de Reglas (Drools)**
- **Responsabilidad**: Ejecutar reglas de negocio dinámicas para validar solicitudes y determinar flujos.
- **Dependencias**:
  - Repositorio de Reglas
- **Contratos**:
  - API REST para ejecución de reglas

### 4. **Servicio de Notificaciones**
- **Responsabilidad**: Enviar notificaciones a usuarios y sistemas externos (email, SMS, webhooks).
- **Dependencias**:
  - Proveedores de Notificaciones (SendGrid, Twilio)
- **Contratos**:
  - API REST para envío de notificaciones

### 5. **Servicios de Negocio**
- **Responsabilidad**: Implementar la lógica de negocio específica de cada dominio (ej. Gestión de Portafolios, Evaluación de Riesgos).
- **Dependencias**:
  - Base de Datos de Negocio
  - Motor de Reglas
  - Servicio de Notificaciones
- **Contratos**:
  - OpenAPI 3.1 (`contratos/openapi.yaml`)

### 6. **Base de Datos**
- **Responsabilidad**: Almacenar datos de negocio, usuarios y reglas.
- **Dependencias**:
  - Ninguna
- **Contratos**:
  - Esquemas definidos en `contratos/openapi.yaml`

## Vista de Despliegue

```mermaid
C4Deployment
  title Despliegue del Sistema de APIs

  Deployment_Node(cloud, "AWS Cloud") {
    Deployment_Node(api_gateway, "API Gateway") {
      Container(api_gw, "API Gateway", "Kong", "Enruta solicitudes a servicios internos")
    }

    Deployment_Node(auth_service, "Servicio de Autenticación") {
      Container(auth, "Keycloak", "Keycloak", "Autenticación y autorización")
    }

    Deployment_Node(rule_engine, "Motor de Reglas") {
      Container(engine, "Drools", "Drools", "Ejecución de reglas de negocio")
    }

    Deployment_Node(notification_service, "Servicio de Notificaciones") {
      Container(notifications, "Servicio de Notificaciones", "Spring Boot", "Envío de notificaciones")
    }

    Deployment_Node(business_services, "Servicios de Negocio") {
      Container(portfolio, "Gestión de Portafolios", "Spring Boot", "Lógica de negocio de portafolios")
      Container(risk, "Evaluación de Riesgos", "Spring Boot", "Lógica de negocio de riesgos")
    }

    Deployment_Node(database, "Base de Datos") {
      Container(db, "PostgreSQL", "PostgreSQL", "Almacenamiento de datos")
    }
  }

  Rel(api_gw, auth, "Autenticación", "HTTPS")
  Rel(api_gw, engine, "Validación de reglas", "HTTPS")
  Rel(api_gw, portfolio, "Gestión de portafolios", "HTTPS")
  Rel(api_gw, risk, "Evaluación de riesgos", "HTTPS")
  Rel(portfolio, db, "Almacenamiento", "JDBC")
  Rel(risk, db, "Almacenamiento", "JDBC")
  Rel(notifications, auth, "Autenticación", "HTTPS")
  Rel(engine, db, "Almacenamiento de reglas", "JDBC")
  Rel(auth, db, "Almacenamiento de usuarios", "JDBC")
```

## Límites y Contratos

### Límites entre Componentes

| **Componente Origen**       | **Componente Destino**      | **Contrato**                     | **Tipo de Comunicación** |
|------------------------------|------------------------------|-----------------------------------|--------------------------|
| API Gateway                  | Sistema de Autenticación     | OAuth 2.0 / OpenID Connect        | Síncrona (HTTPS)         |
| API Gateway                  | Motor de Reglas              | API REST                          | Síncrona (HTTPS)         |
| API Gateway                  | Servicios de Negocio         | OpenAPI 3.1                       | Síncrona (HTTPS)         |
| Servicios de Negocio         | Base de Datos                | JDBC                              | Síncrona                 |
| Servicios de Negocio         | Servicio de Notificaciones   | API REST                          | Asíncrona (Webhooks)     |
| Motor de Reglas              | Base de Datos                | JDBC                              | Síncrona                 |

### Contratos de APIs

Los contratos detallados de las APIs se encuentran en:
- `contratos/openapi.yaml`: Definición de endpoints, esquemas, ejemplos y versiones.
- `atributos-de-calidad.md`: Métricas y umbrales de calidad para cada API.

## Flujos Críticos

### Flujo 1: Evaluación de Madurez de APIs
```mermaid
sequenceDiagram
  actor Arquitecto as Arquitecto
  participant Catalogo as Catálogo de APIs
  participant Evaluacion as Evaluación de Madurez
  participant Modelo as Modelo de Madurez
  participant Propuesta as Propuestas de Mejora

  Arquitecto->>Catalogo: Identificar APIs
  Catalogo-->>Arquitecto: Lista de APIs
  Arquitecto->>Modelo: Consultar criterios de madurez
  Modelo-->>Arquitecto: Modelo de madurez
  Arquitecto->>Evaluacion: Evaluar APIs
  Evaluacion-->>Arquitecto: Resultados de evaluación
  Arquitecto->>Propuesta: Proponer mejoras
  Propuesta-->>Arquitecto: Plan de acción
```

### Flujo 2: Procesamiento de una Solicitud de API
```mermaid
sequenceDiagram
  actor Cliente as Cliente
  participant Gateway as API Gateway
  participant Auth as Sistema de Autenticación
  participant Engine as Motor de Reglas
  participant Business as Servicios de Negocio
  participant Notifications as Servicio de Notificaciones

  Cliente->>Gateway: Solicitud (ej. POST /portfolios)
  Gateway->>Auth: Validar token
  Auth-->>Gateway: Token válido
  Gateway->>Engine: Validar reglas
  Engine-->>Gateway: Reglas cumplidas
  Gateway->>Business: Procesar solicitud
  Business->>Business: Lógica de negocio
  Business->>Notifications: Enviar notificación
  Business-->>Gateway: Respuesta
  Gateway-->>Cliente: Respuesta (ej. 201 Created)
```

## Decisiones Arquitectónicas Clave

1. **Uso de API Gateway**: Centralizar el enrutamiento, autenticación y limitación de tasa para todas las APIs externas.
2. **Modelo de Madurez de APIs**: Adoptar el modelo de Pragma para estandarizar la evaluación y mejora de APIs.
3. **Contratos OpenAPI**: Documentar todas las APIs con OpenAPI 3.1 para garantizar consistencia y compatibilidad.
4. **Despliegue en AWS**: Aprovechar la escalabilidad y servicios gestionados de AWS para el despliegue.

Para más detalles, consultar los ADRs en el directorio `adr/`.