# Gera Forms — Product Vision

**Status:** Approved
**Approved:** 2026-09-21
**Lifecycle Phase:** 01 — Discovery
**Milestone:** MVP
**Last reviewed:** 2026-09-21

---

## 1. Product Overview

Gera Forms es una plataforma para la creación, gestión, asignación, completado y consulta de formularios, diseñada para funcionar tanto con conexión a Internet como sin ella.

El producto busca reemplazar el uso actual de Google Forms en escenarios de relevamiento de campo donde los Encuestadores pueden encontrarse en lugares sin acceso a Internet o datos móviles.

Gera Forms deberá permitir que los Encuestadores continúen trabajando desde smartphones, tablets o computadoras aun cuando no exista conectividad, conservando localmente los formularios descargados, las encuestas realizadas, sus modificaciones y los archivos asociados.

Cuando vuelva a existir conectividad, el Encuestador podrá sincronizar manualmente con el servidor las encuestas pendientes.

El funcionamiento offline constituye una capacidad central del producto y no una funcionalidad complementaria.

---

## 2. Problem

La organización realiza relevamientos mediante formularios en ubicaciones donde la conectividad a Internet puede ser inexistente, inestable o insuficiente.

El uso de herramientas que dependen de conectividad dificulta garantizar que un Encuestador pueda acceder a un formulario, completarlo y conservar el relevamiento cuando se encuentra sin conexión.

Además, determinados relevamientos pueden requerir registrar la ubicación en la que fueron realizados, recopilar archivos, fotografías, documentos u otra información durante el trabajo de campo.

Gera Forms busca resolver estos problemas mediante una plataforma preparada específicamente para operar online y offline, permitiendo almacenar temporalmente la información en el dispositivo y sincronizarla posteriormente con el servidor.

---

## 3. Product Vision

Gera Forms deberá convertirse en una plataforma centralizada para la gestión de formularios, Encuestadores y resultados de una única organización.

La plataforma permitirá que usuarios Administradores:

* administren usuarios;
* creen formularios;
* configuren sus preguntas;
* publiquen versiones de los formularios;
* habiliten formularios para determinados Encuestadores;
* consulten las encuestas realizadas;
* consulten los resultados recopilados;
* consulten información de auditoría cuando corresponda.

Los usuarios Encuestadores podrán utilizar Gera Forms desde smartphones Android o iPhone mediante una Progressive Web App (PWA), así como desde computadoras compatibles.

Los Encuestadores deberán poder descargar previamente los formularios habilitados para utilizarlos posteriormente tanto online como offline.

---

## 4. Target Organization

Gera Forms estará destinado inicialmente a una única organización.

No se requiere para el MVP soportar múltiples organizaciones independientes ni un modelo funcional multi-tenant.

Los usuarios, formularios, versiones, asignaciones, encuestas y resultados pertenecerán al mismo ámbito organizacional.

---

## 5. User Roles

Gera Forms tendrá dos roles:

1. Administrador.
2. Encuestador.

### 5.1. Administrador

El Administrador será responsable de la gestión de la plataforma.

Entre sus capacidades esperadas se encuentran:

* crear usuarios;
* administrar usuarios;
* crear formularios;
* configurar preguntas;
* configurar posibles respuestas;
* configurar las opciones generales del formulario;
* publicar versiones de formularios;
* habilitar formularios para determinados Encuestadores;
* consultar encuestas completadas;
* consultar resultados;
* consultar información de auditoría.

Las capacidades específicas y permisos detallados serán definidos posteriormente en Product Requirements y en las especificaciones correspondientes.

### 5.2. Encuestador

El Encuestador será responsable de realizar los relevamientos.

Deberá poder:

* autenticarse en Gera Forms;
* acceder a los formularios que tenga habilitados;
* descargar formularios al dispositivo;
* utilizar formularios descargados online u offline;
* iniciar encuestas;
* guardar encuestas incompletas;
* continuar encuestas posteriormente;
* completar encuestas;
* modificar encuestas todavía no sincronizadas;
* consultar el estado de sincronización;
* iniciar manualmente la sincronización;
* conservar localmente archivos asociados a las encuestas;
* eliminar manualmente archivos locales cuando corresponda.

El Encuestador no podrá crear formularios ni administrar usuarios.

---

## 6. User Management

Los usuarios de Gera Forms serán creados por usuarios Administradores.

