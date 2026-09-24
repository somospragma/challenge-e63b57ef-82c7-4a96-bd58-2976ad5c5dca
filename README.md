# Evaluación y optimización de madurez de APIs

El sistema de APIs de Pragma necesita una evaluación de su madurez actual y un plan de optimización. El candidato deberá identificar las APIs existentes, evaluar su madurez según el modelo de Pragma y proponer mejoras. Las APIs interactúan con el motor de reglas, el sistema de autenticación y el servicio de notificaciones. El objetivo es asegurar que las APIs cumplan con los estándares de calidad y rendimiento establecidos por Pragma.

## Informacion General

| Campo | Valor |
|-------|-------|
| **Tema** | implementación de economía de APIs con evaluación de madurez Pragma |
| **Nivel** | senior-l2 |
| **Tipo** | practical |
| **Tiempo estimado** | 10 horas |

## Fases del Reto

### Fase 0: Configuración del Proyecto

**Objetivo:** Obtener el proyecto base funcional enviando el Código Base a un asistente de IA, que lo analizará, corregirá errores y generará un ZIP listo para usar.

**Tiempo estimado:** 15-30 minutos

**Instrucciones:**

- Asegúrate de tener instalado para ejecutar el proyecto: Un IDE o editor de código.
- Copia todo el contenido del campo **Código Base** de este reto — incluyendo el texto de instrucciones que aparece al inicio.
- Abre un asistente de IA (Claude en claude.ai, ChatGPT o Gemini — se recomienda Claude), pega el contenido copiado en el chat y envíalo.
- El asistente analizará los archivos, corregirá errores y generará un archivo ZIP descargable. Descárgalo y extráelo en la carpeta donde quieras trabajar.
- Verifica que el proyecto arranca sin errores.

**Entregable:** El proyecto compila/arranca sin errores.

<details>
<summary>Pistas de conocimiento</summary>

- Copia el Código Base completo incluyendo el texto de instrucciones al inicio — esas instrucciones le indican al asistente exactamente qué hacer con los archivos.
- Si el asistente no genera el ZIP automáticamente al terminar el análisis, escríbele: "genera el ZIP ahora".
- Si el proyecto tiene errores al arrancar, comparte el mensaje de error con el mismo asistente para que lo corrija.

</details>

### Fase 1: Identificación y catalogación de APIs

**Objetivo:** Catalogar todas las APIs existentes en el sistema de Pragma.

**Tiempo estimado:** 2 horas

**Instrucciones:**

- Identificar y listar todas las APIs presentes en el sistema.
- Categorizar cada API según su función y dependencias.

**Entregable:** Lista completa y categorizada de APIs.

<details>
<summary>Pistas de conocimiento</summary>

- Considera APIs tanto internas como externas.
- Incluye información sobre las dependencias de cada API.

</details>

### Fase 2: Evaluación de madurez de APIs

**Objetivo:** Evaluar la madurez de cada API según el modelo de Pragma.

**Tiempo estimado:** 3 horas

**Instrucciones:**

- Aplicar el modelo de madurez de APIs de Pragma a cada API identificada.
- Documentar el nivel de madurez actual de cada API.

**Entregable:** Documento con la evaluación de madurez de cada API.

<details>
<summary>Pistas de conocimiento</summary>

- Revisa el modelo de madurez de APIs de Pragma.
- Identifica áreas de mejora para cada API.

</details>

### Fase 3: Propuesta de mejoras

**Objetivo:** Proponer mejoras para elevar la madurez de las APIs.

**Tiempo estimado:** 3 horas

**Instrucciones:**

- Identificar mejoras específicas para cada API basadas en la evaluación de madurez.
- Documentar un plan de acción para implementar estas mejoras.

**Entregable:** Plan de acción con propuestas de mejora para cada API.

<details>
<summary>Pistas de conocimiento</summary>

- Considera mejoras en la documentación, rendimiento y seguridad.
- Prioriza las mejoras según su impacto y facilidad de implementación.

</details>

### Fase 4: Presentación y discusión

**Objetivo:** Presentar y discutir las propuestas de mejora con el equipo.

**Tiempo estimado:** 2 horas

**Instrucciones:**

- Preparar una presentación de las propuestas de mejora.
- Discutir las propuestas con el equipo y recopilar feedback.

**Entregable:** Presentación de las propuestas de mejora.

<details>
<summary>Pistas de conocimiento</summary>

- Usa ejemplos y casos de uso para ilustrar tus propuestas.
- Sé abierto a recibir feedback y a ajustar tus propuestas en consecuencia.

</details>

## Dimensiones Evaluadas

- **queEs**: ¿Qué es la economía de APIs y cómo se relaciona con la evaluación de madurez?
- **paraQueSirve**: ¿Para qué sirve evaluar la madurez de las APIs en el contexto de Pragma?
- **comoSeUsa**: ¿Cómo se aplica el modelo de madurez de APIs de Pragma en la práctica?
- **erroresComunes**: ¿Cuáles son los errores comunes al evaluar y mejorar la madurez de las APIs?
- **queDecisionesImplica**: ¿Qué decisiones implica proponer mejoras para las APIs?

## Criterios de Evaluacion

- Identificar y catalogar todas las APIs presentes en el sistema.
- Evaluar la madurez de cada API según el modelo de Pragma.
- Proponer mejoras específicas para elevar la madurez de las APIs.
- Presentar y discutir las propuestas de mejora con el equipo.

## Como trabajar con un asistente de IA

Hay dos caminos, elegi uno:

- **AGENTS.md** (recomendado) — instrucciones nativas del repo. Abri esta carpeta con tu agente local (Claude Code, Cursor, Codex, Copilot, Gemini) y las carga solo. Sabe que archivos faltan y con que comando se verifica, y completa el scaffold escribiendo en disco.
- **PROMPT_MEJORA.md** — para copiar y pegar en un chat (claude.ai, ChatGPT). Devuelve un ZIP con el proyecto. Sirve si no tenes un agente en el IDE.

Ninguno de los dos resuelve las fases del reto: eso es tu trabajo.

## Verificacion

El proyecto esta listo para trabajar cuando este comando corre sin errores:

```bash
python3 -c "import glob,sys; assert glob.glob('adr/*.md') and glob.glob('diagramas/*.mmd'), 'faltan ADRs o diagramas'"
```

---

*Reto generado automaticamente por Challenge Generator - Pragma*
