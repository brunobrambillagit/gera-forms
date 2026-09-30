# Gera Forms — Product Vision

**Status:** Draft  
**Revision:** 2  
**Lifecycle Phase:** 01 — Discovery  
**Milestone:** MVP  
**Previous approved baseline:** 2026-09-21  
**Last reviewed:** 2026-09-29  

---

# 1. Product Overview

Gera Forms es una plataforma para la creación, gestión, asignación, completado y consulta de formularios, diseñada para funcionar tanto con conexión a Internet como sin ella.

El producto busca reemplazar el uso actual de Google Forms en escenarios de relevamiento de campo donde los Encuestadores pueden encontrarse en lugares sin acceso a Internet o datos móviles.

Gera Forms deberá permitir que los Encuestadores continúen trabajando desde smartphones, tablets o computadoras aun cuando no exista conectividad, conservando localmente los formularios descargados, las encuestas realizadas, sus modificaciones y los archivos asociados.

Las encuestas podrán guardarse como borradores editables mientras se trabaja online u offline.

Cuando exista conectividad, el Encuestador podrá finalizar manualmente una encuesta individual o seleccionar múltiples encuestas para finalizarlas conjuntamente.

La finalización representa el envío definitivo de una encuesta al sistema central. Una encuesta enviada exitosamente dejará de ser editable por el Encuestador.

El funcionamiento offline constituye una capacidad central del producto y no una funcionalidad complementaria.

---

# 2. Problem

La organización realiza relevamientos mediante formularios en ubicaciones donde la conectividad a Internet puede ser inexistente, inestable o insuficiente.

El uso de herramientas que dependen de conectividad dificulta garantizar que un Encuestador pueda acceder a un formulario, completarlo y conservar el relevamiento cuando se encuentra sin conexión.

Además, determinados relevamientos pueden requerir registrar la ubicación en la que fueron realizados, recopilar archivos, fotografías, documentos u otra información durante el trabajo de campo.

Gera Forms busca resolver estos problemas mediante una plataforma preparada específicamente para operar online y offline, permitiendo almacenar temporalmente la información en el dispositivo y enviarla posteriormente al sistema central cuando exista conectividad.

---

# 3. Product Vision

Gera Forms deberá convertirse en una plataforma centralizada para la gestión de formularios, Encuestadores y resultados de una única organización.

La plataforma permitirá que usuarios Administradores:

* administren usuarios;
* creen y modifiquen usuarios;
* activen y desactiven usuarios;
* administren permisos;
* restablezcan contraseñas;
* creen formularios;
* guarden formularios como borrador;
* configuren sus preguntas;
* definan preguntas obligatorias u opcionales;
* publiquen versiones de formularios;
* habiliten formularios para uno, varios o todos los Encuestadores;
* deshabiliten formularios respetando el trabajo pendiente;
* consulten encuestas enviadas;
* consulten resultados;
* busquen y filtren resultados;
* consulten visualizaciones básicas;
* consulten información de auditoría cuando corresponda.

Los usuarios Encuestadores podrán utilizar Gera Forms desde smartphones Android o iPhone mediante una Progressive Web App (PWA), así como desde computadoras compatibles.

Los Encuestadores deberán poder descargar previamente los formularios habilitados para utilizarlos posteriormente tanto online como offline.

---

# 4. Target Organization

Gera Forms estará destinado inicialmente a una única organización.

No se requiere para el MVP soportar múltiples organizaciones independientes ni un modelo funcional multi-tenant.

Los usuarios, formularios, versiones, asignaciones, encuestas y resultados pertenecerán al mismo ámbito organizacional.

---

# 5. User Roles

Gera Forms tendrá dos roles funcionales iniciales:

1. Administrador.
2. Encuestador.

Los roles representan perfiles funcionales generales.

Adicionalmente, los usuarios podrán poseer permisos administrables dentro del ámbito permitido por el producto.

La definición técnica del modelo de autorización y permisos se realizará posteriormente.

## 5.1. Administrador

El Administrador será responsable de la gestión de la plataforma.

Entre sus capacidades esperadas se encuentran:

* crear usuarios;
* modificar usuarios;
* activar usuarios;
* desactivar usuarios;
* administrar permisos;
* restablecer contraseñas;
* crear formularios;
* guardar formularios como borrador;
* configurar preguntas;
* configurar posibles respuestas;
* configurar preguntas como obligatorias u opcionales;
* configurar opciones generales del formulario;
* publicar versiones de formularios;
* habilitar formularios para determinados Encuestadores;
* habilitar formularios para múltiples Encuestadores;
* habilitar formularios para todos los Encuestadores;
* deshabilitar asignaciones respetando encuestas pendientes;
* consultar encuestas enviadas;
* consultar resultados;
* utilizar filtros y búsqueda sobre los resultados;
* consultar visualizaciones básicas;
* consultar información de auditoría.

## 5.2. Encuestador

El Encuestador será responsable de realizar los relevamientos.

Deberá poder:

* autenticarse en Gera Forms;
* acceder a los formularios que tenga habilitados;
* descargar formularios al dispositivo;
* utilizar formularios descargados online u offline;
* iniciar encuestas;
* guardar encuestas como borradores;
* continuar encuestas posteriormente;
* modificar borradores;
* consultar el identificador y estado de sus encuestas;
* finalizar una encuesta cuando exista conectividad;
* seleccionar y finalizar conjuntamente múltiples encuestas cuando exista conectividad;
* consultar el estado de envío;
* reintentar envíos fallidos;
* conservar localmente archivos asociados a las encuestas;
* eliminar manualmente archivos locales cuando corresponda.

El Encuestador no podrá crear formularios ni administrar usuarios salvo que futuras decisiones de producto modifiquen expresamente esta regla.

---

# 6. User Management

Los usuarios de Gera Forms serán creados por usuarios Administradores.

No se contempla inicialmente el auto-registro.

Cada usuario deberá disponer como mínimo de:

* nombre completo;
* nombre de usuario;
* contraseña;
* rol;
* estado;
* correo electrónico;
* teléfono.

El Administrador podrá:

* crear usuarios;
* modificar sus datos;
* activar usuarios;
* desactivar usuarios;
* habilitar permisos;
* retirar permisos;
* restablecer contraseñas.

Los usuarios no podrán ser eliminados definitivamente mediante la administración funcional normal del producto.

Cuando un usuario deje de estar habilitado para operar, deberá ser desactivado.

La desactivación deberá preservar la información histórica asociada al usuario.

La definición técnica de credenciales, almacenamiento de contraseñas, sesiones y autorización será realizada posteriormente durante las fases correspondientes.

---

# 7. Form Creation

Los formularios serán creados exclusivamente por usuarios Administradores.

Un formulario podrá permanecer como borrador mientras está siendo preparado.

El Administrador podrá guardar y modificar un formulario borrador tantas veces como sea necesario sin generar una nueva versión por cada guardado.

Una nueva versión se generará únicamente mediante la acción de publicación.

La experiencia de creación deberá permitir definir preguntas utilizando diferentes tipos de respuesta.

Como referencia funcional inicial se consideran:

* texto simple;
* texto largo;
* selección de una opción;
* selección múltiple;
* teléfonos;
* correos electrónicos;
* observaciones;
* fotografías;
* documentos;
* archivos adjuntos;
* ubicación o dirección.

Cada pregunta deberá poder configurarse individualmente como:

* obligatoria; o
* opcional.

---

# 8. Form Assignment

Los formularios publicados podrán ser habilitados para usuarios Encuestadores.

Un formulario creado o publicado no deberá estar necesariamente disponible para todos los Encuestadores.

El Administrador deberá poder habilitar un formulario:

* para un Encuestador;
* para varios Encuestadores;
* para todos los Encuestadores.

La selección de todos los Encuestadores deberá poder realizarse mediante una acción equivalente a `Seleccionar todos los encuestadores`.

Un Encuestador deberá acceder únicamente a los formularios que tenga habilitados, salvo el tratamiento transitorio requerido por una desasignación con trabajo pendiente.

La asignación de un formulario no implica que este se encuentre descargado en el dispositivo del Encuestador.

Deberán distinguirse conceptualmente los siguientes estados:

* formulario existente;
* formulario borrador;
* formulario publicado;
* formulario habilitado para un Encuestador;
* formulario descargado en un dispositivo;
* formulario con desasignación pendiente por trabajo local existente.

---

# 9. Form Unassignment

El Administrador podrá retirar a un Encuestador la habilitación de un formulario.

Si el Encuestador no posee encuestas pendientes correspondientes a ese formulario, la desasignación podrá hacerse efectiva normalmente.

