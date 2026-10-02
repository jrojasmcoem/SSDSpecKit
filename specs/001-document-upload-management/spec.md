# Especificación de la funcionalidad: Carga y gestión de documentos

**Rama de la funcionalidad**: `001-document-upload-management`  
**Creado**: 2026-09-30  
**Estado**: Borrador  
**Entrada**: Descripción del usuario: "--file StakeholderDocs/document-upload-and-management-feature.md" (requisitos de
las partes interesadas para la carga y gestión de documentos en ContosoDashboard)

## Escenarios de usuario y pruebas _(obligatorio)_

### Historia de usuario 1 - Subir un documento y consultarlo en "Mis documentos" (Prioridad: P1)

Un empleado selecciona uno o varios archivos de trabajo desde su equipo, indica un título y una categoría (y
opcionalmente descripción, proyecto y etiquetas) y los sube al panel. Tras la subida, los documentos aparecen en
su lista "Mis documentos", desde donde puede descargarlos.

**Por qué esta prioridad**: es el núcleo del valor de negocio: centralizar los documentos en un lugar seguro.
Sin la subida y consulta de documentos propios no existe ninguna otra capacidad.

**Prueba independiente**: se puede probar iniciando sesión como Ni Kang (Employee), subiendo un PDF de menos de
25 MB con título y categoría, y comprobando que aparece en "Mis documentos" con sus metadatos y que se puede
descargar.

**Escenarios de aceptación**:

1. **Dado** que he iniciado sesión como empleado, **Cuando** selecciono un PDF de menos de 25 MB, indico el título
   "Documento de prueba" y la categoría "Personal Files" y confirmo la subida, **Entonces** veo un indicador de
   progreso, después un mensaje de éxito, y el documento aparece en "Mis documentos" con título, categoría,
   fecha de subida, tamaño y proyecto asociado (si lo hay).
2. **Dado** que estoy en el formulario de subida, **Cuando** intento subir un archivo de 30 MB, **Entonces** el
   sistema rechaza el archivo con un mensaje que indica el límite de 25 MB y no se guarda nada.
3. **Dado** que estoy en el formulario de subida, **Cuando** selecciono un archivo de un tipo no admitido
   (p. ej., un ejecutable), **Entonces** el sistema lo rechaza indicando los tipos permitidos.
4. **Dado** que estoy en el formulario de subida, **Cuando** intento confirmar sin título o sin categoría,
   **Entonces** el sistema me indica los campos obligatorios y no inicia la subida.
5. **Dado** que selecciono varios archivos válidos a la vez, **Cuando** confirmo la subida, **Entonces** cada
   archivo se guarda como un documento independiente y se informa del resultado de cada uno.
6. **Dado** que tengo documentos subidos, **Cuando** pulso descargar en uno de ellos, **Entonces** recibo el
   archivo original con su nombre original.
7. **Dado** que soy miembro de un proyecto, **Cuando** subo un documento y lo asocio a ese proyecto, **Entonces**
   el documento queda vinculado al proyecto; **y Dado** que NO soy miembro de un proyecto, **Entonces** ese
   proyecto no aparece como opción al subir.

---

### Historia de usuario 2 - Organizar y buscar documentos (Prioridad: P2)

Un usuario ordena y filtra su lista de documentos y busca documentos por texto para localizar rápidamente lo
que necesita, viendo solo los documentos a los que tiene acceso.

**Por qué esta prioridad**: resuelve el problema principal señalado por el negocio (dificultad para localizar
documentos) una vez que existen documentos en el sistema.

**Prueba independiente**: con varios documentos subidos por distintos usuarios, se puede probar ordenando,
filtrando y buscando desde la cuenta de un usuario y verificando que los resultados son correctos y que no
aparecen documentos ajenos sin permiso.

**Escenarios de aceptación**:

1. **Dado** que tengo varios documentos, **Cuando** ordeno por título, fecha de subida, categoría o tamaño,
   **Entonces** la lista se reordena según el criterio elegido (ascendente o descendente).
2. **Dado** que tengo documentos de varias categorías y proyectos, **Cuando** filtro por categoría, proyecto o
   rango de fechas, **Entonces** solo se muestran los documentos que cumplen todos los filtros activos.
