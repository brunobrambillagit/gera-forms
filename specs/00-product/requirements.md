# Gera Forms — Product Requirements

**Status:** Approved
**Lifecycle Phase:** 02 — Product Requirements
**Milestone:** MVP
**Source:** `specs/00-product/vision.md` — Approved
**Approved:** 2026-09-21
**Last reviewed:** 2026-09-21

---

# 1. Purpose

Este documento define los requisitos de producto de Gera Forms derivados de la visión aprobada.

Los requisitos describen qué comportamiento debe proporcionar el producto sin determinar todavía cómo deberá implementarse técnicamente.

Cada requisito posee un identificador estable `PR-*` que deberá utilizarse posteriormente para mantener trazabilidad con User Stories, Acceptance Criteria, Feature Specifications, Implementation Plans, Tasks, Tests y Validation.

---

# 2. Priority Model

Los requisitos utilizan las siguientes prioridades:

* **P0 — Mandatory / Blocker:** requisito obligatorio cuya ausencia impide considerar viable el producto o completar correctamente su flujo principal.
* **P1 — High / MVP:** requisito de alta prioridad esperado para completar el MVP.
* **P2 — Useful / Deferrable:** requisito relevante que puede diferirse sin invalidar el flujo principal.
* **P3 — Future:** requisito identificado para una evolución posterior del producto.

La prioridad representa importancia de producto y no orden de implementación.

---

# 3. Requirement Status

Los requisitos podrán encontrarse en los siguientes estados:

* `DRAFT`
* `APPROVED`
* `DEFERRED`
* `SUPERSEDED`

Todos los requisitos de este documento permanecen en estado `DRAFT` hasta la aprobación explícita de esta línea base.

---

# 4. Requirement Domains

Los requisitos se organizan en los siguientes dominios:

* `AUTH` — Usuarios, roles y autenticación
* `FORM` — Creación y gestión de formularios
* `VERSION` — Publicación y versionado
* `ASSIGN` — Habilitación y descarga
* `SURVEY` — Realización y edición de encuestas
* `OFFLINE` — Operación offline
* `SYNC` — Sincronización
* `LOCATION` — Ubicación
* `FILE` — Archivos y adjuntos
* `AUDIT` — Auditoría
* `RESULT` — Resultados
* `PLATFORM` — Plataforma y restricciones generales
* `FUTURE` — Capacidades posteriores al MVP

---

# 5. AUTH — Users, Roles and Authentication

## PR-AUTH-001 — Supported Roles

**Priority:** P0
**Status:** DRAFT

**Requirement:**
Gera Forms deberá soportar exactamente dos roles funcionales iniciales:

* Administrador;
* Encuestador.

**Rationale:**
La visión aprobada define estos dos perfiles como los únicos roles necesarios para el alcance inicial.

**Dependencies:**
None.

**Notes:**
La definición detallada de permisos se realizará posteriormente.

---

## PR-AUTH-002 — Administrator User Management

**Priority:** P0
**Status:** DRAFT

**Requirement:**
Un usuario Administrador deberá poder crear y administrar usuarios de Gera Forms.

**Rationale:**
Los usuarios deberán ser gestionados internamente por la organización.

**Dependencies:**
PR-AUTH-001.

**Notes:**
El ciclo de vida detallado de usuarios deberá especificarse posteriormente.

---

## PR-AUTH-003 — No Self-Registration

**Priority:** P0
**Status:** DRAFT

**Requirement:**
Gera Forms no deberá permitir el auto-registro de usuarios dentro del alcance inicial.

Los usuarios deberán ser creados por un Administrador.

**Rationale:**
El acceso a la plataforma está destinado exclusivamente a usuarios autorizados por la organización.

**Dependencies:**
PR-AUTH-002.

---

## PR-AUTH-004 — Authenticated Survey Access

**Priority:** P0
**Status:** DRAFT

**Requirement:**
Solamente usuarios Encuestadores autenticados y previamente creados en Gera Forms podrán acceder a formularios habilitados para realizar encuestas.

**Rationale:**
Los formularios de relevamiento no serán públicos ni anónimos.

**Dependencies:**
PR-AUTH-001, PR-AUTH-002.

---

## PR-AUTH-005 — Initial Online Authentication

**Priority:** P0
**Status:** DRAFT

**Requirement:**
El primer inicio de sesión de un usuario en un dispositivo deberá realizarse con conectividad suficiente para validar su identidad contra el sistema central.

