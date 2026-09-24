# Atributos de Calidad del Sistema de APIs

Este documento define los atributos de calidad críticos para el sistema de APIs de Pragma, incluyendo escenarios, métricas y umbrales cuantificables. Estos atributos guían la evaluación de madurez y las propuestas de mejora.

## 1. Disponibilidad

### Escenario
El sistema debe estar disponible para procesar solicitudes de APIs externas bajo condiciones normales y de alta carga.

### Métrica
- **Tiempo de Actividad (Uptime)**: Porcentaje de tiempo en que el sistema está disponible durante un período de 30 días.
- **Tiempo de Inactividad (Downtime)**: Tiempo acumulado en minutos durante el cual el sistema no está disponible.

### Umbrales
| Nivel de Madurez | Tiempo de Actividad | Tiempo de Inactividad (mensual) |
|-------------------|---------------------|----------------------------------|
| Nivel 1           | ≥ 99.0%             | ≤ 432 minutos                    |
| Nivel 2           | ≥ 99.5%             | ≤ 216 minutos                    |
| Nivel 3           | ≥ 99.9%             | ≤ 43 minutos                     |
| Nivel 4           | ≥ 99.95%            | ≤ 22 minutos                     |
| Nivel 5           | ≥ 99.99%            | ≤ 4 minutos                      |

## 2. Rendimiento

### Escenario
El sistema debe responder a las solicitudes de APIs dentro de un tiempo aceptable, incluso bajo carga.

### Métrica
- **Latencia Percentil 95 (P95)**: Tiempo de respuesta en el percentil 95 para solicitudes exitosas.
- **Throughput**: Número de solicitudes procesadas por segundo (RPS).

### Umbrales
| Nivel de Madurez | Latencia P95 (ms) | Throughput (RPS) |
|-------------------|-------------------|------------------|
| Nivel 1           | ≤ 1000            | ≥ 100            |
| Nivel 2           | ≤ 500             | ≥ 500            |
| Nivel 3           | ≤ 200             | ≥ 1000           |
| Nivel 4           | ≤ 100             | ≥ 2000           |
| Nivel 5           | ≤ 50              | ≥ 5000           |

## 3. Escalabilidad

### Escenario
El sistema debe escalar horizontalmente para manejar aumentos en la carga sin degradación del rendimiento.

### Métrica
- **Factor de Escalabilidad**: Número máximo de réplicas que el sistema puede desplegar sin degradación del rendimiento.
- **Tiempo de Escalado**: Tiempo requerido para desplegar una nueva réplica bajo carga.

### Umbrales
| Nivel de Madurez | Factor de Escalabilidad | Tiempo de Escalado (segundos) |
|-------------------|------------------------|-----------------------------|
| Nivel 1           | 2 réplicas             | ≤ 300                       |
| Nivel 2           | 5 réplicas             | ≤ 120                       |
| Nivel 3           | 10 réplicas            | ≤ 60                        |
| Nivel 4           | 20 réplicas            | ≤ 30                        |
| Nivel 5           | 50 réplicas            | ≤ 10                        |

## 4. Seguridad

### Escenario
El sistema debe proteger los datos y garantizar la autenticación y autorización adecuada para todas las solicitudes.

### Métrica
- **Cobertura de Autenticación**: Porcentaje de endpoints que requieren autenticación.
- **Cobertura de Autorización**: Porcentaje de endpoints que verifican permisos basados en roles.
- **Vulnerabilidades Críticas**: Número de vulnerabilidades críticas identificadas en pruebas de seguridad.

### Umbrales
| Nivel de Madurez | Cobertura de Autenticación | Cobertura de Autorización | Vulnerabilidades Críticas |
|-------------------|----------------------------|---------------------------|---------------------------|
| Nivel 1           | ≥ 80%                      | ≥ 60%                     | ≤ 5                       |
| Nivel 2           | ≥ 90%                      | ≥ 80%                     | ≤ 2                       |
| Nivel 3           | 100%                       | 100%                      | 0                         |
| Nivel 4           | 100%                       | 100%                      | 0 (con pruebas trimestrales) |
| Nivel 5           | 100%                       | 100%                      | 0 (con pruebas continuas) |

## 5. Consistencia de Datos

### Escenario
El sistema debe garantizar que los datos sean consistentes entre solicitudes, incluso en entornos distribuidos.

### Métrica
- **Tiempo de Consistencia (Time to Consistency)**: Tiempo máximo para que los datos se propaguen y sean consistentes en todos los nodos.
- **Tasa de Errores de Consistencia**: Porcentaje de solicitudes que resultan en inconsistencias de datos.

### Umbrales
| Nivel de Madurez | Tiempo de Consistencia (ms) | Tasa de Errores de Consistencia |
|-------------------|-----------------------------|----------------------------------|
| Nivel 1           | ≤ 5000                      | ≤ 1%                            |
| Nivel 2           | ≤ 1000                      | ≤ 0.1%                          |
| Nivel 3           | ≤ 200                       | ≤ 0.01%                         |
| Nivel 4           | ≤ 100                       | 0%                              |
| Nivel 5           | ≤ 50                        | 0%                              |

## 6. Mantenibilidad

### Escenario
El sistema debe ser fácil de mantener, modificar y extender sin introducir errores.

### Métrica
- **Cobertura de Pruebas**: Porcentaje de código cubierto por pruebas unitarias, de integración y de extremo a extremo.
- **Frecuencia de Despliegues**: Número de despliegues por mes.
- **Tiempo Medio de Resolución (MTTR)**: Tiempo promedio para resolver incidentes en producción.