3. **Dado** que existen documentos accesibles para mí, **Cuando** busco un término que aparece en el título, la
   descripción, las etiquetas, el nombre de quien lo subió o el nombre del proyecto, **Entonces** obtengo los
   documentos coincidentes en menos de 2 segundos.
4. **Dado** que otro usuario tiene un documento personal no compartido conmigo, **Cuando** busco un término que
   coincide con ese documento, **Entonces** ese documento NO aparece en mis resultados.
5. **Dado** que una búsqueda o filtro no devuelve resultados, **Cuando** se muestra la lista, **Entonces** veo un
   mensaje claro de "sin resultados" y la opción de limpiar filtros.

---

### Historia de usuario 3 - Documentos de proyecto (Prioridad: P2)

Al abrir un proyecto, sus miembros ven todos los documentos asociados a él y pueden descargarlos. El Project
Manager del proyecto puede subir documentos al proyecto y eliminar cualquier documento del mismo.

**Por qué esta prioridad**: aporta visibilidad sobre qué documentos pertenecen a cada proyecto, otro de los
problemas de negocio identificados, y aprovecha la pantalla de proyecto existente.

**Prueba independiente**: se puede probar subiendo un documento asociado al proyecto de ejemplo y verificando
que todos sus miembros lo ven en la página del proyecto y que un usuario no miembro no puede acceder a él.

**Escenarios de aceptación**:

1. **Dado** que soy miembro de un proyecto, **Cuando** abro los detalles del proyecto, **Entonces** veo la lista
   de documentos asociados con título, categoría, fecha, tamaño y autor de la subida, y puedo descargarlos.
2. **Dado** que soy el Project Manager del proyecto, **Cuando** subo un documento desde la página del proyecto,
   **Entonces** queda asociado automáticamente a ese proyecto.
3. **Dado** que soy el Project Manager del proyecto, **Cuando** elimino un documento del proyecto subido por
   otro miembro y confirmo, **Entonces** el documento se elimina de forma permanente.
4. **Dado** que NO soy miembro del proyecto (y no soy Administrator), **Cuando** intento acceder a un documento
   del proyecto mediante un enlace directo, **Entonces** el sistema deniega el acceso sin revelar el contenido
   ni los metadatos del documento.

---

### Historia de usuario 4 - Gestionar mis documentos: vista previa, edición, sustitución y eliminación (Prioridad: P3)

Quien subió un documento puede previsualizarlo (PDF e imágenes) sin descargarlo, editar sus metadatos,
sustituir el archivo por una versión actualizada y eliminarlo tras confirmar.

**Por qué esta prioridad**: mejora la calidad y vigencia de la información almacenada, pero el sistema ya
aporta valor sin ella.

**Prueba independiente**: se puede probar sobre un documento propio existente: previsualizarlo, cambiar título
y etiquetas, sustituir el archivo y, finalmente, eliminarlo verificando que desaparece de todas las vistas.

**Escenarios de aceptación**:

1. **Dado** que tengo acceso a un PDF o una imagen, **Cuando** elijo "Vista previa", **Entonces** el documento se
   muestra en el navegador en menos de 3 segundos sin descargarse.
2. **Dado** que tengo acceso a un documento de otro tipo (p. ej., Word), **Cuando** consulto sus acciones,
   **Entonces** no se ofrece vista previa y sí la descarga.
3. **Dado** que subí un documento, **Cuando** edito su título, descripción, categoría o etiquetas y guardo,
   **Entonces** los cambios se reflejan en todas las vistas.
4. **Dado** que subí un documento, **Cuando** lo sustituyo por un archivo nuevo válido, **Entonces** las
   descargas posteriores devuelven el archivo nuevo y el archivo anterior deja de estar disponible.
5. **Dado** que subí un documento, **Cuando** elijo eliminarlo, **Entonces** se me pide confirmación y, al
   confirmar, se elimina de forma permanente de todas las vistas (mis documentos, proyecto, tareas, compartidos).
6. **Dado** que NO subí un documento y no soy su Project Manager, **Cuando** intento editarlo, sustituirlo o
   eliminarlo, **Entonces** el sistema no ofrece la acción y rechaza cualquier intento directo.

---