**Rationale:**
El acceso offline solo podrá habilitarse a partir de una autenticación online válida previa.

**Dependencies:**
PR-AUTH-004.

---

## PR-AUTH-006 — Offline Access Window

**Priority:** P0
**Status:** DRAFT

**Requirement:**
Después de una autenticación online válida, el usuario podrá acceder offline desde ese dispositivo durante un máximo de 24 horas desde dicha autenticación.

**Rationale:**
Los Encuestadores necesitan operar temporalmente sin conectividad sin mantener sesiones offline indefinidas.

**Dependencies:**
PR-AUTH-005.

**Notes:**
La estrategia técnica de autenticación offline no se define en este documento.

---

## PR-AUTH-007 — Offline Access Expiration

**Priority:** P0
**Status:** DRAFT

**Requirement:**
Una vez vencido el período autorizado de acceso offline, el usuario deberá autenticarse nuevamente online antes de continuar utilizando Gera Forms.

**Rationale:**
La autorización offline posee una vigencia limitada.

**Dependencies:**
PR-AUTH-006.

---

## PR-AUTH-008 — Preservation After Authentication Expiration

**Priority:** P0
**Status:** DRAFT

**Requirement:**
El vencimiento de la autorización offline no deberá eliminar ni invalidar información de trabajo almacenada localmente, incluyendo:

* formularios descargados;
* encuestas incompletas;
* encuestas pendientes de sincronización;
* archivos asociados;
* historial de modificaciones.

Una vez autenticado nuevamente online, el usuario deberá poder continuar desde el estado previamente almacenado.

**Rationale:**
El vencimiento de una sesión no debe provocar pérdida de relevamientos.

**Dependencies:**
PR-AUTH-006, PR-AUTH-007.

---

# 6. FORM — Form Creation and Management

## PR-FORM-001 — Administrator Form Creation

**Priority:** P0
**Status:** DRAFT

**Requirement:**
Solamente usuarios Administradores podrán crear formularios.

**Rationale:**
La creación y administración de formularios corresponde al rol Administrador.

**Dependencies:**
PR-AUTH-001.

---

## PR-FORM-002 — Form Question Configuration

**Priority:** P0
**Status:** DRAFT

**Requirement:**
El Administrador deberá poder agregar, configurar y organizar preguntas dentro de un formulario.

**Rationale:**
La creación flexible de formularios constituye una capacidad central de Gera Forms.

**Dependencies:**
PR-FORM-001.

---

## PR-FORM-003 — Basic Question Types

**Priority:** P0
**Status:** DRAFT

**Requirement:**
Gera Forms deberá soportar en el MVP tipos básicos de preguntas suficientes para demostrar creación y realización de formularios, incluyendo como mínimo:

* texto simple;
* texto largo;
* selección de una opción;
* selección de múltiples opciones.

**Rationale:**
Estos tipos permiten demostrar el flujo principal de creación y realización de formularios.

**Dependencies:**
PR-FORM-002.

**Notes:**
El catálogo completo será refinado durante User Stories y MVP Scope.

---

## PR-FORM-004 — Extended Data Types

**Priority:** P1
**Status:** DRAFT

**Requirement:**
Gera Forms deberá permitir recopilar mediante formularios información adicional como:

* teléfonos;
* correos electrónicos;
* observaciones;
* fotografías;
* documentos;
* archivos adjuntos;
* ubicación o dirección.

**Rationale:**
La plataforma debe permitir realizar relevamientos de campo con información equivalente a los tipos de datos identificados en la visión del producto.

**Dependencies:**
PR-FORM-002.

---

## PR-FORM-005 — Form Availability Control

**Priority:** P0
**Status:** DRAFT

**Requirement:**
La creación de un formulario no deberá hacerlo automáticamente utilizable por Encuestadores.

El formulario deberá atravesar las acciones de publicación y habilitación correspondientes antes de estar disponible para ellos.

**Rationale:**
Creación, publicación, asignación y descarga representan estados funcionales diferentes.

**Dependencies:**
PR-FORM-001.

---

# 7. VERSION — Form Publication and Versioning

## PR-VERSION-001 — Form Publication

**Priority:** P0
**Status:** DRAFT

**Requirement:**
El Administrador deberá poder publicar un formulario para generar una versión utilizable.

**Rationale:**
Los formularios requieren una instancia publicada estable antes de ser utilizados en relevamientos.