Si existen encuestas pendientes, la desasignación deberá quedar en un estado transitorio que preserve la posibilidad de completar y enviar el trabajo ya iniciado.

El formulario deberá permanecer disponible únicamente en la medida necesaria para resolver las encuestas pendientes existentes.

Cuando no queden encuestas pendientes asociadas a dicho formulario, la desasignación deberá hacerse efectiva y el formulario dejará de estar habilitado para el Encuestador.

La desasignación diferida no deberá provocar pérdida de encuestas, archivos ni información almacenada localmente.

Los criterios exactos sobre qué acciones permanecen habilitadas durante dicho estado transitorio serán definidos mediante User Stories y Acceptance Criteria.

---

# 10. Form Download

Antes de poder utilizar un formulario, el Encuestador deberá descargarlo explícitamente al dispositivo.

Esta descarga será requerida independientemente de si el Encuestador planea utilizar el formulario online u offline.

Incluso cuando exista conexión a Internet, el flujo normal requerirá que el formulario haya sido previamente descargado.

Un formulario que nunca haya sido descargado en el dispositivo no podrá utilizarse cuando el dispositivo se encuentre offline.

La descarga deberá permitir que el formulario quede disponible localmente para su utilización posterior.

---

# 11. Authentication and Offline Access

El primer inicio de sesión de un usuario en un dispositivo requerirá conexión con el servidor.

Una vez realizada correctamente una autenticación online, el usuario podrá continuar accediendo a Gera Forms desde ese dispositivo sin conexión durante un período máximo de 24 horas desde su último inicio de sesión online válido.

Si el usuario intenta acceder offline y no dispone de una autorización local válida correspondiente a una autenticación online previa, no podrá iniciar sesión.

Una vez vencido el período de 24 horas, será necesaria una nueva autenticación online antes de volver a utilizar Gera Forms.

La expiración de la autorización no deberá eliminar:

* formularios descargados;
* encuestas borrador;
* encuestas con errores de envío;
* archivos almacenados localmente;
* historial local asociado.

Si la autorización vence mientras existe trabajo pendiente, dicha información permanecerá almacenada localmente.

Cuando el usuario vuelva a autenticarse correctamente online, podrá continuar trabajando desde el estado en que había quedado.

La estrategia técnica utilizada para implementar autenticación y autorización offline será definida posteriormente durante Architecture.

---

# 12. Survey Completion

Los formularios serán completados por usuarios Encuestadores previamente registrados en Gera Forms.

No se contempla inicialmente que personas anónimas o usuarios externos completen formularios mediante enlaces públicos.

El Encuestador podrá utilizar los formularios descargados tanto online como offline.

Una encuesta podrá:

* iniciarse;
* guardarse como borrador;
* continuarse posteriormente;
* modificarse mientras permanezca como borrador;
* validarse;
* finalizarse cuando exista conexión;
* enviarse al sistema central;
* reintentarse si ocurre un error durante el envío.

Guardar y Finalizar son acciones funcionalmente diferentes.

`Guardar` deberá conservar el estado actual de la encuesta como borrador editable.

`Finalizar` deberá validar la encuesta y, cuando exista conectividad, iniciar su envío definitivo al sistema central.

La acción `Finalizar` no estará disponible para completar el envío cuando el dispositivo se encuentre sin conexión.

Una encuesta almacenada localmente deberá conservarse aunque se cierre Gera Forms, se pierda conectividad o venza la autorización offline del usuario.

---

# 13. Survey Identification

Cada encuesta deberá disponer de un identificador numérico visible que permita distinguirla de otras encuestas.

El identificador deberá poder ser consultado tanto por el Encuestador dentro de su ámbito de acceso como por el Administrador.

Además del identificador, la encuesta deberá conservar su relación con información contextual como:

* formulario;
* versión;
* Encuestador;
* fecha;
* estado;
* respuestas.

La estrategia técnica utilizada para generar el identificador se definirá posteriormente.

---

# 14. Survey Editing and Audit

Mientras una encuesta permanezca como borrador y no haya sido enviada exitosamente, podrá ser modificada por el Encuestador.

Las modificaciones deberán quedar registradas mediante una auditoría detallada.

Como mínimo, la auditoría deberá permitir identificar:

* pregunta modificada;
* valor anterior;
* valor nuevo;
* usuario que realizó la modificación;
* fecha y hora de la modificación.

