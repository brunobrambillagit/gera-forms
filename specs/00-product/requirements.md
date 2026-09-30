# Gera Forms — Product Requirements

**Status:** Approved  
**Revision:** 2  
**Lifecycle Phase:** 02 — Product Requirements  
**Milestone:** MVP  
**Source:** `specs/00-product/vision.md` — Revision 2 approved 
**Previous approved baseline:** 2026-09-21  
**Last reviewed:** 2026-09-30 

---

# 1. Purpose

Este documento define los requisitos de producto de Gera Forms derivados de Product Vision.

Los requisitos describen qué comportamiento debe proporcionar el producto sin determinar cómo deberá implementarse técnicamente.

Cada requisito posee un identificador estable `PR-*` que deberá utilizarse posteriormente para mantener trazabilidad con User Stories, Acceptance Criteria, Feature Specifications, Implementation Plans, Tasks, Tests y Validation.

Revision 2 conserva los identificadores existentes de la baseline anterior y agrega nuevos identificadores únicamente cuando las decisiones CL-014 a CL-025 incorporan comportamiento adicional.

`PR-SYNC-002` permanece retirado y su identificador no podrá reutilizarse.

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

Los requisitos podrán encontrarse en:

* `DRAFT`
* `APPROVED`
* `DEFERRED`
* `SUPERSEDED`
* `RETIRED`

Los requisitos incluidos en Revision 2 permanecen en `DRAFT` hasta la aprobación explícita de esta nueva línea base.

La baseline aprobada el 2026-09-21 permanece como antecedente histórico.

---

# 4. Requirement Domains

Los requisitos se organizan en:

* `AUTH` — Usuarios, roles, permisos y autenticación
* `FORM` — Creación y gestión de formularios
* `VERSION` — Publicación y versionado
* `ASSIGN` — Habilitación, deshabilitación y descarga
* `SURVEY` — Realización y edición de encuestas
* `OFFLINE` — Operación offline
* `SYNC` — Finalización, envío y sincronización
* `LOCATION` — Ubicación
* `FILE` — Archivos y adjuntos
* `AUDIT` — Auditoría
* `RESULT` — Resultados
* `PLATFORM` — Plataforma y restricciones generales
* `FUTURE` — Capacidades posteriores al MVP

---

# 5. AUTH — Users, Roles, Permissions and Authentication

## PR-AUTH-001 — Supported Roles

**Priority:** P0  
**Status:** DRAFT

**Requirement:**  
Gera Forms deberá soportar exactamente dos roles funcionales iniciales:

* Administrador;
* Encuestador.

**Rationale:**  
Estos dos perfiles representan los actores funcionales definidos para el alcance inicial.

**Dependencies:**  
None.

**Notes:**  
Los permisos funcionales administrables no implican la creación de nuevos roles.

---

## PR-AUTH-002 — Administrator User Management

**Priority:** P0  
**Status:** DRAFT

**Requirement:**  
Un Administrador deberá poder crear y modificar usuarios, activarlos, desactivarlos y restablecer sus contraseñas.

**Rationale:**  
Los usuarios deberán ser gestionados internamente por la organización.

**Dependencies:**  
PR-AUTH-001.

---

## PR-AUTH-003 — No Self-Registration

**Priority:** P0  
**Status:** DRAFT

**Requirement:**  
Gera Forms no deberá permitir el auto-registro de usuarios dentro del alcance inicial.

Los usuarios deberán ser creados por un Administrador.

**Rationale:**  
El acceso está destinado exclusivamente a usuarios autorizados por la organización.

**Dependencies:**  
PR-AUTH-002.

---

## PR-AUTH-004 — Authenticated Survey Access

**Priority:** P0  
**Status:** DRAFT

**Requirement:**  
Solamente Encuestadores autenticados, activos y previamente creados en Gera Forms podrán acceder a los formularios correspondientes a su ámbito de acceso.

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
Los Encuestadores necesitan operar temporalmente sin conectividad sin mantener autorizaciones offline indefinidas.

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
El vencimiento de la autorización offline no deberá eliminar ni invalidar:

* formularios descargados;
* encuestas borrador;
* encuestas pendientes o con error de envío;
* archivos asociados;
* historial de modificaciones.

Una vez autenticado nuevamente online, el usuario deberá poder continuar desde el estado previamente almacenado.

**Rationale:**  
El vencimiento de una autorización no debe provocar pérdida de relevamientos.

**Dependencies:**  
PR-AUTH-006, PR-AUTH-007.

