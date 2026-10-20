# Workshop interno MoC (21-oct-2026): preguntas abiertas

**Objetivo:** cerrar **qué queremos** antes de hablar con Intelex del **cómo** (como pidió Shaun el 20-oct).

**Referencia que manda:** `MOC Proposal.xlsx` (Sam). Cada pregunta indica su origen para saber si es una decisión nuestra o una propuesta del BA.

**Leyenda de origen:**
- **[SAM]**: fichero MOC Proposal.
- **[20-oct]**: pre-design interno.
- **[19-oct]**: App Overview con Intelex.
- **[BRD]**: BO-61 v2.0, B.3.
- **[BA]**: propuesta de Rodrigo / Claude, no pedida por nadie, a validar.

---

## A. Aprobaciones (núcleo del diseño)

1. **Cadena para un Major:** ¿Local → Regional → Global, o Local → Global? El fichero de Sam da el nivel por grado, pero no si los niveles son acumulativos. Khesar habló de verificación local "antes de escalar a regional y hasta Shaun / Stylianos". **[SAM] [20-oct]**
2. **¿Cuántos aprobadores hay en cada nivel?** Sam indica "Local Approval – TM", pero ¿es solo el TM? El procedimiento actual y el BRD exigen un mínimo de 2 en los niveles bajos y 3 en el más alto. **[SAM] [BRD]**
3. **Secuencia:** ¿el siguiente nivel se lanza solo cuando el anterior ha aprobado? Se acordó así el 20-oct. ¿Lo confirmamos como requisito duro para Intelex? **[20-oct] [19-oct]**
4. **Aprobadores adicionales:** ¿cualquier MOC Coordinator puede añadir aprobadores ad hoc (por ejemplo, el GM de un país en un nivel 1)? **[20-oct]**
5. **Rechazo frente a devolución:** cuando un aprobador devuelve el MOC para corregirlo, ¿se conservan las aprobaciones ya dadas? Hoy, un rechazo anula todas. **[BRD]**

## B. Clasificación del cambio

6. ¿Damos por buena la matriz tipo × grado del fichero de Sam, en la última versión que haya circulado? ¿Cuándo la revisa Shaun con Stylianos? **[SAM] [20-oct]**
7. **¿Un MOC puede tener varios tipos de cambio?** Alonso propuso una pregunta Sí/No por cada tipo, con su grado (lo que implica varios tipos). El diseño actual es un desplegable de un solo tipo. Si hay varios, ¿manda el de mayor grado? **[20-oct]**
8. **Lista de "Automatic Major":** aterrizaje de techo flotante, entrada a tanque y equipos críticos de seguridad están en el fichero de Sam. ¿Añadimos la sobrecapacidad de granel seco (Shaun, "maybe") y los equipos críticos fuera de servicio (Khesar)? **[SAM] [20-oct]**

## C. Workflow

9. ¿Confirmamos las 6 etapas del fichero de Sam y que la emergencia vaya de Initiation a Approval? **[SAM]**
10. **Emergencia:** ¿se completa el dossier a posteriori? ¿En cuántos días? Shaun quiere "simple, solo documentar la aprobación". El BRD pide una regularización retrospectiva. **[20-oct] [BRD]**
11. **Workflow simplificado** (cambios organizativos o de IT): ¿lo pedimos para esta fase o primero cerramos el completo, como dijo Shaun? ¿Reutilizamos **Replacement in Kind** (renombrado como "Simplified MOC?") como interruptor? Ya trae un camino que salta etapas, así que no haría falta un workflow nuevo. Mientras se decide, no se elimina: está **en espera** en el workbook. **[20-oct] [19-oct] [BRD]**

> El Excel `Impala - MoC Workshop Interno 21-oct - Preguntas.xlsx` es la versión de trabajo de esta lista. Para cada pregunta incluye por qué se pregunta, la pregunta en inglés, las opciones y columnas para anotar la respuesta.
12. **Plazos (SLA) por etapa:** ¿cuántos días en Evaluation, Design & Analysis y en Approval? El estándar no trae ninguno; la propuesta es 30 y 14 días. **[19-oct] [BA]**
13. **Bloqueos entre etapas:** ¿se puede pasar a Approval con preguntas del checklist sin responder o con tareas abiertas? Intelex avisó de que el estándar no obliga a nada. **[19-oct]**

## D. Checklist (screening questions)

14. ¿El checklist cambia según el grado (Minor corto, Major completo)? ¿O solo según el segmento (Universal + Liquids/Dry)? Sam dijo que "puede complicarse". **[20-oct]**
15. ¿Las respuestas son Sí / No / N/A? El estándar trae solo Sí/No. **[BRD] [BA]**
16. ¿Los checklists por site quedan para la fase 2, y mientras tanto se usan acciones con su checklist local adjunto? **[20-oct]**

## E. Tareas frente a Action Plans

17. **¿Para qué queremos Action Plans si el MOC ya tiene tareas?** **[19-oct] [20-oct]**
    - **Tareas MOC:** viven dentro del MOC, **bloquean el avance de etapa** y solo se ven en la app de MoC.
    - **Action Plans:** el módulo global de acciones, el mismo que usan Incidentes y Observaciones (bandeja única "mis acciones", reporting de acciones abiertas). Hoy no tienen vínculo con el MOC.
    - **Lo que se dijo el 20-oct:** Alonso quiere poder trazar una acción hasta su MOC. Sam prefiere "alinearlo con los demás módulos". No se cerró si las acciones **sustituyen** a las tareas o las **complementan**.
    - **Propuesta BA a debatir:**
      - Tareas para lo que bloquea etapa: HAZOP, PSSR, formación previa al arranque.
      - Action Plans solo para acciones que no bloquean (post-arranque, permisos o licencias locales, hallazgos de la verificación).
      - Así se evita duplicar mecanismos.

## F. Roles, seguridad y notificaciones

18. ¿Quién es el MOC Coordinator en cada terminal: el HSE del terminal? Intelex exige al menos uno en la jerarquía o no deja crear MOCs. **[19-oct]**
19. Nombres de los aprobadores regionales y globales (HSEC y Operaciones) por región. **[SAM]**
20. **Notificaciones nuevas:** aviso de emergencia, de temporal a punto de caducar y de tareas o aprobaciones vencidas. ¿Las queremos? ¿A quién se escala y en cuántos días? Nadie las pidió explícitamente: son propuesta BA, apoyada en el SOW (que incluye "notifications and reminders") y en el BRD (temporales y vencidos). **[BA] [BRD]**
21. ¿Duración máxima de un temporal (el estándar trae 180 días) y número máximo de extensiones (el BRD dice 3)? **[BRD]**
22. ¿Quitamos el permiso de borrar al Person Responsible, por trazabilidad? **[BA]**

## G. Campos del BRD (confirmar si los queremos en esta fase)

23. Change Owner y Operational Owner, motivo y base técnica (texto largo), equipo afectado, plan de implementación, personas afectadas y las 3 verificaciones post-MoC (campo, comunicación, impactos). Son requisitos Must del BRD, pero no estaban en el fichero de Sam. ¿Entran todos o alguno sobra? **[BRD]**
