# ADR 004: Marco para Propuestas de Mejora de APIs

## Contexto

El sistema de APIs de Pragma ha sido evaluado según el modelo de madurez interno, identificando brechas en aspectos como documentación, rendimiento, seguridad y escalabilidad. Para cerrar estas brechas, es necesario establecer un marco estructurado que permita proponer, priorizar y planificar mejoras de manera alineada con los atributos de calidad definidos (ej: latencia < 200ms para APIs externas, disponibilidad > 99.9%).

El marco debe:
- Establecer criterios de priorización basados en impacto técnico y valor de negocio.
- Definir plantillas para documentar cada propuesta de mejora.
- Incluir un flujo de aprobación y seguimiento de implementación.
- Asegurar que las mejoras propuestas sean medibles y verificables.

## Opciones Consideradas

### Opción 1: Propuestas ad-hoc sin marco formal
- **Descripción**: Cada equipo propone mejoras sin estructura común, priorizando según criterios locales.
- **Ventajas**: Flexibilidad y rapidez en la generación de ideas.
- **Desventajas**: Falta de alineación entre equipos, dificultad para priorizar a nivel global, riesgo de soluciones parciales.

### Opción 2: Marco basado en RFCs (Request for Comments)
- **Descripción**: Usar un formato similar a los RFCs de IETF, con secciones para contexto, propuesta, impacto y alternativas.
- **Ventajas**: Estructura clara y probada en la industria.
- **Desventajas**: Puede ser excesivamente formal para el contexto actual de Pragma.

### Opción 3: Marco ligero con plantilla estandarizada y matriz de priorización
- **Descripción**: Definir una plantilla simple para documentar cada propuesta, junto con una matriz de priorización basada en impacto y esfuerzo.
- **Ventajas**: Equilibrio entre estructura y flexibilidad, alineación con los atributos de calidad definidos.
- **Desventajas**: Requiere disciplina para mantener el marco actualizado.

## Decisión

Se adopta la **Opción 3**: un marco ligero con plantilla estandarizada y matriz de priorización. Esta opción permite:
- Documentar cada propuesta de manera consistente.
- Priorizar mejoras basadas en criterios objetivos.
- Facilitar la revisión y aprobación por parte de los stakeholders.

El marco incluirá:
1. **Plantilla de propuesta**:
   - **Título**: Nombre descriptivo de la mejora.
   - **API afectada**: Enlace al catálogo de APIs (ver ADR 002).
   - **Contexto**: Problema o oportunidad identificada.
   - **Propuesta**: Descripción detallada de la mejora.
   - **Impacto**: Beneficios esperados (ej: reducción de latencia, mejora en seguridad).
   - **Métricas**: Indicadores para medir el éxito (ej: latencia < 150ms).
   - **Esfuerzo**: Estimación de esfuerzo (bajo/medio/alto).
   - **Dependencias**: APIs o sistemas afectados.
   - **Riesgos**: Posibles efectos negativos.

2. **Matriz de priorización**:
   - **Impacto técnico**: Alto/Medio/Bajo (basado en atributos de calidad como latencia, disponibilidad).
   - **Valor de negocio**: Alto/Medio/Bajo (basado en alineación con objetivos estratégicos).
   - **Esfuerzo**: Alto/Medio/Bajo.
   - **Prioridad final**: Calculada como (Impacto técnico + Valor de negocio) / Esfuerzo.

## Consecuencias

### Positivas
- **Alineación**: Las mejoras propuestas estarán alineadas con los atributos de calidad y objetivos estratégicos de Pragma.
- **Transparencia**: El proceso de priorización será transparente y basado en criterios objetivos.
- **Medición**: Cada mejora podrá ser verificada mediante métricas cuantificables.

### Negativas
- **Sobrecarga inicial**: Requiere tiempo para documentar y priorizar las primeras propuestas.
- **Mantenimiento**: El marco deberá ser actualizado periódicamente para reflejar cambios en prioridades o atributos de calidad.

### Riesgos
- **Falta de adopción**: Si los equipos no adoptan el marco, las propuestas podrían seguir siendo ad-hoc.
- **Priorización subjetiva**: La matriz de priorización podría ser malinterpretada si los criterios no son claros.

### Mitigaciones
- **Capacitación**: Talleres para equipos sobre cómo usar el marco.
- **Revisión periódica**: Evaluar la efectividad del marco cada 3 meses.
- **Ejemplos**: Incluir ejemplos de propuestas bien documentadas en el repositorio.