No se contempla inicialmente el auto-registro.

Para utilizar Gera Forms como Encuestador será necesario disponer previamente de una cuenta creada dentro de la plataforma.

La definición detallada del ciclo de vida de usuarios, activación, desactivación, recuperación de acceso y demás reglas de administración será realizada posteriormente.

---

## 7. Form Creation

Los formularios serán creados exclusivamente por usuarios Administradores.

La experiencia de creación deberá permitir definir preguntas utilizando diferentes tipos de respuesta.

Como referencia funcional inicial se consideran, entre otros:

* texto simple;
* texto largo;
* selección de opciones;
* selección múltiple;
* teléfonos;
* correos electrónicos;
* observaciones;
* fotografías;
* documentos;
* archivos adjuntos;
* ubicación o dirección.

El catálogo definitivo de tipos de pregunta y cuáles serán incluidos en el MVP se determinarán durante Product Requirements y MVP Scope.

---

## 8. Form Assignment

Los formularios podrán ser habilitados para determinados usuarios Encuestadores.

Un formulario creado o publicado no deberá estar necesariamente disponible para todos los Encuestadores.

El Administrador deberá poder determinar qué Encuestadores tienen habilitado cada formulario.

Un Encuestador deberá acceder únicamente a los formularios que tenga habilitados.

La asignación de un formulario no implica que este se encuentre descargado en el dispositivo del Encuestador.

Por lo tanto, deberán distinguirse conceptualmente los siguientes estados:

* formulario existente;
* formulario publicado;
* formulario habilitado para un Encuestador;
* formulario descargado en un dispositivo.

---

## 9. Form Download

Antes de poder utilizar un formulario, el Encuestador deberá descargarlo explícitamente al dispositivo.

Esta descarga será requerida independientemente de si el Encuestador planea utilizar el formulario online u offline.

Por lo tanto, incluso cuando exista conexión a Internet, el flujo normal requerirá que el formulario haya sido previamente descargado.

Un formulario que nunca haya sido descargado en el dispositivo no podrá utilizarse cuando el dispositivo se encuentre offline.

La descarga deberá permitir que el formulario quede disponible localmente para su utilización posterior.

---

## 10. Authentication and Offline Access

El primer inicio de sesión de un usuario en un dispositivo requerirá conexión con el servidor.

Una vez realizada correctamente una autenticación online, el usuario podrá continuar accediendo a Gera Forms desde ese dispositivo sin conexión durante un período máximo de 24 horas desde su último inicio de sesión online válido.

Si el usuario intenta acceder offline y no dispone de una autorización local válida correspondiente a una autenticación online previa, no podrá iniciar sesión.

Una vez vencido el período de 24 horas, será necesaria una nueva autenticación online antes de volver a utilizar Gera Forms.

La expiración de la autorización no deberá eliminar:

* formularios descargados;
* encuestas incompletas;
* encuestas completadas pendientes de sincronización;
* archivos almacenados localmente;
* historial local asociado.

Si la autorización vence mientras existen encuestas incompletas o pendientes de sincronización, dicha información permanecerá almacenada localmente.

Cuando el usuario vuelva a autenticarse correctamente online, podrá continuar trabajando desde el estado en que había quedado.

La estrategia técnica utilizada para implementar autenticación y autorización offline será definida posteriormente durante Architecture.

---

## 11. Form Completion

Los formularios serán completados por usuarios Encuestadores previamente registrados en Gera Forms.

No se contempla inicialmente que personas anónimas o usuarios externos completen formularios mediante enlaces públicos.

El Encuestador podrá utilizar los formularios descargados tanto online como offline.

Una encuesta podrá:

* iniciarse;
* guardarse parcialmente;
* continuarse posteriormente;
* completarse;
* modificarse antes de su sincronización;
* sincronizarse posteriormente con el servidor.

Una encuesta almacenada localmente deberá conservarse aunque se cierre Gera Forms, se pierda conectividad o venza la autorización offline del usuario.

---

## 12. Survey Editing

Una encuesta todavía no sincronizada podrá ser modificada por el Encuestador.

Las modificaciones deberán quedar registradas mediante una auditoría detallada.

Como mínimo, la auditoría deberá permitir identificar:

* pregunta modificada;
* valor anterior;
* valor nuevo;
* usuario que realizó la modificación;
* fecha y hora de la modificación.

