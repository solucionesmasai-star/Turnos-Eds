# Turnos EDS v0.4

Primera aplicación local para visualizar y regenerar un ciclo maestro de turnos 24/7.

## Cambio principal v0.4 — vacaciones manuales

- Solo puede existir **un Atendedor FT con vacaciones por ciclo de 28 días**.
- Las vacaciones **nunca se asignan aleatoriamente**.
- Botón **Asignar vacaciones**:
  1. seleccionar Atendedor 1–28;
  2. elegir fecha real Desde;
  3. elegir fecha real Hasta;
  4. guardar vacaciones y generar horario.
- El rango debe quedar completamente dentro del ciclo visible.
- Asignar una nueva VAC reemplaza la VAC anterior del ciclo; nunca crea una segunda persona de vacaciones.
- También se puede quitar la VAC del ciclo.
- El motor genera la malla restante respetando el rango VAC fijo.

## Reglas preservadas

- 28 FT + 8 PT.
- PT sin cambios: 5 V-S-D y 3 S-D; ninguno hace noche.
- Máximo 2 libres por semana para FT.
- Máximo 6 días consecutivos, incluyendo cruce entre ciclos.
- Bloque nocturno protegido Libre → N → N → Libre.
- 2 nocturnos por día.
- 42 h planificadas por semana FT.
- Semanas con libres juntos: salida -30 min.
- Semanas con libres separados: dos salidas -15 min.
- Inicio diurno no antes de 06:00.
- M1 no se utiliza como base sábado/domingo.
- Ningún turno cruza medianoche.
- Licencias médicas y compensatorios se registran por separado de VAC.

## Uso

Abra `index.html` directamente o publique el repositorio en GitHub Pages / Vercel.

No requiere dependencias ni proceso de build.