### Historia de usuario 5 - Compartir documentos (Prioridad: P3)

El propietario de un documento lo comparte con usuarios concretos o con un equipo. Los destinatarios reciben
una notificación dentro de la aplicación y ven el documento en su sección "Compartidos conmigo".

**Por qué esta prioridad**: sustituye el envío de documentos por correo o unidades compartidas, reduciendo
riesgos de seguridad, pero depende de que la subida y la consulta ya funcionen.

**Prueba independiente**: se puede probar compartiendo un documento personal de Ni Kang con Floris Kregel y
verificando la notificación y la aparición en "Compartidos conmigo" de Floris.

**Escenarios de aceptación**:

1. **Dado** que soy propietario de un documento, **Cuando** lo comparto con un usuario concreto, **Entonces** ese
   usuario recibe una notificación en la aplicación y el documento aparece en su sección "Compartidos conmigo".
2. **Dado** que soy propietario de un documento, **Cuando** lo comparto con un equipo, **Entonces** todos los
   miembros del equipo en ese momento reciben la notificación y ven el documento en "Compartidos conmigo".
3. **Dado** que un documento se ha compartido conmigo, **Cuando** lo abro, **Entonces** puedo verlo y descargarlo,
   pero no editarlo, sustituirlo, eliminarlo ni volver a compartirlo.
4. **Dado** que el propietario elimina un documento compartido, **Cuando** accedo a "Compartidos conmigo",
   **Entonces** el documento ya no aparece.
5. **Dado** que no soy propietario de un documento, **Cuando** intento compartirlo, **Entonces** la acción no está
   disponible.

---

### Historia de usuario 6 - Integración con tareas y panel principal (Prioridad: P4)

Desde el detalle de una tarea, los usuarios ven los documentos relacionados, adjuntan documentos existentes o
suben uno nuevo. El panel principal muestra un widget de "Documentos recientes" y el recuento de documentos en
las tarjetas de resumen.

**Por qué esta prioridad**: aumenta la adopción al integrar los documentos en el trabajo diario, pero es una
mejora sobre las capacidades principales.

**Prueba independiente**: se puede probar subiendo un documento desde una tarea y comprobando que queda
asociado a la tarea y a su proyecto, y que aparece en el widget del panel.

**Escenarios de aceptación**:

1. **Dado** que estoy viendo una tarea a la que tengo acceso, **Cuando** subo un documento desde ella,
   **Entonces** el documento queda vinculado a la tarea y asociado automáticamente al proyecto de la tarea.
2. **Dado** que estoy viendo una tarea, **Cuando** adjunto un documento existente al que tengo acceso,
   **Entonces** aparece en la lista de documentos de la tarea.
3. **Dado** que he subido documentos, **Cuando** abro el panel principal, **Entonces** el widget "Documentos
   recientes" muestra mis 5 últimos documentos subidos, del más reciente al más antiguo.
4. **Dado** que abro el panel principal, **Cuando** se muestran las tarjetas de resumen, **Entonces** una de ellas
   indica el número de documentos que he subido.
5. **Dado** que soy miembro de un proyecto, **Cuando** otro miembro añade un documento a ese proyecto,
   **Entonces** recibo una notificación en la aplicación.

---

### Historia de usuario 7 - Auditoría e informes para administradores (Prioridad: P5)

El sistema registra toda la actividad sobre documentos y los administradores consultan informes de uso para
auditoría y cumplimiento.

**Por qué esta prioridad**: necesaria para auditoría y cumplimiento, pero no bloquea el uso diario.

**Prueba independiente**: se puede probar realizando subidas, descargas, comparticiones y eliminaciones con
distintos usuarios y comprobando, como System Administrator, que aparecen en el registro y en los informes.

**Escenarios de aceptación**:

1. **Dado** que un usuario sube, descarga, comparte o elimina un documento, **Cuando** la acción finaliza,
   **Entonces** queda registrada con usuario, acción, documento y fecha/hora.
2. **Dado** que soy Administrator, **Cuando** abro los informes de documentos, **Entonces** veo los tipos de
   documento más subidos, los usuarios que más suben y los patrones de acceso (descargas por documento y
   periodo).