Una vez que una encuesta haya sido sincronizada exitosamente con el servidor, dejará de ser editable por el Encuestador.

La información de auditoría deberá poder ser consultada por el propio Encuestador cuando corresponda y por usuarios Administradores.

---

## 13. Manual Synchronization

La sincronización de encuestas no será automática.

El Encuestador deberá iniciar explícitamente la sincronización.

La plataforma deberá ofrecer acciones equivalentes a:

* `Sincronizar formulario`;
* `Sincronizar todos los formularios`.

Cada encuesta deberá permitir identificar claramente su estado de sincronización.

Los estados definidos inicialmente son:

* `Pendiente de sincronización`;
* `Sincronizando`;
* `Sincronizado`;
* `Error de sincronización`.

Una encuesta solo deberá considerarse sincronizada cuando el proceso haya finalizado exitosamente.

Una encuesta con error de sincronización deberá conservarse localmente para permitir un intento posterior.

---

## 14. Form Versioning

Los formularios publicados tendrán versiones.

Cada acción de publicación realizada por un Administrador deberá generar una nueva versión del formulario.

Conceptualmente:

* Formulario A — v1;
* Formulario A — v2;
* Formulario A — v3;
* etc.

Cada versión publicada deberá tratarse como una versión única e inmutable para efectos de las encuestas recopiladas con ella, manteniendo al mismo tiempo la relación con el formulario y sus versiones anteriores.

Las respuestas recopiladas deberán permanecer asociadas a la versión exacta utilizada para realizar la encuesta.

La publicación de una nueva versión no deberá modificar la estructura ni la interpretación de las encuestas recopiladas con versiones anteriores.

Por ejemplo, si `Formulario A v1` posee cinco preguntas y posteriormente `Formulario A v2` posee diez preguntas, las encuestas realizadas con v1 deberán continuar visualizándose e interpretándose utilizando la estructura correspondiente a v1.

---

## 15. Form Version Update

Un Encuestador podrá continuar utilizando una versión descargada aunque exista una versión más reciente disponible, siempre que existan encuestas incompletas o pendientes de sincronización correspondientes a la versión anterior.

Cuando exista una versión nueva, Gera Forms deberá informar al Encuestador mediante un mensaje equivalente a:

> Nueva versión del formulario disponible. Complete y sincronice todas las encuestas pendientes de la versión actual para poder actualizar el formulario.

El Encuestador no podrá actualizar a la nueva versión mientras existan:

* encuestas incompletas de la versión anterior; o
* encuestas completadas pendientes de sincronización de la versión anterior.

Una vez finalizadas y sincronizadas todas las encuestas correspondientes a la versión anterior, podrá realizarse la actualización a la versión más reciente.

El dispositivo deberá conservar solamente la última versión disponible del formulario una vez completado correctamente el proceso de actualización.

Las respuestas históricas permanecerán asociadas en el servidor a la versión con la que fueron recopiladas.

---

## 16. Location Capture

Cada formulario permitirá que el Administrador configure el tratamiento de la ubicación.

Las opciones serán:

* `Ubicación obligatoria`;
* `Ubicación opcional`;
* `Sin ubicación`.

Cuando corresponda registrar una ubicación, Gera Forms deberá contemplar diferentes mecanismos:

1. obtener la ubicación desde los servicios de ubicación del dispositivo;
2. ingresar manualmente una dirección;
3. seleccionar manualmente una ubicación mediante un mapa.

Cuando la ubicación sea obligatoria, la encuesta deberá cumplir las reglas de ubicación correspondientes antes de poder considerarse completada.

Cuando sea opcional, el Encuestador podrá completar la encuesta sin proporcionar ubicación.

Cuando el formulario esté configurado como `Sin ubicación`, no será necesario recopilar información de ubicación.

Las reglas exactas para determinar qué mecanismo satisface una ubicación obligatoria y el funcionamiento técnico de GPS, mapas, geocodificación y disponibilidad offline serán definidos posteriormente.

---

## 17. Offline Files and Attachments

Gera Forms deberá permitir utilizar archivos adjuntos durante el trabajo offline.

Esto podrá incluir, según los tipos de preguntas habilitados:

* fotografías;
* documentos;
* otros archivos admitidos por el formulario.

