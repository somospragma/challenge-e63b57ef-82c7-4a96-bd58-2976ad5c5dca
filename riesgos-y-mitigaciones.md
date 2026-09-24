# Riesgos Técnicos y Mitigaciones para el Sistema de APIs de Pragma

## Introducción
Este documento identifica los riesgos técnicos asociados a la implementación y operación de las APIs del sistema de Pragma, evaluando su impacto potencial y proponiendo estrategias de mitigación. Los riesgos se priorizan según su probabilidad de ocurrencia y su impacto en los atributos de calidad definidos en `atributos-de-calidad.md`, como disponibilidad, rendimiento, seguridad y mantenibilidad.

---

## 1. Riesgos Identificados

### 1.1. Riesgo: Falta de estandarización en el diseño de APIs
**Descripción:**
Las APIs actuales presentan inconsistencias en el diseño de endpoints, esquemas de request/response y códigos de error, lo que dificulta su consumo por parte de clientes internos y externos. Esto afecta la **usabilidad** y **mantenibilidad** del sistema.

**Impacto:**
- **Alto** en la experiencia del desarrollador (DX).
- **Medio** en la integración con sistemas externos, aumentando el tiempo de onboarding.
- **Bajo** en la seguridad, aunque podría introducir vulnerabilidades por malinterpretación de esquemas.

**Probabilidad:** Alta (observado en el catálogo actual de APIs).

**Evidencias:**
- Endpoints con naming inconsistente (ej: `/users/get` vs `/users/retrieve`).
- Respuestas con estructuras heterogéneas (ej: errores devueltos como strings en algunos casos y objetos en otros).
- Falta de versiones claras en los endpoints, lo que complica la evolución sin romper compatibilidad.

**Métricas afectadas:**
- **Usabilidad:** Tiempo promedio de integración de un nuevo cliente (umbral: < 2 días).
- **Mantenibilidad:** Número de issues reportados por inconsistencias en APIs (umbral: < 5/mes).

---

### 1.2. Riesgo: Dependencia crítica de servicios externos no resilientes
**Descripción:**
Varias APIs dependen de servicios externos como el **motor de reglas** y el **sistema de autenticación**, los cuales no implementan mecanismos de resiliencia (timeouts, retries, circuit breakers). Esto afecta la **disponibilidad** y **tolerancia a fallos** del sistema.

**Impacto:**
- **Crítico** en disponibilidad (umbral: 99.95% mensual).
- **Alto** en rendimiento, al introducir latencias no gestionadas.

**Probabilidad:** Media (los servicios externos tienen SLA, pero no se han auditado sus mecanismos de resiliencia).

**Evidencias:**
- Ausencia de políticas de retry en las llamadas al motor de reglas (ej: reglas de negocio que tardan > 500ms en responder).
- Falta de circuit breakers en el cliente del sistema de autenticación, lo que podría saturar el servicio bajo carga.
- Logs que muestran fallos en cascada cuando un servicio externo se degrada.

**Métricas afectadas:**
- **Disponibilidad:** Porcentaje de uptime mensual (umbral: ≥ 99.95%).
- **Rendimiento:** Latencia percentil 95 de las APIs (umbral: < 300ms).

---

### 1.3. Riesgo: Exposición de datos sensibles en APIs públicas
**Descripción:**
Algunas APIs exponen información sensible (ej: tokens de autenticación, datos personales) en respuestas o logs, lo que viola políticas de **seguridad** y **cumplimiento normativo** (GDPR, LGPD).

**Impacto:**
- **Crítico** en seguridad y cumplimiento.
- **Alto** en reputación, con potenciales multas regulatorias.

**Probabilidad:** Media (auditorías previas han identificado fugas menores).

**Evidencias:**
- Respuestas de APIs que incluyen campos como `user_internal_id` o `session_token`.
- Logs de acceso que registran headers con información sensible (ej: `Authorization: Bearer <token>`).
- Falta de validación de esquemas en respuestas para filtrar campos sensibles.

**Métricas afectadas:**
- **Seguridad:** Número de incidentes de fuga de datos reportados (umbral: 0).
- **Cumplimiento:** Porcentaje de APIs auditadas que cumplen con políticas de datos sensibles (umbral: 100%).

---

### 1.4. Riesgo: Ausencia de monitoreo y alertas proactivas
**Descripción:**
El sistema carece de monitoreo centralizado para métricas clave de las APIs (latencia, errores, throughput), lo que impide detectar degradaciones antes de que afecten a los usuarios. Esto impacta la **observabilidad** y la **disponibilidad**.