3. **Dado** que NO soy Administrator, **Cuando** intento acceder a los informes, **Entonces** se me deniega el
   acceso.
4. **Dado** que soy Administrator, **Cuando** busco o accedo a cualquier documento, **Entonces** tengo acceso
   completo con fines de auditoría.

---

### Casos límite

- Subida interrumpida o fallida (p. ej., error de almacenamiento o disco lleno): no debe quedar ningún
  documento "fantasma" en las listas; el usuario recibe un mensaje de error claro y puede reintentar.
- Archivo que no supera el análisis de virus/malware: se rechaza, no se almacena y se informa al usuario sin
  detalles técnicos.
- Archivo de exactamente 25 MB: se acepta; cualquier archivo que supere 25 MB se rechaza.
- Archivo vacío (0 bytes): se rechaza con un mensaje explicativo.
- Nombre de archivo con caracteres especiales, espacios o muy largo (p. ej., `Q4 Report (2025) - Finance & Ops.pdf`):
  se acepta y se conserva el nombre original para mostrarlo y descargarlo.
- Dos usuarios suben archivos con el mismo nombre: ambos se almacenan como documentos distintos sin sobrescribirse.
- Extensión que no coincide con el contenido real (p. ej., un ejecutable renombrado a `.pdf`): se rechaza.
- Un usuario deja de ser miembro de un proyecto: pierde el acceso a los documentos del proyecto que no subió ni
  le fueron compartidos; los documentos que subió permanecen en el proyecto.
- Se comparte un documento con un usuario que ya tiene acceso: no se duplica en "Compartidos conmigo" ni se
  envía una notificación repetida.
- Un documento vinculado a una tarea o compartido se elimina: desaparece de la tarea y de "Compartidos conmigo".
- Etiquetas duplicadas o con distinto uso de mayúsculas: se tratan como la misma etiqueta.
- Lista con 500 documentos: se carga en menos de 2 segundos.

## Requisitos _(obligatorio)_

### Requisitos funcionales

**Subida y validación**

- **FR-001**: Los usuarios autenticados DEBEN poder seleccionar y subir uno o varios archivos en una misma
  operación.
- **FR-002**: El sistema DEBE aceptar únicamente PDF, documentos de Microsoft Office (Word, Excel,
  PowerPoint), archivos de texto e imágenes JPEG y PNG, y rechazar cualquier otro tipo con un mensaje que
  indique los tipos permitidos.
- **FR-003**: El sistema DEBE rechazar archivos de más de 25 MB y archivos vacíos, indicando el motivo.
- **FR-004**: El sistema DEBE exigir título y categoría en cada subida; descripción, proyecto asociado y
  etiquetas DEBEN ser opcionales.
- **FR-005**: La categoría DEBE elegirse de la lista fija: Project Documents, Team Resources, Personal Files,
  Reports, Presentations, Other.
- **FR-006**: Los usuarios DEBEN poder añadir etiquetas libres a un documento.
- **FR-007**: El sistema DEBE registrar automáticamente fecha y hora de subida, usuario que sube, tamaño del
  archivo y tipo de archivo.
- **FR-008**: El sistema DEBE mostrar un indicador de progreso durante la subida y un mensaje de éxito o error
  al finalizar, por cada archivo.
- **FR-009**: El sistema DEBE analizar cada archivo en busca de virus y malware antes de almacenarlo y
  rechazar los archivos infectados o sospechosos.
- **FR-010**: El sistema DEBE garantizar que una subida fallida no deje documentos visibles ni registros
  incompletos.
- **FR-011**: El sistema DEBE almacenar los archivos de forma que solo sean accesibles a través de la
  aplicación y tras comprobar permisos; nunca mediante una dirección pública directa.
- **FR-012**: Un usuario SOLO DEBE poder asociar un documento a proyectos de los que es miembro.

**Organización, navegación y búsqueda**

- **FR-013**: Los usuarios DEBEN disponer de una vista "Mis documentos" con todos los documentos que han subido,
  mostrando título, categoría, fecha de subida, tamaño y proyecto asociado.
- **FR-014**: La vista "Mis documentos" DEBE permitir ordenar por título, fecha de subida, categoría y tamaño.
- **FR-015**: La vista "Mis documentos" DEBE permitir filtrar por categoría, proyecto asociado y rango de
  fechas, combinables entre sí.
