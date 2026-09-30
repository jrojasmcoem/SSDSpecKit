---
description: "Plantilla de lista de tareas para la implementación de una funcionalidad"
---

# Tareas: [FEATURE NAME]

**Entrada**: Documentos de diseño en `/specs/[###-feature-name]/`
**Prerrequisitos**: plan.md (obligatorio), spec.md (obligatorio para las historias de usuario), research.md, data-model.md, contracts/

**Pruebas**: Los ejemplos siguientes incluyen tareas de prueba. Las pruebas son OPCIONALES: inclúyelas solo si se solicitan explícitamente en la especificación.

**Organización**: Las tareas se agrupan por historia de usuario para permitir implementar y probar cada historia de forma independiente.

## Formato: `[ID] [P?] [Story] Descripción`

- **[P]**: Puede ejecutarse en paralelo (archivos distintos, sin dependencias)
- **[Story]**: Historia de usuario a la que pertenece la tarea (p. ej., US1, US2, US3)
- Incluye rutas de archivo exactas en las descripciones

## Convenciones de rutas

- **Proyecto único**: `src/`, `tests/` en la raíz del repositorio
- **Aplicación web**: `backend/src/`, `frontend/src/`
- **Móvil**: `api/src/`, `ios/src/` o `android/src/`
- Las rutas mostradas asumen un proyecto único; ajústalas según la estructura de plan.md

<!--
  ============================================================================
  IMPORTANTE: Las tareas siguientes son EJEMPLOS solo a modo ilustrativo.

  El comando /speckit.tasks DEBE reemplazarlas por tareas reales basadas en:
  - Las historias de usuario de spec.md (con sus prioridades P1, P2, P3...)
  - Los requisitos de la funcionalidad en plan.md
  - Las entidades de data-model.md
  - Los endpoints de contracts/

  Las tareas DEBEN organizarse por historia de usuario para que cada historia pueda:
  - Implementarse de forma independiente
  - Probarse de forma independiente
  - Entregarse como un incremento del MVP

  NO mantengas estas tareas de ejemplo en el tasks.md generado.
  ============================================================================
-->

## Fase 1: Configuración (infraestructura compartida)

**Propósito**: Inicialización del proyecto y estructura básica

- [ ] T001 Crear la estructura del proyecto según el plan de implementación
- [ ] T002 Inicializar el proyecto [lenguaje] con las dependencias de [framework]
- [ ] T003 [P] Configurar herramientas de linting y formato

---

## Fase 2: Fundamentos (prerrequisitos bloqueantes)

**Propósito**: Infraestructura base que DEBE estar completa antes de implementar CUALQUIER historia de usuario

**⚠️ CRÍTICO**: Ninguna historia de usuario puede empezar hasta completar esta fase

Ejemplos de tareas fundamentales (ajústalas a tu proyecto):

- [ ] T004 Configurar el esquema de base de datos y el framework de migraciones
- [ ] T005 [P] Implementar el framework de autenticación/autorización
- [ ] T006 [P] Configurar el enrutamiento de la API y los middleware
- [ ] T007 Crear los modelos/entidades base de los que dependen todas las historias
- [ ] T008 Configurar la gestión de errores y la infraestructura de logging
- [ ] T009 Configurar la gestión de configuración por entorno

**Punto de control**: Base lista; la implementación de historias de usuario puede empezar en paralelo

---

## Fase 3: Historia de usuario 1 - [Título] (Prioridad: P1) 🎯 MVP

**Objetivo**: [Breve descripción de lo que aporta esta historia]

**Prueba independiente**: [Cómo verificar que esta historia funciona por sí sola]

### Pruebas de la historia de usuario 1 (OPCIONAL - solo si se solicitan pruebas) ⚠️

> **NOTA: Escribe estas pruebas PRIMERO y asegúrate de que FALLAN antes de implementar**

- [ ] T010 [P] [US1] Prueba de contrato para [endpoint] en tests/contract/test\_[nombre].py
- [ ] T011 [P] [US1] Prueba de integración para [recorrido de usuario] en tests/integration/test\_[nombre].py