**Dependencies:**
PR-FORM-001, PR-FORM-002.

---

## PR-VERSION-002 — Automatic Version Generation

**Priority:** P0
**Status:** DRAFT

**Requirement:**
Cada nueva publicación de un formulario deberá generar automáticamente una nueva versión identificable del formulario.

**Rationale:**
Los relevamientos deben conservar una relación inequívoca con la estructura exacta utilizada al momento de su realización.

**Dependencies:**
PR-VERSION-001.

---

## PR-VERSION-003 — Published Version Immutability

**Priority:** P0
**Status:** DRAFT

**Requirement:**
Una versión publicada utilizada para recopilar encuestas deberá conservar su estructura histórica y no deberá ser modificada retroactivamente por publicaciones posteriores.

**Rationale:**
Los resultados históricos deben continuar interpretándose según la estructura con la que fueron recopilados.

**Dependencies:**
PR-VERSION-002.

---

## PR-VERSION-004 — Survey-to-Version Association

**Priority:** P0
**Status:** DRAFT

**Requirement:**
Toda encuesta deberá quedar asociada a la versión exacta del formulario utilizada para realizarla.

**Rationale:**
Es necesario preservar la integridad histórica de las respuestas.

**Dependencies:**
PR-VERSION-002, PR-VERSION-003.

---

## PR-VERSION-005 — Historical Version Results

**Priority:** P0
**Status:** DRAFT

**Requirement:**
Los resultados correspondientes a una versión anterior deberán continuar visualizándose e interpretándose utilizando la estructura de dicha versión aunque existan versiones posteriores.

**Rationale:**
Una nueva publicación no debe alterar el significado de información histórica.

**Dependencies:**
PR-VERSION-003, PR-VERSION-004.

---

## PR-VERSION-006 — New Version Notification

**Priority:** P1
**Status:** DRAFT

**Requirement:**
Cuando exista una nueva versión de un formulario descargado, Gera Forms deberá informar al Encuestador que existe una actualización disponible.

**Rationale:**
El Encuestador debe conocer la existencia de una versión posterior sin perder trabajo pendiente de la versión actual.

**Dependencies:**
PR-VERSION-002, PR-ASSIGN-004.

---

## PR-VERSION-007 — Version Update Blocking

**Priority:** P0
**Status:** DRAFT

**Requirement:**
El Encuestador no podrá reemplazar la versión descargada de un formulario mientras existan, para esa versión:

* encuestas incompletas; o
* encuestas completadas pendientes de sincronización.

**Rationale:**
La versión utilizada debe permanecer disponible mientras existan relevamientos locales que dependan de ella.

**Dependencies:**
PR-VERSION-004, PR-SURVEY-003, PR-SYNC-001.

---

## PR-VERSION-008 — Version Update Eligibility

**Priority:** P0
**Status:** DRAFT

**Requirement:**
La actualización a una versión posterior podrá realizarse cuando todas las encuestas correspondientes a la versión actualmente descargada hayan sido completadas y sincronizadas correctamente.

**Rationale:**
La actualización debe realizarse sin dejar relevamientos locales dependientes de la versión anterior.

**Dependencies:**
PR-VERSION-007.

---

## PR-VERSION-009 — Single Local Form Version

**Priority:** P1
**Status:** DRAFT

**Requirement:**
Después de una actualización exitosa, el dispositivo deberá conservar para uso operativo únicamente la última versión descargada del formulario.

**Rationale:**
El Encuestador no necesita mantener múltiples versiones operativas de un mismo formulario.

**Dependencies:**
PR-VERSION-008.

---

# 8. ASSIGN — Form Assignment and Download

## PR-ASSIGN-001 — Form Assignment

**Priority:** P0
**Status:** DRAFT

**Requirement:**
El Administrador deberá poder habilitar un formulario para Encuestadores específicos.

**Rationale:**
No todos los formularios deberán estar disponibles para todos los Encuestadores.

**Dependencies:**
PR-AUTH-001, PR-VERSION-001.

---

## PR-ASSIGN-002 — Assigned Forms Visibility

**Priority:** P0
**Status:** DRAFT

**Requirement:**
Un Encuestador deberá visualizar únicamente los formularios que tenga habilitados.

**Rationale:**
La disponibilidad de formularios debe respetar las asignaciones realizadas por los Administradores.

**Dependencies:**
PR-ASSIGN-001.

---

## PR-ASSIGN-003 — Explicit Form Download

