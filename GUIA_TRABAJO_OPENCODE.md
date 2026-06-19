# Guía de trabajo con OpenCode

> **Uso diario:** prompts copiables, reglas de alcance y verificaciones.  
> **Para decidir qué flujo usar:** consulta [`REFERENCIA_OPENCODE.md`](./REFERENCIA_OPENCODE.md).

---

No todo necesita spec. No todo necesita plan. Pero todo necesita alcance claro.

---

# 1. Plantillas de prompts

## 1.0. Bloque común de reglas para BUILD

Estas reglas aplican **solo a plantillas de ejecución** (<font color="#2563EB">🔨 BUILD</font>). No las uses en fases de PLAN o REVIEW. Se incluyen aquí para evitar repetirlas en cada plantilla BUILD:

```txt
Alcance:
- Modifica solo los archivos necesarios.
- Reutiliza la estructura y estilos existentes.
- No añadas dependencias salvo que sea imprescindible y lo justifiques.
- No cambies arquitectura salvo que sea necesario y lo expliques antes.
- No avances otras tareas.
- Mantén HTML semántico y responsive.
- Revisa accesibilidad básica: alt correcto, heading coherente y foco si aplica.

Al terminar, muestra:
- Archivos modificados.
- Cambios realizados.
- Comandos ejecutados.
- Resultado de build/check si procede.
```

Las plantillas que usan este bloque lo indican con: **Aplica el bloque común de reglas (1.0).**

---

## 1.1. Plantilla de aterrizaje de sesión nueva

Usar al abrir una sesión nueva de OpenCode y querer entender el estado actual antes de ejecutar cambios.

No debe modificar archivos.

No debe ejecutar specs.

No debe leer todas las specs.

**Fase:** <font color="#3B82F6">📋 PLAN</font> | **Modelo:** DeepSeek V4 Pro / GPT-5.5

Prompt para copiar y pegar:

```txt
Estoy empezando una sesión nueva del proyecto [NOMBRE_PROYECTO].

Objetivo:
Aterrizar en el estado actual del proyecto antes de ejecutar cambios.

Lee solo:

- AGENTS.md
- docs/handoff.md
- README.md
- package.json

No modifiques archivos.
No ejecutes ninguna spec.
No avances tareas.
No leas todas las specs.

Devuélveme:

1. Estado actual del proyecto.
2. Stack detectado.
3. Última situación registrada en docs/handoff.md.
4. Incidencias pendientes, si las hay.
5. Próximo paso recomendado.
6. Fase recomendada para ese siguiente paso: EXPLORE, PLAN, BUILD o VERIFY.
7. Comandos mínimos que convendría ejecutar antes de tocar código.
```

Ejemplo aplicado:

```txt
Estoy empezando una sesión nueva del proyecto Portfolio 3.0 — Spanioulis.

Objetivo:
Aterrizar en el estado actual del proyecto antes de ejecutar cambios.

Lee solo:

- AGENTS.md
- docs/handoff.md
- README.md
- package.json

No modifiques archivos.
No ejecutes ninguna spec.
No avances tareas.
No leas todas las specs.

Devuélveme:

1. Estado actual del proyecto.
2. Stack detectado.
3. Última situación registrada en docs/handoff.md.
4. Incidencias pendientes, si las hay.
5. Próximo paso recomendado.
6. Fase recomendada para ese siguiente paso: EXPLORE, PLAN, BUILD o VERIFY.
7. Comandos mínimos que convendría ejecutar antes de tocar código.
```

---

## 1.2. Plantilla para cambio pequeño sin spec

Usar cuando la tarea sea pequeña, localizada y no requiera una spec formal.

**Fase:** <font color="#2563EB">🔨 BUILD</font> | **Modelo:** GLM-5.1 / DeepSeek V4 Pro

Prompt para copiar y pegar:

```txt
Añade una mejora pequeña y localizada siguiendo estas reglas.

Alcance:
- Modifica solo los archivos necesarios.
- Reutiliza la estructura y estilos existentes.
- No añadas dependencias.
- No cambies arquitectura.
- No avances otras tareas.
- Mantén HTML semántico y responsive.
- Revisa accesibilidad básica: alt correcto, heading coherente y foco si aplica.

Al terminar, muestra:
- Archivos modificados.
- Cambios realizados.
- Comandos ejecutados.
- Resultado de build/check si procede.

Objetivo concreto:
[AQUÍ EL OBJETIVO]
```

Ejemplo aplicado:

```txt
Añade una mejora pequeña y localizada siguiendo estas reglas.

Alcance:
- Modifica solo los archivos necesarios.
- Reutiliza la estructura y estilos existentes.
- No añadas dependencias.
- No cambies arquitectura.
- No avances otras tareas.
- Mantén HTML semántico y responsive.
- Revisa accesibilidad básica: alt correcto, heading coherente y foco si aplica.

Al terminar, muestra:
- Archivos modificados.
- Cambios realizados.
- Comandos ejecutados.
- Resultado de build/check si procede.

Objetivo concreto:
Añade una sección simple con título e imagen en la home.
```

---

## 1.3. Plantilla para cambio pequeño con micro-plan

Usar cuando el cambio parece pequeño, pero quieres que OpenCode piense antes de tocar archivos.

**Fase:** <font color="#3B82F6">📋 PLAN</font> | **Modelo:** DeepSeek V4 Pro / GPT-5.5

Prompt para copiar y pegar:

```txt
Quiero hacer una mejora pequeña y localizada.

Antes de modificar archivos, dime brevemente:
- Qué archivos tocarías.
- Si crearías componente nuevo o reutilizarías uno existente.
- Riesgos mínimos.
- Si ves necesario crear una spec formal o no.

No ejecutes cambios todavía.
Devuélveme el micro-plan y espera confirmación antes de modificar archivos.

Objetivo concreto:
[AQUÍ EL OBJETIVO]
```

Ejemplo aplicado:

```txt
Quiero hacer una mejora pequeña y localizada.

Antes de modificar archivos, dime brevemente:
- Qué archivos tocarías.
- Si crearías componente nuevo o reutilizarías uno existente.
- Riesgos mínimos.
- Si ves necesario crear una spec formal o no.

No ejecutes cambios todavía.
Devuélveme el micro-plan y espera confirmación antes de modificar archivos.

Objetivo concreto:
Añade una sección simple con título e imagen en la home.
```

---

## 1.4. Plantilla para pedir <font color="#3B82F6">📋 PLAN</font>

Usar cuando quieres revisar el enfoque antes de ejecutar.

**Fase:** <font color="#3B82F6">📋 PLAN</font> | **Modelo:** DeepSeek V4 Pro / GPT-5.5

Prompt para copiar y pegar:

```txt
Crea un plan para esta tarea.

No modifiques archivos todavía.

Objetivo:
[AQUÍ EL OBJETIVO]

El plan debe incluir:
- Archivos que tocarías.
- Orden de ejecución.
- Riesgos.
- Verificaciones necesarias.
- Qué no debe hacerse todavía.
- Si ves necesario crear una spec formal.

No ejecutes cambios.
```

---

## 1.5. Plantilla para ejecutar un <font color="#3B82F6">📋 PLAN</font> aprobado

Usar cuando OpenCode ya ha creado un plan y tú lo has revisado.

**Fase:** <font color="#2563EB">🔨 BUILD</font> | **Modelo:** GLM-5.1 / GPT-5.5

Prompt para copiar y pegar:

```txt
Sí, apruebo el plan. Ejecuta los cambios siguiendo exactamente este alcance:

[PEGAR AQUÍ EL PLAN APROBADO O SUS TAREAS]

Aplica el bloque común de reglas (1.0) y además:
- No amplíes el alcance.
- Si aparece un problema que obliga a cambiar el plan, para y explica la situación antes de seguir.

Al terminar, muestra también:
- Problemas encontrados.
- Estado final.
- Próximo paso recomendado.
```

---

## 1.6. Plantilla para ejecutar una spec

Usar cuando la tarea ya está definida en una spec.

**Fase:** <font color="#2563EB">🔨 BUILD</font> | **Modelo:** GLM-5.1 / GPT-5.5

Prompt para copiar y pegar:

```txt
Ejecuta únicamente la spec:

specs/XXX-nombre.md

Antes de tocar nada, lee:
- AGENTS.md
- docs/handoff.md
- la spec indicada

Aplica el bloque común de reglas (1.0).

No avances a la siguiente spec.
No amplíes el alcance.

Al terminar, actualiza la spec si procede y muestra también:
- Problemas encontrados.
- Estado final de la spec.
- Próxima spec recomendada.
```

Versión con más contexto (documentación adicional):

```txt
Ejecuta únicamente la spec:

specs/XXX-nombre.md

Antes de tocar nada, lee:
- AGENTS.md
- docs/handoff.md
- docs/project-context.md
- specs/XXX-nombre.md

Aplica el bloque común de reglas (1.0).

No avances a la siguiente spec.
No amplíes el alcance.

Al terminar, actualiza docs/handoff.md y la spec, y muestra también:
- Problemas encontrados.
- Estado final de la spec.
- Próxima spec recomendada.
```

---

## 1.7. Plantilla para bug o incidencia