### Implementación de la historia de usuario 1

- [ ] T012 [P] [US1] Crear el modelo [Entidad1] en src/models/[entidad1].py
- [ ] T013 [P] [US1] Crear el modelo [Entidad2] en src/models/[entidad2].py
- [ ] T014 [US1] Implementar [Servicio] en src/services/[servicio].py (depende de T012, T013)
- [ ] T015 [US1] Implementar [endpoint/funcionalidad] en src/[ubicación]/[archivo].py
- [ ] T016 [US1] Añadir validación y gestión de errores
- [ ] T017 [US1] Añadir logging para las operaciones de la historia de usuario 1

**Punto de control**: En este punto, la historia de usuario 1 debe ser totalmente funcional y probable de forma independiente

---

## Fase 4: Historia de usuario 2 - [Título] (Prioridad: P2)

**Objetivo**: [Breve descripción de lo que aporta esta historia]

**Prueba independiente**: [Cómo verificar que esta historia funciona por sí sola]

### Pruebas de la historia de usuario 2 (OPCIONAL - solo si se solicitan pruebas) ⚠️

- [ ] T018 [P] [US2] Prueba de contrato para [endpoint] en tests/contract/test\_[nombre].py
- [ ] T019 [P] [US2] Prueba de integración para [recorrido de usuario] en tests/integration/test\_[nombre].py

### Implementación de la historia de usuario 2

- [ ] T020 [P] [US2] Crear el modelo [Entidad] en src/models/[entidad].py
- [ ] T021 [US2] Implementar [Servicio] en src/services/[servicio].py
- [ ] T022 [US2] Implementar [endpoint/funcionalidad] en src/[ubicación]/[archivo].py
- [ ] T023 [US2] Integrar con los componentes de la historia de usuario 1 (si es necesario)

**Punto de control**: En este punto, las historias de usuario 1 Y 2 deben funcionar de forma independiente

---

## Fase 5: Historia de usuario 3 - [Título] (Prioridad: P3)

**Objetivo**: [Breve descripción de lo que aporta esta historia]

**Prueba independiente**: [Cómo verificar que esta historia funciona por sí sola]

### Pruebas de la historia de usuario 3 (OPCIONAL - solo si se solicitan pruebas) ⚠️

- [ ] T024 [P] [US3] Prueba de contrato para [endpoint] en tests/contract/test\_[nombre].py
- [ ] T025 [P] [US3] Prueba de integración para [recorrido de usuario] en tests/integration/test\_[nombre].py

### Implementación de la historia de usuario 3

- [ ] T026 [P] [US3] Crear el modelo [Entidad] en src/models/[entidad].py
- [ ] T027 [US3] Implementar [Servicio] en src/services/[servicio].py
- [ ] T028 [US3] Implementar [endpoint/funcionalidad] en src/[ubicación]/[archivo].py

**Punto de control**: Todas las historias de usuario deben ser ahora funcionales de forma independiente

---

[Añade más fases de historias de usuario según sea necesario, siguiendo el mismo patrón]

---

## Fase N: Pulido y aspectos transversales

**Propósito**: Mejoras que afectan a varias historias de usuario

- [ ] TXXX [P] Actualizar la documentación en docs/
- [ ] TXXX Limpieza y refactorización del código
- [ ] TXXX Optimización de rendimiento en todas las historias
- [ ] TXXX [P] Pruebas unitarias adicionales (si se solicitan) en tests/unit/
- [ ] TXXX Refuerzo de la seguridad
- [ ] TXXX Ejecutar la validación de quickstart.md

---

## Dependencias y orden de ejecución

### Dependencias entre fases

- **Configuración (Fase 1)**: Sin dependencias; puede empezar de inmediato
- **Fundamentos (Fase 2)**: Depende de completar la Configuración; BLOQUEA todas las historias de usuario
- **Historias de usuario (Fase 3+)**: Todas dependen de completar la fase de Fundamentos
  - Después pueden avanzar en paralelo (si hay personal)
  - O secuencialmente por prioridad (P1 → P2 → P3)
