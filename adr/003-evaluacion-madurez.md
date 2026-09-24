# ADR 003: Proceso de Evaluación de Madurez de APIs

## Contexto
Para implementar el Modelo de Madurez de APIs de Pragma (ADR 001), es necesario definir un proceso de evaluación que permita medir el estado actual de cada API y priorizar mejoras. Actualmente, no existe un proceso estandarizado para evaluar la madurez de las APIs.

## Opciones Consideradas
1. **Evaluación Manual**
   - **Descripción**: Evaluar cada API manualmente utilizando una checklist basada en el modelo de madurez.
   - **Ventajas**: Flexibilidad y adaptabilidad.
   - **Desventajas**: Subjetividad y consumo de tiempo.

2. **Herramientas de Evaluación Automatizada**
   - **Descripción**: Utilizar herramientas como API Science, Runscope o Postman para automatizar la evaluación de métricas técnicas.
   - **Ventajas**: Precisión y escalabilidad.
   - **Desventajas**: Limitado a métricas técnicas, sin evaluar gobernanza o documentación.

3. **Evaluación Híbrida**
   - **Descripción**: Combinar herramientas automatizadas para métricas técnicas con evaluación manual para gobernanza y documentación.
   - **Ventajas**: Equilibrio entre precisión y cobertura.
   - **Desventajas**: Requiere coordinación entre equipos.

## Decisión
Se adoptará un **proceso de evaluación híbrida**, que combine herramientas automatizadas para métricas técnicas (ej. latencia, disponibilidad, cumplimiento de estándares REST) con evaluación manual para dimensiones como gobernanza, documentación y seguridad. Las métricas a evaluar incluyen:
- **Diseño**: Cumplimiento con estándares RESTful/GraphQL.
- **Seguridad**: Autenticación, autorización y protección contra amenazas.
- **Documentación**: Disponibilidad de OpenAPI/Swagger y ejemplos.
- **Gobernanza**: Versionado, ciclo de vida y gestión de dependencias.

## Consecuencias
- **Positivas**:
  - Evaluación objetiva y estandarizada.
  - Identificación clara de áreas de mejora.
- **Negativas**:
  - Requiere herramientas y esfuerzo inicial.
  - Necesidad de coordinación entre equipos para evaluación manual.