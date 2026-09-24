# AGENTS.md

Instrucciones para el agente de IA que abra este repositorio (Claude Code, Cursor, Codex, Copilot, Gemini). Se cargan solas: no hay que pegar nada en ningun chat.

## Que es este repositorio

Es el codigo base de un reto de aprendizaje de Pragma: **Evaluación y optimización de madurez de APIs**.

| | |
|---|---|
| Tema | implementación de economía de APIs con evaluación de madurez Pragma |
| Nivel | senior-l2 |
| Chapter | Arquitectura |
| Especialidad | Soluciones |
| Stack | Markdown / C4 Model + ADR |
| Patron arquitectonico | Arquitectura de Documentación con ADRs y C4 Model |
| Tiempo estimado | 10 horas |

## Receta del stack

Esqueleto obligatorio:

- `adr/`
- `arquitectura.md`
- `diagramas/*.mmd`
- `atributos-de-calidad.md`

Dependencias:

- Mermaid.js n/a
- OpenAPI 3.1 3.1.0
- Modelo de Madurez de APIs de Pragma n/a
- C4 Model n/a
- ADR Template n/a

## Tu tarea

Dejar este conjunto de artefactos en estado **verificable**: que el comando de verificacion corra sin errores. Escribi los archivos en disco, en este repositorio. No generes ZIPs ni archivos adjuntos.

En orden:

1. Corre `python3 -c "import glob,sys; assert glob.glob('adr/*.md') and glob.glob('diagramas/*.mmd'), 'faltan ADRs o diagramas'"` y mira que falla.
2. Completa lo que falte de la lista de abajo: manifiesto de dependencias, punto de entrada, capa de interfaz y las capas del patron declarado.
3. Arregla SOLO los errores que impiden compilar o arrancar.
4. Volve a correr `python3 -c "import glob,sys; assert glob.glob('adr/*.md') and glob.glob('diagramas/*.mmd'), 'faltan ADRs o diagramas'"` hasta que pase.
5. Pará ahí.

## Regla dura: las fases son trabajo del humano

**PROHIBIDO implementar los entregables de las fases.** El valor del reto esta en que la persona los resuelva. Tu trabajo es que tenga un proyecto que arranca; el hueco pedagogico se queda como esta.

No resuelvas nada de esto:

- **Fase 1 — Identificación y catalogación de APIs**: Lista completa y categorizada de APIs.
- **Fase 2 — Evaluación de madurez de APIs**: Documento con la evaluación de madurez de cada API.
- **Fase 3 — Propuesta de mejoras**: Plan de acción con propuestas de mejora para cada API.
- **Fase 4 — Presentación y discusión**: Presentación de las propuestas de mejora.

Distincion operativa:

- **Arreglar** (si): import faltante, tipo que no existe, dependencia sin declarar, error de sintaxis, archivo referenciado que no existe.
- **No tocar** (no): logica de negocio incompleta, validaciones ausentes, secretos hardcodeados, APIs deprecadas que funcionan, concurrencia insegura, patrones mejorables. Eso es lo que la persona tiene que encontrar.

## Superficie de practica (NO completes)

Estos archivos SON el ejercicio de la persona. No los implementes; deja stubs. No toques la logica que el reto pide completar.

- [ ] `contratos/openapi.yaml` — El topic pide el contrato de API: openapi.yaml es el ejercicio.
- [ ] `adr/001-modelo-madurez-apis.md` — El topic pide decisiones de arquitectura: el ADR es el ejercicio.
- [ ] `adr/002-catalogacion-apis.md` — El topic pide decisiones de arquitectura: el ADR es el ejercicio.
- [ ] `adr/003-evaluacion-madurez.md` — El topic pide decisiones de arquitectura: el ADR es el ejercicio.
- [ ] `adr/004-propuestas-mejora.md` — El topic pide decisiones de arquitectura: el ADR es el ejercicio.

## Lo que falta y tenes que completar

### 1. Archivos que la arquitectura declara (2 de 16)

La propuesta arquitectonica del reto los lista y no llegaron al repo. Crealos con implementacion real, respetando la capa en la que viven:

- [ ] `diagramas/contenedores.mmd`
- [ ] `diagramas/flujo-critico.mmd`

### Presentes (14)

- `diagramas/contexto.mmd`
- `evaluaciones/catalogo-apis.md`
- `evaluaciones/madurez-apis.md`
- `propuestas/plan-accion.md`
- `propuestas/presentacion.md`
- `README.md`
- `arquitectura.md`
- `atributos-de-calidad.md`
- `riesgos-y-mitigaciones.md`
- `adr/001-modelo-madurez-apis.md`
- `adr/002-catalogacion-apis.md`
- `adr/003-evaluacion-madurez.md`
- `adr/004-propuestas-mejora.md`
- `contratos/openapi.yaml`

### Capas del patron declarado

Cada una tiene que existir como directorio real con al menos un archivo. Codigo plano en la raiz no satisface el patron.

- `adr`
- `diagramas`
- `contratos`
- `evaluaciones`
- `propuestas`

## Verificacion

```bash
python3 -c "import glob,sys; assert glob.glob('adr/*.md') and glob.glob('diagramas/*.mmd'), 'faltan ADRs o diagramas'"
```

El comando tiene que pasar SIN implementar los archivos de la superficie de practica: solo andamiaje.

Ese comando pasando es la definicion de "terminado" para vos.

## Convenciones que tenes que respetar

- Un solo ecosistema: no declares librerias de otro lenguaje ni mezcles gestores de paquetes.
- Toda libreria que uses tiene que estar declarada en el manifiesto de dependencias.
- Todo import declarado tiene que usarse; todo tipo usado tiene que existir o venir de una dependencia declarada.
- El patron es **Arquitectura de Documentación con ADRs y C4 Model**: los contratos (interfaces, puertos) los define la capa interna y los implementa la externa, nunca al revés.
- Los archivos que crees llevan implementacion real, no stubs: sin `TODO`, sin cuerpos vacios, sin `// getters y setters`.

## Contexto del candidato

Sirve para calibrar el nivel del codigo, no para resolver las fases.

- Perfil: Chapter Arquitectura, Especialidad Soluciones, Tecnología APIs, Senior
- Brecha que el reto ataca: Comprende y aplica Economía de APIs teniendo en cuenta el assessment de madurez creado en Pragma.
- Mision: Candidato Senior con experiencia en arquitectura de soluciones, enfocado en cerrar brechas en gestión y evaluación de madurez de APIs.

---

*Generado por Challenge Generator — Pragma. `README.md` tiene el enunciado completo del reto para la persona. `PROMPT_MEJORA.md` es la variante para pegar en un chat, si se prefiere ese flujo.*
