# Catálogo de APIs del Sistema Pragma

## Introducción
Este documento presenta el catálogo completo de APIs identificadas en el sistema Pragma. Cada API se clasifica según su función, dependencias y nivel de exposición (interna/externa).

## APIs del Motor de Reglas

### API: Evaluación de Reglas (`/rules/evaluate`)
- **Tipo**: REST
- **Método**: POST
- **Descripción**: Evalúa una regla de negocio basada en parámetros proporcionados.
- **Dependencias**:
  - Servicio de Autenticación (validación de token JWT)
  - Base de datos de reglas (consulta de definición de reglas)
- **Exposición**: Interna y Externa (consumida por clientes externos)
- **Versión Actual**: 1.0.0
- **Documentación**: [OpenAPI](./../contratos/openapi.yaml#/paths/~1rules~1evaluate)
- **Ejemplo de Uso**:
  ```json
  {
    "ruleId": "rule-123",
    "parameters": {
      "userId": "user-456",
      "context": {
        "riskLevel": "high"
      }
    }
  }
  ```

### API: Gestión de Reglas (`/rules`)
- **Tipo**: REST
- **Métodos**: GET, POST, PUT, DELETE
- **Descripción**: Permite crear, leer, actualizar y eliminar reglas de negocio.
- **Dependencias**:
  - Servicio de Autenticación
  - Base de datos de reglas
- **Exposición**: Interna
- **Versión Actual**: 1.2.0
- **Documentación**: [OpenAPI](./../contratos/openapi.yaml)
- **Notas**: Requiere permisos de administrador.

## APIs de Autenticación

### API: Generación de Tokens (`/auth/token`)
- **Tipo**: REST
- **Método**: POST
- **Descripción**: Genera un token JWT para autenticación en endpoints protegidos.
- **Dependencias**:
  - Servicio de Autenticación (validación de credenciales)
  - Base de datos de usuarios
- **Exposición**: Interna y Externa
- **Versión Actual**: 1.1.0
- **Documentación**: [OpenAPI](./../contratos/openapi.yaml#/paths/~1auth~1token)
- **Ejemplo de Uso**:
  ```json
  {
    "clientId": "client-789",
    "clientSecret": "secret-abc"
  }
  ```

### API: Validación de Tokens (`/auth/validate`)
- **Tipo**: REST
- **Método**: POST
- **Descripción**: Valida un token JWT y retorna información del usuario.
- **Dependencias**:
  - Servicio de Autenticación
- **Exposición**: Interna
- **Versión Actual**: 1.0.0
- **Documentación**: [OpenAPI](./../contratos/openapi.yaml)
- **Notas**: Usada internamente por otros servicios.

## APIs de Notificaciones

### API: Envío de Notificaciones (`/notifications/send`)
- **Tipo**: REST
- **Método**: POST
- **Descripción**: Envía notificaciones a usuarios a través de diferentes canales.
- **Dependencias**:
  - Servicio de Autenticación
  - Servicio de Notificaciones (email, SMS, push)
- **Exposición**: Interna
- **Versión Actual**: 1.3.0
- **Documentación**: [OpenAPI](./../contratos/openapi.yaml#/paths/~1notifications~1send)
- **Ejemplo de Uso**:
  ```json
  {
    "userId": "user-456",
    "message": "Tu evaluación de riesgo ha sido aprobada.",
    "channel": "email"
  }
  ```

### API: Gestión de Suscripciones (`/notifications/subscriptions`)
- **Tipo**: REST
- **Métodos**: GET, POST, DELETE
- **Descripción**: Permite gestionar suscripciones de usuarios a tipos de notificaciones.
- **Dependencias**:
  - Servicio de Autenticación
  - Base de datos de suscripciones
- **Exposición**: Interna
- **Versión Actual**: 1.0.0
- **Documentación**: [OpenAPI](./../contratos/openapi.yaml)

## APIs de Reportes

### API: Generación de Reportes (`/reports/generate`)
- **Tipo**: REST
- **Método**: POST
- **Descripción**: Genera reportes basados en consultas parametrizadas.
- **Dependencias**:
  - Servicio de Autenticación
  - Base de datos de transacciones
- **Exposición**: Interna
- **Versión Actual**: 1.1.0
- **Documentación**: [OpenAPI](./../contratos/openapi.yaml)
- **Notas**: Usada por el módulo de analítica.

## Resumen de Exposición
| Categoría               | APIs Internas | APIs Externas |
|-------------------------|----------------|----------------|
| Motor de Reglas        | 1              | 1              |
| Autenticación           | 1              | 1              |
| Notificaciones          | 2              | 0              |
| Reportes                | 1              | 0              |

## Dependencias entre APIs
- La API de Evaluación de Reglas depende de la API de Autenticación para validar tokens.
- La API de Envío de Notificaciones depende de la API de Autenticación para validar tokens.
- Todas las APIs internas dependen del Servicio de Autenticación.

## Versiones de APIs
| API                          | Versión Actual |
|------------------------------|----------------|
| Evaluación de Reglas         | 1.0.0          |
| Gestión de Reglas            | 1.2.0          |
| Generación de Tokens         | 1.1.0          |
| Validación de Tokens         | 1.0.0          |
| Envío de Notificaciones      | 1.3.0          |
| Gestión de Suscripciones     | 1.0.0          |
| Generación de Reportes       | 1.1.0          |

## Próximos Pasos
1. Evaluar la madurez de cada API según el modelo de Pragma.
2. Identificar oportunidades de mejora en documentación, seguridad y rendimiento.
3. Proponer un plan de acción para elevar la madurez de las APIs.