**Priority:** P0
**Status:** DRAFT

**Requirement:**
El Encuestador deberá descargar explícitamente un formulario antes de poder utilizarlo.

**Rationale:**
La descarga constituye el mecanismo funcional mediante el cual un formulario pasa a estar disponible localmente.

**Dependencies:**
PR-ASSIGN-002.

---

## PR-ASSIGN-004 — Download Required for Online and Offline Use

**Priority:** P0
**Status:** DRAFT

**Requirement:**
La descarga previa del formulario será obligatoria tanto para su utilización online como offline.

**Rationale:**
Gera Forms utilizará un flujo consistente en el que los formularios operativos son formularios previamente descargados.

**Dependencies:**
PR-ASSIGN-003.

---

## PR-ASSIGN-005 — Offline Availability

**Priority:** P0
**Status:** DRAFT

**Requirement:**
Un formulario correctamente descargado deberá permanecer disponible para su utilización cuando el dispositivo se encuentre sin conexión, mientras el usuario posea autorización offline válida.

**Rationale:**
El trabajo en lugares sin conectividad constituye uno de los problemas centrales que Gera Forms debe resolver.

**Dependencies:**
PR-ASSIGN-004, PR-AUTH-006.

---

# 9. SURVEY — Survey Execution and Editing

## PR-SURVEY-001 — Start Survey

**Priority:** P0
**Status:** DRAFT

**Requirement:**
Un Encuestador deberá poder iniciar una encuesta utilizando un formulario descargado que tenga habilitado.

**Rationale:**
Constituye el inicio del flujo principal de relevamiento.

**Dependencies:**
PR-ASSIGN-004.

---

## PR-SURVEY-002 — Partial Survey Save

**Priority:** P0
**Status:** DRAFT

**Requirement:**
El Encuestador deberá poder guardar una encuesta incompleta y continuarla posteriormente.

**Rationale:**
Los relevamientos de campo pueden interrumpirse y no deben requerir completarse en una única sesión.

**Dependencies:**
PR-SURVEY-001.

---

## PR-SURVEY-003 — Local Survey Persistence

**Priority:** P0
**Status:** DRAFT

**Requirement:**
Las encuestas iniciadas deberán conservarse localmente hasta que corresponda su sincronización o finalización del flujo definido.

**Rationale:**
El trabajo del Encuestador no debe depender de conectividad continua.

**Dependencies:**
PR-SURVEY-001.

---

## PR-SURVEY-004 — Pre-Synchronization Editing

**Priority:** P0
**Status:** DRAFT

**Requirement:**
Una encuesta podrá modificarse mientras todavía no haya sido sincronizada exitosamente.

**Rationale:**
El Encuestador puede necesitar corregir información antes de enviarla definitivamente.

**Dependencies:**
PR-SURVEY-002.

---

## PR-SURVEY-005 — Post-Synchronization Lock

**Priority:** P0
**Status:** DRAFT

**Requirement:**
Una encuesta sincronizada exitosamente deberá quedar bloqueada para edición por parte del Encuestador.

**Rationale:**
La sincronización exitosa representa el cierre de la edición local de la encuesta.

**Dependencies:**
PR-SURVEY-004, PR-SYNC-005.

---

# 10. OFFLINE — Offline Operation

## PR-OFFLINE-001 — Core Offline Operation

**Priority:** P0
**Status:** DRAFT

**Requirement:**
Gera Forms deberá permitir realizar el flujo operativo de relevamiento sin conexión utilizando formularios previamente descargados.

**Rationale:**
El funcionamiento offline constituye una capacidad central del producto.

**Dependencies:**
PR-AUTH-006, PR-ASSIGN-005.

---

## PR-OFFLINE-002 — Offline Survey Creation

**Priority:** P0
**Status:** DRAFT

**Requirement:**
El Encuestador deberá poder iniciar y completar nuevas encuestas mientras se encuentre offline utilizando formularios descargados.

**Rationale:**
Los relevamientos deben poder realizarse en lugares sin conectividad.

**Dependencies:**
PR-OFFLINE-001.

---

## PR-OFFLINE-003 — Offline Survey Continuation

**Priority:** P0
**Status:** DRAFT

**Requirement:**
El Encuestador deberá poder continuar offline encuestas previamente iniciadas y almacenadas localmente.

**Rationale:**
La pérdida de conectividad no deberá interrumpir permanentemente un relevamiento.

