<!--
Sync Impact Report
- Cambio de versión: plantilla sin versionar → 1.0.0
- Principios definidos (antes: marcadores de plantilla):
  - [PRINCIPLE_1_NAME] → I. Offline-first con fines formativos
  - [PRINCIPLE_2_NAME] → II. Abstracción de infraestructura
  - [PRINCIPLE_3_NAME] → III. Seguridad en profundidad (NO NEGOCIABLE)
  - [PRINCIPLE_4_NAME] → IV. Arquitectura por capas y coherencia con el código existente
  - [PRINCIPLE_5_NAME] → V. Desarrollo guiado por especificaciones
  - Añadido: VI. Rendimiento medible y simplicidad
- Secciones añadidas: Restricciones técnicas y de seguridad; Flujo de desarrollo y puertas de calidad
- Secciones eliminadas: ninguna
- Plantillas revisadas:
  - ✅ .specify/templates/plan-template.md (la "Constitution Check" se deriva de este archivo; sin cambios)
  - ✅ .specify/templates/spec-template.md (sin cambios necesarios)
  - ✅ .specify/templates/tasks-template.md (sin cambios necesarios)
- TODOs diferidos: ninguno
-->

# Constitución de ContosoDashboard

## Principios fundamentales

### I. Offline-first con fines formativos

ContosoDashboard es una aplicación de FORMACIÓN y DEBE funcionar íntegramente en local y sin conexión.

- Ninguna funcionalidad DEBE requerir servicios en la nube, suscripciones ni dependencias externas
  en tiempo de ejecución (base de datos en SQL Server LocalDB, archivos en el sistema de archivos
  local, autenticación simulada).
- Toda limitación conocida respecto a un entorno de producción DEBE documentarse (README o
  artefactos de la funcionalidad) en lugar de ocultarse.
- El código DEBE demostrar buenas prácticas, simplificadas para el contexto formativo.

**Justificación**: el laboratorio debe poder ejecutarse en cualquier equipo sin costes de nube ni
credenciales externas.

### II. Abstracción de infraestructura

Toda dependencia de infraestructura (almacenamiento de archivos, base de datos, identidad, escaneo
de virus, etc.) DEBE consumirse a través de una interfaz registrada mediante inyección de
dependencias.

- La implementación local (p. ej., `LocalFileStorageService`) y la futura implementación en la nube
  (p. ej., `AzureBlobStorageService`) DEBEN ser intercambiables solo cambiando la configuración de
  DI, sin modificar la lógica de negocio, la UI ni el esquema de base de datos.
- Las rutas y claves de almacenamiento DEBEN ser portables entre local y nube
  (p. ej., `{userId}/{projectId|personal}/{guid}.{ext}`).
- Las páginas y componentes NO DEBEN acceder directamente a `System.IO`, al `DbContext` ni a SDK
  externos; DEBEN hacerlo a través de servicios.

**Justificación**: garantiza una ruta de migración a Azure (Azure SQL, Blob Storage, Microsoft Entra
ID) sin reescrituras.

### III. Seguridad en profundidad (NO NEGOCIABLE)

La seguridad DEBE aplicarse en varias capas: middleware, atributos de página y comprobaciones en la
capa de servicios.

- Toda página protegida DEBE llevar `[Authorize]` (o la política de rol correspondiente).
- Todo método de servicio que devuelva o modifique datos de un recurso DEBE verificar que el usuario
  actual tiene permiso sobre ese recurso concreto (protección IDOR), según el modelo de roles
  Employee → TeamLead → ProjectManager → Administrator.
- Los usuarios SOLO DEBEN ver los datos para los que están autorizados, incluidos los resultados de
  búsqueda, los listados y los widgets.
- Las entradas de usuario DEBEN validarse en el servidor. Para archivos: lista blanca de extensiones
  y tipos MIME, límite de tamaño y nombres generados por GUID; NUNCA se usarán nombres de archivo
  proporcionados por el usuario para construir rutas.
- Los archivos subidos DEBEN almacenarse fuera de `wwwroot` y servirse solo mediante endpoints que
  apliquen autorización.
- Se DEBEN mantener las cabeceras de seguridad existentes (CSP, X-Frame-Options, etc.) y la
  configuración segura de cookies.

**Justificación**: aunque la autenticación es simulada, la autorización y la validación son reales y
constituyen el núcleo pedagógico del proyecto.

### IV. Arquitectura por capas y coherencia con el código existente

Las nuevas funcionalidades DEBEN integrarse en la arquitectura actual sin reescrituras importantes.

- Se DEBE respetar la separación Models / Data / Services / Pages / Shared.
- Las entidades DEBEN usar claves `int`, igual que `User` y `Project`; los valores de catálogo
  simples (p. ej., categorías) se PUEDEN guardar como texto cuando la especificación lo indique.
- Los cambios de esquema DEBEN realizarse mediante Entity Framework Core y mantener los datos de
  ejemplo existentes.
- Las operaciones con efectos en varios recursos DEBEN ordenarse para evitar estados inconsistentes
  (p. ej., generar ruta única → guardar archivo → guardar metadatos).
- La integración con funcionalidades existentes (tareas, proyectos, notificaciones, panel) DEBE
  reutilizar sus servicios en lugar de duplicar lógica.

