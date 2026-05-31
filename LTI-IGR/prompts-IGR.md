# Prompts

## Prompt 1:

Agent: Claude Code - Sonnet 4.6

### Request:

Basándote en el fichero **casos-de-uso.md** que se encuentra dentro de "LTI-IGR/.claude/commands", quiero que generes un fichero similar pero para utilizarlo como generardor de user stories.

Te muestro un ejemplo de como quiero utilizar el nuevo **user-stories.md** que generes:

    /user-stories PRD: Como un residente que usa la bicicleta diariamente, quiero poder programar reservas recurrentes para asegurar mi transporte a la hora de ir al trabajo.

Y, deberá generar todas las user stories necesarias para cubrir la funcionalidad definida en un PRD (documento de requisitos de producto).

Punto importantes que debe cumplir una buena user story:

    1. Formato estándar

        Una user story sigue una estructura simple pero poderosa:

            "Como [tipo de usuario], quiero [acción/funcionalidad] para [beneficio/valor]"

    2. Genera el fichero en inglés.

    3. Cada user story que genere se deberá guardar en LTI-IGR/user-stories/[nombre-user-story]

    4. Cada user story deberá cumplir con los Criterios INVEST que son los siguientes:

        - I —> Independent (Independiente): Cada story debe poder desarrollarse y entregarse sin depender de otras. Esto permite flexibilidad en la priorización.

        - N —> Negotiable (Negociable): No es un contrato rígido. Los detalles de implementación se discuten entre el equipo y el Product Owner. La story define el "qué", no el "cómo".

        - V —> Valuable (Valiosa): Debe entregar valor real al usuario o al negocio. Si no puedes explicar por qué importa, probablemente no debería estar en el backlog.

        - E —> Estimable (Estimable): El equipo debe poder estimar el esfuerzo necesario. Si no pueden, la story necesita más refinamiento o ser dividida.

        - S —> Small (Pequeña): Suficientemente pequeña para completarse en un sprint (idealmente 2-4 días de trabajo). Si es demasiado grande, hay que dividirla.

        - T —> Testable (Testeable): Debe tener criterios claros de aceptación que permitan verificar si está "hecha" o no.

    5. Acceptance Criteria: el formato Given/When/Then:

        Los criterios de aceptación (Acceptance Criteria o AC) definen las condiciones que una story debe cumplir para considerarse completa. Sin AC claros, el desarrollador no sabe exactamente qué construir y QA no sabe qué testear.

        El formato más usado en la industria viene de Behavior-Driven Development (BDD) y usa la estructura Given/When/Then (también conocida como sintaxis Gherkin):

        Given (Dado): la precondición o estado inicial

        When (Cuando): la acción que el usuario realiza

        Then (Entonces): el resultado esperado

        Ejemplo para nuestra story de reservas recurrentes:

        Scenario 1: Programar reserva recurrente

        Given soy un usuario registrado con método de pago activo

        When configuro una reserva recurrente para lunes a viernes a las 7:30 AM en la estación "Plaza Mayor"

        Then el sistema crea reservas automáticas para cada día laborable y me envía una confirmación semanal

    6. Ejemplo práctico:

        PRD Básico
            Objetivo del Producto: Proveer una plataforma fácil de usar para que los usuarios puedan reservar y alquilar bicicletas en diferentes estaciones de la ciudad.

            Funcionalidades Principales:

            Reserva de bicicletas en estaciones seleccionadas.

            Sistema de pago integrado para procesar transacciones.

            Visualización de disponibilidad en tiempo real.

            Sistema de recomendaciones basado en IA para sugerir rutas y bicicletas según el perfil del usuario.

        Ejemplo de uso:

            **prompt**: Dado el objetivo de producto [...] y las funcionalidades principales [...], define los títulos de las historias de usuario principales siguiendo el formato estándar

            __Respuesta__

            Uso de IA para generar y enriquecer User Stories
            En este ejemplo se muestran diferentes prompts que ayudan a generar el backlog o enriquecer el contenido existente con IA.

            Prompt para generar User Stories sin contexto:

            Genera cinco user stories para un sistema de reservas de bicicletas considerando diferentes tipos de usuarios y sus necesidades

            Ejemplo de Respuesta:

                User Story 1: Turista Explorador

                Como un turista que visita la ciudad por primera vez, quiero reservar una bicicleta fácilmente desde mi smartphone para explorar los lugares turísticos recomendados.

                User Story 2: Residente Local

                Como un residente que usa la bicicleta diariamente, quiero poder programar reservas recurrentes para asegurar mi transporte a la hora de ir al trabajo.

                User Story 3: Usuario Ocasional

                Como alguien que usa bicicletas esporádicamente, deseo recibir notificaciones sobre la disponibilidad de bicicletas en mi área para decidir cuándo alquilar una.

                User Story 4: Usuario con Discapacidad

                Como una persona con discapacidad, necesito que la plataforma me muestre opciones de bicicletas adaptadas y estaciones de fácil acceso.

                User Story 5: Planificador Familiar

                Como padre que planea actividades familiares, quiero reservar múltiples bicicletas de diferentes tamaños y tipos en una sola transacción.

                Prompt para pasar de funcionalidades a User Stories, con el contexto del PRD:

                Dado el objetivo de producto [...] y las funcionalidades principales [...], define los títulos de las historias de usuario principales siguiendo el formato estándar