- **Pulido (fase final)**: Depende de completar todas las historias de usuario deseadas

### Dependencias entre historias de usuario

- **Historia de usuario 1 (P1)**: Puede empezar tras Fundamentos (Fase 2); sin dependencias con otras historias
- **Historia de usuario 2 (P2)**: Puede empezar tras Fundamentos (Fase 2); puede integrarse con US1 pero debe poder probarse de forma independiente
- **Historia de usuario 3 (P3)**: Puede empezar tras Fundamentos (Fase 2); puede integrarse con US1/US2 pero debe poder probarse de forma independiente

### Dentro de cada historia de usuario

- Las pruebas (si se incluyen) DEBEN escribirse y FALLAR antes de implementar
- Modelos antes que servicios
- Servicios antes que endpoints
- Implementación principal antes que integración
- Completar la historia antes de pasar a la siguiente prioridad

### Oportunidades de paralelismo

- Todas las tareas de Configuración marcadas con [P] pueden ejecutarse en paralelo
- Todas las tareas de Fundamentos marcadas con [P] pueden ejecutarse en paralelo (dentro de la Fase 2)
- Al completar Fundamentos, todas las historias pueden empezar en paralelo (si la capacidad del equipo lo permite)
- Todas las pruebas de una historia marcadas con [P] pueden ejecutarse en paralelo
- Los modelos de una historia marcados con [P] pueden ejecutarse en paralelo
- Distintos miembros del equipo pueden trabajar en paralelo en historias diferentes

---

## Ejemplo de paralelismo: historia de usuario 1

```bash
# Lanzar juntas todas las pruebas de la historia de usuario 1 (si se solicitan pruebas):
Task: "Prueba de contrato para [endpoint] en tests/contract/test_[nombre].py"
Task: "Prueba de integración para [recorrido de usuario] en tests/integration/test_[nombre].py"

# Lanzar juntos todos los modelos de la historia de usuario 1:
Task: "Crear el modelo [Entidad1] en src/models/[entidad1].py"
Task: "Crear el modelo [Entidad2] en src/models/[entidad2].py"
```

---

## Estrategia de implementación

### Primero el MVP (solo historia de usuario 1)

1. Completar la Fase 1: Configuración
2. Completar la Fase 2: Fundamentos (CRÍTICO - bloquea todas las historias)
3. Completar la Fase 3: Historia de usuario 1
4. **DETENERSE Y VALIDAR**: Probar la historia de usuario 1 de forma independiente
5. Desplegar/demostrar si está lista

### Entrega incremental

1. Completar Configuración + Fundamentos → Base lista
2. Añadir historia de usuario 1 → Probar de forma independiente → Desplegar/Demostrar (¡MVP!)
3. Añadir historia de usuario 2 → Probar de forma independiente → Desplegar/Demostrar
4. Añadir historia de usuario 3 → Probar de forma independiente → Desplegar/Demostrar
5. Cada historia aporta valor sin romper las anteriores

### Estrategia con equipo en paralelo

Con varios desarrolladores:

1. El equipo completa Configuración + Fundamentos en conjunto
2. Una vez terminados los Fundamentos:
   - Desarrollador A: Historia de usuario 1
   - Desarrollador B: Historia de usuario 2
   - Desarrollador C: Historia de usuario 3
3. Las historias se completan e integran de forma independiente

---

## Notas

- Tareas [P] = archivos distintos, sin dependencias
- La etiqueta [Story] asocia la tarea a una historia de usuario concreta para trazabilidad
- Cada historia de usuario debe poder completarse y probarse de forma independiente
- Verifica que las pruebas fallan antes de implementar
- Haz commit después de cada tarea o grupo lógico
- Detente en cualquier punto de control para validar la historia de forma independiente
- Evita: tareas vagas, conflictos en el mismo archivo, dependencias entre historias que rompan su independencia
