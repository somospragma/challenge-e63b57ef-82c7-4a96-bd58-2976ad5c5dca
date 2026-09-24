# Plan de Acción para la Optimización de APIs

## Contexto

El sistema actual de APIs en Pragma presenta variaciones significativas en su nivel de madurez, lo que impacta directamente en la consistencia, mantenibilidad y escalabilidad de los servicios expuestos. Tras la evaluación realizada en las fases anteriores, se identificaron oportunidades de mejora en áreas clave como documentación, versionamiento, seguridad, rendimiento y gobernanza.

Este plan de acción propone un conjunto de iniciativas priorizadas para elevar el nivel de madurez de las APIs, alineadas con el modelo de madurez de Pragma y los atributos de calidad definidos en el proyecto. Las propuestas están organizadas por dimensión de mejora y priorizadas según su impacto en los objetivos estratégicos de la organización y su factibilidad técnica.


## Dimensiones de Mejora

### 1. Documentación y Descubrimiento

**Problema Identificado:**
- Falta de documentación estandarizada y accesible para desarrolladores internos y externos.
- Ausencia de catálogo centralizado que permita descubrir y entender las APIs disponibles.
- Documentación desactualizada o incompleta en varias APIs críticas.

**Propuestas:**

#### 1.1 Implementar un Portal de Desarrolladores
- **Descripción:** Crear un portal centralizado que sirva como punto único de acceso a la documentación de todas las APIs, incluyendo OpenAPI/Swagger UI, guías de uso, ejemplos de código y casos de uso.
- **Impacto:**
  - Reduce el tiempo de onboarding de nuevos desarrolladores.
  - Mejora la adopción de APIs por parte de equipos internos y partners.
  - Facilita el descubrimiento de APIs existentes, evitando duplicación de esfuerzos.
- **Factibilidad:** Alta. Herramientas como SwaggerHub, Backstage o Redocly pueden integrarse con los contratos OpenAPI existentes.
- **Acciones:**
  1. Seleccionar y configurar la herramienta para el portal (ej: Backstage con plugin de OpenAPI).
  2. Generar documentación automática a partir de los contratos OpenAPI.
  3. Complementar con guías de uso, ejemplos y casos de prueba.
  4. Implementar autenticación y control de acceso basado en roles.
- **Responsables:** Equipo de Arquitectura + Equipo de Desarrollo.
- **Plazo:** 4 semanas.
- **Costo:** Medio (licencias de herramientas, si aplica, y esfuerzo de configuración).

#### 1.2 Establecer Proceso de Actualización de Documentación
- **Descripción:** Definir un proceso obligatorio para actualizar la documentación de una API cada vez que se modifique su contrato (OpenAPI) o su comportamiento. Incluir revisiones por pares y aprobación antes de publicar cambios.
- **Impacto:**
  - Asegura que la documentación esté siempre alineada con la implementación.
  - Reduce errores y malentendidos en el uso de las APIs.
- **Factibilidad:** Alta. Puede integrarse en el flujo de CI/CD.
- **Acciones:**
  1. Modificar el pipeline de CI/CD para validar que los cambios en los contratos OpenAPI incluyan actualizaciones en la documentación.
  2. Asignar responsables de documentación para cada API.
  3. Implementar revisiones por pares para cambios en documentación.
  4. Incluir métricas de cobertura de documentación en el dashboard de calidad.
- **Responsables:** Equipo de DevOps + Dueños de APIs.
- **Plazo:** 3 semanas.
- **Costo:** Bajo (principalmente esfuerzo de configuración y adopción de procesos).


### 2. Versionamiento y Retrocompatibilidad

**Problema Identificado:**
- Ausencia de estrategia clara de versionamiento en varias APIs.
- Cambios en contratos sin considerar impacto en consumidores.
- Falta de soporte para múltiples versiones activas.

**Propuestas:**

