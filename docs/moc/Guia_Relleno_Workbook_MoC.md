# Guía de relleno: Configuration Workbook de Management of Change (Intelex)

**Proyecto:** implantación de Intelex en Impala
**Documento base:** `Impala - Configuration Workbook - Management of Change v1 (baseline Intelex).xlsx`
**Aplicación:** Management of Change 1.3.0, sobre la plataforma 6.6.6.2
**Rol:** Senior Business Analyst de Impala

---

## 0. Estado actual: v1.2 rellenada con requisitos de Impala (20-oct-2026)

**Archivos en `docs/moc/`:**

| Archivo | Qué es |
|---|---|
| `... v1 (baseline Intelex).xlsx` | El original de Intelex, sin tocar |
| `... v1.2 (Impala requirements DRAFT).xlsx` | **El workbook relleno**: cambios A/R/M resaltados en amarillo y una columna "Impala Notes" en cada hoja |
| `Impala - MOC Screening Questions - Data Load Draft.xlsx` | 79 screening questions (67 Universal + 9 Liquids + 3 Dry) en formato del objeto Screening Question Setup |

**Fuentes:**
- SOW v1.5.
- App Overview con Intelex (19-oct).
- Pre-design interno de Impala (20-oct).
- `MOC Proposal.xlsx` (workflow propuesto, matriz Change Impact y checklist).

### Diseño volcado en el workbook

| Tema | Decisión / requisito | Estado |
|---|---|---|
| Workflow | Initiation → **Evaluation, Design & Analysis** → **Approval** → Implementation → Start Up → Follow Up. Se elimina Pre-Approval; Emergency va directo a Approval. | Decidido por Impala; Intelex debe confirmar alcance |
| Replacement in Kind | Se elimina el campo y el camino. Un cambio "like-for-like" no es un cambio según el procedimiento. | Decidido |
| Clasificación | Type of Change (8 tipos, reutilizando el objeto MOC Category) × Grade (Minor/Moderate/Major, que es la lista Change Impact). Sustituye el scoring de Level 1–5. Lista de "Automatic Major". | Propuesto; falta el OK de Global HSE |
| Aprobaciones | Minor: TM. Moderate: TM → Regional HSEC + Ops. Major: TM → Regional → Global HSEC + Ops. **Secuenciales.** Se reutilizan los 6 objetos de aprobación renombrados. | Intelex debe proponer la solución |
| Location Roles | MOC Coordinator, Terminal Manager, Regional HSEC, Regional Ops, Global HSEC, Global Ops. Las variaciones locales se resuelven asignando roles, no cambiando el workflow. | Falta nominar personas |
| Checklist | Universal en la ubicación raíz, Liquids y Dry en sus segmentos. Carga por Excel. Los checklists por site quedan para la fase 2. | Draft en revisión (Sam) |
| Campos nuevos | Grade Guidance por tipo (hide/show), Automatic Major, Emergency Justification, SCE afectado y tag, Approval Level (calculado), Approval Notes, Actual Implementation Date, grid de Action Plans. | Propuesto |
| Notificaciones | N06/N07 corregidas; nuevas N11 (Emergency), N12 (Temporary expiry), N13/N14 (vencimientos). Escalado definido en Notification Schedules. | SLA pendientes |

### Riesgo principal: alcance frente al SOW

El SOW describe el MoC como *"Standard Workflow – No modifications"*, pero también incluye *"Moderate configurations"*. Esta segunda categoría permite *"minor modifications to workflow stages"*, campos con hide/show y cálculos básicos.

- **Debería caber en Moderate:** quitar, fusionar o reordenar etapas, Type × Grade, guías con hide/show y Approval Level calculado.
- **Puede acabar en Change Order:** las aprobaciones secuenciales y las validaciones nuevas (AH13–AH15).

Recomendación: presentarlo en el workshop del 27-oct como configuración Moderate y que sea Intelex quien argumente lo contrario. Si hay que recortar, la alternativa a las aprobaciones secuenciales es que el MOC Coordinator envíe el siguiente nivel manualmente, aunque eso depende de la disciplina de cada usuario.

### Pendiente antes de firmar