### Response:

    Se ha generado el comando "user-stories.md".

</br>

## Prompt 2:

Agent: Claude Code - Sonnet 4.6

### Request:

    @LTI-IGR/.claude/commands/user-stories.md El fichero README_PRD.md actúa como PRD con todos los links a la información necesaria que define las funcionalidades clave para crear un sistema ATS (Applicant-Tracking System). Define las user stories principales. Idioma para las user stories: inglés. La terminología debe ser acorde al sector ATS.

    Si tienes algunas dudas pregunta.

### Questions 1 - IA:

    How side should the "principal" user stories reach across the PRD?

        a) Three core funnel domains (Recommended)
        Cover the value loop that has detailed specs: Requisitions & Job Posting, Cnadidate Applciation & Screening, Interviews & Hire Decision. Aprox. 18-22 stories spanning P0 + the key P1 (AI matching, multi-board distribution, self-scheduling). This is what the PRD calls the 'core value loop'.

        b) Core funnel + Offeres & Analytics
        The three core domains plus the catalogued Offers (UC-OFF) and Analytics/Compliance (UC-AN) use cases. Aprox. 28-32 stories. Broader, but Offers/Analytics have no detailed spec yet (stories inferred from the catalog).

        c) Full MVP catalog
        Every P0/P1 use case in the master catalog including Auth & Access (UC-AUTH). Aprox. 40+ stories. Most exhaustive; many stories derived from on-line catalog entries with inferred actors/scenarios.

### Response to IA:

Elegida **opción a)**.

### Questions 2 - IA:

    Which priority levels should the stories cover?

        a) P0 + key P1 (Recommended)
        All must-have MVP stories plus the standout P1 differentiators (AI candidate-job matching, multi-board distribution, candidate self-scheduling). Best 'principal' coverage.

        b) PO only
        Strictly must-have-for-MVP stories. Tightest backlog; defers AI matching and board distribution to later.

        c) P0 + P1+ P2
        Everithing including post-MVP items (programmatic advertising, async video, calibration analytics). Largest backlog.

### Response to IA:

Elegida **opción b)**.

### Final Response:

    Se ha generado 22 user stories y, añadido en la carpeta LTI-IGR/user-stories.

</br>

## Prompt 3:

Agent: Claude Code - Sonnet 4.6

### Request:

Basándote en el fichero **casos-de-uso.md** que se encuentra dentro de "LTI-IGR/.claude/commands", quiero que generes un fichero similar pero para utilizarlo como generardor de un backlog.

Te muestro un ejemplo de como quiero utilizar el nuevo **backlog.md** que generes:

    /backlog Analiza las user stories existentes del sistema ATS (Applicant-Tracking Syste) y, que se encuentran en la carpeta [ruta y nombre de la caperta] y, genera un backlog.

Deberá generar un backlog priorizado que cumpla con los siguientes puntos:

    1. Genera el fichero en inglés.

    2. Factores para la Priorización del Backlog

        Valor del Negocio: Identificar las user stories y mejoras que aportan el mayor valor al negocio o a los usuarios finales. Esto incluye impacto en la retención de usuarios, atractivo para nuevos usuarios y potencial de ingresos.

        Urgencia: Determinar qué características son más urgentes en términos de necesidades del mercado o compromisos con los stakeholders.

        Dependencias: Reconocer y priorizar tareas que otras tareas dependen para su implementación. Esto asegura un flujo de trabajo lógico y eficiente.

        Coste de implementación: Considerar el esfuerzo, los recursos y el tiempo necesarios para cada tarea. Priorizar aquellas con la mejor relación costo-beneficio.

        Riesgos y obstáculos potenciales: Evaluar los riesgos asociados con cada user story o mejora y su impacto potencial en el proyecto.

        Feedback del usuario: Integrar las opiniones y preferencias de los usuarios, especialmente en áreas críticas de la interfaz de usuario y la experiencia del usuario.

        Madurez tecnológica: Considerar la madurez y la viabilidad de las soluciones tecnológicas propuestas para cada tarea.

    3. Proceso de priorización

        Revisión de Stakeholders: Involucrar a los stakeholders clave en el proceso de priorización para asegurar que el backlog refleje los objetivos del negocio.

        Sesiones de Priorización con el Equipo: Utilizar técnicas como Planning Poker o la matriz de Eisenhower para consensuar la importancia de cada tarea.

        Iteración y Reevaluación: El backlog debe ser dinámico, reevaluando y ajustando las prioridades regularmente a medida que avanza el proyecto y surgen nuevos datos.

    4. Cuando el comando sea llamado, el backlog que genere lo deberá guardar en LTI-IGR/backlog.md