---

## PR-AUTH-009 — User Account Data

**Priority:** P1  
**Status:** DRAFT

**Requirement:**  
Cada usuario deberá disponer como mínimo de:

* nombre completo;
* nombre de usuario;
* contraseña;
* rol;
* estado;
* correo electrónico;
* teléfono.

**Rationale:**  
Estos datos fueron definidos como información mínima necesaria para administrar las cuentas de Gera Forms.

**Dependencies:**  
PR-AUTH-002.

---

## PR-AUTH-010 — User Non-Deletion

**Priority:** P0  
**Status:** DRAFT

**Requirement:**  
Los usuarios no deberán poder eliminarse definitivamente mediante la administración funcional normal.

Cuando un usuario deje de estar habilitado para operar, deberá poder ser desactivado conservando su información histórica.

**Rationale:**  
Las encuestas y auditorías históricas necesitan conservar su relación con los usuarios que participaron en ellas.

**Dependencies:**  
PR-AUTH-002.

---

## PR-AUTH-011 — User Permission Management

**Priority:** P1  
**Status:** DRAFT

**Requirement:**  
El Administrador deberá poder habilitar y retirar permisos funcionales a los usuarios dentro de las capacidades admitidas por Gera Forms.

**Rationale:**  
La administración requiere controlar capacidades habilitadas sin crear ni eliminar cuentas para cada cambio de acceso.

**Dependencies:**  
PR-AUTH-001, PR-AUTH-002.

**Notes:**  
La matriz definitiva de permisos y el mecanismo técnico de autorización se especificarán posteriormente.

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
Gera Forms deberá soportar como mínimo:

* texto simple;
* texto largo;
* selección de una opción;
* selección de múltiples opciones.

**Rationale:**  
Estos tipos permiten cubrir el flujo básico de creación y realización de formularios.

**Dependencies:**  
PR-FORM-002.

---

## PR-FORM-004 — Extended Data Types

**Priority:** P1  
**Status:** DRAFT

**Requirement:**  
Gera Forms deberá permitir recopilar:

* teléfonos;
* correos electrónicos;
* observaciones;
* fotografías;
* documentos;
* archivos adjuntos;
* ubicación o dirección.

**Rationale:**  
La plataforma debe permitir relevamientos de campo con los tipos de información definidos por Product Vision.

**Dependencies:**  
PR-FORM-002.

---

## PR-FORM-005 — Form Availability Control

**Priority:** P0  
**Status:** DRAFT

**Requirement:**  
La creación de un formulario no deberá hacerlo automáticamente utilizable por Encuestadores.

El formulario deberá atravesar publicación y habilitación antes de estar disponible.

**Rationale:**  
Creación, publicación, asignación y descarga representan estados funcionales diferentes.

**Dependencies:**  
PR-FORM-001.

---

## PR-FORM-006 — Form Draft Saving

**Priority:** P0  
**Status:** DRAFT

**Requirement:**  
El Administrador deberá poder guardar y modificar un formulario como borrador tantas veces como sea necesario sin generar una nueva versión por cada guardado.

**Rationale:**  
La preparación de un formulario requiere un espacio de trabajo editable previo a su publicación.

**Dependencies:**  
PR-FORM-001.

---

## PR-FORM-007 — Required and Optional Questions

**Priority:** P0  
**Status:** DRAFT

**Requirement:**  
El Administrador deberá poder configurar individualmente cada pregunta como:

* obligatoria; o
* opcional.

Una encuesta no podrá finalizarse mientras incumpla preguntas obligatorias aplicables.

**Rationale:**  
Cada pregunta puede poseer reglas de obligatoriedad diferentes.

**Dependencies:**  
PR-FORM-002.

---

# 7. VERSION — Form Publication and Versioning

## PR-VERSION-001 — Form Publication

**Priority:** P0  
**Status:** DRAFT

**Requirement:**  
El Administrador deberá poder utilizar una acción `Publicar formulario` para generar una versión utilizable.

**Rationale:**  
Los formularios requieren una instancia publicada estable antes de utilizarse en relevamientos.

**Dependencies:**  
PR-FORM-001, PR-FORM-002, PR-FORM-006.

---

## PR-VERSION-002 — Automatic Version Generation

**Priority:** P0  
**Status:** DRAFT

**Requirement:**  
Cada nueva publicación deberá generar automáticamente una nueva versión identificable.

Guardar o modificar un borrador no deberá generar una versión.