Los archivos deberán poder almacenarse localmente junto con la encuesta correspondiente mientras no exista conectividad.

Cuando el Encuestador inicie la sincronización, los archivos asociados deberán formar parte de la información a sincronizar cuando corresponda.

Una sincronización exitosa no eliminará automáticamente los archivos almacenados localmente.

Los archivos permanecerán en el dispositivo hasta que el Encuestador decida eliminarlos manualmente.

La eliminación de la copia local de un archivo ya sincronizado no deberá eliminar la copia correctamente almacenada en el servidor.

Las políticas técnicas de almacenamiento, límites de tamaño, formatos admitidos, seguridad y gestión del espacio local serán definidas posteriormente.

---

## 18. Data Collected

Gera Forms podrá recopilar información de distinta naturaleza, incluyendo:

* datos personales;
* datos filiatorios;
* teléfonos;
* correos electrónicos;
* direcciones;
* ubicación;
* observaciones;
* fotografías;
* documentos;
* archivos adjuntos;
* respuestas estructuradas a preguntas del formulario.

Debido a la naturaleza de esta información, privacidad, seguridad, autorización, almacenamiento local, transmisión y protección de datos deberán considerarse requisitos relevantes del producto.

Las políticas concretas correspondientes serán definidas en fases posteriores y no deberán inferirse durante Discovery.

---

## 19. Primary Workflow

El flujo principal esperado de Gera Forms será:

1. un Administrador accede a Gera Forms;
2. crea un formulario;
3. configura las preguntas y opciones del formulario;
4. configura el comportamiento de ubicación;
5. publica una versión del formulario;
6. habilita el formulario para determinados Encuestadores;
7. un Encuestador se autentica en Gera Forms;
8. visualiza los formularios que tiene habilitados;
9. selecciona y descarga los formularios que necesita utilizar;
10. realiza relevamientos online u offline;
11. las encuestas se almacenan localmente;
12. puede guardar encuestas incompletas y continuarlas posteriormente;
13. puede modificar encuestas todavía no sincronizadas;
14. las modificaciones quedan registradas mediante auditoría detallada;
15. las encuestas completadas quedan pendientes de sincronización;
16. cuando existe conectividad, el Encuestador inicia manualmente la sincronización;
17. Gera Forms informa el estado de cada sincronización;
18. una encuesta correctamente sincronizada deja de ser editable por el Encuestador;
19. el Administrador puede consultar los resultados sincronizados;
20. si existe una nueva versión del formulario, el Encuestador deberá finalizar y sincronizar los pendientes de la versión anterior antes de actualizarla.

Este flujo representa el valor principal que deberá demostrar el MVP.

---

## 20. MVP Vision

El MVP deberá demostrar de punta a punta el flujo principal de Gera Forms.

Como mínimo, deberá permitir demostrar:

* existencia de los roles Administrador y Encuestador;
* creación y administración básica de usuarios por un Administrador;
* autenticación de usuarios;
* capacidad de acceso offline durante el período autorizado;
* creación de formularios por un Administrador;
* utilización de distintos tipos básicos de preguntas;
* configuración de ubicación;
* publicación y versionado de formularios;
* habilitación de formularios para determinados Encuestadores;
* descarga explícita de formularios;
* utilización de formularios descargados online;
* utilización de formularios descargados offline;
* almacenamiento local de encuestas;
* posibilidad de guardar y continuar encuestas;
* edición de encuestas no sincronizadas;
* auditoría detallada de modificaciones;
* almacenamiento local de archivos;
* sincronización manual;
* visualización de estados de sincronización;
* conservación de información ante errores de sincronización;
* bloqueo de edición luego de una sincronización exitosa;
* consulta de resultados por parte del Administrador;
* coexistencia correcta de resultados correspondientes a distintas versiones de un mismo formulario;
* actualización controlada de versiones descargadas.

La clasificación definitiva de estos comportamientos en requisitos P0, P1, P2 o P3 será realizada durante Product Requirements y MVP Scope.

---

## 21. Deployment and Platform Constraints

Gera Forms deberá implementarse como una Progressive Web App.

Deberá poder utilizarse desde:

* smartphones Android;
* iPhone;
* computadoras compatibles.

La infraestructura central destinada a las APIs de gestión de usuarios, formularios, sincronización y demás capacidades centralizadas deberá poder alojarse en una VPS.