**Impacto:**
- **Alto** en disponibilidad, al no detectar fallos hasta que son reportados por usuarios.
- **Medio** en rendimiento, al no identificar cuellos de botella.

**Probabilidad:** Alta (no hay evidencias de dashboards o alertas configuradas).

**Evidencias:**
- Ausencia de dashboards de métricas en herramientas como Prometheus/Grafana.
- Logs dispersos en diferentes servicios sin correlación.
- Falta de alertas para umbrales críticos (ej: latencia > 500ms, error rate > 1%).

**Métricas afectadas:**
- **Observabilidad:** Porcentaje de métricas clave monitoreadas (umbral: 100%).
- **Disponibilidad:** Tiempo medio de detección de fallos (MTTD) (umbral: < 5 minutos).

---

### 1.5. Riesgo: Documentación obsoleta o incompleta
**Descripción:**
La documentación de las APIs (OpenAPI/Swagger) está desactualizada o carece de ejemplos de uso, lo que afecta la **usabilidad** y **mantenibilidad**. Esto aumenta el tiempo de integración y los errores de consumo.

**Impacto:**
- **Alto** en la experiencia del desarrollador (DX).
- **Medio** en la productividad de equipos internos.

**Probabilidad:** Alta (observado en el archivo `contratos/openapi.yaml`).

**Evidencias:**
- Esquemas OpenAPI sin ejemplos de request/response.
- Endpoints documentados con descripciones genéricas (ej: "Este endpoint devuelve datos").
- Falta de documentación para códigos de error específicos.

**Métricas afectadas:**
- **Usabilidad:** Número de solicitudes de soporte por falta de documentación (umbral: < 2/semana).
- **Mantenibilidad:** Tiempo promedio para actualizar la documentación tras cambios en APIs (umbral: < 1 día).

---

### 1.6. Riesgo: Falta de estrategia de versionado para APIs
**Descripción:**
No existe una estrategia clara para el versionado de APIs, lo que dificulta la evolución sin romper compatibilidad con clientes existentes. Esto afecta la **mantenibilidad** y **evolutividad** del sistema.

**Impacto:**
- **Alto** en la capacidad de innovación, al limitar cambios en APIs.
- **Medio** en la satisfacción del cliente, al introducir breaking changes inesperados.

**Probabilidad:** Alta (no se menciona versionado en `contratos/openapi.yaml`).

**Evidencias:**
- Endpoints sin prefijo de versión (ej: `/v1/users`).
- Falta de políticas para deprecación de versiones antiguas.
- Ausencia de tests de compatibilidad regresiva.

**Métricas afectadas:**
- **Mantenibilidad:** Número de breaking changes introducidos por trimestre (umbral: 0).
- **Evolutividad:** Tiempo promedio para implementar una nueva versión de API (umbral: < 1 semana).

---

### 1.7. Riesgo: Sobrecarga en el servicio de notificaciones
**Descripción:**
El servicio de notificaciones recibe un alto volumen de solicitudes desde múltiples APIs, sin mecanismos de rate limiting o cola de priorización. Esto afecta la **disponibilidad** y **rendimiento** del sistema.

**Impacto:**
- **Crítico** en disponibilidad del servicio de notificaciones.
- **Alto** en la experiencia del usuario final, al retrasar notificaciones críticas.

**Probabilidad:** Media (observado en logs de tráfico).

**Evidencias:**
- Picos de tráfico en horarios específicos sin throttling.
- Ausencia de colas (ej: Kafka, SQS) para manejar carga.
- Falta de priorización de notificaciones (ej: urgentes vs informativas).

**Métricas afectadas:**
- **Disponibilidad:** Porcentaje de uptime del servicio de notificaciones (umbral: ≥ 99.9%).
- **Rendimiento:** Latencia percentil 95 de envío de notificaciones (umbral: < 200ms).

---

## 2. Estrategias de Mitigación

