# Turnos EDS v2.1

Versión basada en la v1.7 del planificador maestro de turnos EDS.

## Objetivo de esta versión

La v2.1 incorpora una rotación semanal automática orientada a equidad e igualdad entre los atendedores FT, manteniendo la continuidad operacional y los turnos bisagra.

## Familias de turno FT

- N: 00:00–09:00
- M1: 06:00–15:00
- M2: 07:00–16:00
- B1: 09:00–18:00
- B2: 11:00–20:00
- T1: 13:00–22:00
- T2: 15:00–24:00

M3 fue eliminado. Su capacidad se redistribuye entre M2, B1 y B2 según la plantilla diaria.

## Rotación semanal equitativa

Cada FT tiene una familia preferente que avanza semanalmente:

Mañana → Bisagra → Tarde → Mañana

Los puntos de partida se escalonan entre los trabajadores para evitar que todo el equipo cambie de familia el mismo lunes.

El motor no se limita a una asignación fija: además considera la carga acumulada visible de cada trabajador dentro del ciclo para compensar automáticamente diferencias entre Mañana, Bisagra y Tarde.

Los bloques N continúan funcionando de manera independiente a esta rotación.

## Turnos bisagra

B1 y B2 se mantienen expresamente en el motor.

Su función es:

- suavizar los cambios de turno;
- mantener continuidad de atención durante los relevos;
- cubrir la transición entre mañana y tarde;
- evitar que el cliente perciba cortes bruscos en la dotación;
- absorber capacidad residual antes de sobrecargar los extremos M1/T2.

## Reglas duras preservadas

- exactamente 2 N por día;
- patrón Libre → N → N → N → Tarde;
- antes de iniciar un bloque N debe existir Libre según el patrón maestro;
- después de T1 o T2 no se permite M1 ni M2 al día siguiente;
- máximo 6 días continuos;
- máximo 2 libres por semana;
- 42 h semanales base según el patrón vigente;
- PT mantienen su programación fija;
- vacaciones manuales;
- licencias médicas por rango de fechas;
- compensatorios;
- lectura pública y edición autenticada mediante Supabase;
- cobertura objetivo: mínimo 8 entre 06:00–07:00 L-V y mínimo 9 desde las 07:00 en franja crítica.

## Part-time

No se modificó la estructura PT existente:

- PT1, PT2, PT3, PT4 y PT5: viernes, sábado y domingo;
- PT6, PT7 y PT8: sábado y domingo;
- PT no realizan turno N.

## Supabase

La aplicación sigue utilizando el workspace compartido `principal`.

- Invitados: lectura.
- Usuarios autenticados: lectura y escritura.
- `localStorage`: respaldo local.
- La `service_role` no debe usarse en frontend.

La configuración pública se encuentra en `config.js`.

Si las tablas compartidas aún no existen, ejecutar una sola vez:

`supabase/shared_workspace.sql`

## Archivos

- `index.html`: aplicación completa.
- `config.js`: configuración pública de Supabase.
- `.gitignore`: archivos que no deben subirse.
- `supabase/shared_workspace.sql`: creación idempotente de las tablas compartidas y políticas RLS.

## Cambio principal respecto de v1.7

La v1.7 distribuía los turnos principalmente mediante plantillas diarias. La v2.1 mantiene esas necesidades operativas, elimina M3 y agrega una capa de rotación semanal y compensación automática de carga para repartir de manera más equitativa Mañana, Bisagra y Tarde.


## Ajustes v2.1

- Se reorganiza la distribución por grupos separados: Mañana (M1/M2), Bisagra (B1/B2) y Tarde (T1/T2).
- Para volver desde el grupo Tarde al grupo Mañana debe existir un día Libre intermedio.
- Se mantiene el patrón L → N → N → N → Tarde y los turnos bisagra B1/B2.


## Optimización v2.1

- B2 cambia a 12:00–21:00.
- T1 cambia a 14:00–23:00.
- T2 se mantiene 15:00–24:00.
- El motor calcula automáticamente la mezcla M1/M2/B1/B2/T1/T2 según la dotación disponible y los PT fijos.
- Prioridad 1: al menos 9 atendedores entre 07:00 y 23:00.
- Prioridad 2: evitar más de 15 atendedores simultáneos; 14 es el objetivo preferente cuando la estructura lo permite.
- La redistribución conserva B1/B2 y las reglas de rotación y descanso.


## Cambios v2.1 — Generar versión

- El botón **Generar versión** ahora reasigna realmente los ciclos entre los FT seleccionados.
- Se rota el patrón completo de cada trabajador: días trabajados, libres y posición dentro del superciclo.
- El bloque nocturno NNN queda asociado al ciclo/patrón, por lo que también cambia de trabajador al generar una nueva versión.
- VAC, LM, COMP, nombres, PT y fecha de inicio del ciclo se conservan.
- Después de reasignar, el motor recalcula turnos M/B/T, cobertura y validaciones.