### Umbrales
| Nivel de Madurez | Cobertura de Pruebas | Frecuencia de Despliegues | MTTR (horas) |
|-------------------|----------------------|---------------------------|--------------|
| Nivel 1           | ≥ 60%                | ≤ 4                       | ≤ 24        |
| Nivel 2           | ≥ 70%                | ≤ 8                       | ≤ 12        |
| Nivel 3           | ≥ 80%                | ≤ 16                      | ≤ 6         |
| Nivel 4           | ≥ 90%                | ≤ 30                      | ≤ 2         |
| Nivel 5           | ≥ 95%                | Diario                    | ≤ 1         |

## 7. Observabilidad

### Escenario
El sistema debe proporcionar visibilidad en tiempo real de su estado, rendimiento y errores.

### Métrica
- **Cobertura de Logs**: Porcentaje de componentes que generan logs estructurados.
- **Cobertura de Métricas**: Porcentaje de componentes que exponen métricas de rendimiento.
- **Cobertura de Trazas**: Porcentaje de solicitudes que tienen trazabilidad de extremo a extremo.

### Umbrales
| Nivel de Madurez | Cobertura de Logs | Cobertura de Métricas | Cobertura de Trazas |
|-------------------|-------------------|-----------------------|----------------------|
| Nivel 1           | ≥ 70%             | ≥ 50%                 | ≥ 30%                |
| Nivel 2           | ≥ 80%             | ≥ 70%                 | ≥ 60%                |
| Nivel 3           | ≥ 90%             | ≥ 80%                 | ≥ 80%                |
| Nivel 4           | 100%              | 100%                  | 100%                 |
| Nivel 5           | 100%              | 100%                  | 100% (con correlación de IDs) |

## 8. Usabilidad de APIs

### Escenario
Las APIs deben ser fáciles de usar, bien documentadas y consistentes en su diseño.

### Métrica
- **Completitud de Documentación**: Porcentaje de endpoints documentados en OpenAPI.
- **Consistencia de Diseño**: Porcentaje de endpoints que siguen las convenciones de diseño de APIs (ej. RESTful).
- **Facilidad de Integración**: Número de pasos requeridos para integrar una nueva API.

### Umbrales
| Nivel de Madurez | Completitud de Documentación | Consistencia de Diseño | Facilidad de Integración (pasos) |
|-------------------|-------------------------------|------------------------|-----------------------------------|
| Nivel 1           | ≥ 70%                         | ≥ 60%                  | ≤ 10                              |
| Nivel 2           | ≥ 80%                         | ≥ 80%                  | ≤ 5                               |
| Nivel 3           | ≥ 90%                         | ≥ 90%                  | ≤ 3                               |
| Nivel 4           | 100%                          | 100%                   | ≤ 2                               |
| Nivel 5           | 100%                          | 100%                   | ≤ 1 (SDKs disponibles)            |

## Modelo de Madurez de APIs de Pragma

El modelo de madurez de APIs de Pragma clasifica las APIs en cinco niveles, basados en los atributos de calidad definidos anteriormente:

| **Nivel** | **Descripción**                                                                 |
|-----------|---------------------------------------------------------------------------------|
| Nivel 1   | APIs básicas con funcionalidad mínima y sin garantías de calidad.             |
| Nivel 2   | APIs funcionales con documentación básica y algunos atributos de calidad cumplidos. |
| Nivel 3   | APIs bien diseñadas con documentación completa y la mayoría de atributos de calidad cumplidos. |
| Nivel 4   | APIs robustas con alto cumplimiento de atributos de calidad y observabilidad avanzada. |
| Nivel 5   | APIs de excelencia con todos los atributos de calidad en su nivel máximo y mejora continua. |

### Evaluación de Madurez

Para evaluar la madurez de una API, se asigna un puntaje a cada atributo de calidad basado en los umbrales definidos. El nivel de madurez de la API se determina como el nivel más bajo en el que todos los atributos cumplen con los umbrales correspondientes.

Ejemplo de Evaluación:

| Atributo               | Valor Actual | Nivel Alcanzado |
|------------------------|--------------|-----------------|
| Disponibilidad         | 99.9%        | Nivel 4         |
| Rendimiento            | 150 ms (P95) | Nivel 3         |
| Escalabilidad          | 10 réplicas  | Nivel 3         |
| Seguridad              | 100%         | Nivel 3         |
| Consistencia de Datos  | 200 ms       | Nivel 3         |
| Mantenibilidad         | 85%          | Nivel 3         |
| Observabilidad         | 90%          | Nivel 3         |
| Usabilidad de APIs     | 90%          | Nivel 3         |

**Nivel de Madurez de la API**: Nivel 3

## Herramientas para Medición

| Atributo               | Herramienta                                 |
|------------------------|---------------------------------------------|
| Disponibilidad         | AWS CloudWatch, Prometheus                  |
| Rendimiento            | AWS CloudWatch, New Relic, Datadog          |
| Escalabilidad          | AWS Auto Scaling, Kubernetes HPA            |
| Seguridad              | OWASP ZAP, SonarQube, AWS Inspector         |
| Consistencia de Datos  | Datadog, AWS X-Ray                          |
| Mantenibilidad         | SonarQube, CodeClimate                      |
| Observabilidad         | Datadog, AWS CloudWatch, OpenTelemetry      |
| Usabilidad de APIs     | Swagger UI, Postman, OpenAPI Validator      |