#### 2.1 Adoptar Estrategia de Versionamiento por URI
- **Descripción:** Implementar versionamiento explícito en la URI de todas las APIs (ej: `/api/v1/recursos`). Esto facilita la gestión de múltiples versiones activas y proporciona claridad a los consumidores.
- **Impacto:**
  - Permite evolucionar las APIs sin romper consumidores existentes.
  - Facilita la migración gradual de consumidores a nuevas versiones.
  - Mejora la trazabilidad de cambios.
- **Factibilidad:** Alta. Requiere cambios en las rutas de las APIs y configuración de enrutamiento.
- **Acciones:**
  1. Actualizar los contratos OpenAPI para incluir versionamiento en la URI.
  2. Modificar las implementaciones de las APIs para soportar múltiples versiones.
  3. Configurar el API Gateway para enrutar solicitudes según la versión.
  4. Comunicar el cambio a todos los consumidores y proporcionar guías de migración.
- **Responsables:** Equipo de Desarrollo + Equipo de DevOps.
- **Plazo:** 6 semanas.
- **Costo:** Medio (esfuerzo de desarrollo y pruebas).

#### 2.2 Implementar Deprecación Controlada
- **Descripción:** Establecer un proceso formal para deprecación de versiones antiguas, incluyendo ventanas de tiempo claras, notificaciones a consumidores y soporte para migración.
- **Impacto:**
  - Reduce el riesgo de cambios disruptivos.
  - Proporciona transparencia a los consumidores sobre el ciclo de vida de las APIs.
- **Factibilidad:** Alta. Requiere definición de políticas y herramientas de monitoreo.
- **Acciones:**
  1. Definir política de deprecación (ej: 6 meses de soporte para versiones antiguas).
  2. Implementar headers de deprecación en respuestas de APIs obsoletas.
  3. Monitorear el uso de versiones obsoletas.
  4. Notificar a consumidores sobre versiones a ser deprecadas con antelación.
  5. Proporcionar herramientas y guías para facilitar la migración.
- **Responsables:** Equipo de Arquitectura + Equipo de Desarrollo.
- **Plazo:** 4 semanas.
- **Costo:** Bajo (principalmente definición de procesos y herramientas de monitoreo).


### 3. Seguridad y Gobernanza

**Problema Identificado:**
- Ausencia de políticas de seguridad consistentes en todas las APIs.
- Falta de validación centralizada de esquemas y payloads.
- Autenticación y autorización implementadas de manera inconsistente.

**Propuestas:**

#### 3.1 Implementar Validación Centralizada de Esquemas
- **Descripción:** Configurar el API Gateway para validar automáticamente los payloads de solicitudes y respuestas contra los esquemas OpenAPI definidos. Rechazar solicitudes que no cumplan con el contrato.
- **Impacto:**
  - Reduce errores por datos inválidos.
  - Mejora la consistencia de los datos manejados por las APIs.
  - Detecta tempranamente cambios no autorizados en contratos.
- **Factibilidad:** Alta. Herramientas como Kong, Apigee o AWS API Gateway soportan esta funcionalidad.
- **Acciones:**
  1. Configurar el API Gateway para validar esquemas OpenAPI.
  2. Definir políticas de manejo de errores para solicitudes inválidas.
  3. Monitorear y registrar solicitudes rechazadas.
  4. Integrar la validación en el pipeline de CI/CD.
- **Responsables:** Equipo de DevOps + Equipo de Seguridad.
- **Plazo:** 3 semanas.
- **Costo:** Medio (configuración de herramientas y pruebas).

#### 3.2 Establecer Políticas de Autenticación y Autorización
- **Descripción:** Implementar un sistema centralizado de autenticación y autorización para todas las APIs, utilizando estándares como OAuth 2.0 y OpenID Connect. Definir roles y permisos basados en las necesidades de los consumidores.
- **Impacto:**
  - Mejora la seguridad al reducir la superficie de ataque.
  - Facilita la gestión de accesos para consumidores.
  - Asegura que solo usuarios autorizados accedan a recursos sensibles.