Una vez que una encuesta haya sido enviada exitosamente al sistema central mediante `Finalizar` o `Finalizar todos`, dejará de ser editable por el Encuestador.

La información de auditoría deberá poder ser consultada por usuarios Administradores.

El acceso del propio Encuestador a su información de auditoría permanece como una capacidad de menor prioridad y será determinado por el alcance del MVP.

---

# 15. Manual Finalization and Submission

El envío de encuestas no será automático.

El Encuestador deberá iniciar explícitamente el envío.

La plataforma deberá ofrecer acciones funcionalmente equivalentes a:

* `Finalizar`;
* `Finalizar todos`.

`Finalizar` deberá operar sobre una encuesta individual.

`Finalizar todos` deberá permitir al Encuestador seleccionar manualmente qué encuestas desea enviar conjuntamente.

Solo podrán enviarse encuestas que satisfagan las validaciones requeridas por su formulario.

Una encuesta seleccionada que no cumpla las validaciones deberá requerir corrección antes de poder ser enviada.

La existencia de una encuesta inválida no deberá impedir el envío de otras encuestas seleccionadas que sí sean válidas.

Las encuestas no seleccionadas deberán permanecer como borradores sin modificaciones.

Tanto `Finalizar` como `Finalizar todos` requerirán conectividad.

Cada encuesta deberá permitir identificar claramente su estado de envío/sincronización.

Los estados funcionales iniciales serán:

* `Pendiente de sincronización`;
* `Sincronizando`;
* `Sincronizado`;
* `Error de sincronización`.

Una encuesta solo deberá considerarse sincronizada cuando su envío haya finalizado exitosamente.

Una encuesta con error de sincronización deberá conservarse localmente para permitir un intento posterior.

---

# 16. Form Versioning

Los formularios publicados tendrán versiones.

El Administrador podrá modificar el formulario para preparar su siguiente versión.

Estas modificaciones deberán formar parte del estado de trabajo o borrador del formulario y no deberán modificar retroactivamente la versión ya publicada.

Cada nueva acción `Publicar formulario` deberá generar una nueva versión.

Conceptualmente:

* Formulario A — v1;
* modificaciones preparatorias;
* Publicar formulario;
* Formulario A — v2;
* modificaciones preparatorias;
* Publicar formulario;
* Formulario A — v3.

Cada versión publicada deberá tratarse como una versión única e inmutable para efectos de las encuestas recopiladas con ella, manteniendo la relación con el formulario y sus versiones anteriores.

Las respuestas recopiladas deberán permanecer asociadas a la versión exacta utilizada para realizar la encuesta.

La publicación de una nueva versión no deberá modificar la estructura ni la interpretación de las encuestas recopiladas con versiones anteriores.

---

# 17. Form Version Update

Un Encuestador podrá continuar utilizando una versión descargada aunque exista una versión más reciente disponible mientras existan encuestas pendientes correspondientes a la versión anterior.

Cuando exista una versión nueva, Gera Forms deberá informar al Encuestador que existe una actualización disponible.

El Encuestador no podrá actualizar a la nueva versión mientras existan encuestas borrador o encuestas que todavía no hayan sido enviadas exitosamente correspondientes a la versión anterior.

Una vez resuelto todo el trabajo pendiente de la versión anterior, podrá realizarse la actualización a la versión más reciente.

El dispositivo deberá conservar solamente la última versión operativa del formulario una vez completado correctamente el proceso de actualización.

Las respuestas históricas permanecerán asociadas en el servidor a la versión con la que fueron recopiladas.

---

# 18. Location Capture

Cada formulario permitirá que el Administrador configure el tratamiento de la ubicación.

Las opciones serán:

* `Ubicación obligatoria`;
* `Ubicación opcional`;
* `Sin ubicación`.

Cuando corresponda registrar una ubicación, Gera Forms deberá contemplar:

1. obtener la ubicación desde los servicios de ubicación del dispositivo;
2. ingresar manualmente una dirección;
3. seleccionar manualmente una ubicación mediante un mapa.

Cuando la ubicación sea obligatoria, la encuesta deberá cumplir las reglas de ubicación correspondientes antes de poder finalizarse.

Cuando sea opcional, el Encuestador podrá finalizar la encuesta sin proporcionar ubicación.

Cuando el formulario esté configurado como `Sin ubicación`, no será necesario recopilar información de ubicación.

Las reglas técnicas de GPS, mapas, geocodificación y disponibilidad offline serán definidas posteriormente.

