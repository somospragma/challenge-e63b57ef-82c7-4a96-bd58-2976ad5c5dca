# ADR 001: Modelo de Madurez de APIs de Pragma

## Contexto
En Pragma, las APIs son un activo estratégico que requiere estandarización para garantizar calidad, seguridad y escalabilidad. Actualmente, existe una diversidad de APIs con distintos niveles de madurez, lo que dificulta su gobernanza y optimización. Se requiere definir un modelo de madurez que permita evaluar y mejorar sistemáticamente el estado de las APIs.

## Opciones Consideradas
1. **Modelo de Madurez de Richardson**
   - **Descripción**: Clasifica las APIs en niveles según su cumplimiento con REST (nivel 0: POX, nivel 1: recursos, nivel 2: verbos HTTP, nivel 3: HATEOAS).
   - **Ventajas**: Enfoque técnico claro y ampliamente adoptado.
   - **Desventajas**: No aborda aspectos como seguridad, documentación o gobernanza.

2. **Modelo de Madurez de Pragma (Personalizado)**
   - **Descripción**: Modelo adaptado a las necesidades de Pragma, que incluye dimensiones técnicas, de seguridad, documentación y gobernanza.
   - **Ventajas**: Alineado con los objetivos estratégicos de Pragma.
   - **Desventajas**: Requiere definición y validación interna.

3. **Modelo de Madurez de API Evangelist**
   - **Descripción**: Enfoque holístico que evalúa madurez en áreas como diseño, seguridad, escalabilidad y experiencia de desarrollador.
   - **Ventajas**: Cubre múltiples dimensiones.
   - **Desventajas**: Complejidad en la implementación.

## Decisión
Se adoptará el **Modelo de Madurez de Pragma**, personalizado para incluir las siguientes dimensiones:
- **Diseño**: Cumplimiento con estándares RESTful o GraphQL.
- **Seguridad**: Implementación de autenticación, autorización y protección contra amenazas.
- **Documentación**: Disponibilidad de OpenAPI/Swagger, ejemplos y guías.
- **Gobernanza**: Versionado, ciclo de vida y dependencias gestionadas.

## Consecuencias
- **Positivas**:
  - Estándar claro para evaluar y mejorar APIs.
  - Alineación con los objetivos estratégicos de Pragma.
- **Negativas**:
  - Requiere esfuerzo inicial para definir y validar el modelo.
  - Necesidad de herramientas para automatizar la evaluación.

---