**Rationale:**  
El versionado debe representar publicaciones funcionales y no cada modificación de trabajo.

**Dependencies:**  
PR-VERSION-001.

---

## PR-VERSION-003 — Published Version Immutability

**Priority:** P0  
**Status:** DRAFT

**Requirement:**  
Una versión publicada deberá conservar su estructura histórica y no deberá ser modificada retroactivamente por cambios destinados a una publicación posterior.

**Rationale:**  
Los resultados históricos deben interpretarse según la estructura con la que fueron recopilados.

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
Los resultados correspondientes a versiones anteriores deberán continuar visualizándose e interpretándose utilizando la estructura correspondiente a esas versiones.

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
El Encuestador debe conocer la existencia de una versión posterior sin perder trabajo pendiente.

**Dependencies:**  
PR-VERSION-002, PR-ASSIGN-004.

---

## PR-VERSION-007 — Version Update Blocking

**Priority:** P0  
**Status:** DRAFT

**Requirement:**  
El Encuestador no podrá reemplazar la versión descargada mientras existan para esa versión:

* encuestas borrador;
* encuestas pendientes de envío;
* encuestas con error de envío.

**Rationale:**  
La versión utilizada debe permanecer disponible mientras existan relevamientos locales dependientes de ella.

**Dependencies:**  
PR-VERSION-004, PR-SURVEY-003, PR-SYNC-001.

---

## PR-VERSION-008 — Version Update Eligibility

**Priority:** P0  
**Status:** DRAFT

**Requirement:**  
La actualización podrá realizarse cuando no quede trabajo pendiente correspondiente a la versión actualmente descargada y las encuestas que debían enviarse hayan sido recibidas exitosamente.

**Rationale:**  
La actualización no debe dejar relevamientos locales dependientes de la versión anterior.

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
El Administrador deberá poder habilitar un formulario publicado para Encuestadores específicos.

**Rationale:**  
No todos los formularios deberán estar disponibles para todos los Encuestadores.

**Dependencies:**  
PR-AUTH-001, PR-VERSION-001.

---

## PR-ASSIGN-002 — Assigned Forms Visibility

**Priority:** P0  
**Status:** DRAFT

**Requirement:**  
Un Encuestador deberá visualizar los formularios que tenga habilitados, incluyendo cuando corresponda aquellos que permanezcan transitoriamente disponibles por una desasignación con trabajo pendiente.

**Rationale:**  
La disponibilidad debe respetar las asignaciones y preservar trabajo pendiente.

**Dependencies:**  
PR-ASSIGN-001, PR-ASSIGN-007.

---

## PR-ASSIGN-003 — Explicit Form Download

**Priority:** P0  
**Status:** DRAFT

**Requirement:**  
El Encuestador deberá descargar explícitamente un formulario antes de poder utilizarlo.

**Rationale:**  
La descarga permite que el formulario pase a estar disponible localmente.

**Dependencies:**  
PR-ASSIGN-002.

---

## PR-ASSIGN-004 — Download Required for Online and Offline Use

**Priority:** P0  
**Status:** DRAFT

**Requirement:**  
La descarga previa será obligatoria tanto para utilización online como offline.

**Rationale:**  
Gera Forms utilizará un flujo consistente basado en formularios previamente descargados.

**Dependencies:**  
PR-ASSIGN-003.

---

## PR-ASSIGN-005 — Offline Availability

**Priority:** P0  
**Status:** DRAFT

**Requirement:**  
Un formulario correctamente descargado deberá permanecer disponible offline mientras el usuario posea autorización offline válida y el formulario continúe dentro de su ámbito operativo.

**Rationale:**  
El trabajo sin conectividad constituye una capacidad central.

**Dependencies:**  
PR-ASSIGN-004, PR-AUTH-006.

---

## PR-ASSIGN-006 — Multiple and All-Surveyor Assignment

**Priority:** P1  
**Status:** DRAFT

**Requirement:**  
El Administrador deberá poder habilitar un formulario:

* para un Encuestador;
* para múltiples Encuestadores seleccionados;
* para todos los Encuestadores mediante una acción equivalente a `Seleccionar todos los encuestadores`.

**Rationale:**  
La administración debe permitir asignaciones colectivas sin requerir operaciones individuales repetitivas.

**Dependencies:**  
PR-ASSIGN-001.

---

## PR-ASSIGN-007 — Deferred Form Unassignment

**Priority:** P0  
**Status:** DRAFT

