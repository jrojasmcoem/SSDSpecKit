# Plan de implementación: [FEATURE]

**Rama**: `[###-feature-name]` | **Fecha**: [DATE] | **Spec**: [enlace]
**Entrada**: Especificación de la funcionalidad en `/specs/[###-feature-name]/spec.md`

**Nota**: Esta plantilla la completa el comando `/speckit.plan`, disponible en Copilot Chat mediante `.github/prompts/speckit.plan.prompt.md`.

## Resumen

[Extraer de la spec: requisito principal + enfoque técnico derivado de la investigación]

## Contexto técnico

<!--
  ACCIÓN REQUERIDA: Reemplaza el contenido de esta sección con los detalles técnicos
  del proyecto. La estructura se presenta a modo orientativo para guiar
  el proceso de iteración.
  NO traduzcas las etiquetas **Language/Version**, **Primary Dependencies**,
  **Storage** ni **Project Type**: el script update-agent-context las lee literalmente.
-->

**Language/Version**: [p. ej., Python 3.11, Swift 5.9, Rust 1.75 o NEEDS CLARIFICATION]  
**Primary Dependencies**: [p. ej., FastAPI, UIKit, LLVM o NEEDS CLARIFICATION]  
**Storage**: [si aplica, p. ej., PostgreSQL, CoreData, archivos o N/A]  
**Pruebas**: [p. ej., pytest, XCTest, cargo test o NEEDS CLARIFICATION]  
**Plataforma objetivo**: [p. ej., servidor Linux, iOS 15+, WASM o NEEDS CLARIFICATION]
**Project Type**: [single/web/mobile - determina la estructura del código fuente]  
**Objetivos de rendimiento**: [específicos del dominio, p. ej., 1000 req/s, 10k líneas/s, 60 fps o NEEDS CLARIFICATION]  
**Restricciones**: [específicas del dominio, p. ej., <200ms p95, <100MB de memoria, funcionamiento sin conexión o NEEDS CLARIFICATION]  
**Escala/Alcance**: [específicos del dominio, p. ej., 10k usuarios, 1M LOC, 50 pantallas o NEEDS CLARIFICATION]

## Verificación de la constitución

_PUERTA: Debe superarse antes de la investigación de la Fase 0. Volver a comprobar tras el diseño de la Fase 1._

[Puertas determinadas a partir del archivo de constitución]

## Estructura del proyecto

### Documentación (esta funcionalidad)

```text
specs/[###-feature]/
├── plan.md              # Este archivo (salida del comando /speckit.plan)
├── research.md          # Salida de la Fase 0 (comando /speckit.plan)
├── data-model.md        # Salida de la Fase 1 (comando /speckit.plan)
├── quickstart.md        # Salida de la Fase 1 (comando /speckit.plan)
├── contracts/           # Salida de la Fase 1 (comando /speckit.plan)
└── tasks.md             # Salida de la Fase 2 (comando /speckit.tasks - NO lo crea /speckit.plan)
```

### Código fuente (raíz del repositorio)

<!--
  ACCIÓN REQUERIDA: Reemplaza el árbol de ejemplo con la estructura concreta
  de esta funcionalidad. Elimina las opciones no usadas y amplía la estructura elegida con
  rutas reales (p. ej., apps/admin, packages/algo). El plan entregado no debe
  incluir las etiquetas de Opción.
-->

```text
# [ELIMINAR SI NO SE USA] Opción 1: Proyecto único (POR DEFECTO)
src/
├── models/
├── services/
├── cli/
└── lib/

tests/
├── contract/
├── integration/
└── unit/

# [ELIMINAR SI NO SE USA] Opción 2: Aplicación web (cuando se detecta "frontend" + "backend")
backend/
├── src/
│   ├── models/
│   ├── services/
│   └── api/
└── tests/

frontend/
├── src/
│   ├── components/
│   ├── pages/
│   └── services/
└── tests/

# [ELIMINAR SI NO SE USA] Opción 3: Móvil + API (cuando se detecta "iOS/Android")
api/
└── [igual que el backend anterior]

ios/ o android/
└── [estructura específica de la plataforma: módulos, flujos de UI, pruebas de plataforma]
```

**Decisión de estructura**: [Documenta la estructura elegida y referencia los
directorios reales indicados arriba]

## Seguimiento de complejidad

> **Rellenar SOLO si la Verificación de la constitución tiene violaciones que deban justificarse**

| Violación                   | Por qué es necesaria | Alternativa más simple descartada porque  |
| --------------------------- | -------------------- | ----------------------------------------- |
| [p. ej., 4.º proyecto]      | [necesidad actual]   | [por qué 3 proyectos no bastan]           |
| [p. ej., patrón Repository] | [problema concreto]  | [por qué el acceso directo a BD no basta] |