### Response:

    Se ha generado el comando "backlog.md".

</br>

## Prompt 4:

Agent: Claude Code - Sonnet 4.6

### Request:

    @LTI-IGR/.claude/commands/backlog.md User stories en la carpeta "LTI-IGR/user-stories"

    Si tienes algunas dudas pregunta.

### Response:

    Se ha generado el fichero backlog.md y, añadido en la carpeta LTI-IGR.

</br>

## Prompt 5:

Agent: Claude Code - Sonnet 4.6

### Request:

Basándote en el fichero **casos-de-uso.md** que se encuentra dentro de "LTI-IGR/.claude/commands", quiero que generes un fichero similar pero para utilizarlo como generardor de tickets a partir de una user story. El comando que generes guardalo en la carpeta de LTI/IGR/.claude/commands.

Los tickets deberán cumplir los siguientes puntos:

    1. Genera el fichero en inglés.

    2. Un ticket de trabajo es una descripción detallada de una tarea que debe ser realizada. En Agile, estos suelen estar formateados como user stories, que incluyen detalles sobre el usuario, la necesidad y el resultado deseado.

    3. Los componentes mínimos de un ticket de trabajo son un título breve y descriptivo, detalles en profundidad sobre lo que necesita hacerse, la urgencia de la tarea en una escala de clasificación conocida, y una estimación del tiempo o esfuerzo requerido para completarla.

    4. Tipos de Tickets de trabajo
        Características (Features): Descripciones de funcionalidades que el producto debe tener. Vinculados directamente a historias de usuario

        Tareas Técnicas: Mejoras de infraestructura, refactoring de código, etc.

        Bugs/Errores: Problemas detectados o conocidos que necesitan resolverse.

        Mejoras: Sugerencias y mejoras basadas en el feedback del usuario.

        Investigación (spike): es un elemento del Product Backlog orientado a la investigación o experimentación, cuya finalidad es obtener el aprendizaje necesario para implementar la funcionalidad solicitada por el Product Owner o cliente. En estos casos, se suele dividir la user story en 2, una relativa a la investigación, y otra posterior relativa a la característica a implementar.

    5. Componentes de un Ticket de trabajo

        5.1. Título Claro y Conciso: Un resumen breve que refleje la esencia de la tarea. Debe ser lo suficientemente descriptivo para que cualquier miembro del equipo entienda rápidamente de qué se trata el tickect.

        5.2. Descripción Detallada:

            Propósito: Explicación de por qué es necesaria la tarea y qué problema resuelve.

            Detalles Específicos: Información adicional sobre requerimientos específicos, restricciones, o condiciones necesarias para la realización de la tarea.

        5.3. Criterios de Aceptación:

            Expectativas Claras: Lista detallada de condiciones que deben cumplirse para que el trabajo en el ticket se considere completado.

            Pruebas de Validación: Pasos o pruebas específicas que se deben realizar para verificar que la tarea se ha completado correctamente

        5.4. Prioridad:

            Nivel de Urgencia: Una clasificación de la importancia y la urgencia de la tarea, lo cual ayuda a determinar el orden en que deben ser abordadas las tareas dentro del backlog.

        5.5. Estimación de Esfuerzo:

            Puntos de Historia o Tiempo Estimado: Una evaluación del tiempo o esfuerzo que se espera que tome completar el ticket. Esto es esencial para la planificación y gestión del tiempo del equipo.

        5.6. Asignación:

            Responsable: Quién o qué equipo será responsable de completar la tarea. Esto asegura que todos los involucrados entiendan quién está a cargo de cada parte del proyecto.

        5.7. Etiquetas o Tags:

            Categorización: Etiquetas que ayudan a clasificar el ticket por tipo (bug, mejora, tarea, etc.), por características del producto (UI, backend, etc.), o por sprint/versión.

        5.8. Comentarios y Notas:

            Colaboración: Espacio para que los miembros del equipo agreguen información relevante, hagan preguntas, o proporcionen actualizaciones sobre el progreso de la tarea.

        5.9. Enlaces o Referencias:

            Documentación Relacionada: Enlaces a documentos, diseños, especificaciones o tickets relacionados que proporcionen contexto adicional o información necesaria para la ejecución de la tarea.

        5.10. Historial de Cambios:

            Rastreo de Modificaciones: Un registro de todos los cambios realizados en el ticket, incluyendo actualizaciones de estado, reasignaciones y modificaciones en los detalles o prioridades.

    6. Ejemplo de un Ticket de trabajo bien formulado:

        Un ticket de trabajo bien estructurado es crucial para la gestión eficiente de proyectos Agile. Debe proporcionar toda la información necesaria de manera clara y accesible para facilitar la ejecución de las tareas y la colaboración entre los miembros del equipo. Aquí te mostramos un ejemplo que puedes usar como referencia, e incluso usar como plantilla en tu asistente IA para estructurar la información de una manera estándar para tus proyectos:

        Título: Implementación de Autenticación de Dos Factores (2FA)

        Descripción: Añadir autenticación de dos factores para mejorar la seguridad del login de usuarios. Debe soportar aplicaciones de autenticación como Authenticator y mensajes SMS.

        Criterios de Aceptación:

            Los usuarios pueden seleccionar 2FA desde su perfil.

            Soporte para Google Authenticator y SMS.

            Los usuarios deben confirmar el dispositivo 2FA durante la configuración.

        Prioridad: Alta

        Estimación: 8 puntos de historia

        Asignado a: Equipo de Backend

        Etiquetas: Seguridad, Backend, Sprint 10

        Comentarios: Verificar la compatibilidad con la base de usuarios internacionales para el envío de SMS.

        Enlaces: Documento de Especificación de Requerimientos de Seguridad

        Historial de Cambios:

            15/01/2025: Creado por [nombre]

            20/01/2025: Prioridad actualizada a Alta por [nombre]

    7. Cuando el comando sea llamado, los tickets se guardarán en LTI-IGR/tickets/[carpeta con el nombre de la user-story]/[nombre-del-ticket].md