1. OK de Global HSE (Stylianos) a la clasificación Type × Grade y a la lista de Automatic Major.
2. Que Intelex confirme: la solución de aprobaciones secuenciales, el vínculo con Action Plans, el workflow simplificado (¿está en el SOW?) y la plantilla de importación de screening questions.
3. Que Impala defina los SLA por etapa, nomine las personas por rol y decida si se reduce el checklist según el grade.

---

## 1. Qué es el workbook y cómo se trabaja

El workbook **no es una plantilla en blanco**. Es la configuración estándar (OOTB) de la app MoC de Intelex, ya documentada hoja por hoja. Nuestro trabajo como Impala es:

1. **Validar** lo que nos vale tal cual.
2. **Marcar los cambios**: añadir, quitar o modificar campos, etapas, roles, notificaciones y permisos.
3. **Registrar cada decisión** en `Decisions & Tasks`.

Intelex configura **exactamente lo que diga el workbook firmado**. Lo que no esté escrito no se construye, y un cambio después de la firma suele ser un change request.

### Reglas de edición (para no romper el archivo)

| Regla | Detalle |
|---|---|
| No tocar las hojas ocultas | `ILX Fields`, `ILX Hidden` y `Action Handlers` son internas de Intelex. `ILX Hidden` alimenta los desplegables. |
| Insertar filas **dentro** de las tablas | Cada bloque es una tabla de Excel. Si añades filas fuera de la tabla se pierden la validación y los subtotales. |
| Columna `Add / Remove` (Fields) | Usar solo el desplegable: **A** = añadir, **R** = quitar, **M** = modificar. Si la fila queda vacía, se acepta el estándar. |
| Columnas Y/N | Usar solo el desplegable `Y` / `N`. |
| No borrar filas del estándar | Si un campo sobra, se marca con **R** y no se borra. Así Intelex ve el delta. |
| Texto en inglés | Captions, emails e instrucciones van en el idioma de la UI que se acuerde. Si hay usuarios en español, decidir si se usa la localización de Intelex (ver §5). |
| Control de versiones | Cada entrega va con una fila nueva en `Cover Sheet` (v1.2, v1.3…), con quién la preparó, la revisó y la aprobó. |

---

## 2. Orden recomendado de relleno

El orden importa porque las hojas dependen unas de otras:

```
1. Workflow ─┬─> 2. Location Roles ─> 3. Security ─> 4. Application Tabs
             ├─> 5. Lookup Values ─> 6. Fields
             └─> 7. Notification Templates ─> 8. Notification Schedules
9. Object Model / Action Handlers (solo revisar)   10. Decisions & Tasks (todo el tiempo)   11. Cover Sheet (al cerrar)
```

**El workflow manda.** Si se cambian las etapas, cambian también las columnas de Mandatory y Read Only en Fields, los triggers de los emails y los Location Roles.

---

## 3. Hoja por hoja: qué hay y qué tiene que decidir Impala

### 3.1 Cover Sheet
- **Qué hay:** índice e historial de versiones (v1 y v1.1 de Intelex).
- **Qué hacemos:** añadir la fila `1.2 | fecha | <BA Impala> | "Requisitos Impala – ronda 1" | Reviewed: HSE Lead | Approved: Process Owner MoC`.

### 3.2 Decisions & Tasks
- **Qué hay:** dos defectos conocidos que Intelex ya registró:
  - `Change Expiry` no se limpia al volver `Temporary Change` a No.
  - Los campos de aprobación no se limpian al alternar `Accept Approval Task`.
- **Qué hacemos:**
  - Poner owner y fecha en esos dos defectos (owner: Intelex).
  - Añadir cada decisión de diseño de Impala: una por fila, con la decisión (no con la discusión) y con owner.
- **Decisiones iniciales que propongo abrir:** ver §6.

### 3.3 Workflow (MOC, MOC Task, MOC Approval)

**MOC: 7 etapas**

| # | Etapa | Owner |
|---|---|---|
| 1 | Initiation | Creador |
| 2 | Pre-Approval | MOC Coordinator |
| 3 | Evaluation | MOC Coordinator |
| 4 | Design & Analysis | MOC Coordinator |
| 5 | Implementation | MOC Coordinator |
| 6 | Start-Up | MOC Coordinator |
| 7 | Follow-Up | MOC Coordinator |