- **FR-016**: La página de detalles de un proyecto DEBE mostrar los documentos asociados a ese proyecto a
  todos sus miembros, que DEBEN poder descargarlos.
- **FR-017**: Los usuarios DEBEN poder buscar documentos por título, descripción, etiquetas, nombre de quien
  lo subió y nombre del proyecto asociado.
- **FR-018**: Los resultados de búsqueda y todas las listas DEBEN incluir únicamente documentos a los que el
  usuario tiene permiso de acceso.

**Acceso y gestión**

- **FR-019**: Los usuarios DEBEN poder descargar cualquier documento al que tengan acceso, recibiendo el
  archivo con su nombre original.
- **FR-020**: El sistema DEBE ofrecer vista previa en el navegador para PDF e imágenes (JPEG, PNG).
- **FR-021**: Quien subió un documento DEBE poder editar su título, descripción, categoría y etiquetas.
- **FR-022**: Quien subió un documento DEBE poder sustituir su archivo por una nueva versión, sujeta a las
  mismas validaciones que una subida; la versión anterior NO se conserva.
- **FR-023**: Quien subió un documento DEBE poder eliminarlo; el Project Manager de un proyecto DEBE poder
  eliminar cualquier documento de su proyecto.
- **FR-024**: Toda eliminación DEBE requerir confirmación explícita y ser permanente, retirando el documento
  de todas las vistas, tareas y comparticiones.

**Permisos por rol**

- **FR-025**: Employee: DEBE poder subir documentos personales y documentos para proyectos de los que es
  miembro, y acceder a los documentos que subió, a los de sus proyectos y a los compartidos con él.
- **FR-026**: Team Lead: además de lo anterior, DEBE poder ver y gestionar (editar metadatos y eliminar) los
  documentos subidos por los miembros de su equipo.
- **FR-027**: Project Manager: además de lo anterior, DEBE poder subir y gestionar todos los documentos
  asociados a los proyectos que dirige.
- **FR-028**: Administrator: DEBE tener acceso completo a todos los documentos con fines de auditoría y
  cumplimiento.
- **FR-029**: El sistema DEBE comprobar los permisos en cada acceso a un documento (listado, vista previa,
  descarga, edición, sustitución, eliminación, compartición), incluidos los accesos por enlace directo, y
  denegar el acceso sin revelar información del documento.

**Compartición**

- **FR-030**: El propietario de un documento DEBE poder compartirlo con usuarios concretos o con un equipo.
- **FR-031**: Los destinatarios DEBEN recibir una notificación en la aplicación al compartirse un documento
  con ellos.
- **FR-032**: Los usuarios DEBEN disponer de una sección "Compartidos conmigo" con los documentos compartidos
  con ellos directamente o a través de su equipo.
- **FR-033**: Los destinatarios de un documento compartido DEBEN tener acceso de solo lectura (ver, previsualizar
  y descargar).

**Integración con funcionalidades existentes**

- **FR-034**: El detalle de una tarea DEBE mostrar los documentos vinculados y permitir adjuntar documentos
  existentes accesibles para el usuario o subir uno nuevo.
- **FR-035**: Los documentos subidos o adjuntados desde una tarea DEBEN asociarse automáticamente al proyecto
  de la tarea.
- **FR-036**: El panel principal DEBE incluir un widget "Documentos recientes" con los 5 últimos documentos
  subidos por el usuario.
- **FR-037**: Las tarjetas de resumen del panel principal DEBEN incluir el número de documentos del usuario.
- **FR-038**: Los miembros de un proyecto DEBEN recibir una notificación en la aplicación cuando se añade un
  documento nuevo al proyecto (excepto quien lo sube).

**Auditoría e informes**

- **FR-039**: El sistema DEBE registrar todas las subidas, descargas, eliminaciones y comparticiones de
  documentos con usuario, acción, documento y fecha/hora.
- **FR-040**: Los administradores DEBEN poder consultar informes de: tipos de documento más subidos, usuarios
  que más suben y patrones de acceso a documentos.
- **FR-041**: Los informes de auditoría DEBEN ser accesibles solo para el rol Administrator.