### 2.1. Estandarización del diseño de APIs
**Acciones:**
1. **Definir un estilo guide** para el diseño de APIs (ej: naming, esquemas de error, paginación) basado en estándares como [REST API Guidelines de Microsoft](https://github.com/microsoft/api-guidelines) o [Zalando RESTful API Guidelines](https://opensource.zalando.com/restful-api-guidelines/).
2. **Implementar validación automática** de esquemas OpenAPI usando herramientas como [Spectral](https://stoplight.io/open-source/spectral) para asegurar cumplimiento.
3. **Crear plantillas** para nuevos endpoints que incluyan:
   - Versión en la URL (ej: `/v1/resource`).
   - Esquema estandarizado de errores (ej: `{ "error": { "code": "string", "message": "string", "details": {} } }`).
   - Paginación para endpoints que devuelven listas.
4. **Revisar y refactorizar** las APIs existentes para alinearlas con el estilo guide.

**Responsable:** Equipo de Arquitectura.
**Plazo:** 4 semanas.
**Métricas de éxito:**
- 100% de APIs cumplen con el estilo guide.
- Reducción del 50% en issues reportados por inconsistencias.

---

### 2.2. Implementación de resiliencia en servicios externos
**Acciones:**
1. **Auditar los servicios externos** (motor de reglas, autenticación) para identificar puntos únicos de fallo.
2. **Implementar circuit breakers** usando librerías como [Resilience4j](https://github.com/resilience4j/resilience4j) (Java) o [Polly](https://github.com/App-vNext/Polly) (.NET) para:
   - Cortar llamadas a servicios degradados.
   - Definir umbrales de error y tiempo de espera.
3. **Configurar retries con backoff exponencial** para llamadas fallidas.
4. **Implementar fallbacks** para servicios críticos (ej: cache local para datos no sensibles).
5. **Monitorear métricas de resiliencia** (ej: tasa de circuit breakers abiertos, tiempo de recuperación).

**Responsable:** Equipo de Infraestructura.
**Plazo:** 3 semanas.
**Métricas de éxito:**
- 0% de fallos en cascada por servicios externos.
- Latencia percentil 95 < 300ms para todas las APIs.

---

### 2.3. Protección de datos sensibles
**Acciones:**
1. **Identificar campos sensibles** en esquemas OpenAPI y marcarlos con anotaciones (ej: `@sensitive`).
2. **Implementar filtros automáticos** para excluir campos sensibles de:
   - Respuestas de APIs.
   - Logs (usar herramientas como [Logback](https://logback.qos.ch/) o [Serilog](https://serilog.net/) con enmascaramiento).
3. **Auditar logs y respuestas** con herramientas como [OWASP ZAP](https://www.zaproxy.org/) para detectar fugas.
4. **Capacitar al equipo** en buenas prácticas de manejo de datos sensibles.

**Responsable:** Equipo de Seguridad.
**Plazo:** 2 semanas.
**Métricas de éxito:**
- 0 incidentes de fuga de datos reportados.
- 100% de APIs auditadas cumplen con políticas de datos sensibles.

---

### 2.4. Implementación de monitoreo y alertas
**Acciones:**
1. **Instrumentar métricas clave** usando herramientas como:
   - [Prometheus](https://prometheus.io/) para métricas (latencia, errores, throughput).
   - [Grafana](https://grafana.com/) para dashboards.
   - [Alertmanager](https://prometheus.io/docs/alerting/alertmanager/) para alertas.
2. **Definir umbrales de alerta** para:
   - Latencia > 500ms.
   - Error rate > 1%.
   - Throughput anómalo.
3. **Configurar alertas** para equipos relevantes (Slack, email).
4. **Implementar tracing distribuido** con [Jaeger](https://www.jaegertracing.io/) o [Zipkin](https://zipkin.io/) para correlacionar logs.

**Responsable:** Equipo de DevOps.
**Plazo:** 3 semanas.
**Métricas de éxito:**
- 100% de métricas clave monitoreadas.
- MTTD < 5 minutos para fallos críticos.

---

### 2.5. Actualización de documentación
**Acciones:**
1. **Automatizar la generación de documentación** a partir de esquemas OpenAPI usando:
   - [Swagger UI](https://swagger.io/tools/swagger-ui/) o [Redoc](https://github.com/Redocly/redoc) para interfaces interactivas.
   - [Spectral](https://stoplight.io/open-source/spectral) para validar ejemplos y descripciones.
2. **Incluir ejemplos reales** para cada endpoint (request/response).
3. **Documentar códigos de error** con descripciones y posibles soluciones.
4. **Establecer un proceso** para actualizar la documentación en cada cambio de API.

**Responsable:** Equipo de Desarrollo.
**Plazo:** 2 semanas.
**Métricas de éxito:**
- 100% de APIs con ejemplos de uso.
- Reducción del 70% en solicitudes de soporte por falta de documentación.

---

### 2.6. Definición de estrategia de versionado
**Acciones:**
1. **Adoptar un esquema de versionado** basado en:
   - **URL path** (ej: `/v1/resource`) para APIs públicas.
   - **Header** (ej: `Accept: application/vnd.pragma.v1+json`) para APIs internas.
2. **Implementar tests de compatibilidad regresiva** para asegurar que cambios no rompan clientes existentes.
3. **Documentar políticas de deprecación** (ej: 6 meses de soporte para versiones antiguas).
4. **Crear un endpoint `/versions`** que liste las versiones disponibles y su estado (activa/deprecated).

**Responsable:** Equipo de Arquitectura.
**Plazo:** 1 semana.
**Métricas de éxito:**
- 0 breaking changes introducidos por trimestre.
- Tiempo promedio para implementar una nueva versión < 1 semana.

---

### 2.7. Optimización del servicio de notificaciones
**Acciones:**
1. **Implementar rate limiting** para evitar sobrecarga.
2. **Introducir colas de priorización** (ej: Kafka, SQS) para:
   - Separar notificaciones urgentes de informativas.
   - Escalar horizontalmente el servicio.
3. **Monitorear métricas de cola** (ej: tamaño, tiempo de procesamiento).
4. **Implementar retries con backoff exponencial** para notificaciones fallidas.

**Responsable:** Equipo de Backend.
**Plazo:** 3 semanas.
**Métricas de éxito:**
- Latencia percentil 95 < 200ms para notificaciones.
- 0% de pérdida de notificaciones críticas.

---

## 3. Priorización de Riesgos
Los riesgos se priorizan según su **impacto** y **probabilidad**, usando la siguiente matriz:

| Impacto \ Probabilidad | Baja | Media | Alta |
|-------------------------|------|-------|------|
| **Crítico**            |  3   |   2   |  1   |
| **Alto**               |  5   |   4   |  2   |
| **Medio**              |  7   |   6   |  5   |
| **Bajo**               |  9   |   8   |  7   |

**Priorización resultante:**

| Riesgo                                      | Prioridad | Impacto   | Probabilidad | Acciones Clave                          |
|---------------------------------------------|------------|-----------|---------------|-----------------------------------------|
| Exposición de datos sensibles               | 1          | Crítico   | Media         | Filtros automáticos, auditoría         |
| Dependencia de servicios externos           | 2          | Crítico   | Media         | Circuit breakers, fallbacks            |
| Falta de monitoreo y alertas                | 3          | Alto      | Alta          | Prometheus/Grafana, Alertmanager       |
| Falta de estandarización en APIs            | 4          | Alto      | Alta          | Estilo guide, Spectral                 |
| Documentación obsoleta                      | 5          | Alto      | Alta          | Swagger UI, ejemplos automatizados     |
| Sobrecarga en servicio de notificaciones    | 6          | Alto      | Media         | Rate limiting, colas de priorización   |
| Falta de estrategia de versionado           | 7          | Alto      | Alta          | Versionado en URL/header, tests        |

---

## 4. Plan de Acción

| Riesgo                                      | Acciones                                | Responsable      | Plazo   | Métricas de Éxito                          |
|---------------------------------------------|-----------------------------------------|------------------|---------|--------------------------------------------|
| Exposición de datos sensibles               | Filtros automáticos, auditoría          | Seguridad        | 2 sem   | 0 incidentes, 100% APIs auditadas         |
| Dependencia de servicios externos           | Circuit breakers, fallbacks             | Infraestructura  | 3 sem   | 0 fallos en cascada, latencia < 300ms     |
| Falta de monitoreo y alertas                | Prometheus/Grafana, Alertmanager       | DevOps           | 3 sem   | 100% métricas, MTTD < 5 min               |
| Falta de estandarización en APIs            | Estilo guide, Spectral                  | Arquitectura     | 4 sem   | 100% APIs cumplen estilo guide            |
| Documentación obsoleta                      | Swagger UI, ejemplos automatizados      | Desarrollo       | 2 sem   | 100% APIs con ejemplos                     |
| Sobrecarga en servicio de notificaciones    | Rate limiting, colas de priorización   | Backend          | 3 sem   | Latencia < 200ms, 0% pérdida de notificaciones |
| Falta de estrategia de versionado           | Versionado en URL/header, tests         | Arquitectura     | 1 sem   | 0 breaking changes, tiempo < 1 sem         |

---

## 5. Seguimiento
- **Reuniones de revisión:** Cada 2 semanas para evaluar el progreso de las mitigaciones.
- **Herramienta de seguimiento:** Tablero en Jira con las tareas definidas en el plan de acción.
- **Reportes:** Métricas clave compartidas semanalmente con los stakeholders.


---

## Anexo: Referencias
- [REST API Guidelines de Microsoft](https://github.com/microsoft/api-guidelines)
- [Zalando RESTful API Guidelines](https://opensource.zalando.com/restful-api-guidelines/)
- [OWASP API Security Top 10](https://owasp.org/www-project-api-security/)
- [Resilience4j](https://github.com/resilience4j/resilience4j)
- [Prometheus](https://prometheus.io/)
- [OpenAPI Specification](https://spec.openapis.org/oas/v3.1.0)