**Dependencies:**
PR-SURVEY-002, PR-OFFLINE-001.

---

## PR-OFFLINE-004 — Local Data Preservation

**Priority:** P0
**Status:** DRAFT

**Requirement:**
La ausencia de conectividad, el cierre de la aplicación o el vencimiento de la autorización offline no deberán provocar pérdida de encuestas o archivos almacenados localmente.

**Rationale:**
La confiabilidad de los datos recopilados es esencial para el trabajo de campo.

**Dependencies:**
PR-AUTH-008, PR-SURVEY-003, PR-FILE-002.

---

# 11. SYNC — Synchronization

## PR-SYNC-001 — Manual Synchronization

**Priority:** P0
**Status:** DRAFT

**Requirement:**
La sincronización de encuestas deberá iniciarse manualmente por el Encuestador.

Gera Forms no deberá sincronizar automáticamente las encuestas pendientes dentro del alcance inicial.

**Rationale:**
El Encuestador deberá controlar explícitamente cuándo enviar los relevamientos almacenados localmente.

**Dependencies:**
PR-SURVEY-003.

---

## PR-SYNC-003 — Global Synchronization

**Priority:** P1
**Status:** DRAFT

**Requirement:**
El Encuestador deberá disponer de una acción para iniciar la sincronización de todas las encuestas pendientes elegibles.

**Rationale:**
Permite reducir el esfuerzo cuando existen relevamientos pendientes correspondientes a múltiples formularios.

**Dependencies:**
PR-SYNC-001.

---

## PR-SYNC-004 — Synchronization Status

**Priority:** P0
**Status:** DRAFT

**Requirement:**
Cada encuesta deberá exponer claramente uno de los siguientes estados de sincronización:

* `Pendiente de sincronización`;
* `Sincronizando`;
* `Sincronizado`;
* `Error de sincronización`.

**Rationale:**
El Encuestador debe poder determinar si la información se encuentra solamente en el dispositivo o ya fue recibida correctamente por el sistema central.

**Dependencies:**
PR-SYNC-001.

---

## PR-SYNC-005 — Successful Synchronization

**Priority:** P0
**Status:** DRAFT

**Requirement:**
Una encuesta solo deberá adoptar el estado `Sincronizado` cuando el proceso de sincronización haya finalizado exitosamente.

**Rationale:**
El sistema no debe presentar como recibida información cuya persistencia central no haya sido confirmada.

**Dependencies:**
PR-SYNC-004.

---

## PR-SYNC-006 — Synchronization Error Preservation

**Priority:** P0
**Status:** DRAFT

**Requirement:**
Cuando una sincronización falle, la encuesta deberá adoptar el estado `Error de sincronización` y conservar localmente toda la información necesaria para permitir un nuevo intento posterior.

**Rationale:**
Los errores de conectividad o transmisión no deberán causar pérdida de información.

**Dependencies:**
PR-SYNC-004.

---

## PR-SYNC-007 — Synchronization Retry

**Priority:** P0
**Status:** DRAFT

**Requirement:**
El Encuestador deberá poder volver a intentar manualmente la sincronización de una encuesta que se encuentre en estado `Error de sincronización`.

**Rationale:**
El trabajo debe poder recuperarse de errores transitorios.

**Dependencies:**
PR-SYNC-006.

---

# 12. LOCATION — Location Capture

## PR-LOCATION-001 — Location Requirement Configuration

**Priority:** P0
**Status:** DRAFT

**Requirement:**
El Administrador deberá poder configurar cada formulario con una de las siguientes modalidades:

* `Ubicación obligatoria`;
* `Ubicación opcional`;
* `Sin ubicación`.

**Rationale:**
No todos los relevamientos requieren el mismo tratamiento de ubicación.

**Dependencies:**
PR-FORM-001.

---

## PR-LOCATION-002 — Device Location

**Priority:** P1
**Status:** DRAFT

**Requirement:**
Cuando corresponda registrar ubicación, Gera Forms deberá permitir obtenerla utilizando los servicios de ubicación disponibles en el dispositivo.

**Rationale:**
Permite registrar la posición desde la que se realiza un relevamiento.

**Dependencies:**
PR-LOCATION-001.

---

## PR-LOCATION-003 — Manual Address

**Priority:** P1
**Status:** DRAFT

**Requirement:**
Cuando corresponda registrar ubicación, el Encuestador deberá poder ingresar manualmente una dirección.