Usar cuando algo falla y no quieres avanzar features.

**Fase:** <font color="#10B981">✅ VERIFY/FIX</font> | **Modelo:** GPT-5.5 / DeepSeek V4 Pro

Prompt para copiar y pegar:

```txt
Revisa y corrige únicamente esta incidencia:

[PEGAR ERROR O DESCRIPCIÓN DEL BUG]

No avances ninguna feature nueva.
No hagas refactors fuera de alcance.
No cambies arquitectura salvo que sea imprescindible y lo justifiques.

Objetivo:
Diagnosticar y corregir el error con el mínimo cambio necesario.

Comprobaciones mínimas:
- Ejecutar los comandos necesarios de diagnóstico.
- Corregir solo lo necesario.
- Ejecutar check/build/dev si procede.
- Verificar la ruta o funcionalidad afectada.

Al terminar, muestra:
- Causa probable.
- Archivos modificados.
- Comandos ejecutados.
- Resultado de verificaciones.
- Confirmación de si el error desapareció.
- Estado final.
```

---

## 1.8. Plantilla para <font color="#10B981">✅ VERIFY</font> sin modificar archivos

Usar cuando solo quieres revisar el estado.

**Fase:** <font color="#10B981">✅ VERIFY</font> | **Modelo:** DeepSeek V4 Pro / GPT-5.5

Prompt para copiar y pegar:

```txt
Verifica el estado actual sin modificar archivos.

Objetivo:
[AQUÍ LO QUE QUIERES COMPROBAR]

No hagas cambios.

Devuélveme:
- Estado actual.
- Archivos relevantes.
- Posibles problemas.
- Verificaciones pendientes.
- Recomendación de siguiente paso.
```

---

## 1.9. Plantilla para aplicar una skill

Usar cuando quieres que OpenCode aplique una skill concreta a una tarea.

**Cuándo usar cada variante:**

| Situación | Variante |
|---|---|
| Skill + cambio importante (accesibilidad, SEO, arquitectura, performance, migraciones, varios archivos) | **A — PLAN primero** |
| Skill + cambio pequeño y cerrado (añadir aria-label, revisar un meta, corregir un alt) | **B — BUILD directo** |

---

### A — Variante PLAN primero

**Fase:** <font color="#3B82F6">📋 PLAN</font> | **Modelo:** DeepSeek V4 Pro / GPT-5.5

Prompt para copiar y pegar:

```txt
Lee AGENTS.md y la skill correspondiente.

Lee esta skill como una norma de trabajo, no como una sugerencia.
Aplícala solo cuando sea relevante para esta tarea.
No leas ni apliques otras specs o skills salvo que estén explícitamente relacionadas.

No modifiques archivos.

Objetivo:
Aplicar esta skill a la siguiente tarea:

[AQUÍ LA TAREA CONCRETA]

Explícame:

1. Cómo aplicarías esta skill a la tarea.
2. Qué archivos revisarías.
3. Qué riesgos o puntos críticos ves.
4. Qué criterios usarías para validar que la skill se ha aplicado bien.
5. Qué plan de ejecución propones.

No ejecutes cambios todavía.
```

---

### B — Variante BUILD directo

Usar solo cuando la tarea es pequeña, concreta y el alcance está cerrado.

**Fase:** <font color="#2563EB">🔨 BUILD</font> | **Modelo:** GLM-5.1 / GPT-5.5

Prompt para copiar y pegar:

```txt
Lee AGENTS.md y la skill correspondiente.

Lee esta skill como una norma de trabajo, no como una sugerencia.
No leas ni apliques otras specs o skills.

Aplica solo esta corrección concreta:

[AQUÍ LA TAREA CONCRETA]

No modifiques nada más.
```

---

## 1.10. Plantilla para crear una spec

Usar cuando necesitas definir una tarea formal antes de ejecutar.

**Fase:** <font color="#3B82F6">📋 PLAN</font> | **Modelo:** DeepSeek V4 Pro / GPT-5.5

Prompt para copiar y pegar:

```txt
Crea una spec para esta feature sin modificar código.

Objetivo:
[AQUÍ EL OBJETIVO]

La spec debe incluir:
- Objetivo concreto.
- Alcance detallado.
- Archivos probables.
- Tareas ordenadas.
- Riesgos detectados.
- Verificaciones necesarias.
- Criterios de aceptación.
- Qué no debe hacerse todavía.

Devuélveme la spec lista para guardar en specs/.
No crees el archivo todavía salvo que te lo pida explícitamente.
```

---

## 1.11. Plantilla para REVIEW sin modificar archivos

Usar cuando quieres una revisión tipo code review de los cambios actuales.