- **Factibilidad:** Alta. Herramientas como Keycloak, Auth0 o AWS Cognito pueden integrarse.
- **Acciones:**
  1. Seleccionar e implementar un proveedor de identidad (ej: Keycloak).
  2. Definir roles y permisos para cada API.
  3. Configurar el API Gateway para validar tokens de acceso.
  4. Actualizar las implementaciones de las APIs para verificar permisos.
  5. Proporcionar guías para desarrolladores sobre cómo obtener tokens de acceso.
- **Responsables:** Equipo de Seguridad + Equipo de Desarrollo.
- **Plazo:** 5 semanas.
- **Costo:** Medio (licencias, si aplica, y esfuerzo de configuración).


### 4. Rendimiento y Escalabilidad

**Problema Identificado:**
- Falta de métricas consistentes de rendimiento.
- Ausencia de estrategias de caching para APIs con alta demanda.
- Tiempos de respuesta variables en APIs críticas.

**Propuestas:**

#### 4.1 Implementar Caching Estratégico
- **Descripción:** Identificar APIs con patrones de uso de solo lectura y alta demanda, e implementar caching en el API Gateway o en la capa de servicio para reducir la carga en los sistemas backend.
- **Impacto:**
  - Reduce la latencia para consumidores.
  - Disminuye la carga en sistemas backend, mejorando la escalabilidad.
  - Reduce costos operativos al disminuir el uso de recursos.
- **Factibilidad:** Media. Requiere análisis de patrones de uso y configuración de caching.
- **Acciones:**
  1. Identificar APIs candidatas para caching (ej: APIs de consulta con baja frecuencia de actualización).
  2. Configurar políticas de caching en el API Gateway.
  3. Implementar invalidación de cache basada en eventos.
  4. Monitorear el impacto del caching en el rendimiento.
- **Responsables:** Equipo de Desarrollo + Equipo de DevOps.
- **Plazo:** 4 semanas.
- **Costo:** Medio (configuración y monitoreo).

#### 4.2 Establecer Métricas de Rendimiento
- **Descripción:** Implementar monitoreo continuo de métricas clave de rendimiento (latencia, throughput, tasa de errores) para todas las APIs, con umbrales de alerta definidos.
- **Impacto:**
  - Permite detectar y resolver problemas de rendimiento proactivamente.
  - Proporciona datos para optimizar APIs.
  - Mejora la experiencia del usuario final.
- **Factibilidad:** Alta. Herramientas como Prometheus, Grafana y ELK pueden integrarse.
- **Acciones:**
  1. Definir métricas clave de rendimiento para cada API.
  2. Configurar herramientas de monitoreo para recolectar métricas.
  3. Establecer umbrales de alerta.
  4. Implementar dashboards para visualizar métricas.
  5. Integrar alertas en el sistema de notificaciones.
- **Responsables:** Equipo de DevOps + Equipo de Arquitectura.
- **Plazo:** 3 semanas.
- **Costo:** Medio (configuración de herramientas y licencias, si aplica).


### 5. Gobernanza y Observabilidad

**Problema Identificado:**
- Falta de visibilidad sobre el uso y estado de las APIs.
- Ausencia de procesos para gestionar el ciclo de vida de las APIs.
- Dificultad para identificar APIs obsoletas o poco utilizadas.

**Propuestas:**

#### 5.1 Implementar Monitoreo de Uso de APIs
- **Descripción:** Configurar herramientas para monitorear el uso de cada API (número de solicitudes, consumidores, errores) y generar reportes periódicos.
- **Impacto:**
  - Proporciona visibilidad sobre el uso real de las APIs.
  - Facilita la identificación de APIs obsoletas o poco utilizadas.
  - Ayuda a priorizar esfuerzos de optimización.