**Rationale:**
La ubicación automática puede no encontrarse disponible o puede requerirse una referencia textual.

**Dependencies:**
PR-LOCATION-001.

---

## PR-LOCATION-004 — Map Location Selection

**Priority:** P1
**Status:** DRAFT

**Requirement:**
Cuando corresponda registrar ubicación, el Encuestador deberá poder seleccionar manualmente una ubicación mediante un mapa cuando dicha capacidad se encuentre disponible.

**Rationale:**
Permite identificar visualmente una ubicación cuando no se utiliza la posición automática del dispositivo.

**Dependencies:**
PR-LOCATION-001.

**Notes:**
El comportamiento online/offline del mapa se determinará posteriormente.

---

## PR-LOCATION-005 — Required Location Validation

**Priority:** P0
**Status:** DRAFT

**Requirement:**
Cuando un formulario esté configurado con `Ubicación obligatoria`, la encuesta no podrá considerarse completada hasta satisfacer una modalidad válida de ubicación.

**Rationale:**
La obligatoriedad configurada por el Administrador debe ser aplicada durante el relevamiento.

**Dependencies:**
PR-LOCATION-001.

**Notes:**
Las modalidades que satisfacen esta regla serán refinadas antes de implementar la funcionalidad.

---

# 13. FILE — Files and Attachments

## PR-FILE-001 — Survey Attachments

**Priority:** P1
**Status:** DRAFT

**Requirement:**
Los formularios deberán poder permitir la incorporación de archivos, incluyendo fotografías y documentos, cuando el tipo de pregunta correspondiente lo permita.

**Rationale:**
Los relevamientos pueden requerir evidencia o documentación complementaria.

**Dependencies:**
PR-FORM-004.

---

## PR-FILE-002 — Offline Attachment Storage

**Priority:** P1
**Status:** DRAFT

**Requirement:**
Los archivos incorporados durante una encuesta deberán poder almacenarse localmente cuando el dispositivo se encuentre offline.

**Rationale:**
La captura de archivos debe formar parte del flujo de relevamiento offline.

**Dependencies:**
PR-FILE-001, PR-OFFLINE-001.

---

## PR-FILE-003 — Attachment Synchronization

**Priority:** P1
**Status:** DRAFT

**Requirement:**
Los archivos asociados a una encuesta deberán poder enviarse al sistema central como parte del proceso de sincronización correspondiente.

**Rationale:**
La encuesta sincronizada debe conservar los archivos recopilados durante el relevamiento.

**Dependencies:**
PR-FILE-002, PR-SYNC-001.

---

## PR-FILE-004 — Local Retention After Synchronization

**Priority:** P1
**Status:** DRAFT

**Requirement:**
La sincronización exitosa de un archivo no deberá eliminar automáticamente su copia local.

**Rationale:**
La política aprobada establece conservación local hasta decisión explícita del Encuestador.

**Dependencies:**
PR-FILE-003.

---

## PR-FILE-005 — Manual Local File Deletion

**Priority:** P1
**Status:** DRAFT

**Requirement:**
El Encuestador deberá poder eliminar manualmente del dispositivo archivos locales que ya no desee conservar.

**Rationale:**
El control de eliminación local corresponde al Encuestador.

**Dependencies:**
PR-FILE-004.

---

## PR-FILE-006 — Server Copy Preservation

**Priority:** P0
**Status:** DRAFT

**Requirement:**
La eliminación de una copia local de un archivo previamente sincronizado no deberá eliminar la copia almacenada correctamente en el sistema central.

**Rationale:**
La limpieza de almacenamiento local no debe provocar pérdida de evidencia ya sincronizada.

**Dependencies:**
PR-FILE-003, PR-FILE-005.

---

# 14. AUDIT — Survey Modification Audit

## PR-AUDIT-001 — Detailed Modification Audit

**Priority:** P1
**Status:** DRAFT

**Requirement:**
Toda modificación realizada sobre una encuesta antes de su sincronización deberá generar información de auditoría detallada.

**Rationale:**
Las modificaciones deben ser trazables.

**Dependencies:**
PR-SURVEY-004.

---

## PR-AUDIT-002 — Audit Information

**Priority:** P1
**Status:** DRAFT

**Requirement:**
Cada registro de modificación deberá identificar como mínimo:

* pregunta modificada;
* valor anterior;
* valor nuevo;
* usuario que realizó la modificación;
* fecha y hora de la modificación.