**Requirement:**  
Cuando el Administrador retire a un Encuestador la habilitación de un formulario y existan encuestas pendientes asociadas, la desasignación deberá permanecer en espera hasta que el trabajo pendiente sea resuelto.

Durante dicho período, Gera Forms deberá preservar el acceso necesario para completar y enviar las encuestas pendientes existentes.

Cuando no queden encuestas pendientes, la desasignación deberá hacerse efectiva automáticamente.

**Rationale:**  
Una revocación de asignación no debe provocar pérdida ni bloqueo irreversible de relevamientos ya iniciados.

**Dependencies:**  
PR-ASSIGN-001, PR-SURVEY-003.

**Notes:**  
Los Acceptance Criteria definirán las acciones permitidas durante el estado transitorio sin ampliar silenciosamente la asignación.

---

# 9. SURVEY — Survey Execution and Editing

## PR-SURVEY-001 — Start Survey

**Priority:** P0  
**Status:** DRAFT

**Requirement:**  
Un Encuestador deberá poder iniciar una encuesta utilizando un formulario descargado y habilitado para iniciar nuevos relevamientos.

**Rationale:**  
Constituye el inicio del flujo principal de relevamiento.

**Dependencies:**  
PR-ASSIGN-004.

---

## PR-SURVEY-002 — Survey Draft Save

**Priority:** P0  
**Status:** DRAFT

**Requirement:**  
El Encuestador deberá poder guardar una encuesta como borrador y continuarla posteriormente.

Guardar no deberá representar el envío definitivo de la encuesta.

**Rationale:**  
Los relevamientos pueden interrumpirse y requerir múltiples sesiones de edición.

**Dependencies:**  
PR-SURVEY-001.

---

## PR-SURVEY-003 — Local Survey Persistence

**Priority:** P0  
**Status:** DRAFT

**Requirement:**  
Las encuestas iniciadas deberán conservarse localmente hasta completar correctamente su flujo de envío o hasta que una política futura expresamente aprobada determine otra cosa.

**Rationale:**  
El trabajo no debe depender de conectividad continua.

**Dependencies:**  
PR-SURVEY-001.

---

## PR-SURVEY-004 — Draft Editing

**Priority:** P0  
**Status:** DRAFT

**Requirement:**  
Una encuesta deberá poder modificarse mientras permanezca como borrador y no haya sido enviada exitosamente.

**Rationale:**  
El Encuestador puede necesitar corregir información antes de su envío definitivo.

**Dependencies:**  
PR-SURVEY-002.

---

## PR-SURVEY-005 — Successful Submission Lock

**Priority:** P0  
**Status:** DRAFT

**Requirement:**  
Una encuesta enviada exitosamente deberá quedar bloqueada para edición por parte del Encuestador.

**Rationale:**  
El envío exitoso representa el cierre definitivo de la edición del relevamiento.

**Dependencies:**  
PR-SURVEY-004, PR-SYNC-005.

---

## PR-SURVEY-006 — Visible Survey Identifier

**Priority:** P1  
**Status:** DRAFT

**Requirement:**  
Cada encuesta deberá poseer un identificador numérico visible para el Administrador y, dentro de su ámbito de acceso, para el Encuestador.

**Rationale:**  
Las encuestas necesitan poder identificarse inequívocamente durante operación, consulta y seguimiento.

**Dependencies:**  
PR-SURVEY-001.

**Notes:**  
La estrategia técnica de generación del identificador se definirá posteriormente.

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
El Encuestador deberá poder iniciar, completar en contenido y guardar nuevas encuestas como borradores mientras se encuentre offline utilizando formularios descargados.

El envío definitivo mediante `Finalizar` requerirá conectividad.

**Rationale:**  
El relevamiento debe poder realizarse sin conectividad aunque su envío se produzca posteriormente.

**Dependencies:**  
PR-OFFLINE-001, PR-SYNC-001.

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
La ausencia de conectividad, el cierre de Gera Forms o el vencimiento de la autorización offline no deberán provocar pérdida de encuestas o archivos almacenados localmente.

**Rationale:**  
La confiabilidad de los datos recopilados es esencial para el trabajo de campo.

**Dependencies:**  
PR-AUTH-008, PR-SURVEY-003, PR-FILE-002.

---

# 11. SYNC — Finalization, Submission and Synchronization

## PR-SYNC-001 — Manual Survey Finalization

**Priority:** P0  
**Status:** DRAFT

**Requirement:**  
El Encuestador deberá iniciar manualmente el envío definitivo de una encuesta mediante una acción funcional equivalente a `Finalizar`.