**Atajos de flujo:**
- `Replacement in Kind = Yes` → salta de Pre-Approval a Implementation.
- `Emergency Change = Yes` → salta de Pre-Approval a Design & Analysis.

**MOC Task y MOC Approval:** Draft → In Progress → Closed, o Rejected (vuelve a Draft).

**Qué tiene que decidir Impala (columnas D a I):**
1. **¿Sirven las 7 etapas?** Muchas organizaciones de HSE fusionan Start-Up y Follow-Up, o añaden una etapa de **Aprobación final / Autorización** antes de Implementation. Cada etapa nueva o eliminada se lleva a Fields y Notifications.
2. **Stage Owner por etapa.** El estándar pone al MOC Coordinator en todas. Lo habitual en Impala sería:
   - Pre-Approval: Responsable de área o Site Manager.
   - Evaluation y Design: MOC Coordinator.
   - Implementation: Responsable de ejecución.
   - Follow-Up: HSE.
3. **Due dates por etapa.** Hoy están todas en N/A. Recomiendo poner un SLA por etapa (por ejemplo, Pre-Approval en 5 días) para que puedan funcionar las escalaciones.
4. **Reglas de bloqueo.** El estándar no deja avanzar con tareas o aprobaciones abiertas. Hay que confirmar si aplica también a Emergency (lo habitual es permitir la regularización a posteriori).
5. **Emergency Change.** Definir el plazo máximo para la regularización documental y quién autoriza.
6. **Temporary Change.** El máximo es de 180 días (AH02/AH03). Validar ese plazo con la política de Impala.

**Cómo escribirlo:** se modifican las celdas de la tabla de etapas. El diagrama (imagen) lo regenera Intelex.

### 3.4 Location Roles
- **Qué hay:** un solo rol, `MOC Coordinator` (de grupo, que baja por la jerarquía y se usa como Workflow Task).
- **Qué hacemos:** añadir un rol por cada actor que reciba tareas o emails por ubicación. Propuesta inicial, a validar:

| Rol | Individual / Grupo | Roll down | Uso |
|---|---|---|---|
| MOC Coordinator | Group | Y | Workflow Task |
| Site / Terminal Manager | Individual | N | Workflow Task (aprobación) |
| HSE Manager | Individual | Y | Workflow Task + Location-Based Notification |
| Engineering / Maintenance Lead | Group | Y | Workflow Task |
| MOC Notification List | Group | Y | Location-Based Notification |

- **Dependencia:** cada rol necesita la estructura de **Location Hierarchy** ya cargada y personas nominadas por ubicación (data load).

### 3.5 Lookup Values
- **Qué hay:** L01 a L07 (Priority, Task Type, Stages, Change Impact, Task Children, Approval Type).
- **Qué hacemos:**
  - **Tipos de aprobación (L07) y de tarea (L02):** el estándar trae Environment, Safety, Engineering, Risk Management, Financial y Start Up. Confirmar si Impala necesita otros, por ejemplo *Operations*, *Legal/Permitting*, *IT/OT*, *Security* o *Customer*. Cada tipo nuevo implica un objeto hijo nuevo (ver Object Model) y es el cambio más caro.
  - **Change Impact y Priority:** alinear con la **matriz de riesgo corporativa de Impala**. Si la matriz es de 5 niveles, no hay que forzarla a 3.
  - **MOC Category:** no es un lookup, es un objeto con datos. Pedir la lista de categorías (proceso, equipo, organizativo, software, personal crítico, normativo…) como data load.
- **Ojo:** L01 y L05 están duplicadas. Ver §4.

### 3.6 Fields (la hoja más larga: 341 filas y 18 tablas)

**Bloques de la hoja:**
- **MOC:** 50 campos, con Mandatory y Read Only por cada una de las 7 etapas (columnas M a Z).
- **MOC Screening Question.**
- **7 tipos de tarea:** Process, Change Communication, Checklist, Documentation, Impact/Hazard Assessment, PSSR y Training.
- **6 tipos de aprobación.**
- **3 objetos de Setup:** Screening Question Setup, Task Setup y Approval Setup.