**Justificación**: preserva la mantenibilidad y hace que las funcionalidades nuevas sean coherentes
para quienes estudian el código.

### V. Desarrollo guiado por especificaciones

Toda funcionalidad nueva DEBE seguir el flujo de Spec Kit: constitución → especificación →
clarificación → plan → tareas → implementación.

- `spec.md` DEBE describir el QUÉ y el PARA QUÉ, sin detalles de implementación, e incluir escenarios
  de aceptación en formato Dado-Cuando-Entonces y criterios de éxito medibles.
- `plan.md` DEBE superar la "Constitution Check" antes de la fase de investigación y volver a
  verificarse tras el diseño; cualquier desviación DEBE justificarse en la tabla de complejidad.
- Cada requisito funcional DEBE poder trazarse a una o más tareas en `tasks.md`.
- La implementación DEBE validarse contra los escenarios de aceptación antes de darse por terminada.

**Justificación**: la trazabilidad requisito → tarea → código es el objetivo del laboratorio y evita
requisitos olvidados o alcance no solicitado.

### VI. Rendimiento medible y simplicidad

- Los objetivos de rendimiento DEBEN expresarse como valores medibles en la especificación
  (p. ej., listados < 2 s para 500 elementos, búsqueda < 2 s, vista previa < 3 s, subida de 25 MB
  < 30 s).
- Las consultas DEBEN filtrarse y paginarse en la base de datos, no en memoria, y usar índices cuando
  el volumen lo requiera.
- Se DEBE elegir la solución más sencilla que cumpla los requisitos (YAGNI); no se añadirán
  abstracciones, paquetes o patrones que no exija la especificación o el principio II.

**Justificación**: los requisitos de rendimiento solo son verificables si son explícitos, y la
simplicidad facilita el aprendizaje.

## Restricciones técnicas y de seguridad

- **Plataforma**: ASP.NET Core con Blazor Server; el framework de destino es el definido en
  `ContosoDashboard/ContosoDashboard.csproj` (actualmente `net10.0`).
- **Datos**: Entity Framework Core con SQL Server LocalDB (SQLite como alternativa aceptada en
  equipos ARM64).
- **Autenticación**: autenticación simulada basada en cookies y claims; NO se DEBEN introducir
  contraseñas reales ni proveedores de identidad externos en el alcance formativo.
- **Interfaz**: Bootstrap 5.3 y Bootstrap Icons, siguiendo el diseño de `MainLayout` y `NavMenu`.
- **Almacenamiento de archivos**: sistema de archivos local fuera de `wwwroot`, detrás de
  `IFileStorageService`.
- **Dependencias**: cualquier paquete NuGet nuevo DEBE justificarse en `plan.md` y no DEBE requerir
  conexión a servicios externos en tiempo de ejecución.
- **Auditoría**: las acciones sensibles (subidas, descargas, eliminaciones, comparticiones, cambios
  de permisos) DEBEN registrarse cuando la especificación lo requiera.
- **Alcance**: el proyecto NO está destinado a producción; los requisitos exclusivos de producción
  (MFA, cifrado gestionado, TLS 1.3, escaneo antivirus real) se DEBEN modelar mediante interfaces o
  documentarse como limitaciones conocidas.

## Flujo de desarrollo y puertas de calidad

1. Cada funcionalidad se desarrolla en su propia rama `NNN-nombre-funcionalidad` creada por
   `/speckit.specify`.
2. Antes de implementar, `spec.md`, `plan.md` y `tasks.md` DEBEN existir y ser coherentes
   (se recomienda `/speckit.analyze`).
3. Puertas obligatorias antes de dar una tarea por completada:
   - `dotnet build` sin errores.
   - La aplicación arranca con `dotnet run` y crea/siembra la base de datos sin intervención manual.
   - Los escenarios de aceptación afectados se verifican manualmente con los usuarios simulados
     (Employee, TeamLead, ProjectManager, Administrator), incluidos los casos de acceso denegado.
   - Se añaden pruebas automatizadas cuando la especificación o el plan las solicitan.
4. Las revisiones de código DEBEN comprobar el cumplimiento de los principios II y III
   (abstracciones y autorización) de forma explícita.
5. Los artefactos de Spec Kit y la documentación se redactan en español; los nombres de código se
   mantienen en inglés.

## Gobernanza

- Esta constitución prevalece sobre cualquier otra práctica o guía del repositorio. En caso de
  conflicto, se aplica la constitución y se corrige el otro documento.
- **Enmiendas**: se realizan mediante `/speckit.constitution`, DEBEN incluir el informe de impacto,
  la justificación del cambio y, si afecta a funcionalidades existentes, un plan de migración.
- **Versionado** (SemVer):
  - MAJOR: eliminación o redefinición incompatible de principios o de la gobernanza.
  - MINOR: nuevo principio o sección, o ampliación material de una guía.
  - PATCH: aclaraciones, redacción o correcciones sin cambio semántico.
- **Cumplimiento**: todo `plan.md` DEBE incluir la "Constitution Check" y toda revisión DEBE verificar
  el cumplimiento; la complejidad adicional DEBE justificarse por escrito.
- La guía de desarrollo en tiempo de ejecución para agentes es `.github/copilot-instructions.md`.

**Versión**: 1.0.0 | **Ratificada**: 2026-09-30 | **Última enmienda**: 2026-09-30