**Fase:** <font color="#10B981">✅ VERIFY</font> | **Modelo:** GPT-5.5 / DeepSeek V4 Pro

Prompt para copiar y pegar:

```txt
Revisa los cambios actuales como code review sin modificar archivos.

Revisa el diff actual si procede.

Revisa:
- Bugs introducidos.
- Regresiones.
- Riesgos detectados.
- Tests o checks faltantes.
- Cambios fuera de alcance.
- Problemas de accesibilidad o SEO si aplica.

Devuélveme:
- Lista de hallazgos ordenados por prioridad.
- Recomendación de siguiente paso.
```

---

## 1.12. Plantilla para continuación de sesión o tarea interrumpida

Usar cuando una tarea quedó a medias y necesitas recuperar estado.

**Fase:** <font color="#3B82F6">📋 PLAN</font> | **Modelo:** DeepSeek V4 Pro / GPT-5.5

Prompt para copiar y pegar:

```txt
Recupera el estado de la sesión anterior.

Lee AGENTS.md y docs/handoff.md.

No ejecutes cambios todavía.

Devuélveme:
1. Qué se hizo en la última sesión.
2. Qué queda pendiente.
3. Qué archivos están implicados.
4. Qué verificaciones faltan.
5. Siguiente paso recomendado.
6. Fase recomendada: EXPLORE, PLAN, BUILD o VERIFY.
```

---

# 2. Reglas de control de alcance

Frases útiles para añadir a cualquier prompt:

```txt
No avances a otra tarea.
```

```txt
No hagas cambios fuera de alcance.
```

```txt
No añadas dependencias salvo que sea imprescindible y lo justifiques.
```

```txt
No cambies arquitectura salvo que sea necesario y lo expliques antes.
```

```txt
Si detectas que este cambio no es pequeño, para y propón crear una spec o un plan.
```

```txt
Antes de modificar archivos, dime qué archivos tocarías.
```

```txt
Ejecuta exactamente el plan aprobado.
```

```txt
No marques la tarea como completada si no pasan las verificaciones.
```

```txt
No leas todas las specs.
```

```txt
No ejecutes ninguna spec.
```

```txt
No leas ni apliques otras specs o skills salvo que estén explícitamente relacionadas con esta tarea.
```

### Git

```txt
Revisa el diff actual antes de hacer cambios si procede.
No reviertas cambios ajenos.
No hagas commit salvo petición explícita.
Separa tus cambios de los cambios existentes.
```

### Problemas fuera de alcance

```txt
Si detectas un problema no relacionado con la tarea actual, no lo corrijas directamente.
Repórtalo como follow-up para una tarea futura.
```

---

# 3. Verificaciones

Las verificaciones dependen del proyecto.

Ejemplos habituales:

```bash
pnpm check
pnpm build
pnpm dev
```

En Astro puede ser:

```bash
pnpm astro check
pnpm build
pnpm dev
```

En algunos casos:

```bash
pnpm astro sync
pnpm preview
```

También puede ser necesario revisar:

```txt
- Consola del navegador.
- Responsive.
- SEO básico.
- Accesibilidad básica.
- Rutas afectadas.
- Formularios.
- Imágenes.
```

Regla:

```txt
Una tarea solo se considera cerrada si pasa las verificaciones necesarias.
```

Si no pasan, el estado debe quedar claro:

```txt
- Completada.
- Completada parcialmente.
- Pendiente de fix.
- Bloqueada.
- En revisión.
```

### Tipos de <font color="#10B981">✅ VERIFY</font>

| Tipo | Descripción | ¿Modifica archivos? | ¿Ejecuta comandos? |
|---|---|---|---|
| <font color="#10B981">✅ VERIFY</font> lectura | Revisar estado, archivos, problemas potenciales | No | No |
| <font color="#10B981">✅ VERIFY</font> comandos | Ejecutar check/build/dev para validar | No | Sí |
| <font color="#10B981">✅ VERIFY/FIX</font> | Diagnosticar y corregir con cambios mínimos | Sí | Sí |

---

# 4. Resumen

```txt
Sesión nueva → PLAN aterrizaje.
Cambio pequeño → prompt directo.
Cambio pequeño con dudas → micro-plan.
Feature importante → spec + plan.
Bug → VERIFY/FIX.
Migración o arquitectura → EXPLORE + PLAN + BUILD + VERIFY.

AGENTS marcan cómo trabajar.
SKILLS aportan criterio especializado.
SPECS definen qué se hace ahora.

No todo necesita spec.
No todo necesita plan.
Pero todo necesita alcance claro.

No leas todo por defecto.
Lee solo lo necesario para la fase actual.
```