### Response:

    Se ha generado el comando "tickets.md".

</br>

## Prompt 6:

Agent: Claude Code - Sonnet 4.6

### Request:

    @LTI-IGR/.claude/commands/tickets.md Crear tickets para la user story "Configure the requisition approval chain". Ruta donde se ha definido: "LTI-IGR/user-stories/configure-approval-chain.md"

    Si tienes dudas que hay que resolver previamente, preguntamelas.

### Questions 1 - IA:

    Scenario 3 stores an SLA per step that 'drivers auto-escalation'. Should this story's tickets include the runtime escalation engine (timer/worker that fires when an approver doesn't act), or only persist the SLA config here and leave escalation enforcement to the approval-flow story (UC-REQ-02) / approve-or-reject-requisition)?

        a) Config only here (Recommended)
        Store SLA per step in this story; the runtime escalation worker is a separate ticket owned by UC-REQ-02. Keeps this story small and focused on configuration. I'll add a dependency note + a thin enabler ticket.

        b) Include full escalation engine
        Add ticket for the scheduler/worker, business-day calendar, and escalation notificaiton here. Larger story, more tickets, some overlap with the approval-flow story.

### Response to IA:

Elegida **opción a)**.

### Questions 2 - IA:

    Scenario 2 needs conditional steps (e.g., senior-level roles add an executive approver). How flexible should the conditional-rule capability be in these tickets?

        a) Predefined conditions (Recommended)
        Support a fixed set of attributes (level, salary band, cost center) with simple match rules. Estimable now, covers the acceptance criteria. No spike need.

        b) Flexible rule builder
        Generic condition/expression builder over arbitrary requisition fields. More powerful but unbounded - I'd add a Spike to scope it before the feature tickets.

### Response to IA:

Elegida **opción a)**.

### Final Response:

    Se han generado 7 tickets correspondientes a la user story "Configure the requisition approval chain" y, añadido en la carpeta LTI-IGR/tickets.

</br>

## Prompt 7:

Agent: Claude Code - Sonnet 4.6

### Request:

    Estima el esfuerzo de los tickets de trabajo usando la metodología (fibonacci, poker, tallas de camiseta) y unidades (horas, puntos de historia) que prefieras.

    Guarda las estimaciones en formato markdown dentro de la carpeta LTI-IGR/tickets/configure-approval-chain" con el nombre "estimate-effort.md".

    Utiliza el idioma: inglés

### Response:

    Se han generado el fichero estimate-effort.md.

</br>
