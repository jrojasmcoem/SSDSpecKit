# Especificación de la funcionalidad: [FEATURE NAME]

**Rama de la funcionalidad**: `[###-feature-name]`  
**Creado**: [DATE]  
**Estado**: Borrador  
**Entrada**: Descripción del usuario: "$ARGUMENTS"

## Escenarios de usuario y pruebas _(obligatorio)_

<!--
  IMPORTANTE: Las historias de usuario deben estar PRIORIZADAS como recorridos de usuario ordenados por importancia.
  Cada historia/recorrido debe poder PROBARSE DE FORMA INDEPENDIENTE: si implementas solo UNA de ellas,
  aún debes tener un MVP (Producto Mínimo Viable) que aporte valor.

  Asigna prioridades (P1, P2, P3, etc.) a cada historia, siendo P1 la más crítica.
  Piensa en cada historia como una porción autónoma de funcionalidad que puede ser:
  - Desarrollada de forma independiente
  - Probada de forma independiente
  - Desplegada de forma independiente
  - Demostrada a los usuarios de forma independiente
-->

### Historia de usuario 1 - [Título breve] (Prioridad: P1)

[Describe este recorrido de usuario en lenguaje sencillo]

**Por qué esta prioridad**: [Explica el valor y por qué tiene este nivel de prioridad]

**Prueba independiente**: [Describe cómo puede probarse de forma independiente; p. ej., "Se puede probar completamente mediante [acción concreta] y aporta [valor concreto]"]

**Escenarios de aceptación**:

1. **Dado** [estado inicial], **Cuando** [acción], **Entonces** [resultado esperado]
2. **Dado** [estado inicial], **Cuando** [acción], **Entonces** [resultado esperado]

---

### Historia de usuario 2 - [Título breve] (Prioridad: P2)

[Describe este recorrido de usuario en lenguaje sencillo]

**Por qué esta prioridad**: [Explica el valor y por qué tiene este nivel de prioridad]

**Prueba independiente**: [Describe cómo puede probarse de forma independiente]

**Escenarios de aceptación**:

1. **Dado** [estado inicial], **Cuando** [acción], **Entonces** [resultado esperado]

---

### Historia de usuario 3 - [Título breve] (Prioridad: P3)

[Describe este recorrido de usuario en lenguaje sencillo]

**Por qué esta prioridad**: [Explica el valor y por qué tiene este nivel de prioridad]

**Prueba independiente**: [Describe cómo puede probarse de forma independiente]

**Escenarios de aceptación**:

1. **Dado** [estado inicial], **Cuando** [acción], **Entonces** [resultado esperado]

---

[Añade más historias de usuario según sea necesario, cada una con su prioridad asignada]

### Casos límite

<!--
  ACCIÓN REQUERIDA: El contenido de esta sección son marcadores de posición.
  Rellénalos con los casos límite adecuados.
-->

- ¿Qué ocurre cuando [condición límite]?
- ¿Cómo gestiona el sistema [escenario de error]?

## Requisitos _(obligatorio)_

<!--
  ACCIÓN REQUERIDA: El contenido de esta sección son marcadores de posición.
  Rellénalos con los requisitos funcionales adecuados.
-->

### Requisitos funcionales

- **FR-001**: El sistema DEBE [capacidad concreta, p. ej., "permitir a los usuarios crear cuentas"]
- **FR-002**: El sistema DEBE [capacidad concreta, p. ej., "validar direcciones de correo electrónico"]
- **FR-003**: Los usuarios DEBEN poder [interacción clave, p. ej., "restablecer su contraseña"]
- **FR-004**: El sistema DEBE [requisito de datos, p. ej., "persistir las preferencias del usuario"]
- **FR-005**: El sistema DEBE [comportamiento, p. ej., "registrar todos los eventos de seguridad"]

_Ejemplo de cómo marcar requisitos poco claros:_

- **FR-006**: El sistema DEBE autenticar a los usuarios mediante [NEEDS CLARIFICATION: método de autenticación no especificado - correo/contraseña, SSO, OAuth?]
- **FR-007**: El sistema DEBE conservar los datos de usuario durante [NEEDS CLARIFICATION: periodo de retención no especificado]

### Entidades clave _(incluir si la funcionalidad implica datos)_

- **[Entidad 1]**: [Qué representa, atributos clave sin detalles de implementación]
- **[Entidad 2]**: [Qué representa, relaciones con otras entidades]

## Criterios de éxito _(obligatorio)_

<!--
  ACCIÓN REQUERIDA: Define criterios de éxito medibles.
  Deben ser medibles e independientes de la tecnología.
-->

### Resultados medibles

- **SC-001**: [Métrica medible, p. ej., "Los usuarios pueden completar la creación de cuenta en menos de 2 minutos"]
- **SC-002**: [Métrica medible, p. ej., "El sistema soporta 1000 usuarios concurrentes sin degradación"]
- **SC-003**: [Métrica de satisfacción, p. ej., "El 90% de los usuarios completa la tarea principal al primer intento"]
- **SC-004**: [Métrica de negocio, p. ej., "Reducir en un 50% los tickets de soporte relacionados con [X]"]