**Rationale:**
Estos datos permiten reconstruir qué información fue modificada, por quién y cuándo.

**Dependencies:**
PR-AUDIT-001.

---

## PR-AUDIT-003 — Administrator Audit Access

**Priority:** P1
**Status:** DRAFT

**Requirement:**
El Administrador deberá poder consultar la auditoría asociada a las encuestas.

**Rationale:**
El rol responsable de gestionar la plataforma necesita capacidad de revisión.

**Dependencies:**
PR-AUDIT-001.

---

## PR-AUDIT-004 — Surveyor Audit Access

**Priority:** P2
**Status:** DRAFT

**Requirement:**
El Encuestador deberá poder consultar la información de auditoría correspondiente a sus propias encuestas cuando dicha información se encuentre disponible en su dispositivo o dentro de su ámbito de acceso.

**Rationale:**
La visión aprobada contempla que el propio Encuestador pueda revisar las modificaciones realizadas.

**Dependencies:**
PR-AUDIT-001.

---

# 15. RESULT — Results

## PR-RESULT-001 — Administrator Results Access

**Priority:** P0
**Status:** DRAFT

**Requirement:**
El Administrador deberá poder consultar las encuestas correctamente sincronizadas.

**Rationale:**
La consulta de los relevamientos recopilados forma parte del flujo principal del producto.

**Dependencies:**
PR-SYNC-005.

---

## PR-RESULT-002 — Results by Form

**Priority:** P0
**Status:** DRAFT

**Requirement:**
El Administrador deberá poder identificar los resultados correspondientes a cada formulario.

**Rationale:**
Los resultados necesitan conservar su contexto funcional.

**Dependencies:**
PR-RESULT-001.

---

## PR-RESULT-003 — Results by Form Version

**Priority:** P0
**Status:** DRAFT

**Requirement:**
El Administrador deberá poder identificar qué versión del formulario fue utilizada para cada encuesta y consultar sus respuestas conforme a dicha versión.

**Rationale:**
La interpretación de resultados depende de la estructura exacta del formulario utilizado.

**Dependencies:**
PR-VERSION-004, PR-RESULT-001.

---

# 16. PLATFORM — Platform and Operational Constraints

## PR-PLATFORM-001 — Progressive Web Application

**Priority:** P0
**Status:** DRAFT

**Requirement:**
Gera Forms deberá ser provisto como una Progressive Web App.

**Rationale:**
La plataforma debe poder utilizarse desde diferentes dispositivos sin requerir aplicaciones móviles nativas específicas.

**Dependencies:**
None.

---

## PR-PLATFORM-002 — Smartphone Support

**Priority:** P0
**Status:** DRAFT

**Requirement:**
Gera Forms deberá poder utilizarse desde smartphones Android y iPhone compatibles con las capacidades requeridas por la aplicación.

**Rationale:**
Los Encuestadores realizarán principalmente relevamientos desde dispositivos móviles.

**Dependencies:**
PR-PLATFORM-001.

---

## PR-PLATFORM-003 — Computer Support

**Priority:** P1
**Status:** DRAFT

**Requirement:**
Gera Forms deberá poder utilizarse desde computadoras compatibles.

**Rationale:**
La visión contempla acceso desde dispositivos móviles y computadoras.

**Dependencies:**
PR-PLATFORM-001.

---

## PR-PLATFORM-004 — Central Server Deployment

**Priority:** P0
**Status:** DRAFT

**Requirement:**
Los servicios centralizados de Gera Forms deberán poder desplegarse en infraestructura de tipo VPS.

**Rationale:**
La VPS constituye una restricción de despliegue definida para el producto.

**Dependencies:**
None.

**Notes:**
La tecnología específica de despliegue será determinada durante Architecture.

---

## PR-PLATFORM-005 — Single Organization

**Priority:** P0
**Status:** DRAFT

**Requirement:**
El alcance inicial de Gera Forms deberá soportar una única organización.

**Rationale:**
No existe actualmente un requisito de operación multi-organización.

**Dependencies:**
None.

---

## PR-PLATFORM-006 — No Required External Integrations

**Priority:** P1
**Status:** DRAFT

**Requirement:**
El MVP no dependerá funcionalmente de integraciones con sistemas externos de la organización.

**Rationale:**
No se identificaron integraciones externas necesarias para resolver el flujo principal.

**Dependencies:**
None.