---

# 19. Offline Files and Attachments

Gera Forms deberá permitir utilizar archivos adjuntos durante el trabajo offline.

Esto podrá incluir:

* fotografías;
* documentos;
* otros archivos admitidos por el formulario.

Los archivos deberán poder almacenarse localmente junto con la encuesta correspondiente mientras no exista conectividad.

Cuando el Encuestador finalice una encuesta, los archivos asociados deberán formar parte de la información a enviar cuando corresponda.

Un envío exitoso no eliminará automáticamente los archivos almacenados localmente.

Los archivos permanecerán en el dispositivo hasta que el Encuestador decida eliminarlos manualmente.

La eliminación de la copia local de un archivo ya enviado correctamente no deberá eliminar la copia almacenada en el sistema central.

Las políticas técnicas de almacenamiento, límites de tamaño, formatos admitidos, seguridad y gestión del espacio local serán definidas posteriormente.

---

# 20. Results

El Administrador deberá poder consultar las encuestas enviadas exitosamente.

Como mínimo, la consulta deberá permitir identificar:

* identificador de encuesta;
* formulario;
* versión;
* Encuestador;
* fecha;
* estado;
* respuestas.

La consulta deberá incorporar capacidades de:

* búsqueda;
* filtros.

Además, Gera Forms deberá proporcionar una visualización básica mediante gráfico de torta para respuestas categóricas cuya naturaleza permita este tipo de agregación.

No se requiere que respuestas de texto libre, archivos, fotografías, documentos, ubicaciones u otros datos no categóricos sean representados mediante gráfico de torta.

Las estadísticas avanzadas y visualizaciones adicionales permanecen como evolución futura.

---

# 21. Data Collected

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

Las políticas técnicas y organizacionales concretas correspondientes serán definidas en fases posteriores y no deberán inferirse durante esta fase.

---

# 22. Primary Workflow

El flujo principal esperado de Gera Forms será:

1. un Administrador accede a Gera Forms;
2. crea o administra los usuarios necesarios;
3. crea un formulario;
4. guarda y modifica el formulario como borrador;
5. configura preguntas, respuestas y obligatoriedad;
6. configura el comportamiento de ubicación;
7. publica una versión del formulario;
8. habilita el formulario para uno, varios o todos los Encuestadores;
9. un Encuestador se autentica en Gera Forms;
10. visualiza los formularios que tiene habilitados;
11. selecciona y descarga los formularios que necesita utilizar;
12. realiza relevamientos online u offline;
13. las encuestas se almacenan localmente como borradores;
14. puede guardar y continuar encuestas posteriormente;
15. puede modificar borradores;
16. las modificaciones quedan registradas mediante auditoría;
17. cuando existe conectividad, puede utilizar `Finalizar` para validar y enviar una encuesta;
18. alternativamente puede utilizar `Finalizar todos`, seleccionar manualmente múltiples encuestas y enviar las que cumplan las validaciones;
19. Gera Forms informa el estado de cada envío;
20. una encuesta enviada exitosamente queda bloqueada para edición;
21. una encuesta con error conserva sus datos para permitir reintento;
22. el Administrador puede consultar los resultados recibidos;
23. puede buscar, filtrar y consultar visualizaciones básicas;
24. si existe una nueva versión del formulario, el Encuestador deberá resolver los pendientes de la versión anterior antes de actualizarla;
25. si una asignación fue retirada mientras existía trabajo pendiente, el formulario permanecerá transitoriamente disponible hasta resolver dicho trabajo y luego quedará deshabilitado.

Este flujo representa el valor principal que deberá demostrar el MVP.

---

# 23. MVP Vision

El MVP deberá demostrar de punta a punta el flujo principal de Gera Forms.

Como mínimo, deberá permitir demostrar:

* existencia de los roles Administrador y Encuestador;
* creación y administración de usuarios;
* activación y desactivación de usuarios;
* administración de permisos;
* restablecimiento de contraseñas;
* autenticación de usuarios;
* acceso offline durante el período autorizado;
* creación de formularios;
* guardado de formularios como borrador;
* configuración de preguntas obligatorias u opcionales;
* utilización de distintos tipos básicos de preguntas;
* configuración de ubicación;
* publicación y versionado de formularios;
* asignación a uno, varios o todos los Encuestadores;
* desasignación diferida cuando exista trabajo pendiente;
* descarga explícita de formularios;
* utilización de formularios descargados online y offline;
* almacenamiento local de encuestas;
* identificación visible de encuestas;
* posibilidad de guardar y continuar encuestas;
* edición de borradores;
* auditoría detallada de modificaciones;
* almacenamiento local de archivos;
* finalización manual de una encuesta;
* selección y finalización conjunta de múltiples encuestas;
* validación previa al envío;
* visualización de estados de envío;
* conservación de información ante errores;
* reintento de envíos fallidos;
* bloqueo de edición luego de un envío exitoso;
* consulta de resultados por parte del Administrador;
* búsqueda y filtros;
* gráfico de torta simple para respuestas categóricas compatibles;
* coexistencia correcta de resultados correspondientes a distintas versiones;
* actualización controlada de versiones descargadas.

La clasificación definitiva del alcance del MVP será formalizada durante `04 — MVP Scope`.

---

# 24. Deployment and Platform Constraints

Gera Forms deberá implementarse como una Progressive Web App.

Deberá poder utilizarse desde:

* smartphones Android;
* iPhone;
* computadoras compatibles.

La infraestructura central destinada a las APIs de gestión de usuarios, formularios, envío de encuestas y demás capacidades centralizadas deberá poder alojarse en una VPS.

El uso de contenedores Docker constituye una alternativa prevista, pero su adopción definitiva será determinada durante Architecture.

No se requieren actualmente integraciones de negocio con sistemas externos.

Las tecnologías específicas de frontend, backend, base de datos, almacenamiento, autenticación, sincronización y despliegue no forman parte de esta visión y serán definidas posteriormente.

---

# 25. Future Product Direction

Más allá del MVP, Gera Forms podrá evolucionar hacia una plataforma más amplia de gestión de formularios, Encuestadores y resultados.

Entre las capacidades futuras identificadas se encuentran:

* exportación de resultados a CSV;
* exportación de resultados a XLSX;
* estadísticas avanzadas;
* visualizaciones y gráficos adicionales;
* capacidades analíticas construidas sobre los resultados;
* nuevas integraciones;
* evolución del modelo organizacional cuando exista una necesidad concreta.

El gráfico de torta simple definido para determinadas respuestas categóricas forma parte de la capacidad inicial de consulta y no deberá confundirse con el módulo futuro de estadísticas y visualizaciones avanzadas.

---

# 26. Explicit Initial Scope Exclusions

No forman parte del alcance inicial:

* formularios públicos anónimos;
* auto-registro de usuarios;
* eliminación funcional definitiva de usuarios;
* múltiples organizaciones independientes;
* arquitectura funcional multi-tenant;
* aplicaciones móviles nativas específicas para Android;
* aplicaciones móviles nativas específicas para iOS;
* envío automático de encuestas;
* integraciones de negocio obligatorias con sistemas externos;
* estadísticas avanzadas;
* dashboards analíticos avanzados.

Estas exclusiones podrán reconsiderarse posteriormente mediante el proceso formal de cambio.

---

# 27. Revision 2 Decisions

Esta revisión incorpora las decisiones funcionales tomadas durante la preparación de User Stories:

* CL-014 — Administración de usuarios.
* CL-015 — Datos del usuario.
* CL-016 — Asignación de formularios.
* CL-017 — Desasignación diferida.
* CL-018 — Borradores de formulario.
* CL-019 — Preparación de una nueva versión.
* CL-020 — Preguntas obligatorias u opcionales.
* CL-021 — Guardar y Finalizar.
* CL-022 — Identificación de encuestas.
* CL-023 — Consulta de resultados.
* CL-024 — Relación entre Guardar, Finalizar y Finalizar todos.
* CL-025 — Selección manual en Finalizar todos.

Las decisiones anteriores complementan y, cuando existe contradicción, sustituyen el comportamiento correspondiente de la baseline aprobada el 2026-09-21.

---

# 28. Approval Status

**Status:** Draft  
**Revision:** 2  
**Previous approved baseline:** 2026-09-21  
**Revision 2 approval:** Pending  

Esta revisión todavía no constituye una nueva línea base aprobada.

La aprobación de Revision 2 deberá realizarse explícitamente antes de utilizarla como fuente autoritativa definitiva para User Stories y Acceptance Criteria.

La aprobación de este documento no autoriza implementación ni selección de arquitectura.

---

**End of vision.md — Revision 2**