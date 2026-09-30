# Instrucciones generales para GitHub Copilot

## Idioma

- Responde SIEMPRE en español, incluso cuando las instrucciones, plantillas o el código estén en inglés.
- Todo artefacto de Spec Kit (`spec.md`, `plan.md`, `research.md`, `data-model.md`, `quickstart.md`, `contracts/`, `tasks.md`, checklists y `constitution.md`) debe redactarse en español.
- Los nombres de código (clases, métodos, variables, archivos), comandos y rutas se mantienen tal cual.

## Tokens de Spec Kit que NO se deben traducir

Los scripts y otros comandos `/speckit.*` dependen de estos textos literales:

- Marcadores: `[NEEDS CLARIFICATION: ...]`, `NEEDS CLARIFICATION`, `N/A`, `[P]`, `[US1]`, `[US2]`...
- Identificadores: `T001`, `FR-001`, `SC-001`, `CHK001`, casillas `- [ ]` / `- [x]`.
- Campos de `plan.md`: `**Language/Version**:`, `**Primary Dependencies**:`, `**Storage**:`, `**Project Type**:` (el valor sí puede ir en español).
- Encabezados: `## Clarifications`, `### Session YYYY-MM-DD`, `## Phase N: Convergence`, `## Active Technologies`, `## Recent Changes`.
- Marcadores de plantilla de la constitución: `[PROJECT_NAME]`, `[PRINCIPLE_1_NAME]`, etc.