**Notes:**
Servicios técnicos que eventualmente sean necesarios para implementar capacidades internas deberán evaluarse durante Architecture y no se consideran automáticamente integraciones de negocio.

---

# 17. FUTURE — Post-MVP Product Direction

## PR-FUTURE-001 — CSV Export

**Priority:** P3
**Status:** DRAFT

**Requirement:**
Gera Forms podrá incorporar exportación de resultados en formato CSV.

**Rationale:**
Permitiría utilizar los resultados recopilados en herramientas externas de análisis.

**Dependencies:**
PR-RESULT-001.

---

## PR-FUTURE-002 — XLSX Export

**Priority:** P3
**Status:** DRAFT

**Requirement:**
Gera Forms podrá incorporar exportación de resultados en formato XLSX.

**Rationale:**
Facilitaría el análisis de información mediante herramientas de hojas de cálculo.

**Dependencies:**
PR-RESULT-001.

---

## PR-FUTURE-003 — Results Statistics

**Priority:** P3
**Status:** DRAFT

**Requirement:**
Gera Forms podrá incorporar un apartado de estadísticas construido a partir de los resultados recopilados.

**Rationale:**
La plataforma podrá evolucionar desde la recopilación hacia la explotación de la información.

**Dependencies:**
PR-RESULT-001.

---

## PR-FUTURE-004 — Results Visualization

**Priority:** P3
**Status:** DRAFT

**Requirement:**
Gera Forms podrá incorporar visualizaciones y gráficos de los resultados recopilados.

**Rationale:**
Permitirá interpretar los relevamientos directamente desde la plataforma.

**Dependencies:**
PR-FUTURE-003.

---

# 18. Explicit Initial Scope Exclusions

Los siguientes elementos no forman parte del alcance inicial aprobado:

* formularios públicos anónimos;
* auto-registro de usuarios;
* múltiples organizaciones independientes;
* arquitectura funcional multi-tenant;
* aplicaciones móviles nativas específicas para Android;
* aplicaciones móviles nativas específicas para iOS;
* sincronización automática de encuestas;
* integraciones de negocio obligatorias con sistemas externos.

Estas exclusiones no impiden su reconsideración futura mediante el proceso formal de cambio.

---

# 19. Requirement Summary

La línea base propuesta contiene los siguientes requisitos:

| Domain    | Requirements |
| --------- | -----------: |
| AUTH      |            8 |
| FORM      |            5 |
| VERSION   |            9 |
| ASSIGN    |            5 |
| SURVEY    |            5 |
| OFFLINE   |            4 |
| SYNC      |            6 |
| LOCATION  |            5 |
| FILE      |            6 |
| AUDIT     |            4 |
| RESULT    |            3 |
| PLATFORM  |            6 |
| FUTURE    |            4 |
| **TOTAL** |       **71** |

Estos requisitos constituyen la primera descomposición formal de la visión aprobada.

---

# 20. Traceability Baseline

La trazabilidad inicial será:

`Product Vision → PR-* → User Stories → Acceptance Criteria → Feature Specifications → Plans → Tasks → Code → Tests → Validation`

Los identificadores `PR-*` definidos en este documento deberán conservarse de forma estable.

Si un requisito deja de ser válido, deberá marcarse según el estado correspondiente en lugar de reutilizar su identificador para otro significado.

---

# 21. Pending Requirement Clarifications

Antes de considerar esta línea base completamente aprobada, deberán revisarse particularmente aquellos requisitos donde el comportamiento detallado todavía deba ser refinado durante las fases posteriores.

Actualmente no se introduce deliberadamente una decisión técnica sobre:

* mecanismo de autenticación;
* almacenamiento local;
* base de datos;
* almacenamiento central de archivos;
* estrategia de sincronización técnica;
* detección de conectividad;
* resolución técnica de errores;
* framework frontend;
* framework backend;
* servicios de mapas;
* geocodificación;
* funcionamiento técnico de GPS;
* infraestructura concreta dentro de la VPS;
* utilización definitiva de Docker.

Estas cuestiones pertenecen a fases posteriores salvo que revelen una nueva decisión de producto.

---

# 22. Approval Status

**Status:** Approved
**Approved:** 2026-09-21

Este documento constituye la primera línea base formal de
Product Requirements de Gera Forms.

Los requisitos PR-* definidos en este documento constituyen
identificadores estables para la trazabilidad posterior.

La aprobación de esta línea base no autoriza implementación
ni selección de arquitectura.