- **Factibilidad:** Alta. Herramientas como AWS CloudWatch, ELK o Prometheus pueden integrarse.
- **Acciones:**
  1. Configurar herramientas de monitoreo para recolectar datos de uso.
  2. Definir métricas clave de uso (ej: solicitudes por consumidor, tasa de errores).
  3. Generar reportes periódicos de uso.
  4. Implementar dashboards para visualizar métricas de uso.
- **Responsables:** Equipo de DevOps + Equipo de Arquitectura.
- **Plazo:** 3 semanas.
- **Costo:** Medio (configuración de herramientas).

#### 5.2 Establecer Proceso de Gobernanza de APIs
- **Descripción:** Definir un proceso formal para la gestión del ciclo de vida de las APIs, incluyendo creación, modificación, deprecación y eliminación. Asignar dueños para cada API y establecer revisiones periódicas.
- **Impacto:**
  - Asegura que las APIs cumplan con los estándares de calidad.
  - Facilita la gestión de cambios y reduce riesgos.
  - Mejora la colaboración entre equipos.
- **Factibilidad:** Media. Requiere definición de procesos y adopción por parte de los equipos.
- **Acciones:**
  1. Definir etapas del ciclo de vida de las APIs.
  2. Asignar dueños para cada API.
  3. Establecer revisiones periódicas de APIs.
  4. Implementar herramientas para gestionar el ciclo de vida (ej: Backstage, Apigee).
  5. Documentar el proceso de gobernanza.
- **Responsables:** Equipo de Arquitectura + Líderes de Equipo.
- **Plazo:** 4 semanas.
- **Costo:** Bajo (principalmente definición de procesos y herramientas).


## Priorización de Propuestas

Las propuestas se priorizan según su impacto en los objetivos estratégicos de la organización y su factibilidad técnica. Se utiliza una matriz de priorización con los siguientes criterios:

| Criterio               | Peso |
|------------------------|------|
| Impacto en objetivos   | 40%  |
| Factibilidad técnica   | 30%  |
| Costo                  | 20%  |
| Plazo                  | 10%  |

**Matriz de Priorización:**

| Propuesta                                      | Impacto | Factibilidad | Costo | Plazo | Puntuación |
|------------------------------------------------|---------|--------------|-------|-------|------------|
| 1.1 Implementar un Portal de Desarrolladores   | Alto    | Alta         | Medio | 4     | 8.2        |
| 1.2 Establecer Proceso de Actualización        | Alto    | Alta         | Bajo  | 3     | 8.7        |
| 2.1 Adoptar Estrategia de Versionamiento       | Alto    | Alta         | Medio | 6     | 7.8        |
| 2.2 Implementar Deprecación Controlada         | Medio   | Alta         | Bajo  | 4     | 7.4        |
| 3.1 Implementar Validación Centralizada        | Alto    | Alta         | Medio | 3     | 8.5        |
| 3.2 Establecer Políticas de Autenticación      | Alto    | Alta         | Medio | 5     | 8.0        |
| 4.1 Implementar Caching Estratégico            | Medio   | Media        | Medio | 4     | 6.8        |
| 4.2 Establecer Métricas de Rendimiento         | Alto    | Alta         | Medio | 3     | 8.5        |
| 5.1 Implementar Monitoreo de Uso               | Medio   | Alta         | Medio | 3     | 7.5        |
| 5.2 Establecer Proceso de Gobernanza           | Alto    | Media        | Bajo  | 4     | 7.8        |

**Priorización Final:**
1. 1.2 Establecer Proceso de Actualización de Documentación
2. 3.1 Implementar Validación Centralizada de Esquemas
3. 4.2 Establecer Métricas de Rendimiento
4. 1.1 Implementar un Portal de Desarrolladores
5. 3.2 Establecer Políticas de Autenticación y Autorización
6. 2.1 Adoptar Estrategia de Versionamiento por URI
7. 5.2 Establecer Proceso de Gobernanza de APIs
8. 2.2 Implementar Deprecación Controlada
9. 5.1 Implementar Monitoreo de Uso de APIs
10. 4.1 Implementar Caching Estratégico