**Funcionamiento sin conexión**

- **FR-042**: Todas las capacidades de esta funcionalidad DEBEN funcionar en el entorno de formación local sin
  conexión a Internet ni servicios externos.

### Entidades clave _(incluir si la funcionalidad implica datos)_

- **Documento**: archivo de trabajo subido por un usuario. Atributos: título, descripción, categoría,
  etiquetas, nombre original del archivo, tipo de archivo, tamaño, fecha/hora de subida, usuario que lo subió
  y ubicación del archivo almacenado. Puede asociarse opcionalmente a un proyecto.
- **Etiqueta**: palabra clave libre asociada a uno o varios documentos para facilitar la búsqueda.
- **Compartición de documento**: relación que concede a un usuario o a un equipo acceso de solo lectura a un
  documento. Atributos: documento, destinatario (usuario o equipo), quién compartió y fecha/hora.
- **Vínculo documento-tarea**: relación entre un documento y una tarea existente; implica la asociación al
  proyecto de la tarea.
- **Registro de actividad de documentos**: evento auditable (subida, descarga, eliminación, compartición) con
  usuario, acción, documento y fecha/hora; se conserva aunque el documento se elimine.
- **Entidades existentes relacionadas**: Usuario (rol y departamento), Proyecto y sus miembros, Tarea y
  Notificación.

## Criterios de éxito _(obligatorio)_

### Resultados medibles

- **SC-001**: El 70 % de los usuarios activos del panel ha subido al menos un documento en los 3 meses
  posteriores al lanzamiento.
- **SC-002**: El tiempo medio para localizar un documento es inferior a 30 segundos.
- **SC-003**: El 90 % de los documentos subidos tiene una categoría correcta.
- **SC-004**: Cero incidentes de seguridad relacionados con el acceso a documentos; en las pruebas, el 100 % de
  los intentos de acceso no autorizado (incluidos enlaces directos) se deniegan.
- **SC-005**: Subir un documento requiere como máximo 3 clics desde la vista de documentos, además de rellenar
  los campos obligatorios.
- **SC-006**: La subida de un archivo de hasta 25 MB finaliza en menos de 30 segundos en condiciones de red
  habituales.
- **SC-007**: Las listas de documentos se cargan en menos de 2 segundos con hasta 500 documentos.
- **SC-008**: Las búsquedas devuelven resultados en menos de 2 segundos.
- **SC-009**: La vista previa de un documento se muestra en menos de 3 segundos.
- **SC-010**: El 100 % de las subidas, descargas, eliminaciones y comparticiones aparece en el registro de
  auditoría.

## Supuestos

- Se reutilizan los usuarios, roles (Employee, Team Lead, Project Manager, Administrator), proyectos, tareas y
  notificaciones existentes, así como la autenticación simulada actual.
- "Equipo" equivale al departamento del usuario: el equipo de un Team Lead son los usuarios de su departamento,
  y compartir con un equipo significa compartir con los usuarios de un departamento.
- El análisis de virus y malware se realiza mediante un componente sustituible; en el entorno de formación sin
  conexión puede ser una implementación simulada que aplique comprobaciones básicas, documentada como
  limitación conocida.
- Los documentos se almacenan en el almacenamiento local del entorno de formación; está prevista una migración
  futura a almacenamiento en la nube sin cambios funcionales.
- La mayoría de los documentos pesa menos de 10 MB y los usuarios conocen los conceptos básicos de gestión de
  archivos.
- Sustituir el archivo de un documento conserva sus metadatos, comparticiones y vínculos.
- Las métricas de adopción (SC-001 a SC-003) se miden tras el lanzamiento; en el entorno de formación se
  validan los criterios verificables mediante pruebas (SC-004 a SC-010).

## Fuera de alcance

- Edición colaborativa en tiempo real.
- Historial de versiones y restauración de versiones anteriores.
- Flujos documentales avanzados (aprobaciones, enrutamiento).
- Integración con sistemas externos (SharePoint, OneDrive).
- Aplicaciones móviles (la versión inicial es solo web).
- Plantillas o generación de documentos.
- Cuotas de almacenamiento y su gestión.
- Papelera o eliminación recuperable.
- Revocación selectiva de comparticiones.
