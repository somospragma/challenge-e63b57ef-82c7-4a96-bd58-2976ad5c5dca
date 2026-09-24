# ADR 002: Metodología para Catalogación de APIs

## Contexto
Para gestionar eficazmente el ecosistema de APIs de Pragma, es necesario identificar y catalogar todas las APIs existentes. Actualmente, no existe un inventario centralizado, lo que dificulta la evaluación de dependencias, la identificación de redundancias y la planificación de mejoras.

## Opciones Consideradas
1. **Catálogo Manual**
   - **Descripción**: Crear un inventario manualmente mediante entrevistas con equipos y revisión de documentación.
   - **Ventajas**: Bajo costo inicial.
   - **Desventajas**: Propenso a errores y desactualización.

2. **Herramienta de Descubrimiento Automatizado**
   - **Descripción**: Utilizar herramientas como Postman, SwaggerHub o Apigee para descubrir y catalogar APIs automáticamente.
   - **Ventajas**: Precisión y actualización en tiempo real.
   - **Desventajas**: Requiere integración con sistemas existentes.

3. **Catálogo Híbrido**
   - **Descripción**: Combinar descubrimiento automatizado con validación manual.
   - **Ventajas**: Equilibrio entre precisión y eficiencia.
   - **Desventajas**: Requiere mantenimiento continuo.

## Decisión
Se adoptará un **catálogo híbrido**, que combine herramientas de descubrimiento automatizado (como OpenAPI/Swagger) con validación manual por parte de los equipos responsables. El catálogo incluirá los siguientes atributos para cada API:
- **Nombre y descripción**.
- **Tipo (REST, GraphQL, SOAP, etc.)**.
- **Dependencias (servicios internos/externos)**.
- **Nivel de exposición (pública, privada, partner)**.
- **Equipo responsable**.

## Consecuencias
- **Positivas**:
  - Inventario centralizado y actualizado.
  - Identificación clara de dependencias y redundancias.
- **Negativas**:
  - Requiere esfuerzo inicial para configurar herramientas.
  - Necesidad de mantenimiento continuo.

---