## Roadmap

| Fase | Propuestas Incluidas                          | Plazo   |
|------|-----------------------------------------------|---------|
| 1    | 1.2, 3.1, 4.2                                 | 3 semanas |
| 2    | 1.1, 3.2                                      | 5 semanas |
| 3    | 2.1, 5.2                                      | 6 semanas |
| 4    | 2.2, 5.1, 4.1                                 | 4 semanas |

**Fase 1 (Semanas 1-3):**
- Establecer proceso de actualización de documentación.
- Implementar validación centralizada de esquemas.
- Configurar métricas de rendimiento.

**Fase 2 (Semanas 4-8):**
- Implementar portal de desarrolladores.
- Establecer políticas de autenticación y autorización.

**Fase 3 (Semanas 9-14):**
- Adoptar estrategia de versionamiento por URI.
- Establecer proceso de gobernanza de APIs.

**Fase 4 (Semanas 15-18):**
- Implementar deprecación controlada.
- Implementar monitoreo de uso de APIs.
- Implementar caching estratégico.


## Riesgos y Mitigaciones

| Riesgo                                      | Impacto | Probabilidad | Mitigación                                                                 |
|---------------------------------------------|---------|--------------|-----------------------------------------------------------------------------|
| Resistencia al cambio por parte de equipos | Alto    | Media        | Involucrar a los equipos desde el inicio y proporcionar capacitación.     |
| Falta de adopción de nuevas herramientas    | Medio   | Alta         | Seleccionar herramientas con buena documentación y soporte.
              | Realizar pilotos con equipos pequeños antes de escalar.                     |
| Sobrecarga de trabajo para equipos         | Alto    | Media        | Priorizar iniciativas y asignar recursos adicionales según sea necesario. |
| Incompatibilidad entre versiones de APIs   | Alto    | Baja         | Implementar pruebas de integración y validación de contratos en CI/CD.    |
| Falta de visibilidad sobre el progreso     | Medio   | Baja         | Implementar dashboards de seguimiento y reportes periódicos.              |


## Métricas de Éxito

Para medir el éxito del plan de acción, se establecerán las siguientes métricas:

| Métrica                                      | Objetivo                     | Herramienta de Medición               |
|---------------------------------------------|------------------------------|---------------------------------------|
| Porcentaje de APIs con documentación actualizada | 100%                   | Portal de Desarrolladores             |
| Tiempo promedio de onboarding de nuevos desarrolladores | < 2 días          | Encuestas a equipos                   |
| Porcentaje de solicitudes rechazadas por validación de esquemas | < 1%         | API Gateway                           |
| Tiempo promedio de respuesta de APIs críticas | < 200 ms             | Herramientas de monitoreo             |
| Porcentaje de APIs con autenticación centralizada | 100%             | API Gateway                           |
| Número de incidentes de seguridad reportados | 0                      | Sistema de tickets                    |
| Porcentaje de APIs con métricas de rendimiento monitoreadas | 100%       | Herramientas de monitoreo             |
| Número de APIs obsoletas identificadas y eliminadas | > 5               | Reportes de uso                       |


## Conclusión

Este plan de acción proporciona una hoja de ruta clara para elevar el nivel de madurez de las APIs de Pragma, alineada con los objetivos estratégicos de la organización y los atributos de calidad definidos. La priorización de iniciativas asegura que los esfuerzos se enfoquen en las áreas de mayor impacto, mientras que el roadmap proporciona visibilidad sobre el progreso esperado.

La implementación de estas propuestas no solo mejorará la calidad técnica de las APIs, sino que también fortalecerá la colaboración entre equipos, mejorará la experiencia de los desarrolladores y reducirá riesgos operativos. Se recomienda revisar periódicamente el progreso del plan y ajustar las prioridades según sea necesario.