**Cómo se rellena cada fila:**
- `Field Name (Caption)` y `Caption in View`: renombrar si Impala usa otra terminología. Marcar **M**.
- `Tooltips/Hints`: el texto de ayuda en la terminología de Impala. Aporta mucho a la adopción.
- `Notes`: reglas de visibilidad, valores por defecto y longitudes.
- `Add / Remove`: **A**, **R** o **M**.
- `Mobile`: indicar si el campo aparece en la app móvil.
- `Mandatory in <etapa>` y `Read Only in <etapa>`: es la matriz de control. La regla de oro es que **lo que se cierra en una etapa pasa a Read Only en las siguientes**.

**Campos que Impala suele necesitar y el estándar no trae (candidatos a A):**

| Campo | Tipo | Por qué |
|---|---|---|
| Área / Activo afectado | Relations (Asset o Equipment) | Para vincular el MoC con el activo y reportar por equipo |
| Tipo de cambio (permanente / temporal / emergencia) | Lookup | Alternativa a 3 Yes/No independientes |
| Riesgo inicial y residual | Lookup (matriz) | Para trazabilidad risk-based y KPI |
| Justificación del cambio | Text (largo) | `Change Description` está limitado a 255 caracteres |
| Coste estimado y CAPEX/OPEX | Currency | Si Financial Approval depende de un umbral |
| Vínculo con incidente o auditoría de origen | Relations | Para trazar los MoC que nacen de una acción correctiva |
| Fecha real de implementación | Date | Para medir el KPI de plazo frente a la fecha solicitada |
| Requiere notificación a autoridad o cliente | Yes/No | Compliance (permisos ambientales, concesiones) |

**Matriz Mandatory / Read Only:** se revisa de forma específica la de `Change Expiry`, que hoy está a la vez marcada como Mandatory y con otras combinaciones raras (ver §4).

**Setup objects (filas 279 a 327):** son la "inteligencia" del MoC. Las screening questions, tareas y aprobaciones se **autogeneran** según categoría, etapa, impacto y los flags Emergency, RIK y Temporary. Aquí no hay que diseñar campos, sino **preparar los datos maestros**:
- **Catálogo de screening questions** por categoría y etapa: el checklist de MoC de Impala.
- **Matriz de tareas automáticas:** para cada combinación de categoría × impacto × etapa, qué tarea se crea, de qué tipo, para quién y con cuántos días de plazo.
- **Matriz de aprobaciones automáticas:** lo mismo, pero con aprobadores.

> Este es el entregable de negocio de más valor del proyecto. Recomiendo prepararlo en un Excel aparte (como plantilla de data load) y referenciarlo desde `Decisions & Tasks`.

### 3.7 Notification Templates
- **Qué hay:** N01 a N10 (Promoted, Rolled Back, Cancelled, Closed, y los emails de asignación, rechazo y cierre de tareas y aprobaciones).
- **Qué hacemos por cada email:**
  1. Validar los destinatarios. Hoy casi todos van solo al Change Requester. Lo normal es añadir el **Stage Owner entrante** en N01 y HSE en N03 y N04.
  2. Revisar asunto y cuerpo. Se usan los placeholders `{#Campo}` tal como vienen en el estándar.
  3. Añadir emails nuevos (por ejemplo, *Emergency Change creado*, con aviso inmediato a HSE Manager y Site Manager, o *Temporary Change próximo a expirar*).
- **Corregir los triggers de N06 y N07,** que están cruzados. Ver §4.

### 3.8 Notification Schedules
- **Qué hay:** la hoja está **vacía**.
- **Qué hacemos:** definir las escaleras de escalado, como mínimo para MOC Task y MOC Approval:

| Días | Relativo a Due Date | Destinatario | Template | Recurrencia |
|---|---|---|---|---|
| 3 | Before | Person Responsible | Recordatorio (nuevo) | Una vez |
| 0 | On | Person Responsible | Vence hoy (nuevo) | Una vez |
| 7 | After | Person Responsible + supervisor inmediato | Vencida (nuevo) | Cada 7 días |
| 14 | After | MOC Coordinator / HSE Manager | Escalado (nuevo) | Una vez |