`Finalizar` deberá:

* requerir conectividad;
* validar la encuesta;
* impedir el envío mientras no cumpla las validaciones obligatorias;
* iniciar el envío al sistema central cuando la encuesta sea válida.

Gera Forms no deberá enviar automáticamente encuestas borrador dentro del alcance inicial.

**Rationale:**  
El Encuestador deberá controlar explícitamente cuándo una encuesta se considera lista para su envío definitivo.

**Dependencies:**  
PR-SURVEY-002, PR-FORM-007.

---

## PR-SYNC-002 — Retired Identifier

**Priority:** N/A  
**Status:** RETIRED

**Requirement:**  
N/A.

**Rationale:**  
Este identificador fue retirado durante la revisión anterior de Product Requirements.

**Dependencies:**  
None.

**Notes:**  
`PR-SYNC-002` no deberá reutilizarse para ningún requisito presente o futuro.

---

## PR-SYNC-003 — Batch Survey Finalization

**Priority:** P1  
**Status:** DRAFT

**Requirement:**  
El Encuestador deberá disponer de una acción equivalente a `Finalizar todos`.

La acción deberá permitir seleccionar manualmente qué encuestas desea enviar.

Cada encuesta seleccionada deberá validarse individualmente.

Las encuestas válidas podrán enviarse aunque otra encuesta seleccionada no cumpla sus validaciones.

Las encuestas no seleccionadas deberán permanecer como borradores sin modificaciones.

**Rationale:**  
Permite enviar conjuntamente múltiples relevamientos manteniendo control explícito sobre cuáles serán enviados.

**Dependencies:**  
PR-SYNC-001.

---

## PR-SYNC-004 — Synchronization Status

**Priority:** P0  
**Status:** DRAFT

**Requirement:**  
Cada encuesta deberá exponer claramente uno de los siguientes estados de envío/sincronización cuando corresponda:

* `Pendiente de sincronización`;
* `Sincronizando`;
* `Sincronizado`;
* `Error de sincronización`.

**Rationale:**  
El Encuestador debe poder determinar si la información permanece local o ya fue recibida correctamente por el sistema central.

**Dependencies:**  
PR-SYNC-001.

---

## PR-SYNC-005 — Successful Synchronization

**Priority:** P0  
**Status:** DRAFT

**Requirement:**  
Una encuesta solo deberá adoptar el estado `Sincronizado` cuando su envío haya finalizado exitosamente y el sistema central haya confirmado su recepción correcta.

**Rationale:**  
No debe presentarse como recibida información cuya persistencia central no haya sido confirmada.

**Dependencies:**  
PR-SYNC-004.

---

## PR-SYNC-006 — Synchronization Error Preservation

**Priority:** P0  
**Status:** DRAFT

**Requirement:**  
Cuando un envío falle, la encuesta deberá adoptar el estado `Error de sincronización` y conservar localmente toda la información necesaria para permitir un intento posterior.

**Rationale:**  
Los errores de conectividad o transmisión no deberán causar pérdida de información.

**Dependencies:**  
PR-SYNC-004.

---

## PR-SYNC-007 — Synchronization Retry

**Priority:** P0  
**Status:** DRAFT

**Requirement:**  
El Encuestador deberá poder volver a intentar manualmente el envío de una encuesta en `Error de sincronización`.

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
El Administrador deberá poder configurar cada formulario con:

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
La ubicación automática puede no estar disponible o puede requerirse una referencia textual.

**Dependencies:**  
PR-LOCATION-001.

---

## PR-LOCATION-004 — Map Location Selection

**Priority:** P1  
**Status:** DRAFT

**Requirement:**  
Cuando corresponda registrar ubicación, el Encuestador deberá poder seleccionar manualmente una ubicación mediante un mapa cuando dicha capacidad se encuentre disponible.

**Rationale:**  
Permite identificar visualmente una ubicación.

**Dependencies:**  
PR-LOCATION-001.

**Notes:**  
El comportamiento online/offline del mapa se determinará posteriormente.

---

## PR-LOCATION-005 — Required Location Validation

**Priority:** P0  
**Status:** DRAFT

**Requirement:**  
Cuando un formulario esté configurado con `Ubicación obligatoria`, la encuesta no podrá finalizarse hasta satisfacer una modalidad válida de ubicación.

**Rationale:**  
La obligatoriedad configurada debe aplicarse antes del envío definitivo.

**Dependencies:**  
PR-LOCATION-001, PR-SYNC-001.

---

