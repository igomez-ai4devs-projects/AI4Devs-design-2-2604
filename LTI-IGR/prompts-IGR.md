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

</br>

### Response:

    Se ha generado el comando "backlog.md".

</br>

## Prompt 2:

Agent: Claude Code - Sonnet 4.6

### Request:

    @LTI-IGR/.claude/commands/backlog.md User stories en la carpeta "LTI-IGR/user-stories"

    Si tienes algunas dudas pregunta.

### Final Response:

    Se ha generado el fichero backlog.md y, añadido en la carpeta LTI-IGR.