- Para los Temporary Change, añadir un aviso 15 días antes de `Change Expiry`. Requiere una template nueva.

### 3.9 Security
- **Qué hay:** permisos por objeto para 5 grupos: System Admin, MoC Coordinator, MoC Administrator (Content), *Risks – Full Access* y *Risks – Standard Access*.
- **Qué hacemos:**
  1. **Sustituir los grupos "Risks – …"**, que vienen heredados de otra app, por los **grupos reales de Impala**. Propuesta:
     - MoC – Full Access (HSE y Coordinadores).
     - MoC – Standard User (cualquier empleado que pueda iniciar un MoC).
     - MoC – Read Only (auditoría y dirección).
     - MoC Admin (Content), que mantiene los setups.
  2. Revisar si el MOC Coordinator necesita **Edit** y **Workflow Actions** sobre el MOC. Hoy solo tiene Create y View, y solo puede actuar cuando es Person Responsible.
  3. Decidir **quién puede Delete**. Recomiendo que solo System Admin pueda borrar y que los demás usen Archive (por trazabilidad y auditoría).
  4. Vigilar la nota `**`: los objetos Task son compartidos con otras apps (Audits, NCR…), así que cambiar sus permisos afecta fuera de MoC.

### 3.10 Application Tabs
- **Qué hay:** New Change Request, MOC List, MOC Tasks, MOC Approvals y MOC Setup (con 3 subtabs).
- **Qué hacemos:**
  - Renombrar las columnas de seguridad con los grupos definitivos de 3.9.
  - Validar las columnas visibles, el orden y el agrupado de cada inventario.
  - Proponer tabs adicionales:
    - *My Open MOCs* (filtrado por usuario).
    - *Temporary Changes – próximos a expirar*.
    - *Emergency Changes pendientes de regularizar*.
- **Corregir el agrupado de la MOC List** (`Grouped By = Category`). Validar si Impala prefiere agrupar por estado o por ubicación.

### 3.11 Object Model y Action Handlers (oculta)
- **Object Model:** solo se revisa. Solo hay que tocarlo si se añade un tipo de tarea o de aprobación (es un objeto hijo nuevo) o si se quiere que los objetos hijos sean location-bound.
- **Action Handlers:** contienen las validaciones de negocio. Hay que validar con Impala:
  - Las reglas de fecha.
  - El límite de 180 días.
  - Cómo se generan las tareas y aprobaciones (CreateTasksForStage y CreateApprovalsForStage).
- Hay defectos de lógica en los Action Handlers. Ver §4.

---

## 4. Inconsistencias detectadas en el baseline (devolver a Intelex)

Las incluyo en `Decisions & Tasks` con Intelex como owner. Están ordenadas por impacto.

| # | Hoja / ubicación | Hallazgo | Impacto | Acción propuesta |
|---|---|---|---|---|
| 1 | Action Handlers AH11 | `If DueDate > TODAY → error "Due Date must be on or after Today"`: la condición está invertida (debería ser `< TODAY`). | **Alto**: bloquearía todas las aprobaciones con fecha futura. | Corregir la lógica. |
| 2 | Notification Templates N06 / N07 | N06 (Rejected) tiene el trigger `In Progress → Closed` y N07 (Closed) tiene `In Progress → Draft`. Están cruzados respecto al workflow. | **Alto**: se enviaría el email contrario. | Intercambiar los triggers. |
| 3 | Fields: Change Impact / Priority / Setup | `Change Impact` usa L05 (Priority) en lugar de L04 (Change Impact). El Screening Setup usa L04, pero Task y Approval Setup usan L05. L01 y L05 son duplicados. | **Alto**: la autogeneración de tareas y aprobaciones podría no casar. | Una sola lista de impacto, usada en todos los objetos. |
| 4 | Security | Los grupos "Risks – Full/Standard Access" vienen heredados de otra app. | Medio | Sustituirlos por los grupos de Impala (§3.9). |
| 5 | Fields: Change Expiry | Tipo = `None`, cuando debería ser Date. | Medio | Corregir. |
| 6 | Fields: approvals | Varias filas de Financial, Risk, Safety y Start Up Approval tienen la sección "Environmental Approval Details" (copy-paste). Engineering Approval no tiene número en la fila de Due Date. | Medio | Corregir la sección de cada fila. |
| 7 | Fields MOC, filas 48 y 49 | `Screening Questions` está duplicado. | Bajo | Eliminar una de las dos. |
| 8 | Workflow vs L03 | "Start Up" y "Follow Up" en el workflow frente a "Start-Up" y "Follow-Up" en el lookup. | Bajo, pero rompe los filtros por nombre | Unificar. |
| 9 | AH05 | El nombre dice "should be less than today", pero la regla exige una fecha igual o posterior a hoy. | Bajo | Renombrar. |
| 10 | Erratas | *Replace in Kind* frente a *Replacement in Kind*, *Precedures*, *MOS Process*, *Resposible*, *Started Confirmed?*, *Platfrom*. | Bajo (imagen) | Corregir. |