# 13. FILE — Files and Attachments

## PR-FILE-001 — Survey Attachments

**Priority:** P1  
**Status:** DRAFT

**Requirement:**  
Los formularios deberán poder permitir incorporación de archivos, incluyendo fotografías y documentos, cuando el tipo de pregunta correspondiente lo permita.

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
La captura de archivos debe formar parte del flujo offline.

**Dependencies:**  
PR-FILE-001, PR-OFFLINE-001.

---

## PR-FILE-003 — Attachment Submission

**Priority:** P1  
**Status:** DRAFT

**Requirement:**  
Los archivos asociados a una encuesta deberán enviarse al sistema central como parte del proceso de finalización correspondiente.

**Rationale:**  
La encuesta recibida debe conservar los archivos recopilados durante el relevamiento.

**Dependencies:**  
PR-FILE-002, PR-SYNC-001.

---

## PR-FILE-004 — Local Retention After Submission

**Priority:** P1  
**Status:** DRAFT

**Requirement:**  
El envío exitoso de un archivo no deberá eliminar automáticamente su copia local.

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
La eliminación de una copia local de un archivo previamente enviado correctamente no deberá eliminar la copia almacenada en el sistema central.

**Rationale:**  
La limpieza local no debe provocar pérdida de evidencia ya recibida.

**Dependencies:**  
PR-FILE-003, PR-FILE-005.

---

# 14. AUDIT — Survey Modification Audit

## PR-AUDIT-001 — Detailed Modification Audit

**Priority:** P1  
**Status:** DRAFT

**Requirement:**  
Toda modificación realizada sobre una encuesta mientras permanezca editable deberá generar información de auditoría detallada.

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
El Encuestador deberá poder consultar la información de auditoría correspondiente a sus propias encuestas cuando dicha información se encuentre disponible dentro de su ámbito de acceso.

**Rationale:**  
Permite al Encuestador revisar las modificaciones realizadas sobre sus relevamientos.

**Dependencies:**  
PR-AUDIT-001.

---

# 15. RESULT — Results

## PR-RESULT-001 — Administrator Results Access

**Priority:** P0  
**Status:** DRAFT

**Requirement:**  
El Administrador deberá poder consultar las encuestas enviadas correctamente al sistema central.

**Rationale:**  
La consulta de relevamientos recopilados forma parte del flujo principal.

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
El Administrador deberá poder identificar qué versión fue utilizada para cada encuesta y consultar sus respuestas conforme a dicha versión.

**Rationale:**  
La interpretación depende de la estructura exacta utilizada.

**Dependencies:**  
PR-VERSION-004, PR-RESULT-001.

---

## PR-RESULT-004 — Result Detail Information

**Priority:** P0  
**Status:** DRAFT

**Requirement:**  
La consulta de una encuesta deberá permitir identificar como mínimo:

* identificador de encuesta;
* formulario;
* versión;
* Encuestador;
* fecha;
* estado;
* respuestas.

**Rationale:**  
El Administrador necesita contexto suficiente para interpretar cada relevamiento.

**Dependencies:**  
PR-RESULT-001, PR-SURVEY-006.

---

## PR-RESULT-005 — Result Search and Filtering

**Priority:** P1  
**Status:** DRAFT

**Requirement:**  
La consulta de resultados deberá proporcionar capacidades de búsqueda y filtros.

**Rationale:**  
La cantidad de encuestas puede impedir una consulta eficiente mediante una lista sin herramientas de localización.

**Dependencies:**  
PR-RESULT-001.

**Notes:**  
Los campos y combinaciones concretas de filtrado se definirán en User Stories y UX.

---

## PR-RESULT-006 — Basic Response Chart

**Priority:** P1  
**Status:** DRAFT

**Requirement:**  
Gera Forms deberá proporcionar al Administrador una visualización básica mediante gráfico de torta para respuestas categóricas cuya naturaleza permita una agregación de este tipo.

No será obligatorio representar mediante gráfico de torta respuestas de texto libre, archivos, fotografías, documentos, ubicaciones u otros datos incompatibles con dicha visualización.

**Rationale:**  
Permite una primera lectura visual simple de respuestas estructuradas sin introducir todavía un módulo analítico avanzado.

**Dependencies:**  
PR-RESULT-001, PR-FORM-003.

---

# 16. PLATFORM — Platform and Operational Constraints

## PR-PLATFORM-001 — Progressive Web Application

**Priority:** P0  
**Status:** DRAFT