El uso de contenedores Docker en dicha VPS constituye actualmente una alternativa prevista, pero su adopción definitiva será determinada durante Architecture.

No se requieren actualmente integraciones con sistemas externos.

Las tecnologías específicas de frontend, backend, base de datos, almacenamiento, autenticación, sincronización y despliegue no forman parte de esta visión y serán definidas posteriormente.

---

## 22. Future Product Direction

Más allá del MVP, Gera Forms podrá evolucionar hacia una plataforma más amplia de gestión de formularios, Encuestadores y resultados.

Entre las capacidades futuras identificadas se encuentran:

* exportación de resultados a CSV;
* exportación de resultados a XLSX;
* visualización gráfica de resultados;
* estadísticas sobre relevamientos;
* análisis de resultados;
* herramientas adicionales para gestión de Encuestadores;
* mejoras en visualización y explotación de la información recopilada.

Estas capacidades representan una dirección futura del producto y no implican automáticamente su inclusión en el MVP.

---

## 23. Current Scope Boundaries

Actualmente se consideran fuera del alcance inicial:

* formularios públicos anónimos;
* auto-registro de usuarios;
* múltiples organizaciones independientes;
* modelo multi-tenant;
* integraciones obligatorias con sistemas externos;
* aplicaciones móviles nativas desarrolladas específicamente para Android;
* aplicaciones móviles nativas desarrolladas específicamente para iOS;
* sincronización automática de encuestas.

Estas exclusiones podrán revisarse posteriormente mediante el proceso formal de cambio establecido por GERA SDD.

---

## 24. Resolved Discovery Clarifications

Durante Discovery se resolvieron las siguientes decisiones:

* **CL-001 — RESOLVED:** acceso offline permitido durante un máximo de 24 horas desde la última autenticación online válida.
* **CL-002 — RESOLVED:** todo formulario debe descargarse explícitamente antes de poder utilizarse, incluso cuando exista conexión.
* **CL-003 — RESOLVED:** la sincronización será iniciada manualmente por el Encuestador.
* **CL-004 — RESOLVED:** se utilizarán los estados `Pendiente de sincronización`, `Sincronizando`, `Sincronizado` y `Error de sincronización`.
* **CL-005 — RESOLVED:** una encuesta podrá modificarse antes de sincronizarse y dejará de ser editable luego de una sincronización exitosa.
* **CL-006 — RESOLVED:** los formularios publicados tendrán versiones independientes y las encuestas permanecerán asociadas a la versión utilizada.
* **CL-007 — RESOLVED:** la ubicación podrá obtenerse desde el dispositivo, ingresarse como dirección o seleccionarse mediante mapa.
* **CL-008 — RESOLVED:** los archivos sincronizados permanecerán almacenados localmente hasta que el Encuestador decida eliminarlos manualmente.
* **CL-009 — RESOLVED:** el vencimiento de la autorización offline no eliminará encuestas o archivos locales; será necesario autenticarse nuevamente online para continuar.
* **CL-010 — RESOLVED:** una nueva versión no podrá reemplazar la versión descargada mientras existan encuestas incompletas o pendientes de sincronización de la versión anterior.
* **CL-011 — RESOLVED:** una vez realizada la actualización, el dispositivo conservará solamente la última versión disponible del formulario.
* **CL-012 — RESOLVED:** las modificaciones de encuestas tendrán auditoría detallada con pregunta, valor anterior, valor nuevo, usuario y fecha/hora.
* **CL-013 — RESOLVED:** el Administrador podrá configurar la ubicación como obligatoria, opcional o no requerida.

---

## 25. Discovery Status

La visión inicial de Gera Forms define:

* el problema principal;
* el propósito del producto;
* los usuarios principales;
* los roles iniciales;
* el flujo principal;
* el funcionamiento esperado online y offline;
* las reglas principales de autenticación offline;
* descarga de formularios;
* sincronización;
* edición;
* auditoría;
* versionado;
* ubicación;
* archivos locales;
* restricciones iniciales de plataforma;
* límites principales de alcance;
* visión inicial del MVP.

Este documento permanece en estado **Draft — Pending Approval** hasta su aprobación explícita.

Una vez aprobado, servirá como entrada para la definición formal de Product Requirements, sin sustituir a `requirements.md`, User Stories, Feature Specifications ni otros artefactos autoritativos posteriores.