---

## 5. Input que necesitamos de Impala (preparar workshop)

Lo marcado como **crítico** bloquea la firma del workbook:

1. **[Crítico]** El procedimiento de MoC vigente de Impala: etapas, roles, umbrales y formularios actuales. Es la fuente de verdad para el mapeo.
2. **[Crítico]** La matriz de riesgo corporativa (niveles de impacto y probabilidad).
3. **[Crítico]** Una matriz RACI por etapa: quién inicia, quién aprueba y quién cierra, con nombre de rol y no de persona.
4. **[Crítico]** El catálogo de categorías de MoC y los checklists de screening por categoría.
5. Las reglas de autogeneración: categoría × impacto × flags → tareas y aprobaciones, con plazo.
6. Los grupos de seguridad y la lista de usuarios por ubicación.
7. Los SLA por etapa y la política de escalado.
8. El idioma de la interfaz y de los emails (¿multilingüe?).
9. Integraciones o vínculos con otras apps de Intelex del proyecto (Incidents, Audits, Risk, Documents).
10. Los KPIs que se quieren reportar. Determinan los campos de fecha y estado que hacen falta (ver §3.6).

---

## 6. Decisiones a registrar en `Decisions & Tasks` (borrador)

| # | Decisión / Tarea | Owner |
|---|---|---|
| 3 | Confirmar las etapas del workflow MOC y el Stage Owner de cada una | Process Owner MoC Impala |
| 4 | Definir los Location Roles adicionales y nominar personas por ubicación | HSE Lead Impala |
| 5 | Unificar la lista Change Impact / Priority con la matriz de riesgo corporativa | HSE Lead + Intelex |
| 6 | Confirmar los tipos de aprobación y de tarea (¿añadir Operations, Legal, IT/OT?) | Process Owner MoC |
| 7 | Definir los grupos de seguridad de MoC que sustituyen a "Risks – …" | IT/Admin Impala |
| 8 | Definir los escalados (Notification Schedules) y los SLA por etapa | Process Owner MoC |
| 9 | Preparar los data loads de categorías, screening, task setup y approval setup | BA Impala |
| 10 | Corregir las inconsistencias del baseline de §4 | Intelex |

---

## 7. Riesgos relevantes

| Riesgo | Prob. | Impacto | Mitigación |
|---|---|---|---|
| Rellenar el workbook sin el procedimiento MoC de Impala validado: la herramienta acaba replicando el estándar y no el proceso real | Media | Alto | Mapear primero el procedimiento contra el workflow (§5.1) |
| Sobre-personalizar (tipos de tarea o aprobación nuevos y etapas extra), lo que encarece la implantación y los upgrades | Media | Medio | Priorizar la configuración (lookups, roles, setups) frente a objetos nuevos |
| Setup data (screening, tareas y aprobaciones) sin preparar al go-live: el MoC no autogenera nada | Alta | Alto | Tratar los data loads como entregable con fecha propia |
| Errores del baseline (§4, filas 1 a 3) que llegan a producción | Media | Alto | Exigir la corrección y probarla en UAT con casos concretos |