**Requirement:**  
Gera Forms deberá ser provisto como una Progressive Web App.

**Rationale:**  
La plataforma debe utilizarse desde diferentes dispositivos sin aplicaciones móviles nativas específicas.

**Dependencies:**  
None.

---

## PR-PLATFORM-002 — Smartphone Support

**Priority:** P0  
**Status:** DRAFT

**Requirement:**  
Gera Forms deberá poder utilizarse desde smartphones Android y iPhone compatibles con las capacidades requeridas.

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
La tecnología específica se determinará durante Architecture.

---

## PR-PLATFORM-005 — Single Organization

**Priority:** P0  
**Status:** DRAFT

**Requirement:**  
El alcance inicial deberá soportar una única organización.

**Rationale:**  
No existe actualmente un requisito de operación multi-organización.

**Dependencies:**  
None.

---

## PR-PLATFORM-006 — No Required External Integrations

**Priority:** P1  
**Status:** DRAFT

**Requirement:**  
El MVP no dependerá funcionalmente de integraciones de negocio con sistemas externos de la organización.

**Rationale:**  
No se identificaron integraciones externas necesarias para resolver el flujo principal.

**Dependencies:**  
None.

**Notes:**  
Servicios técnicos necesarios para capacidades internas se evaluarán durante Architecture.

---

# 17. FUTURE — Post-MVP Product Direction

## PR-FUTURE-001 — CSV Export

**Priority:** P3  
**Status:** DRAFT

**Requirement:**  
Gera Forms podrá incorporar exportación de resultados en formato CSV.

**Rationale:**  
Permitirá utilizar resultados en herramientas externas de análisis.

**Dependencies:**  
PR-RESULT-001.

---

## PR-FUTURE-002 — XLSX Export

**Priority:** P3  
**Status:** DRAFT

**Requirement:**  
Gera Forms podrá incorporar exportación de resultados en formato XLSX.

**Rationale:**  
Facilitará el análisis mediante herramientas de hojas de cálculo.

**Dependencies:**  
PR-RESULT-001.

---

## PR-FUTURE-003 — Advanced Results Statistics

**Priority:** P3  
**Status:** DRAFT

**Requirement:**  
Gera Forms podrá incorporar un apartado de estadísticas avanzadas construido a partir de los resultados recopilados.

**Rationale:**  
La plataforma podrá evolucionar desde recopilación y visualización básica hacia explotación analítica.

**Dependencies:**  
PR-RESULT-001.

---

## PR-FUTURE-004 — Advanced Results Visualization

**Priority:** P3  
**Status:** DRAFT

**Requirement:**  
Gera Forms podrá incorporar visualizaciones y gráficos adicionales o avanzados de los resultados recopilados.

**Rationale:**  
Permitirá ampliar las capacidades de interpretación más allá del gráfico básico incluido en el alcance inicial.

**Dependencies:**  
PR-FUTURE-003, PR-RESULT-006.

---

# 18. Explicit Initial Scope Exclusions

No forman parte del alcance inicial:

* formularios públicos anónimos;
* auto-registro de usuarios;
* eliminación funcional definitiva de usuarios;
* múltiples organizaciones independientes;
* arquitectura funcional multi-tenant;
* aplicaciones móviles nativas específicas para Android;
* aplicaciones móviles nativas específicas para iOS;
* envío automático de encuestas borrador;
* integraciones de negocio obligatorias con sistemas externos;
* estadísticas avanzadas;
* dashboards analíticos avanzados.

Estas exclusiones podrán reconsiderarse mediante el proceso formal de cambio.

---

# 19. Requirement Summary

Revision 2 propone los siguientes requisitos activos:

| Domain | Active Requirements |
| --- | ---: |
| AUTH | 11 |
| FORM | 7 |
| VERSION | 9 |
| ASSIGN | 7 |
| SURVEY | 6 |
| OFFLINE | 4 |
| SYNC | 6 |
| LOCATION | 5 |
| FILE | 6 |
| AUDIT | 4 |
| RESULT | 6 |
| PLATFORM | 6 |
| FUTURE | 4 |
| **TOTAL ACTIVE** | **81** |

Adicionalmente:

| Identifier | Status |
| --- | --- |
| PR-SYNC-002 | RETIRED |

`PR-SYNC-002` no forma parte del total de requisitos activos y no podrá reutilizarse.

---

# 20. Revision 2 Change Summary

Revision 2 incorpora las decisiones CL-014 a CL-025.

Principales cambios respecto de la baseline aprobada el 2026-09-21:

* ampliación de administración de usuarios;
* definición de datos mínimos de usuario;
* prohibición de eliminación funcional de usuarios;
* administración de permisos;
* borradores de formulario;
* preguntas obligatorias u opcionales;
* preparación de nuevas versiones mediante modificación del formulario sin alterar versiones publicadas;
* asignación individual, múltiple o a todos los Encuestadores;
* desasignación diferida cuando existe trabajo pendiente;
* redefinición de Guardar como persistencia de borrador;
* redefinición de Finalizar como validación y envío definitivo;
* incorporación de Finalizar todos con selección manual;
* requisito de conectividad para finalizar;
* validación independiente de encuestas en Finalizar todos;
* identificación numérica visible de encuestas;
* ampliación de consulta de resultados;
* búsqueda y filtros;
* gráfico de torta básico para respuestas categóricas compatibles;
* diferenciación entre visualización básica inicial y analítica avanzada futura;
* corrección de inconsistencias de conteo y estado de la baseline anterior.

---

# 21. Traceability Baseline

La trazabilidad será:

`Product Vision → PR-* → User Stories → Acceptance Criteria → Feature Specifications → Plans → Tasks → Code → Tests → Validation`

Los identificadores `PR-*` deberán conservarse de forma estable.

Un requisito que deje de ser válido deberá cambiar de estado en lugar de permitir que su identificador sea reutilizado para otro significado.

`PR-SYNC-002` constituye el primer identificador explícitamente retirado y deberá permanecer históricamente visible.

---

# 22. Resolved Product Clarifications

Revision 2 incorpora las siguientes decisiones:

* `CL-001` — Autorización offline máxima de 24 horas.
* `CL-002` — Descarga explícita previa de formularios.
* `CL-003` — Envío/sincronización iniciado manualmente.
* `CL-004` — Estados de sincronización.
* `CL-005` — Edición previa al envío exitoso.
* `CL-006` — Asociación de encuestas a versiones.
* `CL-007` — Métodos de ubicación.
* `CL-008` — Conservación local de archivos enviados.
* `CL-009` — Preservación del trabajo ante expiración offline.
* `CL-010` — Bloqueo de actualización con trabajo pendiente.
* `CL-011` — Conservación operativa de la última versión local.
* `CL-012` — Auditoría detallada.
* `CL-013` — Configuración de obligatoriedad de ubicación.
* `CL-014` — Administración de usuarios.
* `CL-015` — Datos mínimos del usuario.
* `CL-016` — Asignación individual, múltiple o total.
* `CL-017` — Desasignación diferida.
* `CL-018` — Borradores de formulario.
* `CL-019` — Preparación de una nueva versión.
* `CL-020` — Preguntas obligatorias u opcionales.
* `CL-021` — Diferencia entre Guardar y Finalizar.
* `CL-022` — Identificación visible de encuestas.
* `CL-023` — Consulta ampliada de resultados.
* `CL-024` — Finalizar y Finalizar todos como acciones de envío.
* `CL-025` — Selección manual para Finalizar todos.

No permanecen clarificaciones de producto bloqueantes conocidas para esta revisión.

---

# 23. Deferred Technical Decisions

Revision 2 no introduce deliberadamente decisiones sobre:

* mecanismo de autenticación;
* implementación del modelo de permisos;
* almacenamiento local;
* base de datos;
* almacenamiento central de archivos;
* protocolo o estrategia técnica de sincronización;
* detección técnica de conectividad;
* resolución técnica de errores;
* generación técnica de identificadores de encuesta;
* framework frontend;
* framework backend;
* servicios de mapas;
* geocodificación;
* funcionamiento técnico de GPS;
* infraestructura concreta dentro de la VPS;
* utilización definitiva de Docker.

Estas cuestiones pertenecen a fases posteriores salvo que revelen una nueva decisión de producto.

---

# 24. Baseline History

## Revision 1

**Status:** Approved  
**Approved:** 2026-09-21  
**Active requirements:** 70

Primera línea base formal de Product Requirements.

`PR-SYNC-002` fue retirado durante su revisión y su identificador quedó reservado históricamente.

## Revision 2

**Status:** Draft  
**Last reviewed:** 2026-09-29  
**Proposed active requirements:** 81  
**Retired identifiers:** 1 (`PR-SYNC-002`)

Incorpora las decisiones CL-014 a CL-025 y corrige inconsistencias documentales detectadas durante la preparación de User Stories.

**End of requirements.md — Revision 2**